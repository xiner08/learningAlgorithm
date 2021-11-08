### 最大子序和
给定一个整数数组nums，找到一个具有最大和的连续子数组(子数组最少包含一个元素)，返回其最大和

### 解题思路：动态规划的思想
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let ans = nums[0]
    let sum = 0
    for(let num of nums){
        if(sum > 0){
            sum += num
        }else{
            sum = num
        }
        ans = Math.max(ans,sum)
    }
    return ans
};
```