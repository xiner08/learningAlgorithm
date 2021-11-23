### 打乱数组
给你一个整数数组 nums ，设计算法来打乱一个没有重复元素的数组。
实现 Solution class:
- Solution(int[] nums) 使用整数数组 nums 初始化对象
- int[] reset() 重设数组到它的初始状态并返回
- int[] shuffle() 返回数组随机打乱后的结果
### 解题思路：重点是要将原属组保存起来，并实现生成一个随机数 + 深copy
```js

/**
 * @param {number[]} nums
 * flat 数组扁平化
 */
var Solution = function(nums) {
    // this.originNum = nums.flat(Infinity)
    this.originNum = nums
    this.arrLengthLength = this.originNum.length
};

/**
 * @return {number[]}
 */
Solution.prototype.reset = function() {
    return this.originNum
};

/**
 * @return {number[]}
 * 深copy 数组的方法   
 *  slice 
 *  concat
 *  ...s
 *  JSON.parse(JSON.stringfy())
 */
Solution.prototype.shuffle = function() {
    let arr = []
    // 深copy 不影响原来的数据
    let arrFirst = JSON.parse(JSON.stringify(this.originNum))
    // let arrFirst = this.originNum.slice()
    for(let i = 0; i < this.arrLengthLength; i ++){
        // 那到一个随机数
        let randomNum = Math.floor(Math.random()*(this.arrLengthLength - i))
        arr.push(arrFirst[randomNum])
        arrFirst.splice(randomNum,1)
    } 
    return arr
};

/**
 * Your Solution object will be instantiated and called as such:
 * var obj = new Solution(nums)
 * var param_1 = obj.reset()
 * var param_2 = obj.shuffle()
 */
```