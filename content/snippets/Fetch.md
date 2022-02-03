---
title: "Fetch API"
date: 2022-02-02
draft: false
toc: true
tags:
    - fetch
    - javascript
    - snippets
---

fetch api is used for fetching resources like api calls.  
It was brower only but is now coming to [node](https://github.com/nodejs/node/commit/6ec225392675c92b102d3caad02ee3a157c9d1b7).

fetch returns a [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response) object which then needs to be turned into JSON.

```javascript
console.log(fetch("http://httpbin.org/get")); // Promise
fetch("http://httpbin.org/get").then(res => console.log(res)); // Response object
fetch("http://httpbin.org/get").then(res => res.json()); // returns aother Promise
fetch("http://httpbin.org/get")
    .then(res => res.json())
    .then(data => console.log(data)); // logs data
```

fetch doesn't stop even if it gets a 404 by default. Use `res.ok` to check if request was ok. (200 lv codes)

`fetch(resource, [, options])`

Basic Usage w/ .then .catch:

```javascript
let content = fetch("http://httpbin.org/")
    .then(res => res.json())
    .then(data => console.log(data))
    .catch(err => console.log(err));
```

Basic Usage w/ async await:

```javascript
async function getData(url) {
    const response = await fetch(url);
    return response.json();
}

const data = await getData(url);
```

Checking for 404:

```javascript
fetch("http://httpbin.org/get").then(res => {
    if (res.ok) {
        console.log("SUCCESS");
    } else {
        console.log("FAILED");
    }
});
```

POST data:

```javascript
fetch("http://httpbin.org/get", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify{
        name: "John"
    }
})
// Remember to set the correct header and stringify body to JSON
```

Available options:

```javascript
fetch("http://httpbin.org/get", {
    method: "GET",
    headers: {},
    body: {},
    mode: "cors",
    credentials: "same-origin",
    cache: "no-cache",
    redirect: "follow",
    referrer: "",
    referrerPolicy: "no-referrer",
    integrity: "",
    keepalive: "",
    signal: "",
});
```
