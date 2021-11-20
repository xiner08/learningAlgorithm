### 整数替换
给定一个正整数 n ，你可以做如下操作：
如果 n 是偶数，则用 n / 2替换 n 。
如果 n 是奇数，则可以用 n + 1或n - 1替换 n 。
n 变为 1 所需的最小替换次数是多少？ (1 <= n <= 2^31 - 1)


### 解题思路： 利用bfs 广度优先搜素实现，重点是要递归考虑到 n + 1 和 n - 1 那个会更小
```js
/**
 * @param {number} n
 * @return {number}
 */
var integerReplacement = function(n) {
    if(n === 1) return 0
    switch (n % 2) {
        case 0:
            return 1 + integerReplacement(n / 2) 
        case 1:
            return 1 + Math.min(integerReplacement(n + 1),integerReplacement(n - 1))
    }
};
```