### 杨辉三角
给定一个非负整数 numRows，生成「杨辉三角」的前 numRows 行。
##### 示例 1:

    输入: numRows = 5
    输出: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

##### 示例 2:

    输入: numRows = 1
    输出: [[1]]

### 解题思路 ：多少行则内部数组的长度为几 且数组中的元素也跟索引有关

```js
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
    let arr = Array(numRows)
    for(let i = 0; i < numRows; i++){
        // 第一个值都是1
        let curArr = [1]
        if(i > 0){
            // 最后一个值都是1
            curArr[i] = 1
            // 往里面添加数据
            for(let j = 1; j < i; j ++){
                // 上一层的 j - 1 + j 等于这一层的 j
                curArr[j] = arr[i - 1][j - 1] + arr[i - 1][j]
            }
        }
        arr[i] = curArr
    }
    return arr
};
```