## 静态方法
- length 数组的长度
- from es6新增
将类似数组的对象或者 set和map数据结构，转化为数组

```js
/**
 * 数组去重的方法 Array.from(new Set(数组本身))
*/
let setFirst = new Set('anaicuhscygstwftgvbnjcskwi')
console.log(Array.from(setFirst)) // ['a', 'n', 'i', 'c', 'u', 'h', 's', 'y', 'g', 't', 'w', 'f', 'v', 'b', 'j', 'k']
/**
 *  map 数据会转化为 二维数组
*/
let map = new Map()
map.set('asa',8)
map.set([1,27,9],8)
console.log(Array.from(map)) // [['asa',8],[[1,27,9],8]]
```
- isArray 
判断一个变量是不是数组
- of 
生成一个新的数组
```js
// 当入参只有一个时
let arr = Array(5)
console.log(arr) // [,,,,] 生成一个长度为传入值的一个空数组
let arr1 = Array.of(5)
console.log(arr1) // [5] 
``` 

## 实例方法
挂载到数组原型上的方法,每一个数组都有的方法
### es6之前的方法
- toString
  - 将数组转化为字符串
- toLocalString
  - 将数组转化为字符串
  - new Date  可以转化时间格式
  - 转化数字，其中会有‘，’
- concat 
  - 拼接两个或多个数组，
  - 返回一个新的数组，
  - 不改变原数组
  - 目前可以使用 ... 扩展运算符代替
- map
  - 数组的映射
  - 不改变原数组，返回一个新的数组
  - 数组的每一项没有返回值时，会返回undefined

- push
  - 向数组的末尾添加元素
  - 返回数组的长度
  - 改变原来的数组
- unshift
  - 将新项目添加到数组的开头
  - 返回一个新的长度
  - 改变原来的数组
- splice
  - 添加/删除数组
  - 必需有一个参数，可以有多个
    - 第一个参数，必需的，指定从什么位置开始
    - 第二个参数，可选的，删除的各数
    - 后面的参数，增加的元素
  - 返回一个新的数组，包含删除的元素
  - 改变原来的数组
- sort 
  - 数组排序
  - 改变原来的数组
  - a-b 正序，b-a 倒序

### es6新增的方法

- at 
根据数组的索引找数组的值，也可以为负值(从数组末尾开始查找，代替了 arr.length -1),不存在返回undefined

```js
let arr = ['jack','tom','aily','jeans']
console.log(arr.at(0)) //jack
console.log(arr.at(5)) // undefined
console.log(arr.at(-1)) // jeans
console.log(arr.at(-5)) // undefined
```


- keys、values、entries 
  - 将数组转化为 Genarate
  - 使用for of 进行遍历