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
  - 在package.json配置文件的scripts节点下，新增dev脚本(使用npm init -y 可以快速初始化一个包管理配置文件package.json)
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
"dev":"webpack" //script节点下的脚本，可以通过npm run执行
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
module。exports = {
  entry：path.join(__dirname,)
}
```