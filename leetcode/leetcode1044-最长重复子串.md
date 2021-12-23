### 最长重复子串
给你一个字符串 s ，考虑其所有 重复子串 ：即，s 的连续子串，在 s 中出现 2 次或更多次。这些出现之间可能存在重叠。

返回 任意一个 可能具有最长长度的重复子串。如果 s 不含重复子串，那么答案为 "" 。

##### 示例 1:

    输入：s = "banana"
    输出："ana"

##### 示例 2:

    输入：s = "abcd"
    输出：""


### 解题思路 ：滑动窗口
```js
/**
 * @param {string} s
 * @return {string}
 */
var longestDupSubstring = function (s) {
  let maxStr = '',curStr = ''
  for (let i = 0, j = 0; i < s.length; i++) {
    curStr = curStr.replace(s[i - 1], '')
    while (curStr.length <= maxStr.length && j < s.length) {
      curStr += s[j], j++
      if (curStr.length > maxStr.length && s.lastIndexOf(curStr) > i){
            maxStr = curStr     
      } 
    }
  }
  return maxStr
};
```


