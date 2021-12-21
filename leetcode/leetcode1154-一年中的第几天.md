### 一年中的第几天
给你一个字符串date ，按 YYYY-MM-DD 格式表示一个 现行公元纪年法 日期。请你计算并返回该日期是当年的第几天。

通常情况下，我们认为 1 月 1 日是每年的第 1 天，1 月 2 日是每年的第 2 天，依此类推。每个月的天数与现行公元纪年法（格里高利历）一致。

##### 示例 1:

    输入：date = "2019-01-09"
    输出：9

##### 示例2:

    输入：date = "2019-02-10"
    输出：41

### 解题思路:  先将每月的天数保存下来，然后相加即可

```js
/**
 * @param {string} date
 * @return {number}
 */
var dayOfYear = function(date) {
    let res = 0
    let dateArr = date.split('-')
    let dateArrY = Number(dateArr[0])
    let dateArrM = Number(dateArr[1])
    let dateArrD = Number(dateArr[2])
    let dateObj = [31,28,31,30,31,30,31,31,30,31,30,31]
    if((dateArrY % 4 === 0 && dateArrY % 100 !== 0) || dateArrY % 400 === 0){
        dateObj[1] =29
    }
    if(dateArrM === 1){
        return  res += dateArrD
    }else{
        for(let i = 0;i < dateArrM;i++){
            if(dateArrM - 1 === i){
                 res += dateArrD
            }else{
                res += dateObj[i]
            }
        }
        return res
    }
    
};
```
