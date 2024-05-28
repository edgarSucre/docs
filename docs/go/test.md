# Tests

## Flags

These flags can be used with the test util `go test`

| Flag               | Description                                                |
| ------------------ | ---------------------------------------------------------- |
| -race              | Detects race conditions. Also can be used with `go build`  |
| -run regexp        | Used to filter which test to run                           |
| -parallel n        | N represents the maximum number of test to run in parallel |
| -failfast          | Indicates to stop tests execution when a failure happens   |
| -v                 | Verbose, print the t.Log messages                          |
| -timeout d         | Panic if any test takes more time than d                   |
| -skip regexp       | Similar to run but for skipping tests                      |
| -short             | Sets a global variable we can use with `t.Short()`         |
| -bench             | To run benchmarks                                          |
| -cover             | Indicates the package coverage                             |
| -coverprofile=name | creates a coverage profile with the specified name         |

---

## Run Tests In Parallel

### Overview
To execute tests in parallel we use the function `t.Parallel()`. This is how it works:
- When `t.Parallel` is executed, the test stops and it's added to a queue.
- Once all package's sequential tests are finished then the parallel tests start.
- The number of test that can be run in Parallel depends on the `-parallel` flag.

### When to use it
It's not recommended to use parallel test just to shorten the time of test execution. It's recommended to use it to test that a function is thread save. A common pattern is to create a table test where every sub-test is executed in parallel so we can make sure there is no race conditions or deadlocks.

### Cleanup
If we need to release resources (io.closer.Close()) after the sub-test we can use `t.Cleanup`. This function accepts a clojure that gets run after all parallel test are complete.

---

## Skip tests
there ware two ways to skip a test, at run time and compile time.

### At run time
```go
func TestExpensiveFunc(t *testing.T) {
    if !runIntegrationTest { // based on logic
        t.Skip()
    }
}

func TestBatchFunc(t *testing.T) {
    if t.Short() {
        t.Skip()
    }
}
```

### AT compile time
We can use build tags to exclude files from the test binaries
```go
// +build integration
package db

import "testing"

func TestDb(t *testing.T) {
    ...
}
```

The file will not be included in the test binary unless we pass the build tag

```bash
go test -tags=integration
```
---

## Benchmarking
The way we benchmark in go is by simply run a function many times and the test tool analyze the operations/second .

``` go
func BenchmarkFibo(b *testing.B) {
    // expensive setup...
	
    b.ResetTimer()  // make sure we measure the actual function
	for i:=0; i < b.N; i++ {
		fib(b.N)
	}
	// tear down
	b.StopTimer() // stop counting
}

// execute the benchmark
go test -bench .
```
---

## Coverage
To determine the package coverage we use the `-cover` flag. To obtain a more detailed report we need a profile.

```bash
// get the profile
go test -coverprofile=cover.out

// visualize it
go tool cover -html=cover.out
```
---

## Utils

Functions and packages designed to facilitate the creation of tests.

### t.Helper()
Marks the function as a helper so it doesn't get reported by logs and errors.

### quick.Check(fn)
`quick.Check` takes a function that accepts the same parameters as the function to be tested and returns a bool.
The parameters are generated with random values automatically.

```go
// function to be tested
func Square(n int) {
    return n * n //possible overflow
}

func TestSquare(t *testing.T) {
    fn := func(n int) bool {
        return Square(n) > 0 // quick.Check assertion
    }

    if err != quick.Check(fn, nil); err != nil {
        t.Error(err) // test failed
    }
}
```

### http/httptest
Utility package to test http requests

### io/iotest
Utility package to test io operation

### Clean cache
If you need to clean test the test cache run:
```bash
go clean -testcache
```