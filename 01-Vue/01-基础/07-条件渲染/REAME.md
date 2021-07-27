## 条件渲染

## v-if
`v-if `指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 `truthy` 值的时候被渲染。
```html
<h1 v-if="awesome">Vue is awesome!</h1>
```
也可以用 `v-else `添加一个“else 块”：
```html
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```
## 在 `<template> `元素上使用 `v-if` 条件渲染分组
因为 `v-if `是一个指令，所以必须将它添加到一个元素上。但是如果想切换多个元素呢？此时可以把一个 `<template> `元素当做不可见的包裹元素，并在上面使用` v-if`。最终的渲染结果将不包含` <template>` 元素。

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```
## v-else
你可以使用 `v-else `指令来表示` v-if `的“else 块”：
```html
<div v-if="Math.random() > 0.5">
  Now you see me
</div>
<div v-else>
  Now you don't
</div>
```
`v-else` 元素必须紧跟在带` v-if` 或者 `v-else-if `的元素的后面，否则它将不会被识别。
