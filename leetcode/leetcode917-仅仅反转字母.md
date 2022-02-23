### 仅仅反转字母
给你一个字符串 s ，根据下述规则反转字符串：

所有非英文字母保留在原有位置。
所有英文字母（小写或大写）位置反转。

返回反转后的 s 。

##### 示例 1：

    输入：s = "ab-cd"
    输出："dc-ba"

##### 示例 2：

    输入：s = "a-bC-dEf-ghIj"
    输出："j-Ih-gfE-dCba"

### 解题思路：前后进行英文字母匹配，交换

```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseOnlyLetters = function(s) {
    // 先用正则对字符串判断是否是全字母
    const isAll = /^[a-zA-Z]+$/.test(s)
    if(isAll){
        return s.split('').reverse().join('')
    }
    let newS = s.split('')
    let left = 0,right = s.length - 1
    while(left < right){
        const isLeftCode = isLetter(newS[left])
        const isRightCode = isLetter(newS[right])
        if(isLeftCode && isRightCode){
            [newS[left],newS[right]] = [newS[right],newS[left]]
            left++
            right--
        }else{
            if(!isLeftCode){
                left++
            }
            if(!isRightCode){
                right--
            }
        }      
    }
    return newS.join('')
};

function isLetter(letter){
    const isCode = letter.charCodeAt()
   return (isCode >= 65 && isCode <= 90) || (isCode >= 97 && isCode <= 122)? true :false
}
```