## 表单处理

当在严格模式中使用 Vuex 时，在属于 Vuex 的 state 上使用 <code>v-model</code> 会比较棘手：

```js
<input v-model="obj.message">
```

假设这里的 <code>obj</code>是在计算属性中返回的一个属于 <code>Vuex store</code> 的对象，在用户输入时，<code>v-model</code> 会试图直接修改 <code>obj.message</code>。在严格模式中，由于这个修改不是在 <code>mutation</code> 函数中执行的, 这里会抛出一个错误。

用“Vuex 的思维”去解决这个问题的方法是：给 <code><input></code> 中绑定 value，然后侦听 <code>input</code> 或者 <code>change</code> 事件，在事件回调中调用一个方法:

```js
<input :value="message" @input="updateMessage">
```

```js
// ...
computed: {
  ...mapState({
    message: state => state.obj.message
  })
},
methods: {
  updateMessage (e) {
    this.$store.commit('updateMessage', e.target.value)
  }
}
```

下面是 mutation 函数：

```js
// ...
mutations: {
  updateMessage (state, message) {
    state.obj.message = message
  }
}
```

## 双向绑定的计算属性

必须承认，这样做比简单地使用“<code>v-model</code> + 局部状态”要啰嗦得多，并且也损失了一些 <code>v-model</code>  中很有用的特性。另一个方法是使用带有 <code>setter</code> 的双向绑定计算属性：

```js
<input v-model="message">
```
```js
// ...
computed: {
  message: {
    get () {
      return this.$store.state.obj.message
    },
    set (value) {
      this.$store.commit('updateMessage', value)
    }
  }
}
```
>! 此处在computed中 计算属性变成了一个对象，这个对象里边的两个方法：一个使用来获取相应的状态，一个是用来改变相应的状态。