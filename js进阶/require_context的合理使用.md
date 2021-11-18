### require.context 工程化的引入多个文件
```js
require.context(directory, useSubdirectories, regExp, mode = 'sync')
```
- directory 表示检索的目录(绝对/相对)
- useSubdirectories 是否检索子目录 布尔
- regExp 匹配文件的正则
- mode 加载模式 (异步/同步)
