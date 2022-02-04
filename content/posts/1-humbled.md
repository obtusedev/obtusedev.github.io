---
title: "humbled"
date: 2022-02-04
draft: false
toc: false
tags:
    - writings
    - ramblings
---

Went through a course for Go and saw a section on Go comments. Here I thought it was easy and that I knew everything there was about comments in Go. `//` and `/**/` inline blocks and block comments.  

I stand corrected and now I understand the depth of comments in Go.
That the comments must end in a period, immediately precede a declaration and start with the name of the item you are documenting.

`godoc` to generate the documentations

```go
// Package route contains app routing logic.
package route

// secretRoute is a string that represents a route that you want hidden.
var secretRoute string

// authenticatedUser returns true if user is logged in
// or false if user is not and an error for everything else.
func authenticatedUser() (bool, error) {
    // code
}
```
