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

