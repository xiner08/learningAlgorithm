### 各位相加
给定一个非负整数 num，反复将各个位上的数字相加，直到结果为一位数。返回这个结果。

##### 示例 1：

    输入: num = 38
    输出: 2 
    解释: 各位相加的过程为：
    38 --> 3 + 8 --> 11
    11 --> 1 + 1 --> 2
    由于 2 是一位数，所以返回 2。

##### 示例 2：

    输入: num = 0
    输出: 0

### 解题思路：

```js

```
### 解题思路：
- 先将num转化为str，然后又转化为数组
- 利用数组的reduce求和

```js
/**
 * @param {number} num
 * @return {number}
 */
var addDigits = function(num) {
    if(num < 10){
        return num
    }else{
       return addDigits( (`${num}`).split('').reduce((a,b)=> Number(a) + Number(b)))
    }
};
```