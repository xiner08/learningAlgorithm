### 有序数组中的单一元素
给你一个仅由整数组成的有序数组，其中每个元素都会出现两次，唯有一个数只会出现一次。

请你找出并返回只出现一次的那个数。

你设计的解决方案必须满足 O(log n) 时间复杂度和 O(1) 空间复杂度。

##### 示例 1:

    输入: nums = [1,1,2,3,3,4,4,8,8]
    输出: 2

##### 示例 2:

    输入: nums =  [3,3,7,7,10,11,11]
    输出: 10

### 解题思路：利用二分的思想，先进行比较，然后得出最后的结果
- 时间复杂度 O(logn)
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNonDuplicate = function(nums) {
    let left = 0,right = nums.length - 1
    while(left < right){
        const mid = Math.floor((right - left) / 2) + left
        // ^ 位异或，^ 1: 偶数 + 1，奇数 - 1
        if (nums[mid] === nums[mid ^ 1]) {
            left = mid + 1
        } else {
            right = mid
        }
    }
    return nums[left]
}
```

