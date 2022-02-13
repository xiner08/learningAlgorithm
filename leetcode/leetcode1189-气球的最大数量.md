### 气球的最大数量
给你一个字符串 text，你需要使用 text 中的字母来拼凑尽可能多的单词 "balloon"（气球）。

字符串 text 中的每个字母最多只能被使用一次。请你返回最多可以拼凑出多少个单词 "balloon"。

##### 示例 1:

    输入：text = "nlaebolko"
    输出：1

##### 示例2:

    输入：text = "loonbalxballpoon"
    输出：2

### 解题思路:  用map将数据先保存下来，然后取map中的最小值，即可
- 时间复杂度 O(n)
```js
/**
 * @param {string} text
 * @return {number}
 */
var maxNumberOfBalloons = function(text) {
    let map = new Map([['a',0],['b',0],['l',0],['o',0],['n',0]])
    const n = text.length
    const BALLOON = 'balloon'
    for(let i = 0; i < n; i++){
        if(BALLOON.indexOf(text[i]) > -1){
            map.set(text[i], 1 + map.get(text[i]))
        }else{
            continue
        }
    }
    let min = n
    for(let i of map){
        if(i[0] === 'l' || i[0] === 'o'){
            min = Math.min(min, Math.floor(i[1]/2))
        }else{
            min = Math.min(min,i[1])
        }
    }
    return min
};
```
