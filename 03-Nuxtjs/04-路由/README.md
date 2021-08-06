## 路由

`Nuxt.js `依据 `pages` 目录结构自动生成 `vue-router` 模块的路由配置。

> 要在页面之间使用路由，我们建议使用` <nuxt-link> `标签。

```html
<template>
  <nuxt-link to="/">首页</nuxt-link>
</template>
```

## 基础路由

假设 `pages` 的目录结构如下：

```text
pages/
--| user/
-----| index.vue
-----| one.vue
--| index.vue
```

那么，`Nuxt.js` 自动生成的路由配置如下：

```js
router: {
  routes: [
    {
      name: 'index',
      path: '/',
      component: 'pages/index.vue'
    },
    {
      name: 'user',
      path: '/user',
      component: 'pages/user/index.vue'
    },
    {
      name: 'user-one',
      path: '/user/one',
      component: 'pages/user/one.vue'
    }
  ]
}
```

### 动态路由

在` Nuxt.js `里面定义带参数的动态路由，需要创建对应的以下划线作为前缀的 `Vue` 文件 或 目录。

以下目录结构：

````text
pages/
--| _slug/
-----| comments.vue
-----| index.vue
--| users/
-----| _id.vue
--| index.vue

````
`Nuxt.js` 生成对应的路由配置表为：

```js
router: {
  routes: [
    {
      name: 'index',
      path: '/',
      component: 'pages/index.vue'
    },
    {
      name: 'users-id',
      path: '/users/:id?',
      component: 'pages/users/_id.vue'
    },
    {
      name: 'slug',
      path: '/:slug',
      component: 'pages/_slug/index.vue'
    },
    {
      name: 'slug-comments',
      path: '/:slug/comments',
      component: 'pages/_slug/comments.vue'
    }
  ]
}

```
你会发现名称为 `users-id` 的路由路径带有 `:id?` 参数，表示该路由是可选的。如果你想将它设置为必选的路由，需要在 `users/_id` 目录内创建一个 `index.vue` 文件。

：API Configuration generate

>! 警告：`generate` 命令会忽略动态路由: `API Configuration generate`

## 路由参数校验

`Nuxt.js` 可以让你在动态路由组件中定义参数校验方法。

举个例子： `pages/users/_id.vue`

```js
export default {
  validate({ params }) {
    // 必须是number类型
    return /^\d+$/.test(params.id)
  }
}
```

如果校验方法返回的值不为 `true` 或 `Promise` 中 `resolve` 解析为 `false` 或抛出 `Error` ，` Nuxt.js` 将自动加载显示 `404` 错误页面或 `500` 错误页面。

想了解关于路由参数校验的信息，请参考 页面校验 API。

## 嵌套路由

你可以通过` vue-router `的子路由创建` Nuxt.js `应用的嵌套路由。

创建内嵌子路由，你需要添加一个 `Vue` 文件，同时添加一个与该文件同名的目录用来存放子视图组件。

>! Warning: 别忘了在父组件(.vue文件) 内增加 `<nuxt-child/>` 用于显示子视图内容。

假设文件结构如

```text
pages/
--| users/
-----| _id.vue
-----| index.vue
--| users.vue
```

`Nuxt.js` 自动生成的路由配置如下：

```js
router: {
  routes: [
    {
      path: '/users',
      component: 'pages/users.vue',
      children: [
        {
          path: '',
          component: 'pages/users/index.vue',
          name: 'users'
        },
        {
          path: ':id',
          component: 'pages/users/_id.vue',
          name: 'users-id'
        }
      ]
    }
  ]
}
```

## 动态嵌套路由

这个应用场景比较少见，但是 `Nuxt.js` 仍然支持：在动态路由下配置动态子路由。

假设文件结构如下：

```text
pages/
--| _category/
-----| _subCategory/
--------| _id.vue
--------| index.vue
-----| _subCategory.vue
-----| index.vue
--| _category.vue
--| index.vue
```

`Nuxt.js` 自动生成的路由配置如下：
```js
router: {
  routes: [
    {
      path: '/',
      component: 'pages/index.vue',
      name: 'index'
    },
    {
      path: '/:category',
      component: 'pages/_category.vue',
      children: [
        {
          path: '',
          component: 'pages/_category/index.vue',
          name: 'category'
        },
        {
          path: ':subCategory',
          component: 'pages/_category/_subCategory.vue',
          children: [
            {
              path: '',
              component: 'pages/_category/_subCategory/index.vue',
              name: 'category-subCategory'
            },
            {
              path: ':id',
              component: 'pages/_category/_subCategory/_id.vue',
              name: 'category-subCategory-id'
            }
          ]
        }
      ]
    }
  ]
}
```
## 未知嵌套深度的动态嵌套路由

如果您不知道 `URL` 结构的深度，您可以使用`_.vue`动态匹配嵌套路径。这将处理与更具体请求不匹配的情况。

文件结构:

```text
pages/
--| people/
-----| _id.vue
-----| index.vue
--| _.vue
--| index.vue
```
将处理这样的请求：
<table data-v-421769f2=""><thead data-v-421769f2=""><tr data-v-421769f2=""><th data-v-421769f2="">Path</th><th data-v-421769f2="">File</th></tr></thead><tbody data-v-421769f2=""><tr data-v-421769f2=""><td data-v-421769f2=""><code data-v-421769f2="">/</code></td><td data-v-421769f2=""><code data-v-421769f2="">index.vue</code></td></tr><tr data-v-421769f2=""><td data-v-421769f2=""><code data-v-421769f2="">/people</code></td><td data-v-421769f2=""><code data-v-421769f2="">people/index.vue</code></td></tr><tr data-v-421769f2=""><td data-v-421769f2=""><code data-v-421769f2="">/people/123</code></td><td data-v-421769f2=""><code data-v-421769f2="">people/_id.vue</code></td></tr><tr data-v-421769f2=""><td data-v-421769f2=""><code data-v-421769f2="">/about</code></td><td data-v-421769f2=""><code data-v-421769f2="">_.vue</code></td></tr><tr data-v-421769f2=""><td data-v-421769f2=""><code data-v-421769f2="">/about/careers</code></td><td data-v-421769f2=""><code data-v-421769f2="">_.vue</code></td></tr><tr data-v-421769f2=""><td data-v-421769f2=""><code data-v-421769f2="">/about/careers/chicago</code></td><td data-v-421769f2=""><code data-v-421769f2="">_.vue</code></td></tr></tbody></table>

Note: 处理 404 页面，现在符合_.vue页面的逻辑。 [有关 404 重定向的更多信息，请点击此处](https://www.nuxtjs.cn/guide/async-data#handling-errors).

## 命名视图

要渲染命名视图，您可以在布局(`layout`) / 页面(`page`)中使用 `<nuxt name="top"/>` 或` <nuxt-child name="top"/> `组件。要指定页面的命名视图，我们需要在`nuxt.config.js`文件中扩展路由器配置：

```js
export default {
  router: {
    extendRoutes(routes, resolve) {
      const index = routes.findIndex(route => route.name === 'main')
      routes[index] = {
        ...routes[index],
        components: {
          default: routes[index].component,
          top: resolve(__dirname, 'components/mainTop.vue')
        },
        chunkNames: {
          top: 'components/mainTop'
        }
      }
    }
  }
}
```

## `SPA fallback`
