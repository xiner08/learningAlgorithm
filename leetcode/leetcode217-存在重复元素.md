### 给定一个数组，判断是否存在重复元素
如果存在一值在数组中出现至少两次，函数返回true,如果数组中每个元素都不相同，则返回false

### 解题思路1：使用数组去重的方式，判断新旧长度是否相等
```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
    let numLen = nums.length
    let numLenRepeat = Array.from(new Set(nums)).length
    return numLen === numLenRepeat ?  false : true 
};  
```

### 解题思路3：用set的size属性去判断长度是否与原来相同
```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
    return new Set(nums).size !== nums.length
}
```

### 解题思路2：用map的has属性去判断当前值是否存在
```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
    let arrMap = new Map()
     for(let i of nums){
        if(arrMap.has(i)){
            return true
        }else{
            arrMap.set(i, 1)
        }
    }
    return false
}
```
