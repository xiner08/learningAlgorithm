### 存在重复元素II
给你一个整数数组 nums 和一个整数 k ，判断数组中是否存在两个 不同的索引 i 和 j ，满足 nums[i] == nums[j] 且 abs(i - j) <= k 。如果存在，返回 true ；否则，返回 false 。

##### 示例 1:

    输入：nums = [1,2,3,1], k = 3
    输出：true

##### 示例 2:

    输入：nums = [1,0,1,1], k = 1
    输出：true

##### 提示:

    1 <= nums.length <= 10^5
    -10^9 <= nums[i] <= 10^9
    0 <= k <= 10^5

### 解题思路： 使用map先将之前的值保存下来，然后再进行比较是否重复
- 时间复杂度 O(n)
- 空间复杂度 O(n)

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
var containsNearbyDuplicate = function(nums, k) {
    if(!k){
        return false
    }
    const nLength = nums.length
    let isRepeat = false
    let map = new Map()
    map.set(nums[0],0)
    for(let i = 1;i < nLength; i++){
      // map.has 的时间复杂度 O(1)
       if(map.has(nums[i]) && i - map.get(nums[i])<= k){
           return true
       }
       map.set(nums[i],i)
    }
    return isRepeat
};
```

### 解题思路： 暴力解法
- 时间复杂度 O(n^2)
- 空间复杂度 O(1)
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
var containsNearbyDuplicate = function(nums, k) {
    if(!k){
        return false
    }
    const nLength = nums.length
    let isRepeat = false
    for(let i = 0;i < nLength - 1; i++){
        for(let j = i + 1; j < nLength; j++){
            if(j>i+k){
                break
            }
            if(nums[i] === nums[j]){
                return true
            }
        }
    }
    return isRepeat
};  
```
