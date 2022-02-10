### 最简分数
给你一个整数 n ，请你返回所有 0 到 1 之间（不包括 0 和 1）满足分母小于等于  n 的 最简 分数 。分数可以以 任意 顺序返回。

##### 示例 1:

    输入：n = 2
    输出：["1/2"]
    解释："1/2" 是唯一一个分母小于等于 2 的最简分数。

##### 示例 2:

    输入：n = 3
    输出：["1/2","1/3","2/3"]

### 解题思路:  暴力解法
- 时间复杂度 O(n^2)
```js
/**
 * @param {number} n
 * @return {string[]}
 */
var simplifiedFractions = function(n) {
    if(n === 1){
        return []
    }
    let res = []
    for(let i = 2; i <= n; i++){
        for(let j = 1; j < i; j++ ){
            if(j === 1){
                res.push(`${j}/${i}`)
            }else if(!Number.isInteger(i/j) && !commonFator(i,j)){
                res.push(`${j}/${i}`)
            }
        }
    }
    return res
};
function commonFator(x,y){
    for(let i = 2; i <= y; i++){
        if(Number.isInteger(x/i) && Number.isInteger(y/i)){
           return true
        }
    }
    return false
}
```
