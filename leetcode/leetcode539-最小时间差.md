### 最小时间差
给定一个 24 小时制（小时:分钟 "HH:MM"）的时间列表，找出列表中任意两个时间的最小时间差并以分钟数表示。

##### 示例 1:

    输入：timePoints = ["23:59","00:00"]
    输出：1

##### 示例 2:

    输入：timePoints = ["00:00","23:59","00:00"]
    输出：0

### 解题思路：先将时间都转化为分钟，然后进行排序，最后求最小值
- 时间复杂度 O(nlogn)
```js
/**
 * @param {string[]} timePoints
 * @return {number}
 */
var findMinDifference = function(timePoints) {
    const tLength = timePoints.length
    if (tLength > 1440) {
        return 0
    }
    let minuteArr = []
    for(let i = 0; i < tLength; i++){
        let curTime = timePoints[i].split(':')
        minuteArr.push(curTime[0] * 60 + Number(curTime[1]))
    }
    minuteArr.sort((a,b) => a - b)
    let min = 1440 - minuteArr[tLength - 1] + minuteArr[0]
    for(let j = 1; j < tLength; j++){
        min = Math.min(min,(minuteArr[j] - minuteArr[j-1]))
        // 存在最下值，不需要遍历了
        if(min === 0){
              return 0
        }
    }
    return min
};

```

### 解题思路：暴力方法，求差值实现 
- 时间复杂度 O(n^2)
```js
/**
 * @param {string[]} timePoints
 * @return {number}
 */
var findMinDifference = function(timePoints) {
    const tLength = timePoints.length
    let min = 720
    for(let i = 0; i < tLength -1; i++){
        for(let j = i + 1; j < tLength; j++){
            let cur = reduceNum(timePoints[i],timePoints[j])
            min = Math.min(min,cur)
            // 当存在最小值时，停止 向下遍历
            if(min === 0){
              return 0
            }
        }
    }
    return min
};

function reduceNum(first,second){
    let midMinute = 720,allMinute = 1440
    let firstTime = first.split(':')
    let firstMinute = Number(firstTime[0]) * 60 + Number(firstTime[1])
    let secondTime = second.split(':')
    let secondMinute = Number(secondTime[0]) * 60 + Number(secondTime[1])
    let absTime = Math.abs(secondMinute - firstMinute)
    if(absTime > midMinute){
        return allMinute - absTime
    }else{
        return absTime
    }
}
```