### 旋转字符串
给定两个字符串, s 和 goal。如果在若干次旋转操作之后，s 能变成 goal ，那么返回 true 。

s 的 旋转操作 就是将 s 最左边的字符移动到最右边。 

例如, 若 s = 'abcde'，在旋转一次之后结果就是'bcdea' 。


##### 示例 1：

    输入: s = "abcde", goal = "cdeab"
    输出: true

##### 示例 2：

    输入: s = "abcde", goal = "abced"
    输出: false

### 解题思路1：
- 先找到s首字母在goal的位置
- 根据位置确定首字母之前和之后的字符串相加是否与s相等确认

```js
/**
 * @param {string} s
 * @param {string} goal
 * @return {boolean}
 */
var rotateString = function(s, goal) {
    const sLength = s.length, gLength =goal.length
    if(sLength !== gLength){
        return false
    }
    let sleft = s[0]
    let index = goal.indexOf(sleft)
    while(index > -1){
        let front = goal.slice(0,index)
        let after = goal.slice(index)
        if(after + front === s){
            return true
        }else{
            index = goal.indexOf(sleft, index + 1)
        }
    }
    return false
};
```

### 解题思路2：

```js
/**
 * @param {string} s
 * @param {string} goal
 * @return {boolean}
 */
var rotateString = function(s, goal) {
   return s.length === goal.length && (s + s).indexOf(goal) !== -1
};
```