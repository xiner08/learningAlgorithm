### 差的绝对值为 K 的数对数目
给你一个整数数组nums和一个整数k，请你返回数对(i, j)的数目，满足i < j且|nums[i] - nums[j]| == k。

|x|的值定义为：

- 如果x >= 0，那么值为x。
- 如果x < 0，那么值为-x。

##### 示例 1:

    输入：nums = [1,2,2,1], k = 1
    输出：4
    解释：差的绝对值为 1 的数对为：
    - [1,2,2,1]
    - [1,2,2,1]
    - [1,2,2,1]
    - [1,2,2,1]
##### 示例2:

    输入：nums = [1,3], k = 3
    输出：0
    解释：没有任何数对差的绝对值为 3 。

### 解题思路： 暴力解法，现将数组排序，然后找到绝对值对应的数目
- 时间复杂度O(nlogn)
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var countKDifference = function(nums, k) {
    nums.sort((a,b) => a - b)
    const l = nums.length
    let res = 0
    for(let i = 0; i < l; i++){
      let curNjum = searchNum(nums,nums[i])
      if(searchNum(nums,nums[i] + k)){
          res += curNjum * searchNum(nums, nums[i] + k)
          i += curNjum - 1
      }
    }
    return res
};
function searchNum(arr,x){
    const firstIndex = arr.indexOf(x)
    const lastIndex = arr.lastIndexOf(x)
    if(firstIndex > -1){
        return lastIndex - firstIndex + 1
    }
    return 0
}
```
### 解题思路：使用map将每一个数存起来，然后在求和
- 时间复杂度 O(n)
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var countKDifference = function(nums, k) {
     let res = 0, n = nums.length
    const map = new Map()
    for (let j = 0; j < n; ++j) {
        res += (map.get(nums[j] - k) || 0) + (map.get(nums[j] + k) || 0)
        map.set(nums[j], (map.get(nums[j]) || 0) + 1)
    }
    return res
}
```