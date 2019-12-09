#  <center>webpack</center>
&emsp;
***
## 1.概念
前端构建工具，基于node.js开发的
- webpack解决的问题
  - 文件依赖关系错综复杂
  - 静态资源请求效率低
  - 模块化支持不友好
  - 浏览器对高级JavaScript特性兼容程度较低

- 使用
  - 安装 `npm i webpack webpack-cli -D`
  - 初始化 webpack.config.js
  - 在package.json配置文件的scripts节点下，新增dev脚本(使用npm init -y 可以快速初始化一个包管理配置文件package.json) /*script节点下的脚本，可以通过npm run执行*/
  - 使用`npm run dev`启动webpack进行项目打包
```js
/*webpack.comfig.js*/
module.exports = {
  mode: 'development'  //mode用来指定构建模式 development和production
}
```
```json
/*package.json*/
"scripts":{
"dev":"webpack"
}
```
&emsp;
***
## 2.webpack的基本使用
### 1.配置打包的入口和出口
- webpack 4.x 中的默认约定
  - 打包的入口文件为 src下的index.js，出口文件为dist下的main.js
- 如果要修改默认配置，可在webpack.config.js中加入如下配置
```js
const path =  require('path')  //导入node.js中 专门操作路径的模块
module.exports = {
  entry：path.join(__dirname,'./src/index.js'),//打包入口文件的路径
  output: {
    path:path.join(__dirname,'./dist'),//输出文件路径
    filename:'bundle.js'  //输出文件的名称
  }
}
```
### 2.webpack的自动打包功能
- 安装支持项目自动打包的工具
  - `npm i webpack-dev-server -D`
- 修改package.json的scripts标签的dev命令
  - `"dev": "webpack-dev-server"`
- 将script脚本的引用路径src改为'/buldle.js'
- 运行npm run dev
#### 相关参数的配置
```json
//package.json中的配置
// --open 打包完成后自动打开浏览器
// --host 配置ip地址
// --port 配置端口号
"scripts":{
  "dev": "webpack-dev-server --open --host 127.0.0.1 --port 8888"
}
```

### 3.webpack配置html-webpack-plugin生成预览页面
- 安装生成预览页面的插件
  - `npm i html-webpack-plugin -D`
- 修改webpack.config.js文件头部区域，添加如下配置信息
```js
const HtmlWebpackPlugin = require('html-webpack-plugin')
const htmlPlugin = new HtmlWebpackPlugin({
  template: './src/index.html',//指定要用到的模板文件
  filename: 'index.html' //指定生成的文件名称，该文件存在于内存中，在项目中不显示
})
```
- 修改webpack.config.js文件中向外暴露的配置对象，新增如下配置节点
```js
module.exports = {
  plugins: [htmlPlugin] //plugin数组是webpack打包期间会用到的一些插件列表
}
```
### 4.webpack中的加载器(打包非js模块)
在实际开发中，webpack默认只能打包以js结尾的文件，非.js结尾的文件只能调用loader加载器才可以正常打包
- less-loader可以打包处理.less相关的文件
- sass-loader可以打包处理.sass相关的文件
- url-loader可以打包处理css中与url路径相关的文件

#### 1.webpack中加载器的基本使用
##### (1)打包css文件
1. 安装css文件的loader
`npm i style-loader css-loader -D`
2. 在webpack.config.js的module对象中添加rules数组，在rules数组中添加loader规则
```js
module.exports {
  module:{
    rules:[
      { test:/\.css$/,use: ['style-loader','css-loader']}
    ]//test表示匹配的文件类型，use表示对应要调用的loader
  }
}
```
3.注意：多个loader的顺序是固定的，调用顺序是从后往前

##### (2)打包less文件
1. 安装less文件的loader
`npm i less-loader less -D`
2. 在webpack.config.js的module对象中添加rules数组，在rules数组中添加loader规则
```js
module.exports {
  module:{
    rules:[
      { test:/\.less$/,use: ['style-loader','css-loader','less-loader']}
    ]
  }
}
```
##### (3)打包scss文件
1. 安装scss文件的loader
`npm i sass-loader node-sass -D`
2. 添加loader规则
```js
module.exports {
  module:{
    rules:[
      { test:/\.scss$/,use: ['style-loader','css-loader','sass-loader']}
    ]
  }
}
```
##### (4)配置postCSS自动添加css的兼容前缀
1. `npm i postcss-loader autoprefixer -D`
2. 在项目的根目录下创建postcss的postcss.config.js，并初始化如下配置
```js
const autoprefixer = require('qutoprefixer')//导入自动添加前缀的插件
module.exports = {
  plugins: [autoprefixer] //挂载插件
}
```
3. 修改loader规则
```js
module.exports {
  module:{
    rules:[
      { test:/\.css$/,use: ['style-loader','css-loader','postcss-loader']}
    ]
  }
}
```
##### (5)打包样式表中的图片和字体文件
1. `npm i url-loader file-load -D`
2. 修改loader规则
```js
module.exports {
  module:{
    rules:[
      { 
      test:/\.jpg|png|gif|bmp|ttf|eot|svg|woff|woff2$/,
      use: 'url-loader?limit=16940'}
    ]
  }
}
//其中?之后的是loader的参数项
//limit用来指定图片的大小，单位是字节(byte)，只有小于limit大小的图片，才会被转为base64的图片
```
##### (6)打包处理js高级语法