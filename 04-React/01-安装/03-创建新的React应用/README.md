## 创建新的 React 应用

 使用集成的工具链，以实现最佳的用户和开发人员体验。
 
 本页将介绍一些流行的 React 工具链，它们有助于完成如下任务：
 
 - 扩展文件和组件的规模。
 - 使用来自 npm 的第三方库。
 - 尽早发现常见错误。
 - 在开发中实时编辑 CSS 和 JS。
 - 优化生产输出。
 - 本页推荐的工具链无需配置即可开始使用。

## 你可能不需要工具链

如果你没有碰到上述的问题，或者还不习惯使用 JavaScript 工具，可以考虑把 React 作为普通的 <code>script</code> 标记添加到 HTML 页面上，以及使用可选的 JSX。

这也是将 React 集成到现有网站最简单的方式。如果你认为更大的工具链有所帮助，可以随时添加！

## 推荐的工具链

React 团队主要推荐这些解决方案：

- 如果你是在学习 React 或创建一个新的单页应用，请使用 [Create React App](https://react.docschina.org/docs/create-a-new-react-app.html#create-react-app)。\
- 如果你是在用 Node.js 构建服务端渲染的网站，试试 [Next.js](https://react.docschina.org/docs/create-a-new-react-app.html#nextjs)。\
- 如果你是在构建面向内容的静态网站，试试 [Gatsby](https://react.docschina.org/docs/create-a-new-react-app.html#gatsby)。\
- 如果你是在打造组件库或将 React 集成到现有代码仓库，尝试更灵活的工具链[更灵活的工具链](https://react.docschina.org/docs/create-a-new-react-app.html#more-flexible-toolchains)。

## Create React App

Create React App 是一个用于学习 React 的舒适环境，也是用 React 创建新的单页应用的最佳方式。

它会配置你的开发环境，以便使你能够使用最新的 JavaScript 特性，提供良好的开发体验，并为生产环境优化你的应用程序。你需要在你的机器上安装 Node >= 8.10 和 npm >= 5.6。要创建项目，请执行：

```bash
npx create-react-app my-app
cd my-app
npm start
```

>注意\
>第一行的 npx 不是拼写错误 —— 它是 npm 5.2+ 附带的 package 运行工具。

Create React App 不会处理后端逻辑或操纵数据库；它只是创建一个前端构建流水线（build pipeline），所以你可以使用它来配合任何你想使用的后端。它在内部使用 Babel 和 webpack，但你无需了解它们的任何细节。

当你准备好部署到生产环境时，执行 npm run build 会在 build 文件夹内生成你应用的优化版本。你能从它的 README 和用户指南了解 Create React App 的更多信息。

## Next.js

[Next.js](https://nextjs.org/) 是一个流行的、轻量级的框架，用于配合 React 打造静态化和服务端渲染应用。它包括开箱即用的样式和路由方案，并且假定你使用 [Node.js](https://nodejs.org/) 作为服务器环境。

从 [Next.js](https://nextjs.org/learn/)的官方指南了解更多。

## Gatsby

[Gatsby](https://www.gatsbyjs.org/) 是用 React 创建静态网站的最佳方式。它让你能使用 React 组件，但输出预渲染的 HTML 和 CSS 以保证最快的加载速度。

从 Gatsby 的[官方指南 ](https://www.gatsbyjs.org/docs/)和[入门示例集](https://www.gatsbyjs.org/docs/gatsby-starters/)了解更多。

## 更灵活的工具链

以下工具链为 React 提供更多更具灵活性的方案。推荐给更有经验的使用者：

- [Neutrino](https://neutrinojs.org/) 把 webpack 的强大功能和简单预设结合在一起。并且包括了 React 应用和 React 组件的预设。
- [Parcel](https://parceljs.org/) 是一个快速的、零配置的网页应用打包器，并且可以搭配 React 一起工作。
- [Razzle](https://github.com/jaredpalmer/razzle) 是一个无需配置的服务端渲染框架，但它提供了比 Next.js 更多的灵活性。

## 从头开始打造工具链

一组 JavaScript 构建工具链通常由这些组成

一组 JavaScript 构建工具链通常由这些组成：

- 一个 package 管理器，比如 Yarn 或 npm。它能让你充分利用庞大的第三方 package 的生态系统，并且轻松地安装或更新它们。
- 一个打包器，比如 webpack 或 Parcel。它能让你编写模块化代码，并将它们组合在一起成为小的 package，以优化加载时间。
- 一个编译器，例如 Babel。它能让你编写的新版本 JavaScript 代码，在旧版浏览器中依然能够工作。
如果你倾向于从头开始打造你自己的 JavaScript 工具链，可以查看[这个指南](https://blog.usejournal.com/creating-a-react-app-from-scratch-f3c693b84658)，它重新创建了一些 Create React App 的功能。

别忘了确保你自定义的工具链针对[生产环境进行了正确配置](https://react.docschina.org/docs/optimizing-performance.html#use-the-production-build)。

