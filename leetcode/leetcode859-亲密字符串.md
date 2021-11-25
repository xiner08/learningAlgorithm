### 亲密字符串
给你两个字符串 s 和 goal ，只要我们可以通过交换 s 中的两个字母得到与 goal 相等的结果，就返回 true ；否则返回 false 。
交换字母的定义是：取两个下标 i 和 j （下标从 0 开始）且满足 i != j ，接着交换 s[i] 和 s[j] 处的字符。例如，在 "abcd" 中交换下标 0 和下标 2 的元素可以生成 "cbad" 。
---
示例 1：
输入：s = "ab", goal = "ba"
输出：true
解释：你可以交换 s[0] = 'a' 和 s[1] = 'b' 生成 "ba"，此时 s 和 goal 相等。
---
示例 2：
输入：s = "ab", goal = "ab"
输出：false
解释：你只能交换 s[0] = 'a' 和 s[1] = 'b' 生成 "ba"，此时 s 和 goal 不相等。

### 解题思路：s的长度小于2 或者 两者长度不相等则返回false
- 当s和goal相等时，且s中有重复数字，则返回true
- 当s和goal相等时，主要进行不相等字符的判断

```js
/**
 * @param {string} s
 * @param {string} goal
 * @return {boolean}
 */
var buddyStrings = function(s, goal) {
    if(s.length !== goal.length || s.length < 2) return false   
    if(s.length > new Set(s).size && s === goal) return true
    let sLength = s.length 
    // 利用字符串拼接来证明两者相等 
    let diffFirst = ''
    let diffTwice = ''
    for(let i = 0; i < sLength; i++){
        if(s[i] !== goal[i]){
            diffFirst = s[i] + diffFirst
            diffTwice = diffTwice + goal[i]
        } 
    }
    return diffFirst.length === 2 && diffFirst === diffTwice 
};
```

```js
/**
 * @param {string} s
 * @param {string} goal
 * @return {boolean}
 */
var buddyStrings = function(s, goal) {
    // s的长度小于2 或者 两者长度不相等则返回false
    if(s.length !== goal.length || s.length < 2) return false   
    // 当s和goal相等时，且s中有重复数字，则返回true
    if(s.length > new Set(s).size && s === goal){
        return true
    } 
    let sLength = s.length 
    let diffFirst = []
    let diffTwice = []
    for(let i = 0; i < sLength; i++){
        if(s[i] !== goal[i]){
            diffFirst.push(s[i])
            diffTwice.push(goal[i])
        } 
    }
    // 数组长度等于2且元素会一一匹配
    return  (diffTwice.join('') === diffFirst.reverse().join('') && diffFirst.length === 2 ) ? true : false 
};
```
