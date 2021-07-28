## 字符串的扩展

 
1. 字符的 Unicode 表示法
2. 字符串的遍历器接口
3. 直接输入 U+2028 和 U+2029
4. JSON.stringify() 的改造
5. 模板字符串  **√**
6. 实例：模板编译
7. 标签模板
8. 模板字符串的限制
 

本章介绍 ES6 对字符串的改造和增强，下一章介绍字符串对象的新增方法。

## 1. 字符的 Unicode 表示法

 JavaScript 共有 6 种方法可以表示一个字符。

```js
'\z' === 'z'  // true
'\172' === 'z' // true
'\x7A' === 'z' // true
'\u007A' === 'z' // true
'\u{7A}' === 'z' // true
```
 ## 2.字符串的遍历器接口

ES6 为字符串添加了遍历器接口（详见《Iterator》一章），使得字符串可以被for...of循环遍历。

```js
let text = String.fromCodePoint(0x20BB7);

for (let i = 0; i < text.length; i++) {
  console.log(text[i]);
}
// " "
// " "

for (let i of text) {
  console.log(i);
}
// "𠮷"
```

## 3.直接输入 U+2028 和 U+2029

JavaScript 字符串允许直接输入字符，以及输入字符的转义形式

## 4.JavaScript 字符串允许直接输入字符，以及输入字符的转义形式

为了确保返回的是合法的 UTF-8 字符，ES2019 改变了JSON.stringify()的行为。如果遇到0xD800到0xDFFF之间的单个码点，或者不存在的配对形式，它会返回转义字符串，留给应用自己决定下一步的处理。

```js
JSON.stringify('\u{D834}') // ""\\uD834""
JSON.stringify('\uDF06\uD834') // ""\\udf06\\ud834""
```

## 5. 模板字符串

模板字符串中  使用反引号 要使用反斜进行转译

如果不想换行，可以使用trim方法消除它。

## 6. 模板编译

它可以紧跟在一个函数名后面，该函数将被调用来处理这个模板字符串。这被称为“标签模板”功能（tagged template）。

```js
alert`hello`
// 等同于
alert(['hello'])
```

模板字符里面有变量，就不是简单的调用了，而是会将模板字符串先处理成多个参数，再调用函数。

```js
let a = 5;
let b = 10;

tag`Hello ${ a + b } world ${ a * b }`;
// 等同于
tag(['Hello ', ' world ', ''], 15, 50);
```

