# Error Handling and Go

Error is a built in type: `error`

One of the common ways it is used:

```go

f, err := os.Open("filename.txt")

if err != nil {
	log.Fatal(err)
}

```

So some functions will return an `error` or `nil`. The standard library follows this and its a good 
convention for designing functions. You may have a custom error type with unique error handling 
strategies for a specific project but this practice works good generally.

### Interface Declaration

```go
// just a string that contains error message
// predeclared in universal scope (global scope)

type error interface {
	Error() string
}

```

### Common Uses

```

errors.New("error message")

```

We take in `string` and convert into `errors.errorString` which counts as an `error` value

---------------------------------------------------------------------

How to use it
```
if [some issue in conditional] {
	return nil, errors.New("something went wrong in conditional")
}
```

Heres a good alternative

```go

fmt.Errorf("explanation of what went wrong with variable %x", f)
// use the same way we used errors.New()
```

Can go even further here. You can return the value (and its type) by simply modifying it:

```go

fmt.Errorf("explanation of what went wrong with variable %x", float64(f))
// using float64() as example, any type will work
```

Now a user of the function can use a `type assertion` and handle any special errors.

This is very useful if you need to know what type of error it is!

Example to examine this:

```go
package net // example package we use 

// error implementation for net (simplified)
type Error interface {
	error
	Timeout() bool // is error time out?
	Termporary() bool // is it temporary error?
}

if err, ok := err.(net.Error); ok && nerr.Temporary(){
	time.Sleep(...)
	continue
}

if err != nil {
	log.Fatal(err)
}

```

So we can see how error object is used.


### Repetitive Error Handling

Because of the design of GO, error handling is very important and you need to explicitly check for 
errors where they occur. Other languages may throw exceptions and such, but in Go its in your hand.
That makes go code very verbose, but we will look at some ways to simplify this.


#### When possible use wrapper functions 
This allows your main function to just return one error, while the wrapper function(s) will do the verbose error checking.

 

