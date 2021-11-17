### 最大单词长度乘积
给定一个字符串数组 words，找到 length(word[i]) * length(word[j]) 的最大值，并且这两个单词不含有公共字母。你可以认为每个单词只包含小写字母。如果不存在这样的两个单词，返回 0。

### 解题思路:  先将两个字符串去重，再去比较两者之和与合并后之和的长度即可实现
```js
/**
 * @param {string[]} words
 * @return {number}
 */
var maxProduct = function(words) {
    let maxRide = 0
    let wordLength = words.length
    for (let i = 0; i < wordLength; i++) {
       // 拿到初始的长度，保存下来
      let wordsFirstLen = words[i].length
      // 将第一个数据进行去重
      let wordsFirst = new Set(words[i])
      for (let j = i + 1; j < wordLength; j++) {
       // 拿到初始的长度，保存下来
        let wordsTwiceLen = words[j].length
        // 将第二个数据去重
        let wordsTwice = new Set(words[j])
        let curMax
        // 小写字母最多26个，大于26则就会重复
        if(wordsFirst.size + wordsTwice.size > 26){
          curMax = 0
        }else{
          // 将合并前的length与合并后去重的length进行比较
          curMax = ((wordsFirst.size + wordsTwice.size ) === new Set([...wordsFirst, ...wordsTwice]).size ? wordsFirstLen * wordsTwiceLen : 0)
        }
        // 比较取得最大值
        maxRide = Math.max(curMax, maxRide)
      }
    }
    return maxRide
};
```