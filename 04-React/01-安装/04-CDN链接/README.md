## CDN 链接

可以通过 CDN 获得 React 和 ReactDOM 的 UMD 版本。

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
```

上述版本仅用于开发环境，不适合用于生产环境。压缩优化后可用于生产的 React 版本可通过如下方式引用：

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
```

如果需要加载指定版本的 react 和 react-dom，可以把 16 替换成所需加载的版本号。

## 为什么要使用 crossorigin 属性?

如果你通过 CDN 的方式引入 React，我们建议你设置 crossorigin 属性：

```html
<script crossorigin src="..."></script>
```

我们同时建议你验证使用的 CDN 是否设置了 Access-Control-Allow-Origin: * HTTP 请求头：

<img src="https://react.docschina.org/static/89baed0a6540f29e954065ce04661048/13ae7/cdn-cors-header.png"  style="width:350px;margin:0 auto" />

这样能在 React 16 及以上的版本中有更好的错误处理体验。