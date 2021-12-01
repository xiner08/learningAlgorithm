### 连续字符
给你一个字符串 s ，字符串的「能量」定义为：只包含一种字符的最长非空子字符串的长度。
请你返回字符串的能量

##### 示例 1:

    输入：s = "leetcode"
    输出：2
    解释：子字符串 "ee" 长度为 2 ，只包含字符 'e' 。

##### 示例 2:

    输入：s = "abbcccddddeeeeedcba"
    输出：5
    解释：子字符串 "eeeee" 长度为 5 ，只包含字符 'e' 。

##### 示例 3:

    输入：s = "triplepillooooow"
    输出：5

### 解题思路 ：
- 先判断s的长度或者s是否有重复字符,返回定值1
- 然后遍历，将前面的字符保存一下，得出结果

```js
/**
 * @param {string} s
 * @return {number}
 */
var maxPower = function(s) {
    if(s.length === 1 || new Set(s).size === s.length){
        return 1
    }
    let arr = s.split('')
    let res = 1
    let maxPower = 1 
    let front = arr[0]
    for(let i = 1,j = arr.length;i < j; i++){
        if(front == arr[i]){
            res++
        }else{
            front = arr[i]
            res = 1
        }
        maxPower = Math.max(res,maxPower)
    }
    return maxPower
};
```

