### 查找和最小的k对数
给定两个以 升序排列 的整数数组 nums1 和 nums2,以及一个整数 k。

定义一对值(u,v)，其中第一个元素来自nums1，第二个元素来自 nums2。

请找到和最小的 k个数对(u1,v1), (u2,v2) ... (uk,vk)。


##### 示例 1:

    输入: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
    输出: [1,2],[1,4],[1,6]
    解释: 返回序列中的前 3 对数：
     [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]

##### 示例2:

    输入: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
    输出: [1,1],[1,1]
    解释: 返回序列中的前 2 对数：
     [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]

##### 提示:

    1 <= nums1.length, nums2.length <= 105
    -109 <= nums1[i], nums2[i] <= 109
    nums1 和 nums2 均为升序排列
    1 <= k <= 1000

### 解题思路 ： 时间复杂度 O(n^2)
暴力解法，直接遍历求和，可得
```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number[][]}
 */
var kSmallestPairs = function(nums1, nums2, k) {
    let oneLength = (nums1.length > 1000)? 1000 :nums1.length
    let twoLength = (nums2.length > 1000)? 1000 :nums2.length
    let arr =[] 
    for(let i = 0; i < oneLength; i++){
        for(let j = 0; j < twoLength; j++){
            if(i + j > 999){
                continue
            }
            arr.push([nums1[i],nums2[j]])
        }
    }
    arr.sort((a,b)=> a[0]- b[0]- b[1] + a[1])
    return arr.slice(0,k)
};
```