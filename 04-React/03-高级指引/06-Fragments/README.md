## Fragments

>React 中的一个常见模式是一个组件返回多个元素。Fragments 允许你将子列表分组，而无需向 DOM 添加额外节点。

```js
render() {
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  );
}
```

还有一种新的[短语法](https://react.docschina.org/docs/fragments.html#short-syntax)可用于声明它们。

## 动机

一种常见模式是组件返回一个子元素列表。以此 React 代码片段为例：

```js
class Table extends React.Component {
  render() {
    return (
      <table>
        <tr>
          <Columns />
        </tr>
      </table>
    );
  }
}
```

<code>Columns</code> 需要返回多个 <code>td</code> 元素以使渲染的 HTML 有效。如果在<code>Columns</code>的 render() 中使用了父 div，则生成的 HTML 将无效。

```js
class Columns extends React.Component {
  render() {
    return (
      <div>
        <td>Hello</td>
        <td>World</td>
      </div>
    );
  }
}
```
得到一个 <code>Table</code> 输出：
```js
<table>
  <tr>
    <div>
      <td>Hello</td>
      <td>World</td>
    </div>
  </tr>
</table>
```
Fragments 解决了这个问题。

## 用法

```js
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Hello</td>
        <td>World</td>
      </React.Fragment>
    );
  }
}
```
这样可以正确的输出 <code>Table</code>：

```js
<table>
  <tr>
    <td>Hello</td>
    <td>World</td>
  </tr>
</table>

```

## 短语法

你可以使用一种新的，且更简短的语法来声明 Fragments。它看起来像空标签:

```js
class Columns extends React.Component {
  render() {
    return (
      <>
        <td>Hello</td>
        <td>World</td>
      </>
    );
  }
}
```

你可以像使用任何其他元素一样使用 `<> </>`，除了它不支持 key 或属性。

带 key 的 Fragments

使用显式 <code>React.Fragment</code> 语法声明的片段可能具有 key。一个使用场景是将一个集合映射到一个 Fragments 数组 - 举个例子，创建一个描述列表：


