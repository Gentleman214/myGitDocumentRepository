# git


### git的三种状态
状态名|状态值|说明
-|-|-
已提交|committed|数据已经安全的保存在本地数据库中
已修改|modified|修改了文件，但还没保存到数据库中
已暂存|staged|表示对一个已修改文件的当前版本做标记，使之包含在下次提交的快照中

***
### git工作流程
1.在工作目录中修改文件；
2.暂存文件，将文件的快照放入暂存区域；
3.提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。

***

### 获取git仓库
#### 1.在现有项目中初始化仓库 
```bash
git init
git status  查看状态
```

***
### 版本回退
#### 1.查看历史记录
```bash
git log
git log --pretty=oneline   //一行显示
git log --graph --pretty=oneline --abbrev-commit  //图状显示
```
第一个参数(一大串类似1094adb...)的是commit ID(版本号)
#### 2.版本回退
- HEAD表示当前版本，HEAD^表示上一个版本，HEAD\^\^表示上上一个,HEAD~n表示往上第n个版本
```bash
git reset --hard HEAD^    //回到上个版本
git reset --hard 版本号    //指定回到某个版本
```
- 找不到版本号可以使用reflog命令还查看
```bash
git reflog    //查看所有分支的所有操作记录
```
#### 3.撤销修改
1. 丢弃工作区的修改
```bash
git checkout -- readme.md  //把readme.md在工作区的修改全部撤销
// readme.md还未暂存，执行上述命令后回退到与版本库一致
//readme.md暂存后又修改过，回退到暂存前
```
2. 丢弃暂存区的修改 
```bash
git reset HEAD readme.md
```
3. 总结
- 想直接丢弃工作区的修改时，用命令`git checkout -- file`
- 改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，然后继续第一步
- 已经提交了不合适的修改到版本库时，想要撤销本次提交，则版本回退，前提是还未push

#### 4.删除文件
```bash
git rm readme.md  
```

***
###  分支管理
#### 1.创建分支
```bash
git checkout -b dev  //创建并切换到dev分支
或
git switch -c dev 
```
```bash
git branch  //查看当前分支
```
```bash
//在分支上工作后
git add
git commit
```
```bash
git checkout master   或   git switch master  //切回主分支
git merge dev  //合并dev分支到当前分支(主分支) ->合并指定分支到当前分支
git merge --no-ff -m "merge with no-ff" dev //表示禁用Fast forward
```
#### 2.删除分支
```bash
git branch -d dev
```
#### 3."储藏"工作现场
```bash
git stash
git stash list  //查看储藏的工作现场
git stash pop  //恢复的同时删除stash
```
***
### 解决冲突
git merge dev时如果有冲突，需要手动解决

