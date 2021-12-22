### 搜索插入位置
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 O(log n) 的算法。

进阶：你可以设计并实现时间复杂度为 O(log n)的算法解决此问题吗？

##### 示例 1:

    输入: nums = [1,3,5,6], target = 5
    输出: 2

##### 示例 2:
  
    输入: nums = [1,3,5,6], target = 2
    输出: 1

### 解题思路 ：二分查找
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    const n = nums.length
    let left = 0, right = n - 1, ans = n;
    while (left <= right) {
        // >> 1 向左移一位
        let mid = ((right - left) >> 1) + left;
        if (target <= nums[mid]) {
            ans = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return ans
};
```

### 解题思路 ： 直接遍历数组，一一比较，得到所需要的结果
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    for(let i = 0,j = nums.length; i < j; i++){
        if(target <= nums[i]){
            return i
        }else if(target > nums[i] && i === j - 1){
            return j
        }
    }
};
```
