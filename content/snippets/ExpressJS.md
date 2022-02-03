---
title: "ExpressJS"
date: 2022-02-02
draft: false
toc: true
tags:
    - express
    - javascript
    - snippets
---

App setup:

```javascript
import express from "express";
const app = express();
const port = 3000;

app.get("/", (req, res) => {
    res.send("hi");
});

app.listen(port, () => {
    console.log(`app running on localhost:${port}`);
});
```

Basic route:

```javascript
app.get("/", (req, res) => {
    res.send("hi");
});
```
