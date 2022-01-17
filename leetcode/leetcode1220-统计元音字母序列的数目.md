### 统计元音字母序列的数目
给你一个整数n，请你帮忙统计一下我们可以按下述规则形成多少个长度为n的字符串：

字符串中的每个字符都应当是小写元音字母（'a', 'e', 'i', 'o', 'u'）
每个元音'a'后面都只能跟着'e'
每个元音'e'后面只能跟着'a'或者是'i'
每个元音'i'后面不能 再跟着另一个'i'
每个元音'o'后面只能跟着'i'或者是'u'
每个元音'u'后面只能跟着'a'
由于答案可能会很大，所以请你返回 模10^9 + 7之后的结果。


##### 示例 1:

    输入：n = 1
    输出：5
    解释：所有可能的字符串分别是："a", "e", "i" , "o" 和 "u"。

##### 示例2:

    输入：n = 2
    输出：10
    解释：所有可能的字符串分别是："ae", "ea", "ei", "ia", "ie", "io", "iu", "oi", "ou" 和 "ua"。

### 解题思路: 将可能的结果先存起来，注意申清楚题

```js
/**
 * @param {number} n
 * @return {number}
 */
/**
 * @param {number} n
 * @return {number}
 */
var countVowelPermutation = function(n) {
    if(n === 1) {
        return 5
    }     
    const mod = 1000000007
    let res  = 0, arr = ['a','e','i','o','u']
    let lastArr = {
            a: 1, e: 1, i: 1, o: 1, u: 1
    }
    for(let i = 1; i < n; i++){
        let originArr = {
             a: 0, e: 0, i: 0, o: 0, u: 0
        }
        for(let j = 0;j < 5; j++){
            switch(j){
                case 0:
                    originArr['e']+= (lastArr['a'] % mod)
                    break
                case 1:
                    originArr['a']+= lastArr['e']%mod
                    originArr['i']+= lastArr['e']%mod
                    break
                case 2:
                    originArr['a']+= lastArr['i']%mod
                    originArr['e']+= lastArr['i']%mod
                    originArr['o']+= lastArr['i']%mod
                    originArr['u']+= lastArr['i']%mod
                    break
                case 3:
                    originArr['i']+= lastArr['o']%mod
                    originArr['u']+= lastArr['o']%mod
                    break
                case 4:
                    originArr['a']+= lastArr['u']%mod
                break
            }
        }
        lastArr = originArr
        if(i === n - 1){
            for(let k of Object.values(lastArr)){
                res= (res + k)% mod
            }
        }
    }
    return res
};
```
