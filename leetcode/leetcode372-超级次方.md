### 超级次方
你的任务是计算 a^b 对 1337 取模，a 是一个正整数，b 是一个非常大的正整数且会以数组形式给出。

##### 示例 1:

    输入：a = 2, b = [3]
    输出：8

##### 示例 2:

    输入：a = 2, b = [1,0]
    输出：1024

##### 示例 3:

    输入：a = 2147483647, b = [2,0,0]
    输出：1198

### 解题思路 ：遍历前者，并将后者的字符一一删除

```js
/**
 * @param {number} a
 * @param {number[]} b
 * @return {number}
 */
var superPow = function(a, b) {
  const MOD = 1337
  if (b.length === 0 || a === 1) {
      return 1
  }
  const pow = b.pop()
  const last = quickPow(a, pow)
  const front = quickPow(superPow(a, b), 10)
  return (last * front) % MOD
  function quickPow(x, n) {
    if (n === 0){
        return 1
    }
    x %= MOD
    if (n < 0) return 1 / (quickPow(x, -n))
    const y = quickPow(x, Math.floor(n / 2))
    return n % 2 === 0 ? y * y % MOD : ((y * y % MOD) * x) % MOD
  }
};

```