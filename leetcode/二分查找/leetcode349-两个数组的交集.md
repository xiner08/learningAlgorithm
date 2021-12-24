### 两个数组的交集
给定两个数组，编写一个函数来计算它们的交集。

##### 示例 1:

    输入：nums1 = [1,2,2,1], nums2 = [2,2]
    输出：[2]

##### 示例 2:
  
    输入：nums1 = [1,2,2,1], nums2 = [2,2]
    输出：[2]

### 解题思路 ：暴力解法，直接遍历
```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    let numsLength = nums1.length
    let nums2Length = nums2.length
    let res = new Set()
    for(let i = 0; i < numsLength; i++){
       for(let j = 0; j < nums2Length; j++){
           if(nums1[i] === nums2[j]){
               res.add(nums1[i])
           }
       }
    }
    return Array.from(res)
};
```
### 解题思路：双指针

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    nums1.sort((a,b)=>a-b)
    nums2.sort((a,b)=>a-b)
    let left1 = 0, right1 = nums1.length, left2 = 0,right2 = nums2.length
    let res = []
    while(left1 < right1 && left2 < right2){
         const num1 = nums1[left1], num2 = nums2[left2]
        if (num1 === num2) {
            if (!res.length || num1 !== res[res.length - 1]) {
                res.push(num1)
            }
            left1++
            left2++
        } else if (num1 < num2) {
            left1++
        } else {
            left2++
        }
    }
    return res
}
```
