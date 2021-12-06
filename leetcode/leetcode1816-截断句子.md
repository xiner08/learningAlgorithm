### 截断句子
句子 是一个单词列表，列表中的单词之间用单个空格隔开，且不存在前导或尾随空格。每个单词仅由大小写英文字母组成（不含标点符号）

例如，"Hello World"、"HELLO" 和 "hello world hello world" 都是句子。

给你一个句子 s​​​​​​ 和一个整数 k​​​​​​ ，请你将 s​​ 截断 ​，​​​使截断后的句子仅含 前 k​​​​​​ 个单词。返回 截断 s​​​​​​ 后得到的句子。

##### 示例 1:

    输入：s = "Hello how are you Contestant", k = 4
    输出："Hello how are you"
    解释：
    s 中的单词为 ["Hello", "how" "are", "you", "Contestant"]
    前 4 个单词为 ["Hello", "how", "are", "you"]
    因此，应当返回 "Hello how are you"

##### 示例 2:

    输入：s = "What is the solution to this problem", k = 4
    输出："What is the solution"
    解释：
    s 中的单词为 ["What", "is" "the", "solution", "to", "this", "problem"]
    前 4 个单词为 ["What", "is", "the", "solution"]
    因此，应当返回 "What is the solution"

### 解题思路： 利用遍历直接实现
```js
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var truncateSentence = function(s, k) {
    let res = ''
    for(let i = 0, j = s.length; i < j; i++){
        if(s[i] === ' '){
            k--
        }
        if(k === 0){
            break
        }
        res += s[i]
    }
    return res
};
```

### 解题思路 ： 利用自带的方法可以快速实现

```js
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var truncateSentence = function(s, k) {
    let arr = s.split(' ')
    if (k === 1) return arr[0]
    if (k === arr.length) return s
    return arr.slice(0, k).join(' ')

    // 或者直接实现，效率很低
    return s.split(' ').slice(0,k).join(' ')
};
```
