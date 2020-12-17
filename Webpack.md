------

#### webpack 4



##### webpack 是模块打包工具

##### 

##### 一些基本命令

```
npx webpack //  去执行项目内的包命令，需要安装 webpack-cli

npm info webpack // 查看版本历史

npx webpack --config webpackconfig.js // 使用别名的webpack配置文件
```



##### Es Module 引入导出规范

```
import Header from './header'

export default Header
```



##### CommonJs 引入导出规范

```
const Header = require('./header')

module.exports = Header
```



##### 在package.json  scripts 中

```
// 同在命令行执行 npx webpack
"bundle": "webpack"
npm run bundle
```



##### 打包输出对应的Chunk Names 在config文件中可以定义，默认为main

```
entry: {
	main: './src/index.js',
},
```



##### file-loader  url-loader

###### url-loader 在options配置项中多了 limit 参数，判断图片大小，来输出图片，还是base64 的图片地址



##### loader 的执行顺序从最后一个开始

```
{
  test: /\.scss$/,
  use: [
    'style-loader',
    'css-loader',
    'sass-loader'
  ]
}
```



##### 在一个scss文件中引入另一个scss文件，同时添加浏览器前缀

https://www.imooc.com/qadetail/224523

```
// webpack.config.js
{
      test: /\.scss$/,
      use: [
        'style-loader',
        {
          loader: 'css-loader',
          options: {
            importLoaders: 2
          }
        },
        'sass-loader',
        'postcss-loader'
      ]
    }
```

```
// postcss.config.js
// npm i postcss-import -D
module.exports = {
  plugins: [
    require('postcss-import'),
    require('autoprefixer')
  ]
}
```



##### html-webpack-plugin 打包结束后，自动生成一个html文件，并引入打包好的js文件



##### 使用clean-webpack-plugin删除重新生成打包文件夹

https://blog.csdn.net/qq_36242361/article/details/90709258

```
const {CleanWebpackPlugin} = require('clean-webpack-plugin')

new CleanWebpackPlugin()
```



##### devtool

```
// delelopment
devtool: 'cheap-module-eval-source-map',

// production
devtool: 'cheap-module-source-map',
```



##### 使用devServer来创建一个本地服务器

https://www.jianshu.com/p/bbb310251935

```
// webpack.config.js
// 还可以配置跨越 proxy
devServer: {
    contentBase: './dist',
    open: true,
    port: 8080,
  },
```



##### HMR 热更新

```
devServer: {
    hot: true,
    hotOnly: true // 热更新失效时，不要刷新页面
  },
```



##### 运行 dev-server 的时候，它自身有新特性，低版本浏览器会报错。建议你用 http-server，直接访问你编译后的代码，可以在低版本浏览器验证兼容性。





##### Tree Shaking

https://segmentfault.com/a/1190000015689240

只支持ES Module 的引入



```
// package.json
// 为false 时，则对 import 的来源文件，没有export的会忽略掉
"sideEffects": false,

// 要忽略一些import的文件时
"sideEffects": [*.css],

```



##### webpack 配置文件拆分

###### webpack-merge

```
const {merge} = require('webpack-merge') // 使用解构
```



##### Code Splitting

###### 同步代码

```
// webpack.config
optimization: {
    splitChunks: {
      chunks: 'all'
    }
  },
```

异步引入模块

异步动态引入js模块，需要安装babel-plugin-dynamic-import-webpack --save，并且在.babelrc中配置"plugins": ["dynamic-import-webpack"]



##### SplitChunksPlugin 配置参数

https://coding.imooc.com/lesson/316.html#mid=22364



###### webpack4.X修改SplitChunksPlugin.vendors.filename报错，解决：注释掉filename

https://segmentfault.com/a/1190000023050468



##### 打包分析

https://github.com/webpack-contrib/webpack-bundle-analyzer



##### 使用webpackPrefetch预加载模块（即在页面加载完成，再去加载交互js）

```
document.addEventListener('click', () => {
  import(/* webpackPrefetch: true */ './click.js').then(({default: fn}) => {
    fn()
  })
})
```



##### webpack.config -> output 设置 chunkFilename

```
output: {
    chunkFilename: '[name].chunk.js' // 异步引入模块时的文件名
  }
```



##### CSS文件的代码分割

###### 要注意原先配置的tree shaking，需要去设置sideEffects

```
// package.json
"sideEffects": [
    "*.css"
  ]
```



##### 关闭terminal 性能的 warning

```
webpack.config.js
performance: false,
```





##### Webpack 与浏览器缓存(Caching)

###### 打包的文件作用

```
main.hash.js // 业务代码
vendor.hash.js // 引入模块代码
```

###### 将js打包文件之间的关联代码抽离出来

旧版的webpack，不加这个，会导致每次打包，hash值都不一样

```
// webpack.common.js
runtimeChunk: {
      name: 'runtime'
    },
```

