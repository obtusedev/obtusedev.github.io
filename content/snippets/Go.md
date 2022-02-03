---
title: "Go"
date: 2022-02-02
draft: false
toc: true
tags:
    - Go
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
```
