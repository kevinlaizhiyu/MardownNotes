## 视图

本章节的内容阐述了如何在 `Nuxt.js` 应用中为指定的路由配置数据和视图，包括应用模板、页面、布局和 `HTML` 头部等内容。

<img src="https://www.nuxtjs.cn/nuxt-views-schema.svg" />

## 模板

你可以定制化` Nuxt.js `默认的应用模板。

定制化默认的 `html` 模板，只需要在 `src` 文件夹下（默认是应用根目录）创建一个 `app.html` 的文件。

默认模板为：

```html
<!DOCTYPE html>
<html {{ HTML_ATTRS }}>
  <head {{ HEAD_ATTRS }}>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
    {{ APP }}
  </body>
</html>
```
举个例子，你可以修改模板添加 IE 的条件表达式：

```html
<!DOCTYPE html>
<!--[if IE 9]><html lang="en-US" class="lt-ie9 ie9" {{ HTML_ATTRS }}><![endif]-->
<!--[if (gt IE 9)|!(IE)]><!--><html {{ HTML_ATTRS }}><!--<![endif]-->
  <head {{ HEAD_ATTRS }}>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
    {{ APP }}
  </body>
</html>
```

## 布局

`Nuxt.js` 允许你扩展默认的布局，或在 `layout` 目录下创建自定义的布局。

## 默认布局

可通过添加 `layouts/default.vue` 文件来扩展应用的默认布局。

默认布局的源码如下：

```html
<template>
  <nuxt />
</template>
```

## 自定义布局

`layouts` 目录中的每个文件 (顶级) 都将创建一个可通过页面组件中的 `layout` 属性访问的自定义布局。

假设我们要创建一个 博客布局 并将其保存到`layouts/blog.vue`:

```html
<template>
  <div>
    <div>我的博客导航栏在这里</div>
    <nuxt />
  </div>
</template>
```
然后我们必须告诉页面 (即`pages/posts.vue`) 使用您的自定义布局：

```vue
<template>
  <!-- Your template -->
</template>
<script>
export default {
  layout: 'blog'
  // page component definitions
}
</script>
```

