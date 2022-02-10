---
title: "Go"
date: 2022-02-02
draft: false
toc: true
tags:
    - go
    - snippets
---

Creating new error:

```go
import (
    "errors"
)

errors.New("New error")
```

Common error handling pattern:

```go
if err != nil {
    // do stuff
}

// shorthand
if res, err := GetResult(); err != nil {
    // handle error
}
```

Connecting to db(sqlite in this case):

```go
import (
    "database/sql"
    _ "github.com/mattn/go-sqlite3" // blank identifier/import to prevent go compiler from removing
)

func run() err {
    db, err := sql.Open("sqlite3", "path/to/db")

    if err != nil {
        return err
    }
    defer db.Close() // close connection just before func finishes
}
```

Comparing variable against multiple strings/conditions:

```go
// "suspect or" since one of the conditions will be true so
// true || false is aways true
if condition != "condition1" || condition != "condition2" {

}

if condition != "condition1" && condition != "condition2" {

}
```

godoc comments:

```go
// Package temperature contains weather related helpers
package temperature

// TemperatureCelcius represents temperature in Celcius.
var TemperatureCelcius float64

// CelsiusFreezingTemp returns a temp.
func CelsiusFreezingTemp() int {
    return 0
}
```

-   Immediately precede packages as well as exported identifiers like exported functions, methods, package variables, constants, structs and ends with period.

Incrementing:

```go
//wrong
func main() {
    i := 7
    inc(i) // no effect since this is copying by value
    fmt.Println(i) // 7
}

func inc(x int) {
    x++
}
```

```go
// right
func main() {
    i := 7
    inc(&i) // send pointer
    fmt.Println(i) // 8
}

func inc(x *int) { // accepting pointer
    *x++ // dereferencing the pointer because without it will increment the memory addr
}
```
