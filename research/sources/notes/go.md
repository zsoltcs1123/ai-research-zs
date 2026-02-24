Sure — here's a Go quick reference tailored to your background.

````markdown
# Go Quick Reference (for C#/Java/TS/Python devs)

## Basics

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go")
}
```
````

## Variables

```go
var x int = 5          // explicit type
var y = 5              // inferred
z := 5                 // short declaration (most common, only inside functions)
const Pi = 3.14        // constant
```

## Functions

```go
func add(a int, b int) int {
    return a + b
}

func divide(a, b float64) (float64, error) {  // multiple returns
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }
    return a / b, nil
}

// calling it
result, err := divide(10, 3)
if err != nil {
    log.Fatal(err)
}
```

## Structs (no classes)

```go
type User struct {
    Name  string   // exported (public) — uppercase
    email string   // unexported (private) — lowercase
    Age   int
}

func (u User) Greet() string {          // value receiver (read-only)
    return "Hi, " + u.Name
}

func (u *User) SetEmail(e string) {     // pointer receiver (mutates)
    u.email = e
}

user := User{Name: "Zoli", Age: 30}
user.SetEmail("z@example.com")
```

## Interfaces (implicit — no "implements")

```go
type Stringer interface {
    String() string
}

// User satisfies Stringer automatically if it has a String() method
func (u User) String() string {
    return u.Name
}
```

## Error Handling (no try/catch)

```go
f, err := os.Open("file.txt")
if err != nil {
    return fmt.Errorf("opening file: %w", err)  // wrap errors with %w
}
defer f.Close()  // runs when enclosing function returns
```

## Collections

```go
// Arrays (fixed size, rarely used directly)
arr := [3]int{1, 2, 3}

// Slices (dynamic, this is what you'll use)
s := []int{1, 2, 3}
s = append(s, 4)
sub := s[1:3]          // [2, 3]

// Maps
m := map[string]int{"a": 1, "b": 2}
m["c"] = 3
val, ok := m["d"]      // ok = false if key missing

// Iteration
for i, v := range s {  // index, value
    fmt.Println(i, v)
}
for k, v := range m {  // key, value
    fmt.Println(k, v)
}
```

## Control Flow

```go
// if (no parens, braces required)
if x > 0 {
    // ...
} else if x == 0 {
    // ...
}

// if with init statement
if err := doThing(); err != nil {
    return err
}

// switch (no break needed, no fallthrough by default)
switch status {
case "active":
    activate()
case "inactive", "disabled":    // multiple values
    deactivate()
default:
    unknown()
}

// for is the only loop keyword
for i := 0; i < 10; i++ {}     // classic
for x < 100 { x *= 2 }         // while
for {}                           // infinite
```

## Goroutines & Channels (concurrency)

```go
// goroutine = lightweight thread
go func() {
    fmt.Println("running concurrently")
}()

// channels = typed pipes between goroutines
ch := make(chan string)

go func() {
    ch <- "hello"           // send
}()

msg := <-ch                 // receive (blocks until value available)

// buffered channel
ch2 := make(chan int, 5)    // won't block until buffer full

// select = switch for channels
select {
case msg := <-ch:
    fmt.Println(msg)
case <-time.After(1 * time.Second):
    fmt.Println("timeout")
}
```

## Generics (Go 1.18+)

```go
func Map[T any, R any](items []T, fn func(T) R) []R {
    result := make([]R, len(items))
    for i, v := range items {
        result[i] = fn(v)
    }
    return result
}
```

## Enums (faked with iota)

```go
type Status int

const (
    Active Status = iota   // 0
    Inactive               // 1
    Disabled               // 2
)
```

## Common Patterns

```go
// Constructor function (no constructors on structs)
func NewUser(name string, age int) *User {
    return &User{Name: name, Age: age}
}

// Stringer (like ToString in C#)
func (u User) String() string {
    return fmt.Sprintf("%s (%d)", u.Name, u.Age)
}

// Type assertion (like casting)
var i interface{} = "hello"
s := i.(string)            // panics if wrong type
s, ok := i.(string)        // safe version
```

## Project Layout

```
myproject/
├── go.mod              # like package.json / .csproj
├── go.sum              # like lock files
├── main.go             # entry point
├── internal/           # private to this module
│   └── service/
├── pkg/                # public/reusable packages
└── cmd/                # multiple entry points
    └── myapp/
        └── main.go
```

## CLI Cheat Sheet

```
go mod init myproject     # init module
go run .                  # compile + run
go build -o myapp .       # compile binary
go test ./...             # run all tests
go fmt ./...              # format code
go vet ./...              # static analysis
go get pkg@latest         # add dependency
```

## Rosetta Stone

| C# / Java / TS             | Go                            |
| -------------------------- | ----------------------------- |
| `class`                    | `type X struct{}`             |
| `interface` + `implements` | `interface` (implicit)        |
| `try/catch/finally`        | `if err != nil` + `defer`     |
| `async/await`              | `go` + channels               |
| `null`                     | `nil` (pointers/slices/maps)  |
| `public/private`           | `Uppercase/lowercase`         |
| `List<T>`                  | `[]T` (slice)                 |
| `Dictionary<K,V>`          | `map[K]V`                     |
| `using/try-with-resources` | `defer`                       |
| `ToString()`               | `String() string`             |
| `nameof`                   | doesn't exist                 |
| `LINQ / streams`           | `for` loops (or generics lib) |
| `enum`                     | `const + iota`                |
| inheritance                | embedding                     |

```

This should cover ~90% of what you'll encounter day-to-day. The official [Tour of Go](https://go.dev/tour/) is worth the 2 hours if you want hands-on practice.
```
