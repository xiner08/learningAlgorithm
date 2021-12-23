### 两数之和II-输入有序数组
给定一个已按照 非递减顺序排列  的整数数组 numbers ，请你从数组中找出两个数满足相加之和等于目标数 target 。

函数应该以长度为 2 的整数数组的形式返回这两个数的下标值。numbers 的下标 从 1 开始计数 ，所以答案数组应当满足 1 <= answer[0] < answer[1] <= numbers.length 。

你可以假设每个输入 只对应唯一的答案 ，而且你 不可以 重复使用相同的元素。

##### 示例 1:

    输入：numbers = [2,7,11,15], target = 9
    输出：[1,2]
    解释：2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。

##### 示例 2:
  
    输入：numbers = [2,3,4], target = 6
    输出：[1,3]

### 解题思路 ：二分查找
```js
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(numbers, target) {
    let left, right = numbers.length - 1, mid
    for (let i = 0; i < numbers.length; i++) {
        left = i + 1
        // 二分查找第二个数
        while (left <= right) {
            mid = left + Math.floor(((right - left) / 2))
            if (numbers[i] + numbers[mid] === target) {
                return [i + 1, mid + 1]
            } else if (numbers[i] + numbers[mid] > target) {
                right = mid - 1
            } else {
                left = mid + 1
            }
        }
    }
};
```
### 解题思路：双指针

```js
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(numbers, target) {
    let left = 0, right = numbers.length - 1
    while(left <= right){
        if(target === (numbers[left] + numbers[right])){
            return [left + 1, right + 1]
        }else if(target < (numbers[left]+numbers[right])){
            right --
        }else{
            left ++
        }
    }
    return [-1,-1]
}
```
