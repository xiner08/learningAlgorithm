## vue项目优化
### 框架版本
  - vue-cli 4.X
  - vue 2.X
### 对于项目进行优化，用到的技术有
- lighthouse 谷歌自带的性能监控插件(需要翻墙下载)
- vue-cli 3.X 以上自带的打包文件大小显示插件
### 优化的方向有:
  - 首屏渲染优化
  - webpack打包优化
  - vue代码优化
  - 开发优化

### 出现的原因：
  - 打包生成的vendor文件过大，需要加载完毕才能展示页面
  - 路由未配置懒加载，初始化加载了所有的路由

## 优化方案:

### 1. 若公司有自己的服务器，将三方js库，以CDN的形式引入(没有采用，没有CDN服务器) [webpack打包]
```js
// vue.config.js
configureWebpack: {
  externals: {
    'vue': 'Vue',
    'vue-router': 'VueRouter',
    'vuex': 'Vuex',
    'element-ui': 'ELEMENT',
    'axios': 'axios',
  }
}
// index.html
<body>
  <div id="app"></div>
  <script src="https://cdn.bootcss.com/vue/2.6.10/vue.min.js"></script>
  <script src="https://cdn.bootcss.com/vuex/3.1.0/vuex.min.js"></script>
  <script src="https://cdn.bootcss.com/vue-router/3.0.4/vue-router.min.js"></script>
  <script src="https://cdn.bootcss.com/axios/0.18.0/axios.min.js"></script>
  <script src="https://cdn.bootcss.com/element-ui/2.7.2/index.js"></script>
</body>
```

### 2. 路由配置懒加载，并可以配置 webpackChunkName [首屏渲染优化]
```js
{
    path: '/Login',
    name: 'Login',
    component: () = >import( /* webpackChunkName: "Login" */  '@/view/Login')
}
```

### 3. 删除预加载 [首屏渲染优化]
```js
// 删除预加载
chainWebpack: config =>{
  config.plugins.delete('prefetch')
}
```

### 4. js代码压缩 [首屏渲染优化，webpack打包优化]
```js
// 压缩js文件
chainWebpack: config =>{
  config.optimization.minimize(true)
}
```

### 5. 图片压缩 [首屏渲染优化，webpack打包优化]
```js
npm i image-webpack-loader --save-dev
// 对图片进行压缩
chainWebpack: config =>{
  config.module
    .rule('images')
    .test(/\.(png|jpe?g|gif)(\?.*)?$/)
    .use('image-webpack-loader')
    .loader('image-webpack-loader')
    .options({ bypassOnDebug: true })
    .end()
 }
```

### 6. webpack合理的使用分包策略 [首屏渲染优化，webpack打包优化]
```js
config.optimization = {
  splitChunks: {
    cacheGroups: {
      vendor: {
        chunks: 'initial',
        test: /[\\/]node_modules[\\/]/,
        name: 'vendor',
        minSize: 30000,
        minChunks: 1,
        priority: 10
      },
      common: {
        chunks: 'initial',
        test: /[\\/]src[\\/]js[\\/]/,
        name: 'common',
        minChunks: 2,
        minSize: 30000,
        priority: 6,
        reuseExistingChunk:true
      }
    }
  }
}
```

### 7. 开启gzip压缩，需要服务端使用nginx开启gzip [首屏渲染优化]
```js
npm i compression-webpack-plugin -D

const CompressionWebpackPlugin = require('compression-webpack-plugin')
const productionGzipExtensions = ['js', 'css']
plugins: [
  new CompressionWebpackPlugin({
    filename: '[path].gz[query]',
    algorithm: 'gzip',
    test: new RegExp('\\.(' + productionGzipExtensions.join('|') + ')$'),
    threshold: 10240,
    minRatio: 0.8
  })
]
```
### 8. 启动多线程打包 [webpack打包优化]
```js
parallel: require("os").cpus().length > 1
```
### 9. 修复热更新失效 [开发优化]
```js
// 修复热更新失效
config.resolve.symlinks(true)
```
## 完整的webpack vue.config.js
```js
const path = require('path');
// 环境判断
const isProduction = process.env.NODE_ENV === 'production'
// 代码压缩
const UglifyJsPlugin = require('uglifyjs-webpack-plugin');
// 开启gzip压缩
const CompressionWebpackPlugin = require('compression-webpack-plugin')
const productionGzipExtensions = ['js', 'css']

function resolve(dir) {
  return path.join(__dirname, dir)
}

module.exports = {
  chainWebpack: (config) => {
    config.resolve.alias
      .set('@', resolve('src'))
      .set('cube-ui', 'cube-ui/lib')
    // 修复热更新失效
    config.resolve.symlinks(true)
    // 生产环境配置
    if(isProduction){
      // 删除预加载
      config.plugins.delete('prefetch')
      // 压缩js文件
      config.optimization.minimize(true)
      // 代码分割
      config.optimization.splitChunks({
        chunks: 'all'
      })
    }
    // 对图片进行压缩
    config.module
      .rule('images')
      .test(/\.(png|jpe?g|gif)(\?.*)?$/)
      .use('image-webpack-loader')
      .loader('image-webpack-loader')
      .options({ bypassOnDebug: true })
      .end()
  },
  productionSourceMap: false,
  configureWebpack: config => {
    if(isProduction){
      config.plugins.push(
        new UglifyJsPlugin({
          uglifyOptions: {
              //生产环境自动删除console
              compress: {
                  drop_debugger: true,
                  drop_console: true,
                  pure_funcs: ['console.log']
              }
          },
          sourceMap: false,
          parallel: true
        }),
        new CompressionWebpackPlugin({
          filename: '[path].gz[query]',
          algorithm: 'gzip',
          test: new RegExp('\\.(' + productionGzipExtensions.join('|') + ')$'),
          threshold: 10240,
          minRatio: 0.8
        })
      )
    }
    config.optimization = {
      splitChunks: {
        chunks: 'all',
        cacheGroups: {
          vendor: {
            chunks: 'initial',
            test: /[\\/]node_modules[\\/]/,
            name: 'vendor',
            minSize: 30000,
            minChunks: 1,
            priority: 10
          },
          common: {
            chunks: 'initial',
            test: /[\\/]src[\\/]js[\\/]/,
            name: 'common',
            minChunks: 2,
            minSize: 30000,
            priority: 6,
            reuseExistingChunk:true
          }
        }
      },
      runtimeChunk: true
    }
  },
  publicPath: './',
  lintOnSave: process.env.NODE_ENV !== 'production',
  // 是否启动多线程打包
  parallel: require("os").cpus().length > 1
};

```

## 下面都是代码方面的优化
### 10. v-for 中key 不要使用索引, 且避免同时使用v-if
- v-for必须为item添加key, 且不为索引
在列表数据进行遍历渲染时，需要为每一项 item 设置唯一 key 值，方便 Vue.js 内部机制精准找到该条列表数据。当 state 更新时，新的状态值和旧的状态值对比，较快地定位到 diff 
- v-for 遍历避免同时使用v-if
V2.x 中v-for 比 v-if 优先级高，先会执行v-for，然后才执行 v-if，因此会先生成DOM，然后才会进行判断处理

### 11. Object.freeze 对data中的数据进行冻结，不进行响应式处理
在vue初始化时，会对data中的每一项进行Object.defineProperty 进行劫持，实现视图的响应数据，但当我们处理的数据不需要改变的时候，就不需要进行劫持，则可以使用，Object.freeze 对数据进行浅冻结，