### 统计特殊四元组
给你一个 下标从 0 开始 的整数数组 nums ，返回满足下述条件的 不同 四元组 (a, b, c, d) 的 数目 ：

nums[a] + nums[b] + nums[c] == nums[d] ，且
a < b < c < d

##### 示例 1:

    输入：nums = [1,2,3,6]
    输出：1
    解释：满足要求的唯一一个四元组是 (0, 1, 2, 3) 因为 1 + 2 + 3 == 6 。

##### 示例 2:

    输入：nums = [3,3,6,4,5]
    输出：0
    解释：[3,3,6,4,5] 中不存在满足要求的四元组。

### 解题思路： 暴力解法，直接遍历 
- 时间复杂度O(n^4)
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var countQuadruplets = function(nums) {
    let n = nums.length,res = 0 
    for(let a = 0;a < n; a++){
        for(let b = a + 1;b < n; b++){
            for(let c = b + 1;c < n; c++){
                for(let d = c + 1;d < n; d++){
                    if(nums[a]+nums[b]+nums[c] === nums[d]){
                        res ++ 
                    }
                }
            }
        }
    }
    return res
};
```

### 解题思路 ： a + b = d - c
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var countQuadruplets = function(nums) {
    const cnts = new Map()
    let ans = 0
    for(let i=1;i<nums.length-2;i++){
      for(let j=0;j<i;j++)
        if(cnts.has(nums[i] + nums[j])){
            cnts.set(nums[i] + nums[j], cnts.get(nums[i] + nums[j]) + 1)
        }
        else{
            cnts.set(nums[i] + nums[j], 1)
        }
      for(let j=i+2;j<nums.length;j++)
        if(cnts.has(nums[j] - nums[i+1])){
            ans += cnts.get(nums[j] - nums[i+1])
        }
    }
    return ans
};
```
