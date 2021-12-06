### 赎金信
为了不在赎金信中暴露字迹，从杂志上搜索各个需要的字母，组成单词来表达意思。

给你一个赎金信 (ransomNote) 字符串和一个杂志(magazine)字符串，判断 ransomNote 能不能由 magazines 里面的字符构成。

如果可以构成，返回 true ；否则返回 false 。

magazine 中的每个字符只能在 ransomNote 中使用一次。

##### 示例 1:

    输入：ransomNote = "a", magazine = "b"
    输出：false

##### 示例 2:

    输入：ransomNote = "aa", magazine = "ab"
    输出：false

##### 示例 3:

    输入：ransomNote = "aa", magazine = "aab"
    输出：true 

### 解题思路 ：遍历前者，并将后者的字符一一删除
```js
/**
 * @param {string} ransomNote
 * @param {string} magazine
 * @return {boolean}
 */
var canConstruct = function(ransomNote, magazine) {
    if(magazine.length < ransomNote.length){
        return false
    }
    for(let i=0,j = ransomNote.length; i < j; i++ ){
        let index = magazine.indexOf(ransomNote[i])
        if(index > -1){
            // magazine
            magazine = magazine.slice(0, index)+ magazine.slice(index + 1,magazine.length)
        }else{
            return false
        }
    }
    return true
};
```
```js
/**
 * @param {string} ransomNote
 * @param {string} magazine
 * @return {boolean}
 */
var canConstruct = function(ransomNote, magazine) {
    if(magazine.length < ransomNote.length){
        return false
    }
    for(let i=0,j = ransomNote.length; i < j; i++ ){
        let index = magazine.indexOf(ransomNote[i])
        if(index > -1){
          // 不需要将字符删除，只需要改变即可
          magazine = magazine.replace(ransomNote[i],1)
        }else{
          return false
        }
    }
    return true
};
```


