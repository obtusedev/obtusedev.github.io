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

Vue 3 setup in script:

```html
<script src="https://unpkg.com/vue@next"></script>
<script>
    let app = Vue.createApp({
        data() {
            return {

            }
        }
    })
    app.mount("#app")
<script>
```

`v-show` vs `v-if`:
`v-show` renders but sets `display: none;` while `v-if` doesn't render at all.  
`v-show` is better if you are toggling a component frequently as it is more performant.

Shorthand:

```
v-on:click -> @click
v-bind:class -> :class
```

Vue directives are refering to `v-if`, `v-else-if`, `v-else`, `v-for`, `v-model` and more.

Chaining directives:

```
@click.prevent.stop
```

Binding class/styles:

```
class="button"
:class="toggle"
:class="{ button: true, toggle }"
:class="[isActive ? activeClass : '']"
:class="{ camelCase: true }"
:class="{ 'kebab-case': true }"
```
