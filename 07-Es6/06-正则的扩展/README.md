## 正则的扩展

1. RegExp 构造函数 （两种）
2. 字符串的正则方法 
3. u 修饰符
4. RegExp.prototype.unicode 属性
5. y 修饰符
6. RegExp.prototype.sticky 属性
7. RegExp.prototype.flags 属性
8. s 修饰符：dotAll 模式
9. 后行断言
10. Unicode 属性类
11. 具名组匹配
12. 正则匹配索引
13. String.prototype.matchAll()

## 1.RegExp 构造函数

```js
var regex = new RegExp('xyz', 'i');
// 等价于
var regex = /xyz/i;


var regex = new RegExp(/xyz/i);
// 等价于
var regex = /xyz/i;

```

## 2.字符串的正则方法

ES6 出现之前，字符串对象共有 4 个方法，可以使用正则表达式：match()、replace()、search()和split()。

## 3. u 修饰符

## 5. y 

除了u修饰符，ES6 还为正则表达式添加了y修饰符，叫做“粘连”（sticky）修饰符。

下面是字符串对象的replace方法的例子。

```js
const REGEX = /a/gy;
'aaxa'.replace(REGEX, '-') // '--xa'
```
上面代码中，最后一个a因为不是出现在下一次匹配的头部，所以不会被替换。

单单一个y修饰符对match方法，只能返回第一个匹配，必须与g修饰符联用，才能返回所有匹配。

```js
'a1a2a3'.match(/a\d/y) // ["a1"]
'a1a2a3'.match(/a\d/gy) // ["a1", "a2", "a3"]
```

y修饰符的一个应用，是从字符串提取 token（词元），y修饰符确保了匹配之间不会有漏掉的字符。

## 6. RegExp.prototype.sticky 属性

与y修饰符相匹配，ES6 的正则实例对象多了sticky属性，表示是否设置了y修饰符。

```js
var r = /hello\d/y;
r.sticky // true
```

## 6. RegExp.prototype.sticky 属性

与y修饰符相匹配，ES6 的正则实例对象多了sticky属性，表示是否设置了y修饰符。

## 7.RegExp.prototype.flags 属性 

ES6 为正则表达式新增了flags属性，会返回正则表达式的修饰符。

```js
// ES5 的 source 属性
// 返回正则表达式的正文
/abc/ig.source
// "abc"

// ES6 的 flags 属性
// 返回正则表达式的修饰符
/abc/ig.flags
// 'gi'
```

## 8.s 修饰符：dotAll 模式

正则表达式中，点（.）是一个特殊字符，代表任意的单个字符，但是有两个例外。一个是四个字节的 UTF-16 字符，这个可以用u修饰符解决；另一个是行终止符（line terminator character）。

所谓行终止符，就是该字符表示一行的终结。以下四个字符属于“行终止符”。

- U+000A 换行符（\n）
- U+000D 回车符（\r）
- U+2028 行分隔符（line separator）
- U+2029 段分隔符（paragraph separator）

```js
/foo.bar/.test('foo\nbar')
// false
```

上面代码中，因为.不匹配\n，所以正则表达式返回false。

但是，很多时候我们希望匹配的是任意单个字符，这时有一种变通的写法。

```js
/foo[^]bar/.test('foo\nbar')
// true
```

这种解决方案毕竟不太符合直觉，ES2018 引入s修饰符，使得.可以匹配任意单个字符。

```js
/foo.bar/s.test('foo\nbar') // true
```

这被称为dotAll模式，即点（dot）代表一切字符。所以，正则表达式还引入了一个dotAll属性，返回一个布尔值，表示该正则表达式是否处在dotAll模式。

```js
const re = /foo.bar/s;
// 另一种写法
// const re = new RegExp('foo.bar', 's');

re.test('foo\nbar') // true
re.dotAll // true
re.flags // 's'
```
/s修饰符和多行修饰符/m不冲突，两者一起使用的情况下，.匹配所有字符，而^和$匹配每一行的行首和行尾。

## 9.后行断言
JavaScript 语言的正则表达式，只支持先行断言（lookahead）和先行否定断言（negative lookahead），不支持后行断言（lookbehind）和后行否定断言（negative lookbehind）。ES2018 引入后行断言，V8 引擎 4.9 版（Chrome 62）已经支持。

“先行断言”指的是，x只有在y前面才匹配，必须写成/x(?=y)/。比如，只匹配百分号之前的数字，要写成/\d+(?=%)/。“先行否定断言”指的是，x只有不在y前面才匹配，必须写成/x(?!y)/。比如，只匹配不在百分号之前的数字，要写成/\d+(?!%)/。

