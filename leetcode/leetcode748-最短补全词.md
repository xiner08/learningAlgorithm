### 最短补全词
给你一个字符串 licensePlate 和一个字符串数组 words ，请你找出并返回 words 中的 最短补全词 

补全词 是一个包含 licensePlate 中所有的字母的单词。在所有补全词中，最短的那个就是 最短补全词 

在匹配 licensePlate 中的字母时：忽略 licensePlate 中的 数字和空格 ,不区分大小写。

如果某个字母在 licensePlate 中出现不止一次，那么该字母在补全词中的出现次数应当一致或者更多。
例如：licensePlate = "aBc 12c"，那么它的补全词应当包含字母 'a'、'b' （忽略大写）和两个 'c' 。可能的 补全词 有 "abccdef"、"caaacab" 以及 "cbca" 。

请你找出并返回 words 中的 最短补全词 。题目数据保证一定存在一个最短补全词。当有多个单词都符合最短补全词的匹配条件时取 words 中 最靠前的 那个。
 
##### 示例 1:

    输入：licensePlate = "1s3 PSt", words = ["step", "steps", "stripe","stepple"]
    输出："steps"
    解释：最短补全词应该包括 "s"、"p"、"s"（忽略大小写） 以及 "t"。
    "step" 包含 "t"、"p"，但只包含一个 "s"，所以它不符合条件。
    "steps" 包含 "t"、"p" 和两个 "s"。
    "stripe" 缺一个 "s"。
    "stepple" 缺一个 "s"。
    因此，"steps" 是唯一一个包含所有字母的单词，也是本例的答案。

##### 示例 2:

    输入：licensePlate = "1s3 456", words = ["looks", "pest", "stew", "show"]
    输出："pest"
    解释：licensePlate 只包含字母 "s" 。所有的单词都包含字母 "s" ，其中 "pest"、"stew"、和 "show" 三者最短。答案是 "pest" ，因为它是三个单词中在 words 里最靠前的那个。

### 解题思路: 时间复杂度O(n^2)
- 利用正则先对数据进行处理
- 遍历补全的数组，将数组每一项与licensePlate进行对比，找出合适的解

```js
/**
 * @param {string} licensePlate
 * @param {string[]} words
 * @return {string}
 */
var shortestCompletingWord = function(licensePlate, words) {
    licensePlate = licensePlate.toLocaleLowerCase()
    let curStr = licensePlate.replace(/[^a-z]+/ig,"")
    let curStrLength = curStr.length
    let res = ''
    for(let i = 0,j = words.length; i < j; i++){
        if(words[i].length < curStrLength){
            continue
        }
        let curWords = words[i]
        let curOrigin = words[i]
        for(let k = 0; k < curStrLength; k++){
           let index = curWords.indexOf(curStr[k])
           if(index > -1){
              curWords = curWords.replace(curStr[k],9)
           }else{
               break
           }
           if(k == curStrLength - 1 ){
               res = !res ? curOrigin : (curOrigin.length < res.length? curOrigin : res)
           }
        }
    }
    return res
}
```
