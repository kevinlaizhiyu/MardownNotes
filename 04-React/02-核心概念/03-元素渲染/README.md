## 元素渲染

元素是构成 React 应用的最小砖块。

元素描述了你在屏幕上想看到的内容。

```js
const element = <h1>Hello, world</h1>;
```

与浏览器的 DOM 元素不同，React 元素是创建开销极小的普通对象。React DOM 会负责更新 DOM 来与 React 元素保持一致。

>注意：\
> 你可能会将元素与另一个被熟知的概念——“组件”混淆起来。我们会在下一个章节介绍组件。组件是由元素构成的。我们强烈建议你不要觉得繁琐而跳过本章节，应当深入阅读这一章节。

## 将一个元素渲染为 DOM

假设你的 HTML 文件某处有一个 <code>div</code>：

```html
<div id="root"></div>
```

我们将其称为“根” DOM 节点，因为该节点内的所有内容都将由 React DOM 管理

仅使用 React 构建的应用通常只有单一的根 DOM 节点。如果你在将 React 集成进一个已有应用，那么你可以在应用中包含任意多的独立根 DOM 节点。

想要将一个 React 元素渲染到根 DOM 节点中，只需把它们一起传入 ReactDOM.render()：

```js
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

[在 CodePen 上尝试](https://react.docschina.org/redirect-to-codepen/rendering-elements/render-an-element)

页面上会展示出 “Hello, world”。

## 更新已渲染的元素

React 元素是不可变对象。一旦被创建，你就无法更改它的子元素或者属性。一个元素就像电影的单帧：它代表了某个特定时刻的 UI。

根据我们已有的知识，更新 UI 唯一的方式是创建一个全新的元素，并将其传入 ReactDOM.render()。

考虑一个计时器的例子：

```js
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```

[在 CodePen 上尝试](https://react.docschina.org/redirect-to-codepen/rendering-elements/update-rendered-element)

这个例子会在 setInterval() 回调函数，每秒都调用 ReactDOM.render()。

>注意：\
>在实践中，大多数 React 应用只会调用一次 ReactDOM.render()。在下一个章节，我们将学习如何将这些代码封装到有状态组件中。
>我们建议你不要跳跃着阅读，因为每个话题都是紧密联系的。

## React 只更新它需要更新的部分

React DOM 会将元素和它的子元素与它们之前的状态进行比较，并只会进行必要的更新来使 DOM 达到预期的状态。

你可以使用浏览器的检查元素工具查看上一个例子来确认这一点

<img src="https://react.docschina.org/c158617ed7cc0eac8f58330e49e48224/granular-dom-updates.gif" style="width:286px;height:auto;margin:0 auto" />

尽管每一秒我们都会新建一个描述整个 UI 树的元素，React DOM 只会更新实际改变了的内容，也就是例子中的文本节点。

根据我们的经验，考虑 UI 在任意给定时刻的状态，而不是随时间变化的过程，能够消灭一整类的 bug。