```js
/\d+(?=%)/.exec('100% of US presidents have been male')  // ["100"]
/\d+(?!%)/.exec('that’s all 44 of them')                 // ["44"]
```
上面两个字符串，如果互换正则表达式，就不会得到相同结果。另外，还可以看到，“先行断言”括号之中的部分（(?=%)），是不计入返回结果的。

“后行断言”正好与“先行断言”相反，x只有在y后面才匹配，必须写成/(?<=y)x/。比如，只匹配美元符号之后的数字，要写成/(?<=\$)\d+/。“后行否定断言”则与“先行否定断言”相反，x只有不在y后面才匹配，必须写成/(?<!y)x/。比如，只匹配不在美元符号后面的数字，要写成/(?<!\$)\d+/。

```js
/(?<=\$)\d+/.exec('Benjamin Franklin is on the $100 bill')  // ["100"]
/(?<!\$)\d+/.exec('it’s is worth about €90')                // ["90"]
```
上面的例子中，“后行断言”的括号之中的部分（(?<=\$)），也是不计入返回结果。

下面的例子是使用后行断言进行字符串替换。

```js
const RE_DOLLAR_PREFIX = /(?<=\$)foo/g;
'$foo %foo foo'.replace(RE_DOLLAR_PREFIX, 'bar');
// '$bar %foo foo'
```
上面代码中，只有在美元符号后面的foo才会被替换。

“后行断言”的实现，需要先匹配/(?<=y)x/的x，然后再回到左边，匹配y的部分。这种“先右后左”的执行顺序，与所有其他正则操作相反，导致了一些不符合预期的行为。

首先，后行断言的组匹配，与正常情况下结果是不一样的。

```js
/(?<=(\d+)(\d+))$/.exec('1053') // ["", "1", "053"]
/^(\d+)(\d+)$/.exec('1053') // ["1053", "105", "3"]
```
上面代码中，需要捕捉两个组匹配。没有“后行断言”时，第一个括号是贪婪模式，第二个括号只能捕获一个字符，所以结果是105和3。而“后行断言”时，由于执行顺序是从右到左，第二个括号是贪婪模式，第一个括号只能捕获一个字符，所以结果是1和053。

其次，“后行断言”的反斜杠引用，也与通常的顺序相反，必须放在对应的那个括号之前。

```js
/(?<=(o)d\1)r/.exec('hodor')  // null
/(?<=\1d(o))r/.exec('hodor')  // ["r", "o"]
```
上面代码中，如果后行断言的反斜杠引用（\1）放在括号的后面，就不会得到匹配结果，必须放在前面才可以。因为后行断言是先从左到右扫描，发现匹配以后再回过头，从右到左完成反斜杠引用。


## 10.Unicode 属性类

ES2018 引入了一种新的类的写法\p{...}和\P{...}，允许正则表达式匹配符合 Unicode 某种属性的所有字符。

```js
const regexGreekSymbol = /\p{Script=Greek}/u;
regexGreekSymbol.test('π') // true
```

上面代码中，\p{Script=Greek}指定匹配一个希腊文字母，所以匹配π成功。

Unicode 属性类要指定属性名和属性值。

```js
\p{UnicodePropertyName=UnicodePropertyValue}
```
对于某些属性，可以只写属性名，或者只写属性值。

```js
\p{UnicodePropertyName}
\p{UnicodePropertyValue}
```

\P{…}是\p{…}的反向匹配，即匹配不满足条件的字符。

注意，这两种类只对 Unicode 有效，所以使用的时候一定要加上u修饰符。如果不加u修饰符，正则表达式使用\p和\P会报错，ECMAScript 预留了这两个类。

由于 Unicode 的各种属性非常多，所以这种新的类的表达能力非常强。

```js
const regex = /^\p{Decimal_Number}+$/u;
regex.test('𝟏𝟐𝟑𝟜𝟝𝟞𝟩𝟪𝟫𝟬𝟭𝟮𝟯𝟺𝟻𝟼') // true
```

上面代码中，属性类指定匹配所有十进制字符，可以看到各种字型的十进制字符都会匹配成功。

\p{Number}甚至能匹配罗马数字。

```js
// 匹配所有数字
const regex = /^\p{Number}+$/u;
regex.test('²³¹¼½¾') // true
regex.test('㉛㉜㉝') // true
regex.test('ⅠⅡⅢⅣⅤⅥⅦⅧⅨⅩⅪⅫ') // true
```

下面是其他一些例子。

