## 目录结构

`Nuxt.js` 的默认应用目录架构提供了良好的代码分层结构，适用于开发或大或小的应用。当然，你也可以根据自己的偏好组织应用代码。

## 目录

### 资源目录

资源目录 `assets` 用于组织未编译的静态资源如 `LESS`、`SASS` 或 `JavaScript`。

### 组件目录

组件目录 `components` 用于组织应用的 `Vue.js` 组件。`Nuxt.js` 不会扩展增强该目录下 `Vue.js` 组件，即这些组件不会像页面组件那样有 `asyncData` 方法的特性。

### 布局目录

布局目录 `layouts` 用于组织应用的布局组件。

若无额外配置，该目录不能被重命名。

### 中间件目录

`middleware` 目录用于存放应用的中间件。


### 页面目录

页面目录 `pages` 用于组织应用的路由及视图。`Nuxt.js` 框架读取该目录下所有的 `.vue` 文件并自动生成对应的路由配置。

若无额外配置，该目录不能被重命名。

### 插件目录

插件目录 `plugins` 用于组织那些需要在 根`vue.js`应用 实例化之前需要运行的 `Javascript` 插件。

### 静态文件目录

静态文件目录 `static` 用于存放应用的静态文件，此类文件不会被 `Nuxt.js` 调用 `Webpack` 进行构建编译处理。服务器启动的时候，该目录下的文件会映射至应用的根路径 `/ `下。

举个例子:` /static/robots.txt` 映射至` /robots.txt`

若无额外配置，该目录不能被重命名。

### `Store` 目录
`store` 目录用于组织应用的 `Vuex` 状态树 文件。 `Nuxt.js` 框架集成了 `Vuex` 状态树 的相关功能配置，在 `store` 目录下创建一个 `index.js` 文件可激活这些配置。

若无额外配置，该目录不能被重命名。

### `nuxt.config.js` 文件

`nuxt.config.js` 文件用于组织 `Nuxt.js` 应用的个性化配置，以便覆盖默认配置。

若无额外配置，该文件不能被重命名。

### `package.json` 文件

`package.json` 文件用于描述应用的依赖关系和对外暴露的脚本接口。

该文件不能被重命名。

### 别名

别名  |  目录 \
`~ 或 @`	  |  `srcDir` \
`~~ 或 @@`	|  `rootDir` 

默认情况下，`srcDir` 和 `rootDir` 相同。

提示: 在您的 `vue` 模板中, 如果你需要引入 `assets` 或者 `static` 目录, 使用 `~/assets/your_image.png` 和 `~/static/your_image.png`方式。
