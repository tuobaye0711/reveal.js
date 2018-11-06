# 细解JavaScript ES7 ES8 ES9 新特性

![Alt text](/img/es_16_17_18.png)

## ES7新特性（ECMAScript 2016）

![Alt text](/img/es2016.png)

ES7在ES6的基础上主要添加了三项内容：Array.prototype.includes()方法、求幂运算符（**）以及函数作用域中严格模式的变更。

###  Array.prototype.includes()方法

includes() 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。

```
var array = [1, 2, 3];

console.log(array.includes(2));
// expected output: true

var pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
// expected output: true

console.log(pets.includes('at'));
// expected output: false
```

Array.prototype.includes()方法接收两个参数：要搜索的值和搜索的开始索引。当第二个参数被传入时，该方法会从索引处开始往后搜索（默认索引值为0）。若搜索值在数组中存在则返回true，否则返回false。 且看下面示例：

```
['a', 'b', 'c', 'd'].includes('b')         // true
['a', 'b', 'c', 'd'].includes('b', 1)      // true
['a', 'b', 'c', 'd'].includes('b', 2)      // false
```

乍一看，includes的作用跟数组的indexOf重叠，为什么要特意增加这么一个api呢？主要区别有以下几点：

- 返回值。看一个函数，先看他们的返回值。indexOf的返回数是值型的，includes的返回值是布尔型，所以在if条件判断的时候includes要简单得多，而indexOf 需要多写一个条件进行判断。

```
var ary = [1];
if (ary.indexOf(1) !== -1) {
    console.log("数组存在1")
}
if (ary.includes(1)) {
    console.log("数组存在1")
}
```

- NaN的判断。如果数组中有NaN，你又正好需要判断数组是否有存在NaN，这时你使用indexOf是无法判断的，你必须使用includes这个方法。

```
var ary1 = [NaN];
console.log(ary1.indexOf(NaN))//-1
console.log(ary1.includes(NaN))//true
```

- 当数组的有空的值的时候，includes会认为空的值是undefined，而indexOf不会。

```
var ary1 = new Array(3);
console.log(ary1.indexOf(undefined));//-1
console.log(ary1.includes(undefined))//true
```

### 求幂运算符（**）
