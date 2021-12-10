### 有效的井字游戏
给你一个字符串数组 board 表示井字游戏的棋盘。当且仅当在井字游戏过程中，棋盘有可能达到 board 所显示的状态时，才返回 true 。

井字游戏的棋盘是一个 3 x 3 数组，由字符 ' '，'X' 和 'O' 组成。字符 ' ' 代表一个空位。

以下是井字游戏的规则：

- 玩家轮流将字符放入空位（' '）中。
- 玩家 1 总是放字符 'X' ，而玩家 2 总是放字符 'O' 。
- 'X' 和 'O' 只允许放置在空位中，不允许对已放有字符的位置进行填充。
- 当有 3 个相同（且非空）的字符填充任何行、列或对角线时，游戏结束。
- 当所有位置非空时，也算为游戏结束。
- 如果游戏结束，玩家不允许再放置字符。

### 解题思路： 利用规律求解
- x的数量比o的数量大于1或者相等
- x与o相等时，x不能为对角、一行、一列
- x大于o时，o不为对角、一行、一列

```js
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var truncateSentence = function(s, k) {
    let res = ''
    for(let i = 0, j = s.length; i < j; i++){
        if(s[i] === ' '){
            k--
        }
        if(k === 0){
            break
        }
        res += s[i]
    }
    return res
};
```

### 解题思路 ： 

```js
/**
 * @param {string[]} board
 * @return {boolean}
 */
var validTicTacToe = function (board) {
    const cnt = { O: 0, X: 0 };
    for (const line of board) {
        for (const xo of line) {
            if (xo !== ' ') cnt[xo]++;
        }
    }
    // 不符合两种情况
    if (cnt.O !== cnt.X && cnt.X - cnt.O !== 1) return false;
    // 获取不会赢的字符
    const will_not_win = cnt.X > cnt.O ? 'O' : 'X';
    // 两对角线
    if (board[0][0] === will_not_win && board[0][0] === board[1][1] && board[0][0] === board[2][2]) return false;
    if (board[0][2] === will_not_win && board[0][2] === board[1][1] && board[0][2] === board[2][0]) return false;
    for (let i = 0; i < 3; i++) {
        // 三行
        if (board[i][0] === will_not_win && board[i][0] === board[i][1] && board[i][0] === board[i][2]) return false;
        // 三列
        if (board[0][i] === will_not_win && board[0][i] === board[1][i] && board[0][i] === board[2][i]) return false;
    }
    return true;
};

```
