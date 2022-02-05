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

Controllers and Middleware: from my understanding a controller is a middleware for a single route and middleware is for several routes. The order of your middlware is very important.

```javascript
// middleware
app.use(express.json());
// controller
app.get("/user/:id", getSingleUserById);
```

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

Importing routes:

```javascript
const userRoute = require("./route/user.js");
app.use("/user", userRoute);
// shortcut without the import statement in beginning
app.use("/user", require("./route/user.js"));
```

`express.json()` and `express.urlencoded()` is only needed for `POST` and `PUT` requests where you need to parse json body data.

```javascript
// npm install body-parser
// express v4.15.0 and older
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false })); // extended true if you are using qs module

// https://github.com/expressjs/express/releases/tag/4.16.0
// express v4.16.0 and newer
app.use(express.json());
app.use(express.urlencoded({ extended: false })); // extended true if you are using qs module
```

Setting environment variables in `package.json`:

```json
"scripts": {
    "dev": "NODE_ENV=development nodemon app.js",
    "prod": "NODE_ENV=production LOGGING=off nodemon app.js"
}
```

Global variables `__dirname` & `__filename`:

```javascript
// CommonJS

let file = __filename;
let here = __dirname;
```

```javascript
// ES6
import { fileURLToPath } from "url";
import path from "path";

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);
```
