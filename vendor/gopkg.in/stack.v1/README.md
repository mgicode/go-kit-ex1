[![GoDoc](https://godoc.org/gopkg.in/stack.v1
?status.svg)](https://godoc.org/gopkg.in/stack.v1
) [![Build Status](https://travis-ci.org/go-stack/stack.svg?branch=master)](https://travis-ci.org/go-stack/stack)

# stack

Package stack implements utilities to capture, manipulate, and format call
stacks. It provides a simpler API than package runtime.

The implementation takes care of the minutia and special cases of interpreting
the program counter (pc) values returned by runtime.Callers.

## Versioning

Package stack publishes stable APIs via gopkg.in. The most recent is v1, which
is imported like so:

    import "gopkg.in/stack.v1"

## Formatting

Package stack's types implement fmt.Formatter, which provides a simple and
flexible way to declaratively configure formatting when used with logging or
error tracking packages.

```go
func DoTheThing() {
    c := stack.Caller(0)
    log.Print(c)          // "source.go:10"
    log.Printf("%+v", c)  // "pkg/path/source.go:10"
    log.Printf("%n", c)   // "DoTheThing"

    s := stack.Trace().TrimRuntime()
    log.Print(s)          // "[source.go:15 caller.go:42 main.go:14]"
}
```

See the docs for all of the supported formatting options.
