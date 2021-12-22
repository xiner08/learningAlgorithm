### 重复叠加字符串匹配
给定两个字符串a 和 b，寻找重复叠加字符串 a 的最小次数，使得字符串 b 成为叠加后的字符串 a 的子串，如果不存在则返回 -1。

注意：字符串 "abc"重复叠加 0 次是 ""，重复叠加 1 次是"abc"，重复叠加 2 次是"abcabc"。

##### 示例 1:

    输入：a = "abcd", b = "cdabcdab"
    输出：3
    解释：a 重复叠加三遍后为 "abcdabcdabcd", 此时 b 是其子串。

##### 示例2:

    输入：a = "a", b = "aa"
    输出：2

### 解题思路：b中是有a
- 先判断b中是否有(a+a)，有的话，说明b中重复a又可能大于4个，否则小于4
- 重点要想到 a + a 来判断是否有两个a
- 重点要想到 a + a + a 来判断是否有三个a

```js
/**
 * @param {string} a
 * @param {string} b
 * @return {number}
 */
var repeatedStringMatch = function(a, b) {
    if(a === b){
        return 1
    }
    let index =  b.indexOf(a + a)
    let res = 0
    while(index > -1){
        res += 2
        b = b.replace((a+a),'')
        index = b.indexOf(a+a)
    }
    if(!b.length){
        return res
    }else{
        let curJudge = judgeTimes(a,b)
        if(curJudge === -1){
            return -1
        }else{
            return res + curJudge
        }
    }
}
// b中没有一个完整的a
function judgeTimes(a, b){
    let bIndex = b.indexOf(a)
    let aIndex = a.indexOf(b)
    let aIndexTwice = (a+a).indexOf(b)
    let aIndexThree = (a+a+a).indexOf(b)
    if(bIndex > -1){
        if(aIndexTwice > -1 ){
            return 2
        }else if(aIndexThree> -1){
            return 3
        }else{
            return -1
        }
    }else{
        if(aIndex === -1 && aIndexTwice > -1){
            return 2
        }else if(aIndex > -1){
            return 1
        }else{
            return -1
        }
    }
} 
```
