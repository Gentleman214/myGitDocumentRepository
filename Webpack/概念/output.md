# 输出（output）
&emsp;&emsp;配置output可以控制webpack如何向硬盘中写入编译文件。即时可以存在多个入口文件，但只指定一个输出位置。
- 单入口对应的output配置
```javascript
const config = {
  output: {
    filename: 'bundle.js', // 输出的js文件名
    path: '/home/proj/public/assets' // 输出的位置， 必须是绝对路径
  }
}
module.exports = config
/* 
*此配置将一个单独的bundle.js文件打包到/home/proj/public/assets目录中
*path必须是绝对路径
*/
````
- 多入口起点对应的output配置
&emsp;&emsp;如果应用创建了多个入口起点或者使用了像CommonsChunkPlugin 这样的插件，则应该使用占位符来确保每个文件具有唯一的名称
```javascript
const config = {
  entry: {
    app: './src/app.js',
    vendor: './src/vendor.js'
  },
  output: {
    filename: [name].js
    path： path.resolve(__dirname, './dist')
  }
}
/*
*写入到硬盘：./dist/app.js, ./dist/search.js
*[name]就是占位符
*/
```