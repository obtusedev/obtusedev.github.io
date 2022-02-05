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

Common project structure/folders:

```
src/
    models: What your data looks like
    controllers: seperating routes from logic
    middleware: general purpose middleware
    routes: routes grouping like api/v1, api/v2
    view: templating engine
    public: public files, css, favicon
    configs: configuration files for template engine, db
    assets: images, video
    services: db/business logic? I usually put this in models. This can also be for 3rd party api like stripe, aws
    helper: helper functions
/test
    tests: test for code

```

Some common naming conventions:

```
user.controller.js
user.model.js
user.route.js

// Easier to get confused when both User.js and user.js are open
models/User.js
routes/user.js
controllers/user.js

Models/User.js
Routes/user.js
Controllers/user.js
```

Middleware are functions that runs when specific route is called.  
Some common middleware is authentication, logging, validating uploads.
The order of your middlware is very important.

The difference between Controllers and Middlewares from my understanding is that a controller is a middleware for a single route and middleware is for several routes. Middlewares are called before your route controllers.

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
// for Content-Type: application/json body req and res
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false })); // extended true if you are using qs module

// https://github.com/expressjs/express/releases/tag/4.16.0
// express v4.16.0 and newer
// for query strings aka ?key=value&name=john
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

Routing for larger applications:

routes/user.js

```javascript
import express from "express";
const router = express.Router();

// matches /user/
router.get("/", (req, res) => {});

export default router;
```

server.js

```javascript
import express from "express";
import userRoutes from "./route/user.js";

// /user not prefixes all routes in userRoutes
app.use("/user", userRoutes);
```

Ways of using middlewares in routes other than `app.use()`:

```javascript
// app.get("/login", authUser, login);
app.get(path, middleware, middleware2);
app.get(path, [array of middlewares], middleware);
// next() is important when using multiple middlewares
```

`next()` in middleware:

```javascript
// next hands off the req to the next middleware
// next is just a convention name
// next is not the same as return

// middleware site wide
app.use(function(req, res, next) => {
    console.log("Logged", req.method);
    next(); // without this the req will hang bc it doesn't know what to do next
})

app.get("/", (req, res, next) => {
    // you can have next but it is rarely needed
    // since this controller is usually the last middleware
})
```

Run middleware after every request/route:

```javascript
app.use(logger);

app.get("/user", (req, res) => {});

// run **after** every request/route
function logger(req, res, next) {
    next();
    console.log("LOGGED");
}
```
