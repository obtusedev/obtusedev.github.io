---
title: JavaScript
---

Self executing function:

```javascript
(async function () {
    const res = await fetch("http://httpbin.org/get");
})(); // () can also be inside next to }
```

`typeof` for undefined:

```javascript
console.log(typeof undef); // "undefined" is returned in quotes so be sure not to === undefined
```

Encoding strings safely for urls

```javascript
let url = "test?";
encodeURIComponent(url); //=> 'test%3F'
```
