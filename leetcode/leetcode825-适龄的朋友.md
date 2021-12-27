### 适龄的朋友
在社交媒体网站上有 n 个用户。给你一个整数数组 ages ，其中 ages[i] 是第 i 个用户的年龄。

如果下述任意一个条件为真，那么用户 x 将不会向用户 y（x != y）发送好友请求：

- age[y] <= 0.5 * age[x] + 7
- age[y] > age[x]
- age[y] > 100 && age[x] < 100
否则，x 将会向 y 发送一条好友请求。

注意，如果 x 向 y 发送一条好友请求，y 不必也向 x 发送一条好友请求。另外，用户不会向自己发送好友请求。

返回在该社交媒体网站上产生的好友请求总数。

 
##### 示例 1:

    输入：ages = [16,16]
    输出：2
    解释：2 人互发好友请求。

##### 示例 2:

    输入：ages = [16,17,18]
    输出：2
    解释：产生的好友请求为 17 -> 16 ，18 -> 17 。

### 解题思路: 时间复杂度O(n^2)
- 直接两次遍历可得响应的结果

```js
/**
 * @param {number[]} ages
 * @return {number}
 */
var numFriendRequests = function(ages) {
    ages.sort((a, b)=> b - a)
    let res = 0,agesLength = ages.length,target
    for(let i = 0; i < agesLength - 1; i++){
        target = 0.5 * ages[i] + 7
       for(let j = i + 1;j < agesLength;j++){
           if(ages[j] <= target){
               break
           }else if(ages[j] === ages[i]){
                res += 2
           }else{
               res ++
           }
       }
    }   
    return res
};
```
