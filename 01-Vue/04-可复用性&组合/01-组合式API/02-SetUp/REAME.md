## Setup

## 参数

使用 `setup` 函数时，它将接收两个参数：

- props
- context

让我们更深入地研究如何使用每个参数。

## Props

`setup` 函数中的第一个参数是 `props`。正如在一个标准组件中所期望的那样，`setup` 函数中的 `props` 是响应式的，当传入新的 `prop` 时，它将被更新。

```js
// MyBook.vue

export default {
  props: {
    title: String
  },
  setup(props) {
    console.log(props.title)
  }
}
```
>!WARNING 
> 但是，因为 props 是响应式的，你不能使用 ES6 解构，它会消除 prop 的响应性。
