### require.context 工程化的引入多个文件
```js
require.context(directory, useSubdirectories, regExp, mode = 'sync')
```
- directory 表示检索的目录(绝对/相对)
- useSubdirectories 是否检索子目录 布尔
- regExp 匹配文件的正则
- mode 加载模式 (异步/同步)
只能在node环境中使用
封装处理的函数
```js
const importAll = (context, reg) => {
  const map = {}
  for (const key of context.keys()) {
    const keyArr = key.split('/')
    keyArr.shift() // 移除.
    map[keyArr.join('.').replace(reg, '')] = context(key)
  }
  return map
}
export default importAll
```

```js
import importAll from '$common/importAll'
const reg = '/.\js$/g'
export default importAll(require.context('./', true, reg), reg)
```