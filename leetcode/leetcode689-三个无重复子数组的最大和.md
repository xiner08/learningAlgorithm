### 三个无重复子数组的最大和
给你一个整数数组 nums 和一个整数 k ，找出三个长度为 k 、互不重叠、且 3 * k 项的和最大的子数组，并返回这三个子数组。

以下标的数组形式返回结果，数组中的每一项分别指示每个子数组的起始位置（下标从 0 开始）。如果有多个结果，返回字典序最小的一个。

##### 示例 1:

    输入：nums = [1,2,1,2,6,7,5,1], k = 2
    输出：[0,3,5]
    解释：子数组 [1, 2], [2, 6], [7, 5] 对应的起始下标为 [0, 3, 5]。
    也可以取 [2, 1], 但是结果 [1, 3, 5] 在字典序上更大。

##### 示例 2:

    输入：nums = [1,2,1,2,1,2,1,2,1], k = 2
    输出：[0,2,4]

### 解题思路 ：滑动窗口的思路
- 一个数组的最大和
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var maxSumOfOneSubarrays = function(nums, k) {
    const ans = []
    let sum = 0,maxSum = 0
    for(let i = 0,j = nums.length; i < j; i++){
      sum += nums[i]
      if(i > k - 1){
        // 当有最大值时，改变ans中的索引
        if(sum > maxSum){
          maxSum = sum
          ans = [i - k + 1]
        }
        // 将之前的减去，使长度保持一致
        sum -= nums[i - k + 1]
      }
    }
    return ans
};
```
- 两个数组的最大和
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
const maxSumOfTwoSubarrays = (nums, k) => {
    const ans = [0, 0];
    let sum1 = 0, maxSum1 = 0, maxSum1Idx = 0;
    let sum2 = 0, maxSum12 = 0;
    for (let i = k; i < nums.length; ++i) {
        sum1 += nums[i - k];
        sum2 += nums[i];
        if (i >= k * 2 - 1) {
            if (sum1 > maxSum1) {
                maxSum1 = sum1;
                maxSum1Idx = i - k * 2 + 1;
            }
            if (maxSum1 + sum2 > maxSum12) {
                maxSum12 = maxSum1 + sum2;
                ans[0] = maxSum1Idx;
                ans[1] = i - k + 1;
            }
            sum1 -= nums[i - k * 2 + 1];
            sum2 -= nums[i - k + 1];
        }
    }
    return ans;
}
```
- 三个数组的最大和

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var maxSumOfThreeSubarrays = function(nums, k) {
     const ans = [0, 0, 0];
    let sum1 = 0, maxSum1 = 0, maxSum1Idx = 0;
    let sum2 = 0, maxSum12 = 0, maxSum12Idx1 = 0, maxSum12Idx2 = 0;
    let sum3 = 0, maxTotal = 0;
    for (let i = k * 2; i < nums.length; ++i) {
        sum1 += nums[i - k * 2];
        sum2 += nums[i - k];
        sum3 += nums[i];
        if (i >= k * 3 - 1) {
            if (sum1 > maxSum1) {
                maxSum1 = sum1;
                maxSum1Idx = i - k * 3 + 1;
            }
            if (maxSum1 + sum2 > maxSum12) {
                maxSum12 = maxSum1 + sum2;
                maxSum12Idx1 = maxSum1Idx;
                maxSum12Idx2 = i - k * 2 + 1;
            }
            if (maxSum12 + sum3 > maxTotal) {
                maxTotal = maxSum12 + sum3;
                ans[0] = maxSum12Idx1;
                ans[1] = maxSum12Idx2;
                ans[2] = i - k + 1;
            }
            sum1 -= nums[i - k * 3 + 1];
            sum2 -= nums[i - k * 2 + 1];
            sum3 -= nums[i - k + 1];
        }
    }
    return ans
};
```