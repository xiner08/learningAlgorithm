### 第k个最小的素数分数
给你一个按递增顺序排序的数组 arr 和一个整数 k 。数组 arr 由 1 和若干 素数  组成，且其中所有整数互不相同。

对于每对满足 0 < i < j < arr.length 的 i 和 j ，可以得到分数 arr[i] / arr[j] 。

那么第 k 个最小的分数是多少呢?  以长度为 2 的整数数组返回你的答案, 这里 answer[0] == arr[i] 且 answer[1] == arr[j] 。

##### 示例1：

    输入：arr = [1,2,3,5], k = 3
    输出：[2,5]
    解释：已构造好的分数,排序后如下所示: 
    1/5, 1/3, 2/5, 1/2, 3/5, 2/3
    很明显第三个最小的分数是 2/5

##### 示例2:

    输入：arr = [1,7], k = 1
    输出：[1,7]

##### 提示：
- 2 <= arr.length <= 1000
- 1 <= arr[i] <= 3 * 104
- arr[0] == 1
- arr[i] 是一个 素数 ，i > 0
- arr 中的所有数字 互不相同 ，且按 严格递增 排序
- 1 <= k <= arr.length * (arr.length - 1) / 2

### 阶梯思路： 优先队列

```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number[]}
 */
var kthSmallestPrimeFraction = function(arr, k) {
    if (arr.length === 2) return arr
    if (k === 1)  return [arr[0], arr[arr.length - 1]]
    const len = arr.length - 1
    const mid = [len]
    const res = [arr[0] / arr[len]]
    let left = 0
    let right = len
    function findMin() {
        let min = 0
        for (let i = 0; i < mid.length; i++) {
            if (res[i] <= res[min]) {
                min = i
            }
        }
        return min
    }
    while (k--) {
      // 找到最小的
      left = findMin()
      right = mid[left]--
      res[left] = arr[left] / arr[mid[left]]
      if (mid[mid.length - 1] !== len) {
          mid.push(len)
          res.push(arr[res.length] / arr[len])
      }
    }
    return [arr[left], arr[right]]
};
```
### 解题思路：
- 对于分数来说 a/b < c/d,则可以的得出 a*d < b * c

```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number[]}
 */
var kthSmallestPrimeFraction = function(arr, k) {
    if (arr.length === 2) return arr
    if (k === 1) return [arr[0], arr[arr.length - 1]]
    const arrLen = arr.length;
    const res = [];
    for (let i = 0; i < arrLen - 1; ++i) {
        for (let j = i + 1; j < arrLen; ++j) {
            res.push([arr[i], arr[j]]);
        }
    }
    res.sort((x, y) => x[0] * y[1] - y[0] * x[1]);
    return res[k - 1];
  };
```

### 解题思路：
- 利用map将构成分数的数，储存卡来
- 将生成的新数组进行保存，并排序
```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number[]}
 */
var kthSmallestPrimeFraction = function(arr, k) {
    if (arr.length === 2) return arr
    if (k === 1) return [arr[0], arr[arr.length - 1]]
    let map = new Map()
    let newArr = []
    let arrLength = arr.length
    for(let i = 0; i < arrLength - 1; i ++){
        for(let j = i + 1; j <= arrLength -1; j++ ){
            map.set(arr[i]/arr[j],[arr[i],arr[j]])
            newArr.push(arr[i]/arr[j])
        }
    }
    newArr.sort((a,b) => a-b)
    return map.get(newArr[k-1])
};
```