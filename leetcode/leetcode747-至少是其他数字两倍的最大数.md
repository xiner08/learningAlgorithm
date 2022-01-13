### 至少是其他数字两倍的最大数
给你一个整数数组 nums ，其中总是存在 唯一的 一个最大整数 。

请你找出数组中的最大元素并检查它是否 至少是数组中每个其他数字的两倍 。如果是，则返回 最大元素的下标 ，否则返回 -1 。


请你找出并返回 words 中的 最短补全词 。题目数据保证一定存在一个最短补全词。当有多个单词都符合最短补全词的匹配条件时取 words 中 最靠前的 那个。
 
##### 示例 1:

    输入：nums = [3,6,1,0]
    输出：1
    解释：6 是最大的整数，对于数组中的其他整数，6 大于数组中其他元素的两倍。6 的下标是 1 ，所以返回 1 。

##### 示例 2:

    输入：nums = [1,2,3,4]
    输出：-1
    解释：4 没有超过 3 的两倍大，所以返回 -1 。

### 解题思路，找到最大和第二大，做比较，即可

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var dominantIndex = function(nums) {
    if(nums.length === 1){ return 0 }
    const nLength = nums.length
    const maxNum = Math.max.apply(null,nums)
    const index = nums.indexOf(maxNum)
    nums.sort((a,b)=>a-b)
    return  ( maxNum/2 >=nums[nLength-2])?index : -1
};
```