### k次去饭后最大化的数组和
给你一个整数数组 nums 和一个整数 k ，按以下方法修改该数组：
- 选择某个下标 i 并将 nums[i] 替换为 -nums[i] 。
重复这个过程恰好 k 次。可以多次选择同一个下标 i 。

以这种方式修改数组后，返回数组 可能的最大和 。
##### 示例 1:

    输入：nums = [4,2,3], k = 1
    输出：5
    解释：选择下标 1 ，nums 变为 [4,-2,3] 。

##### 示例 2:

    输入：nums = [3,-1,0,2], k = 3
    输出：6
    解释：选择下标 (1, 2, 2) ，nums 变为 [3,1,0,2] 。

##### 示例 3:

    输入：nums = [2,-3,-1,5,-4], k = 2
    输出：13
    解释：选择下标 (1, 4) ，nums 变为 [2,3,-1,5,4] 。

### 解题思路 ：核心是找到最小值，判断最小值的位置是否为第一位
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var largestSumAfterKNegations = function(nums, k) {
    nums.sort((a,b)=> a - b)
    while(k > 0){
        if(nums[0] === 0){
            break
        }else if(nums[0] > 0){
            nums[0] =  -nums[0]
            k--
        }else if(nums[0] < 0){
            nums[0] =  -nums[0]
            k--
            let minNum = Math.min(...nums)
            if(minNum ===  nums[0]){
                continue
            }else{
                let index = nums.indexOf(minNum)
                let mid = nums[0]
                nums[0] = minNum
                nums[index] = mid
            }
        }
    }
    return nums.reduce((a,b) =>a + b)
};
```

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var largestSumAfterKNegations = function(nums, k) {
    while(k > 0){
        nums.sort((a,b)=> a - b)
        if(nums[0] === 0){
            break
        }else{
            nums[0] = (nums[0]!= 0 ? -nums[0] : 0)
            k--
        }
    }
    return nums.reduce((a,b) =>a + b)
};
```