```js
// 匹配所有空格
\p{White_Space}

// 匹配各种文字的所有字母，等同于 Unicode 版的 \w
[\p{Alphabetic}\p{Mark}\p{Decimal_Number}\p{Connector_Punctuation}\p{Join_Control}]

// 匹配各种文字的所有非字母的字符，等同于 Unicode 版的 \W
[^\p{Alphabetic}\p{Mark}\p{Decimal_Number}\p{Connector_Punctuation}\p{Join_Control}]

// 匹配 Emoji
/\p{Emoji_Modifier_Base}\p{Emoji_Modifier}?|\p{Emoji_Presentation}|\p{Emoji}\uFE0F/gu

// 匹配所有的箭头字符
const regexArrows = /^\p{Block=Arrows}+$/u;
regexArrows.test('←↑→↓↔↕↖↗↘↙⇏⇐⇑⇒⇓⇔⇕⇖⇗⇘⇙⇧⇩') // true
```


## 11. 具名组匹配

### 简介

正则表达式使用圆括号进行组匹配。

```js
const RE_DATE = /(\d{4})-(\d{2})-(\d{2})/;
上面代码中，正则表达式里面有三组圆括号。使用exec方法，就可以将这三组匹配结果提取出来。

const RE_DATE = /(\d{4})-(\d{2})-(\d{2})/;

const matchObj = RE_DATE.exec('1999-12-31');
const year = matchObj[1]; // 1999
const month = matchObj[2]; // 12
const day = matchObj[3]; // 31
```

组匹配的一个问题是，每一组的匹配含义不容易看出来，而且只能用数字序号（比如matchObj[1]）引用，要是组的顺序变了，引用的时候就必须修改序号。

```js
ES2018 引入了具名组匹配（Named Capture Groups），允许为每一个组匹配指定一个名字，既便于阅读代码，又便于引用。

const RE_DATE = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;

const matchObj = RE_DATE.exec('1999-12-31');
const year = matchObj.groups.year; // "1999"
const month = matchObj.groups.month; // "12"
const day = matchObj.groups.day; // "31"
```

上面代码中，“具名组匹配”在圆括号内部，模式的头部添加“问号 + 尖括号 + 组名”（?<year>），然后就可以在exec方法返回结果的groups属性上引用该组名。同时，数字序号（matchObj[1]）依然有效。

具名组匹配等于为每一组匹配加上了 ID，便于描述匹配的目的。如果组的顺序变了，也不用改变匹配后的处理代码。

如果具名组没有匹配，那么对应的groups对象属性会是undefined。

```js
const RE_OPT_A = /^(?<as>a+)?$/;
const matchObj = RE_OPT_A.exec('');

matchObj.groups.as // undefined
'as' in matchObj.groups // true
```

上面代码中，具名组as没有找到匹配，那么matchObj.groups.as属性值就是undefined，并且as这个键名在groups是始终存在的。


### 解构赋值和替换

有了具名组匹配以后，可以使用解构赋值直接从匹配结果上为变量赋值。

```js
let {groups: {one, two}} = /^(?<one>.*):(?<two>.*)$/u.exec('foo:bar');
one  // foo
two  // bar
```
字符串替换时，使用$<组名>引用具名组。

```js
let re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/u;

'2015-01-02'.replace(re, '$<day>/$<month>/$<year>')
// '02/01/2015'
```

上面代码中，replace方法的第二个参数是一个字符串，而不是正则表达式。

replace方法的第二个参数也可以是函数，该函数的参数序列如下。

```js
'2015-01-02'.replace(re, (
   matched, // 整个匹配结果 2015-01-02
   capture1, // 第一个组匹配 2015
   capture2, // 第二个组匹配 01
   capture3, // 第三个组匹配 02
   position, // 匹配开始的位置 0
   S, // 原字符串 2015-01-02
   groups // 具名组构成的一个对象 {year, month, day}
 ) => {
 let {day, month, year} = groups;
 return `${day}/${month}/${year}`;
});
```

具名组匹配在原来的基础上，新增了最后一个函数参数：具名组构成的一个对象。函数内部可以直接对这个对象进行解构赋值。


### 引用

如果要在正则表达式内部引用某个“具名组匹配”，可以使用\k<组名>的写法。

```js
const RE_TWICE = /^(?<word>[a-z]+)!\k<word>$/;
RE_TWICE.test('abc!abc') // true
RE_TWICE.test('abc!ab') // false
```
数字引用（\1）依然有效。

```js
const RE_TWICE = /^(?<word>[a-z]+)!\1$/;
RE_TWICE.test('abc!abc') // true
RE_TWICE.test('abc!ab') // false
```

这两种引用语法还可以同时使用。

```js
const RE_TWICE = /^(?<word>[a-z]+)!\k<word>!\1$/;
RE_TWICE.test('abc!abc!abc') // true
RE_TWICE.test('abc!abc!ab') // false
```

