## 模板引用

尽管存在 `prop` 和事件，但有时你可能仍然需要直接访问 `JavaScript` 中的子组件。为此，可以使用 `ref` attribute 为子组件或 `HTML` 元素指定引用 `ID`。例如：

```html
<input ref="input" />
```

例如，你希望在组件挂载时，以编程的方式 `focus` 到这个 `input` 上，这可能有用
