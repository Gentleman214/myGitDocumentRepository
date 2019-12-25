# node
## node内置模块
### 1.fs
- 读文件 fs.readFile
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
- 写文件 fs.write
writeFile()的参数依次为文件名、数据和回调函数。如果传入的数据是String，默认按UTF-8编码写入文本文件，如果传入的参数是Buffer，则写入的是二进制文件。回调函数由于只关心成功与否，因此只需要一个err参数。
```js
/* 异步 */
var data = 'hello node.js'
fs.writeFile('out.txt', data, function (err) {
  if (err) {
    console.log(err)
  } else console.log('ok')
})

/* 同步 */
fs.writeFileSync('output.txt', data);
```
- 获取文件信息通过fs.stat()，它返回一个Stat对象
stat.isFile() stat.isDirectory() stat.size stat.birthtime stat.mtime
