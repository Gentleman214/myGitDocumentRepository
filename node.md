# node
## node内置模块
### 1.fs
```js
var fs = require('fs')

// 异步读文件
fs.readFile('sample.txt', 'utf-8', function(err, data){
  if(err){
    console.log(err)
  } else 
  console.log(data)
})

// 同步读文件
try {
  var data = fs.readFileSync('sample.txt', 'utf-8')
  console.log(data)
}
catch(err) {
  console.log(err)
}
```