---
title: "Vue 3"
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
