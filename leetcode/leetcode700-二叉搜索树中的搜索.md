### 二叉搜索树中的搜索
给定二叉搜索树（BST）的根节点和一个值。 你需要在BST中找到节点值等于给定值的节点。 返回以该节点为根的子树。 如果节点不存在，则返回 NULL。
##### 示例：

    给定二叉搜索树:
            4
          / \
          2   7
        / \
        1   3
    和值: 2
##### 你应该返回如下子树:

      2     
     / \   
    1   3
在上述示例中，如果要找的值是 5，但因为没有节点值为 5，我们应该返回 NULL。

### 解题思路 ：利用深度优先搜索实现，BFS + 递归 

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
 * @param {number} val
 * @return {TreeNode}
 */
var searchBST = function(root, val) {
    if(!root) return null
    if(root.val === val) return root
    let treeLeft = searchBST(root.left, val)
    let treeRight = searchBST(root.right, val)
    let res = treeLeft || treeRight
    return res
};
```