正则匹配索引
正则匹配结果的开始位置和结束位置，目前获取并不是很方便。正则实例的exec()方法，返回结果有一个index属性，可以获取整个匹配结果的开始位置，但是如果包含组匹配，每个组匹配的开始位置，很难拿到。

现在有一个第三阶段提案，为exec()方法的返回结果加上indices属性，在这个属性上面可以拿到匹配的开始位置和结束位置。

```js
const text = 'zabbcdef';
const re = /ab/;
const result = re.exec(text);

result.index // 1
result.indices // [ [1, 3] ]
```

上面例子中，exec()方法的返回结果result，它的index属性是整个匹配结果（ab）的开始位置，而它的indices属性是一个数组，成员是每个匹配的开始位置和结束位置的数组。由于该例子的正则表达式没有组匹配，所以indices数组只有一个成员，表示整个匹配的开始位置是1，结束位置是3。

注意，开始位置包含在匹配结果之中，但是结束位置不包含在匹配结果之中。比如，匹配结果为ab，分别是原始字符串的第1位和第2位，那么结束位置就是第3位。

如果正则表达式包含组匹配，那么indices属性对应的数组就会包含多个成员，提供每个组匹配的开始位置和结束位置。

```js
const text = 'zabbcdef';
const re = /ab+(cd)/;
const result = re.exec(text);

result.indices // [ [ 1, 6 ], [ 4, 6 ] ]
```

上面例子中，正则表达式包含一个组匹配，那么indices属性数组就有两个成员，第一个成员是整个匹配结果（abbcd）的开始位置和结束位置，第二个成员是组匹配（cd）的开始位置和结束位置。

下面是多个组匹配的例子。

```js
const text = 'zabbcdef';
const re = /ab+(cd(ef))/;
const result = re.exec(text);

result.indices // [ [1, 8], [4, 8], [6, 8] ]
```

上面例子中，正则表达式包含两个组匹配，所以indices属性数组就有三个成员。

如果正则表达式包含具名组匹配，indices属性数组还会有一个groups属性。该属性是一个对象，可以从该对象获取具名组匹配的开始位置和结束位置。

```js
const text = 'zabbcdef';
const re = /ab+(?<Z>cd)/;
const result = re.exec(text);

result.indices.groups // { Z: [ 4, 6 ] }
```
上面例子中，exec()方法返回结果的indices.groups属性是一个对象，提供具名组匹配Z的开始位置和结束位置。

如果获取组匹配不成功，indices属性数组的对应成员则为undefined，indices.groups属性对象的对应成员也是undefined。

```js
const text = 'zabbcdef';
const re = /ab+(?<Z>ce)?/;
const result = re.exec(text);

result.indices[1] // undefined
result.indices.groups['Z'] // undefined
```

上面例子中，由于组匹配不成功，所以indices属性数组和indices.groups属性对象对应的组匹配成员都是undefined。

## 13.String.prototype.matchAll()

如果一个正则表达式在字符串里面有多个匹配，现在一般使用g修饰符或y修饰符，在循环里面逐一取出。

```js
var regex = /t(e)(st(\d?))/g;
var string = 'test1test2test3';

var matches = [];
var match;
while (match = regex.exec(string)) {
  matches.push(match);
}

matches
// [
//   ["test1", "e", "st1", "1", index: 0, input: "test1test2test3"],
//   ["test2", "e", "st2", "2", index: 5, input: "test1test2test3"],
//   ["test3", "e", "st3", "3", index: 10, input: "test1test2test3"]
// ]
```

上面代码中，while循环取出每一轮的正则匹配，一共三轮。

ES2020 增加了String.prototype.matchAll()方法，可以一次性取出所有匹配。不过，它返回的是一个遍历器（Iterator），而不是数组。

```js
const string = 'test1test2test3';
const regex = /t(e)(st(\d?))/g;

for (const match of string.matchAll(regex)) {
  console.log(match);
}
// ["test1", "e", "st1", "1", index: 0, input: "test1test2test3"]
// ["test2", "e", "st2", "2", index: 5, input: "test1test2test3"]
// ["test3", "e", "st3", "3", index: 10, input: "test1test2test3"]
```

上面代码中，由于string.matchAll(regex)返回的是遍历器，所以可以用for...of循环取出。相对于返回数组，返回遍历器的好处在于，如果匹配结果是一个很大的数组，那么遍历器比较节省资源。

遍历器转为数组是非常简单的，使用...运算符和Array.from()方法就可以了。

```js
// 转为数组的方法一
[...string.matchAll(regex)]

// 转为数组的方法二
Array.from(string.matchAll(regex))
```