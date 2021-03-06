## @ `Array` 扩展

## @` Array.from()`

`Array.from`方法用于将两类对象转为真正的数组: 类似数组的对象(`array-like object`)和可遍历(`iterable`)的对象(包括`ES6`新增的数据结构`Set`和`Map`).

```javascript
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};

// ES5的写法
var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

// ES6的写法
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']

// NodeList对象
let ps = document.querySelectorAll('p');
Array.from(ps).forEach(function (p) {
    console.log(p);
});

// arguments对象
function foo() {
    var args = Array.from(arguments);
  // ...
}
```

## @ `Array.of()`

`Array.of`方法用于将一组值,转换为数组.

```javascript
Array.of(3, 11, 8) // [3,11,8]
Array.of(3) // [3]
Array.of(3).length // 1
```

## `copyWithin()`

数组实例的`copyWithin`方法,在当前数组内部,将指定位置的成员复制到其他位置(会覆盖原有成员),然后返回当前数组.也就是说,使用这个方法,会修改当前数组.

```javascript
	Array.prototype.copyWithin(target, start = 0, end = this.length)
```

它接受三个参数.

- `target`(必需): 从该位置开始替换数据.
- `start`(可选): 从该位置开始读取数据,默认为0.如果为负值,表示倒数.
- `end`(可选): 到该位置前停止读取数据,默认等于数组长度.如果为负值,表示倒数.
-
```javascript
	[1, 2, 3, 4, 5].copyWithin(0, 3)
	// [4, 5, 3, 4, 5]
```

## @ 数组实例的`find()`和`findIndex()`

数组实例的`find`方法,用于找出第一个符合条件的数组成员.它的参数是一个回调函数,所有数组成员依次执行该回调函数,直到找出第一个返回值为`true`的成员,然后返回该成员.如果没有符合条件的成员,则返回`undefined.`

```javascript
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
```

数组实例的`findIndex`方法的用法与`find`方法非常类似,返回第一个符合条件的数组成员的位置,如果所有成员都不符合条件,则返回-1.

```javascript
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
```

## @ 数组实例的`fill()`

fill方法使用给定值,填充一个数组.

```javascript
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```

## @ 数组实例的`includes()`

`Array.prototype.includes`方法返回一个布尔值,表示某个数组是否包含给定的值,与字符串的`includes`方法类似.该方法属于`ES7`,但`Babel`转码器已经支持.

```javascript
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, NaN].includes(NaN); // true
```
