---
title: "bookmarklets"
date: 2022-02-06
draft: true
toc: true
tags:
    - bookmarklets
    - javascript
    - snippets
---

Archiving current webpage:

```javascript
javascript: (() => {
    window.location.href = `https://archive.md/${window.location}`;
})();
```
