# 数组的方法

##  修改器方法

以下方法会改变调用它们的对象自身的值

### copyWithin()

> arr.copyWithin(target[, start[, end]])

在数组内部讲一段元素序列拷贝到另一段元素序列上，覆盖原有的值

### fill()

> arr.fill(value[, start[, end]])

将数组中指定区间的所有元素的值都替换成某个固定的值

### pop()

> arr.pop()

删除数组最后一个元素并返回这个元素

### push()

> arr.push(element1, ..., elementN)

在数组的末尾增加一个或多个元素并返回数组的新长度

### reverse()

> arr.reverse()

颠倒数组中元素的排列顺序

### shift()

> arr.shift()

删除数组第一个元素并返回这个元素

### sort()

> arr.sort([compareFunction])

排序

若未指明`compareFunction`，元素会按照每个字符的unicode位点排序

若指明`compareFunction(a, b)`，则数组会按照调用该函数的返回值排序

- 如果 `compareFunction(a, b)` 小于 0 ，那么 a 会被排列到 b 之前；
- 如果 `compareFunction(a, b)` 等于 0 ， a 和 b 的相对位置不变。
- 如果 `compareFunction(a, b)` 大于 0 ， b 会被排列到 a 之前。

### splice()

> array.splice(start[, deleteCount[, item1[, item2[, ...]]]])

通过删除或替换现有元素或者原地添加新元素来修改数组，以数组形式返回被修改的内容

参数：开始位置，移除的元素个数（默认开始后面所有），新添加的元素

```js
var myFish = ['angel', 'clown', 'trumpet', 'sturgeon'];
var removed = myFish.splice(0, 2, 'parrot', 'anemone', 'blue');

// 运算后的 myFish: ["parrot", "anemone", "blue", "trumpet", "sturgeon"]
// 被删除的元素: ["angel", "clown"]
```

### unshift()

> arr.unshift(element1, ..., elementN)

将一个或多个元素添加到数组的开头，返回改数组的新长度

## 访问方法

### concat()

> var newArr = oldArr.concat(value1[, value2[, ...[, valueN]]])

合并两个或多个数组，不更改现有数组而是返回一个新数组

```js
var alpha = ['a', 'b', 'c'];

var alphaNumeric = alpha.concat(1, [2, 3]);

console.log(alphaNumeric);
// results in ['a', 'b', 'c', 1, 2, 3]
```

### includes()

> arr.includes(valueToFind[, fromIndex])

判断一个数组是否包含一个指定的值，返回true/false

### join()

> arr.join([separator])

将一个数组的所有元素连接成一个字符串并返回这个字符串，即**数组->字符串**

### slice()

> arr.slice([begin[, end]])

返回一个新的数组对象，这一对象是一个由begin和end决定的原数组的浅拷贝[begin, end)

### toString()

> arr.toString()

将数组元素转化成字符串

### toLocalString()

> arr.toLocalString([locales[, options]])

将数组中的元素以各自的toLocalString方法转成字符串

```js
const array = [1, 'a', new Date('21 Dec 1997 14:12:00 UTC')];
const localStr = array.toLocalString
// 1,a,1997/12/21下午10:12:00
```

### indexOf()

> arr.indexOf(searchElement[, fromIndex])

返回在数组中可以找到一个给定元素的第一个索引，若不存在则返回-1

### lastIndexOf()

> arr.lastIndexOf(searchElement[, fromIndex])

同上，从后向前查找

## 迭代器方法

### forEach()

> arr.forEach(callback(currentValue[, index [,array]])[, thisArg])

对数组中的每个元素执行一次给定的函数，总返回undefined

**注意，`forEach`遍历的范围在第一次调用callback前就会确定，调用`forEach`后添加到数组中的项不会被访问到，如果已经存在的值被改变，则传递给callback的值是`forEach`遍历到它们那一刻的值，已删除的项不会被遍历到**

**`forEach`循环无法中止和跳出**

```js
let ratings = [5, 4, 5];
let sum = 0;
let sumFunction = async function (a, b) {
    return a + b;
}

ratings.forEach(async function(rating) {
    sum = await sumFunction(sum, rating);
})

console.log(sum);
// Expected output: 14
// Actual output: 0
```

### entries()

> arr.entries()

返回一个新的Array Iterator对象，该对象包含数组中每个索引的键值对

### keys()

> arr.keys()

同entries，返回的是数组中每个索引键的Array Iterator对象。

### values()

> arr.values()

返回一个新的`Array Iterator`对象，该对象包含数组每个索引的值

### every()

> arr.every(callback(element[, index[, array]])[,thisArg])

测试一个数组内的所有元素是否都能通过某个指定函数的测试，返回一个布尔值

**遍历时的规则同`forEach`**

```js
[12, 5, 8, 130, 44].every((element) => element > 10);
// false

[12, 54, 18, 130, 44].every((element) => element > 10);
// true
```

### some()

> arr.some(callback(element[, index[, array]])[,thisArg])

测试数组中是不是至少有1个元素通过了被提供的函数测试，返回一个布尔值

### filter()

> var newArr = arr.filter(callback(element[, index[, array]])[, thisArg])

创建一个新数组，其包含通过所提供函数实现的测试的所有元素

```js
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
const result = words.filter(word => word.length > 6);
console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

### find()

> arr.find(callback[, thisArg])

返回数组中满足提供的测试函数的第一个元素的值，否则返回undefined

**callback函数会为数组中的每个索引调用即从0到length - 1，而不仅仅时纳休被赋值的索引，所以对于稀疏数组来说该方法的效率要低于那些值遍历有值的索引的方法**

### findIndex()

> arr.findIndex(callback[, thisArg])

回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回-1。

### map()

> var newArr = arr.map(callback(currentValue[, index[, array]])[, thisArg])

创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值

**只在有值的索引上被调用**

### reduce()

> arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])

对数组中的每个元素执行一个reducer函数，将其结果汇总为单个返回值

- `accumulator`: 累计器累计回调的返回值，它是上一次调用回调时返回的累计值或`initialValue`
- `currentValue`: 当前值
- `index`: 当前索引，如果提供了`initialValue`，则起始索引号为0，否则为1
- `initialValue`: 作为第一次调用callback时accumulator的值，如果没有提供初始值，则将使用数组中的第一个元素，在没有初始值的空数组上调用reduce会报错

**如果数组仅有一个元素并且没有提供`initialValue`，或者有提供`initialValue`而数组为空，那么此唯一值会被返回且callback不会执行**

```js
var maxCallback = ( acc, cur ) => Math.max( acc.x, cur.x );
var maxCallback2 = ( max, cur ) => Math.max( max, cur );

// reduce() 没有初始值
[{ x: 2 }, { x: 22 }, { x: 42 }].reduce( maxCallback ); // NaN
[{ x: 2 }, { x: 22 }].reduce( maxCallback ); // 22
[{ x: 2 }].reduce( maxCallback ); // { x: 2 }
[].reduce( maxCallback ); // TypeError

// map/reduce; 这是更好的方案，即使传入空数组或更大数组也可正常执行
[ { x: 22 }, { x: 42 } ].map( el => el.x )
                        .reduce( maxCallback2, -Infinity );
```

### reduceRight()

> arr.reduceRight(callback(accumulator, currentValue[, index[, array]])[, initialValue])

同reduce，但是是从右往左遍历

