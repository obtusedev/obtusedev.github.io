---
title: "CORS - Cross-Origin Resource Sharing"
date: "2022-02-09"
draft: false
toc: true
featuredImg:
images:
tags:
    - CORS
    - express
    - http
---

Examples of `same origin request`
foo.com requesting image on foo.com domain

Examples of `cross origin request`

foo.com fetching data from bar.com
localhost:3000 fetching data from server no localhost:5000

might give a CORS error

SAME-ORIGIN POLICY - browser security

foo.com can get images from foo.com but not from other domains like bar.com

When you make a request there is the Origin header which might look like `Origin: foo.com`

Access-Control-Allow-Origin header needs to match Origin header or '\*' wildcard to match any domain in order to get permission

configuring CORS is done on the server

expressjs example

```javascript
const express = require("express");
const app = express();
const cors = require("cors");

// include CORS headers in every response
app.use(cors({ origin: "https://foo.com" })); // Access-Control-Allow-Origin: http://localhost:5000

// you can also just do
app.use(cors());

app.get("/", (req, res) => {
    res.status(200).json({ title: "hello world" });
});
```

`Access-Control-Max-Age` header for caching permission during 'preflight'

Steps:

1. Browser sends a 'preflight' check with Options HTTP verb with Origin header
2. Server responds with either
    1. yes the origin can make request with the following options. Then the request is made.
        - this may sound inefficient but the server can respond with Access-Control-Max-Age header that lets the browser cache the preflight for certain amount of time.
    2. CORS error.

If you are getting CORS errors then open dev tools and check for 'Access-Control-Allow-Origin' headers.
If it doesn't exists then you need to enable CORS on server.
If it does then you may have mismatch url or those methods are not allowed.
