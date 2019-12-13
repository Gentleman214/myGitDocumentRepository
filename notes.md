***
***
## 编辑并提交代码
### 1.master分支，拉取更新 git pull
### 2.切换到自己的分支并合并主分支  git merge master
### 3.如果要新建开发分支 
git branch chenjun-dev  //创建分支
git push origin chenjun-dev //推送到远程仓库
### 3.写完代码后git add  git commit  或 git commit -am 'xxx'
### 4.切回主分支 git pull  git merge 自己的分支
### 5.git push  //提交到主分支
### 6.git push origin 自己的分支    //提交到自己的分支
git add和git commit 可以简写为 git commit -am '',但 git commit -am 'update' 只能提交已经tracked即追踪过的文件，如果是新文件，必须使用分开的命令。

***
***



# notes

### 1.给浏览器设token
切换到console
前端直接在浏览器中强制设置token
document.cookie='token=63551fdc7cb04295bf8a810c4598b33e'

  /*testApiHost: 'https://www.yaya.cn'*/
  /*testApiHost: 'https://www.zlf.co'*/
  /*testApiHost: 'https://www.iteng.com'*/
  
  
  
### 2.export和export default的区别
#### export
1. export是按需导出，指定导出了哪个模块，用import接收时只能使用`import {} from ''`
2. export可以向外暴露多个成员，import时按需导入
3. export导出的成员，import接受名必须和导出名相同 `export var title = '导出'   import {title} from ''`
4. 如果接收时想换个名称，可以使用import information as info from ''

#### export default
1. export default向外暴露的成员，可以使用任意变量来接收
2. 在一个模块中，export default只允许向外暴露一次
3. 可以同时使用export default和export