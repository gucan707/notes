# String

- **includes**()

  > str.includes(searchString[, position])

  searchString: 要在此字符串中搜索的字符串

  position: 可选，从str的哪个索引位置开始搜索searchString，默认为0

  return: boolean

- **startsWith()**

  > str.startsWith(searchString[, position])

  判断str是否以searchString开头

- **repeat()**

  > str.repeat(count)

  ```js
  // 一个MDN中的例子
  ({toString : () => "abc", repeat : String.prototype.repeat}).repeat(2)
  ```

- **String.raw()**

  > String.raw\`templateString\`
  >
  > String.raw(callSite, ...substitutions)

  模板字符串中`${...}`能正常使用

  ```js
  let name = 'sir'
  String.raw`hi\n${name}`;
  // hi\nsir
  
  String.raw({raw: 'test'}, 0, 1, 2);
  // t0e1s2t,等价于`t${0}e${1}s${2}t`
  
  String.raw({raw: ['foo', 'bar', 'baz']}, 2 + 3, 'Java' + 'Script')
  // foo5barJavaScriptbaz, 等价于`foo${2 + 3}bar${'Java' + 'Script'}baz`
  ```

# Array

- **Array.from()**

  > Array.from(arrayLike[, mapFn[, thisArg]])

  将一个类似数组或可迭代对象创建一个新的浅拷贝的数组实例

  arrayLike: 想要转换成数组的伪数组对象或可迭代对象

  mapFn: 可选，如果指定了该参数，新数组中的每个元素会执行该回调函数

  thisArg: 可选，执行回调mapFn时this对象

  return: 一个新的数组实例

  ```js
  Array.from('foo') // ['f','o','o']
  
  const set = new Set(['foo','bar','foo']);
  Array.from(set); // ['foo','bar']
  
  const map = new Map ([[1, 2], [2, 4], [4, 8]]);
  Array.from(map); // [[1, 2], [2, 4], [4, 8]]
  
  Array.from({length: 5}, (v, i) => i); // [0, 1, 2, 3, 4]
  ```

- **Array.of()**

  > Array.of(element[, element1[, ...[, elementN]]])

  创建一个具有可变数量参数的新数组实例，不考虑参数的数量和类型

  ```js
  Array.of(7) // [7]
  ```

- **fill()**

  > arr.fill(value[, start[, end]])

  用固定值填充数组，[start, end)

  ```js
  // 填充对象为引用类型时
  var arr = Array(3).fill({}); // [{}, {}, {}]
  arr[0].hi = 'hi'; // [{hi: 'hi'}, {hi: 'hi'}, {hi: 'hi'}]
  ```

- **find()**

  > arr.find(callback[, thisArg])

  返回数组中满足测试函数的第一个元素的值

  callback: 接受三个参数，element为当前遍历到的元素，index与array为可选参数

  thisArg: 执行回调时用作this的对象

  ```js
  var inventory = [
      {name: 'apples', quantity: 2},
      {name: 'bananas', quantity: 0},
  ]
  console.log(inventory.find((fruit) => fruit.name === 'apples'))
  // {name: 'apples', quantity: 2}
  ```

- **entries()**

  > arr.entries()

  返回一个新的Array Iterator对象，该对象包含数组中每个索引的键值对(可以使用`for of`)

  ```js
  var arr = ['a', 'b', 'c'];
  var iterator = arr.entries();
  console.log(iterator);
  /*
  	Array Iterator {}
           __proto__:Array Iterator
           next:ƒ next()
           Symbol(Symbol.toStringTag):"Array Iterator"
           __proto__:Object
  */
  
  console.log(iterato.next());
  /*
  	{value: Array(2), done: false}
            done:false
            value:(2) [0, "a"]
             __proto__: Object
  */
  /*
  next.done 用于指示迭代器是否完成：在每次迭代时进行更新而且都是false，直到迭代器结束done才是true
  */
  ```
  
- **keys()**

  > arr.keys()

  返回一个包含数组中每个索引键的Array Iterator对象

  类似entries，对象中的value为数组的index

- **copyWithin()**

  > arr.copyWithin(target[,start[, end]])

  复制数组的一部分到同一数组的另一位置，并返回它，不改变原数组的长度

  `target`: 复制序列到该位置，如果是负数，则从末尾开始计算；如果taget ≥ arr.length则不会发生拷贝，如果target在start之后，复制的序列将被修改以符合arr.length

  `start`: 开始复制元素的起始位置，负数则从末尾计算，默认0

  `end`: 开始复制元素的结束位置，不包含end，默认arr.length

  ```js
  [1, 2, 3, 4, 5].copyWithin(-2);
  // [1, 2, 3, 1, 2]
  
  [1, 2, 3, 4, 5].copyWithin(0, 3);
  // [4, 5, 3, 4, 5]
  
  [1, 2, 3, 4, 5].copyWithin(-2, -3, -1);
  // [1, 2, 3, 3, 4]
  ```

  

# let与const

## let

1. 不存在变量提升

2. 暂时性死区

   ```js
   function bar(x = y, y = 2) {
     return [x, y];
   }
   
   bar(); // 报错
   
   let a = a; // 报错
   ```

3. 不允许重复声明

4. 新增块级作用域（块级作用域中的函数声明也类似let）

## const

规则与let基本相同

const保证的不是变量的值不得改动，二十变量指向的内存地址所保存的数据不得改动，对于简单类型的数据（Number，String，Boolean），值就保存在变量指向的内存地址，因此等同于常量，但是复合类型（Object，Array）变量指向的内存地址保存的只是一个指向实际数据的指针，const保证指针时固定的，而指针指向的数据结构可变性不受控制

## 顶层对象与全局变量

var 与 function 声明的全局变量依然是顶层对象的属性

let，const，class声明的全局变量不属于顶层对象的属性

```js
var a = 1;
window.a // 1

let b = 1;
window.b; // undefined
```

# 解构赋值

## 数组

只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。

```js
// 数组的解构赋值
let [x, y,q = 'b' ...z] = ['a'];
x // "a"
y // undefined
q // b
z // []
```

## 对象

```js
// 对象的解构赋值，实际是对下面的后者baz赋值的简写
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"
foo // error: foo is not defined

let obj = {
  p: [
    'Hello',
    { y: 'World' }
  ]
};

let { p: [x, { y }] } = obj;
x // "Hello"
y // "World"
```

**如果要将一个已经声明的变量用于解构赋值需要特别注意**

```js
let x;
{x} = {x : 1};
// 报错，{x}会被理解为一个代码块而发生语法错误

({x} = {x : 1}); // 正确
```

## 字符串

```js
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```

## 数值与布尔值

解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。(非对象非数组都这样)

```js
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```

## 函数参数

注意区别

```js
function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]
```

```js
function move({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, undefined]
move({}); // [undefined, undefined]
move(); // [0, 0]
```

