### 从英文中重建数字
给你一个字符串 s ，其中包含字母顺序打乱的用英文单词表示的若干数字（0-9）。按 升序 返回原始的数字。
例如，在 "abcd" 中交换下标 0 和下标 2 的元素可以生成 "cbad" 。

示例 1：
输入：s = "owoztneoer"
输出："012"

示例 2：
输入：s = "fviefuro"
输出："45"

### 解题思路：重点是每一个字符在字符串中出现的次数
zero  0  z 出现的此时就是0 的个数
two   2  t 出现的次数就是2 的个数
four  4  u 出现的次数就是4 的个数
six   6  x 出现的次数就是6 的个数
eight 8  g 出现的次数就是8 的个数
one   1  o 出现的次数就是减去 0、2 的个数就是1 的个数
three 3  t 出现的次数就是减去8 的个数就是3 的个数
five  5  f 出现的次数就是减去4 的个数就是5 的个数
seven 7  s 出现的次数就是减去6 的个数就是7 的个数
nine  9  i 出现的次数就是减去5、6、8 的个数 就是9 的个数

```js
/**
 * @param {string} s
 * @return {string}
 */
var originalDigits = function(s) {
    // 新建map 储存 每个字母出现的次数
    let map =new Map()
    for(let char of s){
        map.set(char, (map.get(char) || 0 ) + 1)
    }
    let arr =[]
    arr[0] = map.get('z') || 0
    arr[2] = map.get('w') || 0
    arr[4] = map.get('u') || 0
    arr[6] = map.get('x') || 0
    arr[8] = map.get('g') || 0
    arr[3] = (map.get('h') || 0) - arr[8]
    arr[5] = (map.get('f') || 0) - arr[4]
    arr[7] = (map.get('s') || 0) - arr[6]
    arr[1] = (map.get('o') || 0) - arr[0] -arr[2] -arr[4]
    arr[9] = (map.get('i') || 0) -arr[5] - arr[6] - arr[8]
    let res = ''
    arr.forEach((value,index)=>{
        if(value){
            // 重复次数repeat
            res += index.toString().repeat(value)
        }
    })
    return res
};
```