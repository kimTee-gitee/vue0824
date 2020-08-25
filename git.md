### git 

git 是一个版本管理系统（VCS），可以在任何时间点，将文档的状态作为一份更新记录保存起来，并且在任意的时间点，恢复更新记录

#版本管理
版本管理是一种记录文件变化的方式，方便查阅特定版本号的文件内容

## 人为维护文档版本问题

1、文档数量紊多，命名不清晰，导致文档版本混乱
2、每次编译文档需要赋值，不方便
3、多人同时编辑一个文档，容易产生覆盖

<!-- # git工作流程 -->
## git使用
在使用git前，需要全局配置git

提交用户名  - git config --global user.name "用户名"
提交邮箱    - git config --gllobal user.email "邮箱"

**注：全局配置只执行一次，若需要修改，重复上述命令

## git提交命令
- git init 初始化git仓库
- git status 查看文件状态
- git add . 提交新增文件内容
- git commit -m "commit" 提交文件说明
- git log 查看提交记录
- git remote add origin https://gitee.com/xxxx/xxxxx.git  与远程仓库关联
- git push -u origin master  把本地分支推送到远程

- git clone https://gitee.com/xxxx/xxxxx.git  下载远程master分支

- git pull --rebase origin master  获取远程库与本地同步合并（远程仓库不为空）

- git remote remove origin 断开远程库与本地间的连接

 在git bash中移除本地与git之间的连接

- find . -name ".git" | xargs rm -Rf   移除本地与git之间的连接


# git分支
分支是当前工作目录中代码的一份副本，使用分支，可以让我们从开发支线上分离出来，以免影响开发主线
 #### 查看分支
 - git branch 查看本地分支
 - git branch -a 查看所有分支（本地与远程）
 - git branch -r 查看远程分支
 - git branch -vv 查看本地分支与远程分支之间的关联关系


- git branch 分支名/develop  创建新的分支
- git checkout 分支名/develop 切换分支（在暂存区中覆盖原工作目录中的分支）
- git rm --cached 分支名/develop 从暂存区删除分支
- git branch -d 分支名 删除分支（分支被合并后才允许删除）/（-D强制删除）  
- git merge 来源分支 合并分支
- git rest --hard commitID 从git仓库中将指定的更新记录恢复出来，覆盖暂存区和工作区

##### 主分支(master) 第一次向git仓库中提交更新是自动产生的分支
##### 开发分支(develop) 作为开发的分享，是基于master分支创建的
##### 功能分支(feature) 作为开发具体功能的分支，基于开发分支创建

分支间的关系
功能分支 -> 开发分支 -> 主分支

#### 暂时保存更改
提取分支上所有的改动并且存储起来，可以让开发人员有一个干净的工作副本，临时去网其他工作

应用场景:分支临时切换
*存储临时改动:git stash
*恢复改动:git stash pop

## git远程分支

#### 拉取远程git仓库里的指定分支到本地（本地不存在的分支）

- git checkout -b 本地分支 origin/远程分支  拉取远程里的分支（本地不存在）
- git checkout 分支名  切换分支  

若出现提示：
 fatal: Cannot update paths and switch to branch 'dev2' at the same time.
Did you intend to checkout 'origin/dev2' which can not be resolved as commit?

表示拉取不成功

则需要先执行
* git fetch
在执行
* git checkout -b 本地分支名 origin/远程分支名


#### 本地检出新分支并推送到远程
- git checkout -b develop 分支名 创建并切换本地分支
*[相当于 git branch dev  //创建分支
  git checkout dev  //选择分支
 ]
* 该分支是从当前分支检出的，所以文件内容与当前分支一样

- git branch origin develop 创建远程分支
- git push --set-upstream origin 分支名  推送本地分支到远程仓库

如果远程分支已存在，就在创建本地分支时与其关联
- git checkout -b 本地分支 origin/远程分支

### 合并分支
切回master 
- git checkout master 
- git merge 本地分支  合并分支
- git push origin master  推送

### 删除分支
- git branch -d dev  //删除本地分支
- git push origin -d dev  //删除远程分支



