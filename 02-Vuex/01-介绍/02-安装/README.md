# 安装
## 直接下载 / CDN 引用

https://unpkg.com/vuex(opens new window)

Unpkg.com (opens new window)提供了基于 NPM 的 CDN 链接。以上的链接会一直指向 NPM 上发布的最新版本。您也可以通过 https://unpkg.com/vuex@2.0.0 这样的方式指定特定的版本。

在 Vue 之后引入 vuex 会进行自动安装：

```js
<script src="/path/to/vue.js"></script>
<script src="/path/to/vuex.js"></script>
```

## NPM
```js
npm install vuex --save
```

## Yarn
```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
```

## Promise

Vuex 依赖 Promise (opens new window)。如果你支持的浏览器并没有实现 Promise (比如 IE)，那么你可以使用一个 polyfill 的库，例如 es6-promise (opens new window)。

你可以通过 CDN 将其引入：

```html 
<script src="https://cdn.jsdelivr.net/npm/es6-promise@4/dist/es6-promise.auto.js"></script>

```

然后 window.Promise 会自动可用。

如果你喜欢使用诸如 npm 或 Yarn 等包管理器，可以按照下列方式执行安装：

```sh
npm install es6-promise --save # npm
yarn add es6-promise # Yarn

```

或者更进一步，将下列代码添加到你使用 Vuex 之前的一个地方：

```js
import 'es6-promise/auto'
```

## 自己构建

如果需要使用 dev 分支下的最新版本，您可以直接从 GitHub 上克隆代码并自己构建。

```sh
git clone https://github.com/vuejs/vuex.git node_modules/vuex
cd node_modules/vuex
npm install
npm run build
```

