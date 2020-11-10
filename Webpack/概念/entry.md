# 入口文件
- 单个文件(简写)写法
```javascript
const config = {
  entry: './src/main.js'
}
module.exports = config
```
- 对象语法
```javascript
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
}
module.exports = config
```