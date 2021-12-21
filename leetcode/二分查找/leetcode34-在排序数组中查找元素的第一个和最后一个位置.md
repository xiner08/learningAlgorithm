### 在排序数组中查找元素的第一个和最后一个位置
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 target，返回[-1, -1]。

进阶：

你可以设计并实现时间复杂度为 O(log n)的算法解决此问题吗？

##### 示例 1:

    输入：nums = [5,7,7,8,8,10], target = 8
    输出：[3,4]

##### 示例 2:
  
    输入：nums = [5,7,7,8,8,10], target = 6
    输出：[-1,-1]

### 解题思路 ：二分查找
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function(nums, target) {
    let ans = [-1, -1]  
    // 找到左边的index
    let leftIndex = binarySearch(nums, target, true)
    // 找到右边的index
    let rightIndex = binarySearch(nums, target, false) - 1 
    // 满足下面的条件，才是ok的
    if(leftIndex <= rightIndex && rightIndex < nums.length && nums[leftIndex] === target && nums[rightIndex] === target){
        return [leftIndex, rightIndex]
    }
    return ans
};
function binarySearch(nums, target, lower){
  // left、right、mid 是二分的关键
    let left = 0,right = nums.length - 1, ans = nums.length
    while(left <= right){
        let mid = Math.floor((left + right) / 2)
        if(nums[mid] > target || (lower && nums[mid] >= target)){
            right = mid - 1
            ans = mid
        }else{
            left = mid + 1 
        }
    }
    return ans
}
```

### 解题思路 ： 使用js内置的 indexOf 和 lastIndexOf 直接找出相应的位置

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function(nums, target) {
    let numsLength = nums.length
    if(!numsLength){
        return [-1, -1]
    }
    return [nums.indexOf(target),nums.lastIndexOf(target)]
};
```