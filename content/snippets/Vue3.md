---
title: "Vue 3"
date: 2022-02-02
draft: false
toc: true
tags:
    - vue
    - snippets
---

Preventing template from rendering:

```html
<style>
    [v-cloak] {
        display: none; /* Prevents {{}} from rendering until fully loaded */
    }
</style>
<div id="app" v-cloak></div>
```
