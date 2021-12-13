### 保持城市天际线
在二维数组grid中，grid[i][j]代表位于某处的建筑物的高度。 我们被允许增加任何数量（不同建筑物的数量可能不同）的建筑物的高度。 高度 0 也被认为是建筑物。

最后，从新数组的所有四个方向（即顶部，底部，左侧和右侧）观看的“天际线”必须与原始数组的天际线相同。 城市的天际线是从远处观看时，由所有建筑物形成的矩形的外部轮廓。 请看下面的例子。

建筑物高度可以增加的最大总和是多少？

##### 示例 1:

    例子：
    输入： grid = [[3,0,8,4],[2,4,5,7],[9,2,6,3],[0,3,1,0]]
    输出： 35
    解释： 
    The grid is:
      [ [3, 0, 8, 4], 
      [2, 4, 5, 7],
      [9, 2, 6, 3],
      [0, 3, 1, 0] ]
    从数组竖直方向（即顶部，底部）看“天际线”是：[9, 4, 8, 7]
    从水平水平方向（即左侧，右侧）看“天际线”是：[8, 7, 9, 3]
    在不影响天际线的情况下对建筑物进行增高后，新数组如下：
    gridNew = [ [8, 4, 8, 7],
              [7, 4, 7, 7],
              [9, 4, 8, 7],
              [3, 3, 3, 3] ]

### 解题思路 ： 时间复杂度 O(n^2)

- 先将每一行、每一竖的最大值找到
- 取最大值中的最小值，与原来该位置的数相减求和，即可
```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var maxIncreaseKeepingSkyline = function(grid) {
    let rowLength = grid.length
    let colLength = grid[0].length
    let rowArr = new Array(rowLength)
    let colArr = new Array(colLength)
    for(let i = 0; i < rowLength; i++ ){
        rowArr[i] = Math.max.apply(null,grid[i])
        for(let j = 0; j < colLength; j++){
            if(colArr[j]){
                colArr[j] = Math.max(colArr[j],grid[i][j])
            }else{
                colArr[j] = grid[i][j]
            }
        }
    }
    let sum = 0
     for(let i = 0; i < rowLength; i++ ){
        for(let j = 0; j < colLength; j++ ){
           sum +=(Math.min(rowArr[i],colArr[j]) -grid[i][j])
        }
    }
    return sum
};
```