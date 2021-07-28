## 字符串新增的方法

```text
1. String.fromCodePoint() //处理unicode编码
2. String.raw()  //处理模板字符串 
3. 实例方法：codePointAt() //处理Unicode编码  
4. 实例方法：normalize() //欧洲重音字符的普化
5. 实例方法：includes(), startsWith(), endsWith() 【重点】
6. 实例方法：repeat()
7. 实例方法：padStart()，padEnd()
8. 实例方法：trimStart()，trimEnd()
9. 实例方法：matchAll()
10.实例方法：replaceAll()
```

## 5.实例方法：includes(), startsWith(), endsWith()

- includes()：返回布尔值，表示是否找到了参数字符串。

- startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。

- endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。

```js
let s = 'Hello world!';

s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
```
这三个方法都支持第二个参数，表示开始搜索的位置。

```js
let s = 'Hello world!';

s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
```

上面代码表示，使用第二个参数n时，endsWith的行为与其他两个方法有所不同。它针对前n个字符，而其他两个方法针对从第n个位置直到字符串结束。

## 6.实例方法：repeat()

repeat方法返回一个新字符串，表示将原字符串重复n次。

## 7.实例方法：padStart()，padEnd() 

ES2017 引入了字符串补全长度的功能。如果某个字符串不够指定长度，会在头部或尾部补全。padStart()用于头部补全，padEnd()用于尾部补全。

```js
'x'.padStart(5, 'ab') // 'ababx'
'x'.padStart(4, 'ab') // 'abax'

'x'.padEnd(5, 'ab') // 'xabab'
'x'.padEnd(4, 'ab') // 'xaba'
```
padStart()的常见用途是为数值补全指定位数。下面代码生成 10 位的数值字符串。

```js
'1'.padStart(10, '0') // "0000000001"
'12'.padStart(10, '0') // "0000000012"
'123456'.padStart(10, '0') // "0000123456"
```
另一个用途是提示字符串格式。

```js
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"
```

## 8.实例方法：trimStart()，trimEnd() 

，trimStart()消除字符串头部的空格，trimEnd()消除尾部的空格。它们返回的都是新字符串，不会修改原始字符串。

除了空格键，这两个方法对字符串头部（或尾部）的 tab 键、换行符等不可见的空白符号也有效。

浏览器还部署了额外的两个方法，trimLeft()是trimStart()的别名，trimRight()是trimEnd()的别名。

## 9.实例方法：matchAll()

matchAll()方法返回一个正则表达式在当前字符串的所有匹配

## 10.实例方法：replaceAll()

ES2021 引入了replaceAll()方法，可以一次性替换所有匹配。返回一个新字符串，不会改变原字符串。

```js
String.prototype.replaceAll(searchValue, replacement)
```

上面代码中，searchValue是搜索模式，可以是一个字符串，也可以是一个全局的正则表达式（带有g修饰符）

