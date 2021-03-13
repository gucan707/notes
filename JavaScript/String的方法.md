# String的方法

## charAt()

> str.charAt(index)

从字符串中返回索引为index的字符

## charCodeAt()

> str.charCodeAt(index)

返回0~65535之间的整数，表示给定索引处的UTF-16代码单元

## codePointAt()

> str.codePointAt(index)

返回一个Unicode编码点值的非负整数

## concat()

> str.concat(str2, [, ...strN])

将一个或多个字符串与原字符串连接合并，形成一个新的字符串并返回，不影响原字符串

**强烈建议使用赋值操作符（`+`, `+=`）代替 `concat` 方法。**

## includes()

> str.includes(searchString[, position])

判断一个字符串是否包含在另一个字符串里，返回布尔值

position为开始搜索的位置

**区分大小写**

## endsWith()

> str.endsWith(searchString[, length])

判断当前字符串是否以另外一个给定的字符串“结尾”，返回布尔值

**区分大小写**

## indexOf()

> str.indexOf(searchValue [, fromIndex])

返回str中第一次出现searchValue的索引（searchValue开头的位置），从fromIndex开始搜索，未找到返回-1

**fromIndex 小于0时的情况与fromIndex = 0时的情况相同，大于str.length时返回-1**

**searchValue没有设置的话会被强制设成“undefined”**

```js
'undefined'.indexOf(); // 0
'undefine'.indexOf(); // -1
```

**如果searchValue为空字符串`''`，会产生奇怪的结果：**

```js
// 当fromIndex < str.length时，会直接返回fromIndex (或0
'hello world'.indexOf(''); // 0
'hello world'.indexOf('', 0); // 0
'hello world'.indexOf('', -2); // 0
'hello world'.indexOf('', 3); // 3

// 当fromIndex >= str.length时，会直接返回字符串的长度
'hello world'.indexOf('', 11); // 11
'hello world'.indexOf('', 13); // 11
```

**区分大小写**

## lastIndexOf()

> str.lastIndexOf(searchValue[, fromIndex])

同上，从尾部开始查找

## localeCompare()

> referenceStr.localeCompare(compareString[, locales[, options]])

返回一个数字来指示一个参考字符串是否在排序顺序前面或之后或与给定字符串相同

- `compareString`: 用来比较的字符串

当引用字符串在比较字符串前面时返回 -1，在后面返回 1，相同位置返回0（有的浏览器返回的不是±1，而是其他的正负数

```js
'a'.localeCompare('c'); // -2 or -1
'check'.localeCompare('against'); // 2 or 1
a.localeCompare('a'); // 0
```

## match()

> str.match(regexp)

检索返回一个字符串匹配正则表达式的结果

如果不给参数则返回`[""]`

如果使用g标志，则返回与完整正则表达式匹配的所有结果，但不返回捕获组

如果不使用g标志，仅返回第一个完整匹配及其相关的捕获组

![img](\img\match.png)

捕获组中：

- `group`: 一个捕获组数组或undefined（如果没有定义命名捕获组）
- `index`: 匹配的结果的开始位置
- `input`: 搜索的字符串

## normalize()

> str.normalize([from])

按照指定的一种Unicode正规形式将当前字符串正规化

## padEnd()

> str.padEnd(targetLength [, padString])

用一个字符串填充当前字符串（如果需要会重复填充），返回填充后达到指定长度的字符串，从当前字符串的末尾（右侧开始填充）

- `targetLength`: 当前字符串需要填充到的目标长度，如果这个数值小于当前字符串的长度，则返回当前字符串本身
- `padString`: 填充字符串，默认为`“ ”`

```js
'abc'.padEnd(10);          // "abc       "
'abc'.padEnd(10, "foo");   // "abcfoofoof"
'abc'.padEnd(6, "123456"); // "abc123"
'abc'.padEnd(1);           // "abc"
```

## padStart()

> str.padStart(targetLength [, padString])

同上，从头部开始填充

## repeat()

> str.repeat(count)

构造并返回一个字符串，该字符串包含被链接在一起的指定数量的字符串的副本

## replace()

> str.replace(regexp|substr, newSubStr|function)

返回一个由替换值`replacement`替换部分或所有的模式`pattern`匹配项后的新字符串，`pattern`可以是字符串或正则表达式，如果是字符串则仅替换第一个匹配项，原字符串不改变

## search()

> str.search(regexp)

执行正则表达式和String对象之间的一个搜索匹配

```js
var str = "hey JudE";
var re = /[A-Z]/g;
var re2 = /[.]/g;
console.log(str.search(re)); // returns 4, which is the index of the first capital letter "J"
console.log(str.search(re2)); // returns -1 cannot find '.' dot punctuation
```

## slice()

> str.slice(beginIndex[, endIndex])

提取某个字符串的一部分，并返回一个新的字符串，且不改动原字符串

[begin, end)左闭右开

如果`beginIndex`或`endIndex`是负数，则会被当做`strLength + beginIndex`处理，即倒着查找

```js
var str1 = 'The morning is upon us.', // str1 的长度 length 是 23。
    str2 = str1.slice(1, 8), // he morn
    str3 = str1.slice(4, -2), // morning is upon u
    str4 = str1.slice(12), // is upon us.
    str5 = str1.slice(30); // “”
```

## split()

> str.split([separator[, limit]])

使用指定的分隔符字符串将一个String对象分割成字符串数组，以分割字串来决定每个拆分的位置

若limit有值，则返回找到的前limit给分割元素

```js
var myString = "Hello World. How are you doing?";
var splits = myString.split(" ", 3);
// ["Hello", "World.", "How"]
```

也可以使用数组来作为分隔符

```js
const myString = 'ca,bc,a,bca,bca,bc';
const splits = myString.split(['a','b']);
// ["c", "c,", "c", "c", "c"]
```

## startsWith()

> str.startsWith(searchString[, position])

判断当前字符串是否以另外一个给定的子字符串开头，返回布尔值

## subString()

> str.subString(indexStart[, indexEnd])

返回一个字符串在开始索引到结束索引之间的一个子集

如果indexStart等于indexEnd，返回一个空字符串

如果任一参数小于0或为NaN，则会被当做0

若任一参数大于str.length，则会被当做str.length

如果indexStart大于indexEnd，则最后的执行结果就像两个参数调换了一样

## toLowerCase()

> str.toLowerCase()

将str转为小写形式并返回一个新的字符串，不影响原字符串

## toUpperCase()

同上，大写

## toString()

> str,toString()

返回指定对象的字符串形式

## trim()

> str.trim()

返回str去掉两端的空白字符的一个新的字符串

空白字符包括space，tab，no-break，LF，CR等

还有`trimStart()`, `trimEnd()`方法