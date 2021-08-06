##  安装

`Nuxt.js` 十分简单易用。一个简单的项目只需将 `nuxt` 添加为依赖组件即可。

## 运行 create-nuxt-app

为了快速入门，`Nuxt.js` 团队创建了脚手架工具 `create-nuxt-app`。

确保安装了 `npx`（`npx` 在 `NPM` 版本 `5.2.0` 默认安装了）：

```bash
$ npx create-nuxt-app <项目名>
```

或者用 yarn ：

```bash
$ yarn create nuxt-app <项目名>
```

它会让你进行一些选择:

在集成的服务器端框架之间进行选择:

`None` (Nuxt 默认服务器)
`Express`
`Koa`
`Hapi`
`Feathers`
`Micro`
`Fastify`
`Adonis (WIP)`

选择您喜欢的 UI 框架:

`None` (无)
`Bootstrap`
`Vuetify`
`Bulma`
`Tailwind`
`Element UI`
`Ant Design Vue`
`Buefy`
`iView`
`Tachyons`

选择您喜欢的测试框架:

`None` (随意添加一个)
`Jest`
`AVA`

选择你想要的 `Nuxt` 模式 (`Universal` or `SPA`)

添加 `axios module` 以轻松地将 `HTTP` 请求发送到您的应用程序中。

添加 `EsLint` 以在保存时代码规范和错误检查您的代码。

添加 `Prettier` 以在保存时格式化/美化您的代码。

当运行完时，它将安装所有依赖项，因此下一步是启动项目:

```bash
$ cd <project-name>
$ npm run dev
```
应用现在运行在` http://localhost:3000 `上运行。

注意：`Nuxt.js` 会监听 `pages` 目录中的文件更改，因此在添加新页面时无需重新启动应用程序。

了解模板项目的目录结构： 目录结构。

从头开始新建项目
如果不使用 `Nuxt.js` 提供的 `starter` 模板，我们也可以从头开始新建一个 `Nuxt.js` 应用项目，过程非常简单，只需要 1 个文件和 1 个目录。如下所示：

$ `mkdir` <项目名>
$ `cd` <项目名>
>提示: 将 <项目名> 替换成为你想创建的实际项目名。

新建 `package.json` 文件
`package.json` 文件用来设定如何运行 `nuxt`：

```json
{
"name": "my-app",
"scripts": {
    "dev": "nuxt"
  }
}
```
上面的配置使得我们可以通过运行 `npm run dev` 来运行 `nuxt`。

## 安装 `nuxt`
一旦 `package.json` 创建好， 可以通过以下 `npm` 命令将 `nuxt` 安装至项目中：

```shell
$ npm install --save nuxt
```
## `pages` 目录

`Nuxt.js` 会依据 `pages` 目录中的所有` *.vue `文件生成应用的路由配置。

## 创建 `pages` 目录：

```shell
$ mkdir pages
```
创建我们的第一个页面 `pages/index.vue`：

```vue
<template>
  <h1>Hello world!</h1>
</template>
```
然后启动项目：

```shell
$ npm run dev
```
现在我们的应用运行在 `http://localhost:3000` 上运行。

注意：`Nuxt.js` 会监听 `pages` 目录中的文件更改，因此在添加新页面时无需重新启动应用程序。

了解更多关于 `Nuxt.js` 应用的目录结构： 目录结构。

DISCOVER
Design resources
A worldwide team
Blog
