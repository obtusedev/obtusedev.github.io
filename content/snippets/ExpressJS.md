---
title: "ExpressJS"
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