更多有关 `layout` 属性信息: [API 页面 布局](https://www.nuxtjs.cn/api/pages-layout)
 
## 错误页面

你可以通过编辑 `layouts/error.vue `文件来定制化错误页面.

警告: 虽然此文件放在 `layouts` 文件夹中, 但应该将它看作是一个 页面(`page`).

这个布局文件不需要包含` <nuxt/> `标签。你可以把这个布局文件当成是显示应用错误（`404`，`500` 等）的组件。

默认的错误页面源码在 [这里](https://github.com/nuxt/nuxt.js/blob/dev/packages/vue-app/template/components/nuxt-error.vue).

举一个个性化错误页面的例子 `layouts/error.vue`:

```vue
<template>
  <div class="container">
    <h1 v-if="error.statusCode === 404">页面不存在</h1>
    <h1 v-else>应用发生错误异常</h1>
    <nuxt-link to="/">首 页</nuxt-link>
  </div>
</template>

<script>
  export default {
    props: ['error'],
    layout: 'blog' // 你可以为错误页面指定自定义的布局
  }
</script>
```

## 页面

页面组件实际上是 `Vue` 组件，只不过 `Nuxt.js` 为这些组件添加了一些特殊的配置项（对应 `Nuxt.js` 提供的功能特性）以便你能快速开发通用应用。

```vue
<template>
  <h1 class="red">Hello {{ name }}!</h1>
</template>

<script>
  export default {
    asyncData (context) {
      // called every time before loading the component
      return { name: 'World' }
    },
    fetch () {
      // The fetch method is used to fill the store before rendering the page
    },
    head () {
      // Set Meta Tags for this Page
    },
    // and more functionality to discover
    ...
  }
</script>

<style>
  .red {
    color: red;
  }
</style>
```
`Nuxt.js` 为页面提供的特殊配置项：

<table data-v-421769f2=""><thead data-v-421769f2=""><tr data-v-421769f2=""><th data-v-421769f2="">属性名</th><th data-v-421769f2="">描述</th></tr></thead><tbody data-v-421769f2=""><tr data-v-421769f2=""><td data-v-421769f2="">asyncData</td><td data-v-421769f2="">最重要的一个键, 支持 <a data-v-421769f2="" href="/guide/async-data" class="">异步数据处理</a>，另外该方法的第一个参数为当前页面组件的 <a data-v-421769f2="" href="/api#%E4%B8%8A%E4%B8%8B%E6%96%87%E5%AF%B9%E8%B1%A1" class="">上下文对象</a>。</td></tr><tr data-v-421769f2=""><td data-v-421769f2="">fetch</td><td data-v-421769f2="">与 <code data-v-421769f2="">asyncData</code> 方法类似，用于在渲染页面之前获取数据填充应用的状态树（store）。不同的是 <code data-v-421769f2="">fetch</code> 方法不会设置组件的数据。详情请参考 <a data-v-421769f2="" href="/api/pages-fetch" class="">关于 fetch 方法的文档</a>。</td></tr><tr data-v-421769f2=""><td data-v-421769f2="">head</td><td data-v-421769f2="">配置当前页面的 Meta 标签, 详情参考 <a data-v-421769f2="" href="/api/pages-head" class="">页面头部配置 API</a>。</td></tr><tr data-v-421769f2=""><td data-v-421769f2="">layout</td><td data-v-421769f2="">指定当前页面使用的布局（<code data-v-421769f2="">layouts</code> 根目录下的布局文件）。详情请参考 <a data-v-421769f2="" href="/api/pages-layout" class="">关于 布局 的文档</a>。</td></tr><tr data-v-421769f2=""><td data-v-421769f2="">loading</td><td data-v-421769f2="">如果设置为<code data-v-421769f2="">false</code>，则阻止页面自动调用<code data-v-421769f2="">this.$nuxt.$loading.finish()</code>和<code data-v-421769f2="">this.$nuxt.$loading.start()</code>,您可以手动控制它,请看<a data-v-421769f2="" href="https://nuxtjs.org/examples/custom-page-loading" rel="nofollow noopener noreferrer" target="_blank">例子</a>,仅适用于在 nuxt.config.js 中设置<code data-v-421769f2="">loading</code>的情况下。请参考<a data-v-421769f2="" href="/api/configuration-loading" class="">API 配置 <code data-v-421769f2="">loading</code> 文档</a>。</td></tr><tr data-v-421769f2=""><td data-v-421769f2="">transition</td><td data-v-421769f2="">指定页面切换的过渡动效, 详情请参考 <a data-v-421769f2="" href="/api/pages-transition" class="">页面过渡动效</a>。</td></tr><tr data-v-421769f2=""><td data-v-421769f2="">scrollToTop</td><td data-v-421769f2="">布尔值，默认: <code data-v-421769f2="">false</code>。 用于判定渲染页面前是否需要将当前页面滚动至顶部。这个配置用于 <a data-v-421769f2="" href="/guide/routing#%E5%B5%8C%E5%A5%97%E8%B7%AF%E7%94%B1" class="">嵌套路由</a>的应用场景。</td></tr><tr data-v-421769f2=""><td data-v-421769f2="">validate</td><td data-v-421769f2="">校验方法用于校验 <a data-v-421769f2="" href="/guide/routing#%E5%8A%A8%E6%80%81%E8%B7%AF%E7%94%B1" class="">动态路由</a>的参数。</td></tr><tr data-v-421769f2=""><td data-v-421769f2="">middleware</td><td data-v-421769f2="">指定页面的中间件，中间件会在页面渲染之前被调用， 请参考 <a data-v-421769f2="" href="/guide/routing#%E4%B8%AD%E9%97%B4%E4%BB%B6" class="">路由中间件</a>。</td></tr></tbody></table>

## HTML 头部

`Nuxt.js` 使用了 `vue-meta` 更新应用的 头部标签(`Head`) and `html` 属性。

`Nuxt.js` 使用以下参数配置` vue-meta`:

```js
{
  keyName: 'head', // 设置 meta 信息的组件对象的字段，vue-meta 会根据这 key 值获取 meta 信息
  attribute: 'n-head', // vue-meta 在监听标签时所添加的属性名
  ssrAttribute: 'n-head-ssr', // 让 vue-meta 获知 meta 信息已完成服务端渲染的属性名
  tagIDKeyName: 'hid' // 让 vue-meta 用来决定是否覆盖还是追加 tag 的属性名
}
```

## 默认 `Meta` 标签

`Nuxt.js` 允许你在 `nuxt.config.js` 里定义应用所需的所有默认 `meta` 标签，在 `head` 字段里配置就可以了：

注意: `Nuxt.js` 使用 `hid` 而不是默认值 `vmid` 识别元素 `key`

一个使用自定义 `viewport` 和 谷歌字体 的配置示例：

```js
head: {
  meta: [
    { charset: 'utf-8' },
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css?family=Roboto' }
  ]
}
```
想了解 `head` 变量的所有可选项的话，请查阅 `vue-meta` 使用文档。

关于 `Nuxt.js` 应用 `HTML` 头部配置的更多信息，请参考 `HTML` 头部配置 `API`。

个性化特定页面的 `Meta` 标签

关于个性化特定页面的 `Meta` 标签，请参考 页面头部配置 `API`。

>注意: 为了避免子组件中的 `meta` 标签不能正确覆盖父组件中相同的标签而产生重复的现象，建议利用 `hid` 键为 `meta` 标签配一个唯一的标识编号。请阅读关于 `vue-meta` 的更多信息。













