### 二叉树的坡度
给定一个二叉树，计算 整个树 的坡度 。
一个树的 节点的坡度 定义即为，该节点左子树的节点之和和右子树节点之和的 差的绝对值 。如果没有左子树的话，左子树的节点之和为 0 ；没有右子树的话也是一样。空结点的坡度是 0 。
整个树 的坡度就是其所有节点的坡度之和。

### 解题思路：利用bfc深度优先遍历，递归左侧和右侧的和，然后进行相加实现
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var findTilt = function(root) { 
    // 返回的结果
    let sum = 0
    function dfs (node) {
        // 若不存在，返回0
        if (!node)  return 0
        // 递归左侧的数据
        const left = dfs(node.left)
        // 递归右侧的数据
        const right = dfs(node.right)
        // 数据相加
        sum += Math.abs(left - right)
        // 返回当前的值
        return node.val + left + right
    }
    dfs(root)
    return sum
}
```