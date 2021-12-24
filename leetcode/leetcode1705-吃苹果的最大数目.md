### 吃苹果的最大数目
有一棵特殊的苹果树，一连 n 天，每天都可以长出若干个苹果。在第 i 天，树上会长出 apples[i] 个苹果，这些苹果将会在 days[i] 天后（也就是说，第 i + days[i] 天时）腐烂，变得无法食用。也可能有那么几天，树上不会长出新的苹果，此时用 apples[i] == 0 且 days[i] == 0 表示。

你打算每天 最多 吃一个苹果来保证营养均衡。注意，你可以在这 n 天之后继续吃苹果。

给你两个长度为 n 的整数数组 days 和 apples ，返回你可以吃掉的苹果的最大数目。

##### 示例 1:

    输入：apples = [1,2,3,5,2], days = [3,2,1,4,2]
    输出：7
    解释：你可以吃掉 7 个苹果：
    - 第一天，你吃掉第一天长出来的苹果。
    - 第二天，你吃掉一个第二天长出来的苹果。
    - 第三天，你吃掉一个第二天长出来的苹果。过了这一天，第三天长出来的苹果就已经腐烂了。
    - 第四天到第七天，你吃的都是第四天长出来的苹果

##### 示例2:

    输入：apples = [3,0,0,0,0,2], days = [3,0,0,0,0,2]
    输出：5
    解释：你可以吃掉 5 个苹果：
    - 第一天到第三天，你吃的都是第一天长出来的苹果。
    - 第四天和第五天不吃苹果。
    - 第六天和第七天，你吃的都是第六天长出来的苹果。

### 解题思路: 贪心 + 优化队列

```js
/**
 * @param {number[]} apples
 * @param {number[]} days
 * @return {number}
 */
var eatenApples = function (apples, days) {
    const n = apples.length
    const heap = new Heap([], (a, b) => a[1] > b[1])
    let i = 0
    let res = 0
    while (i < n || heap.size) {
        if (i < n && apples[i] > 0) heap.push([apples[i], i + days[i]])
        while (heap.size && (heap.top[0] === 0 || heap.top[1] < i + 1)) heap.pop()
        if (heap.size) {
            heap.top[0]--
            res++
        }
        i++
    }
    return res
};

class Heap {
    constructor(data, cmp) {
        this.data = [null, ...data]
        this.cmp = cmp
        for (let i = this.data.length >> 1; i > 0; i--) {
            this.down(i)
        }
    }
    get size() {
        return this.data.length - 1
    }
    get top() {
        return this.data[1]
    }
    swap(i, j) {
        [this.data[i], this.data[j]] = [this.data[j], this.data[i]]
    }
    up(x) {
        if (x <= 1) return
        const p = x >> 1
        if (this.cmp(this.data[p], this.data[x])) {
            this.swap(x, p)
            this.up(p)
        }
    }
    down(x) {
        const y = x;
        const n = this.data.length;
        if (x >= n) return
        const l = x << 1
        const r = l + 1
        if (l < n && this.cmp(this.data[x], this.data[l])) x = l
        if (r < n && this.cmp(this.data[x], this.data[r])) x = r
        if (x !== y) {
            this.swap(x, y)
            this.down(x)
        }
    }
    push(item) {
        this.up(this.data.push(item) - 1)
    }
    pop() {
        this.swap(1, this.data.length - 1)
        const res = this.data.pop()
        this.down(1)
        return res
    }
}
```
