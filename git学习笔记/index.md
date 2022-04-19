# Git学习笔记


# git的使用方法



## 基本命令

> 暂存区(将你的工作结果暂时保存,以便对比)

```shell
git add 		\\添加到暂存区
git status 		\\查看状态
git diff 		\\查看修改后的文件和暂存区的区别
git restore filename \\恢复文件到暂存区的状态(丢弃工作区的改动)
git restore --staged filename  		\\取消文件在暂存区(无论是删除还是多次修改,状态均为未提交,)

```

> HEAD(指向你最后一次提交的结果,相当于游戏里的存档)当前版本

```shell
git commit -m "提交的信息"
		   -a 可以将所有已跟踪文件中的执行修改或删除操作的文件都提交到本地仓库，即使它们没有经过git add添加到暂存区(新添加的文件不可以提交到仓库,建议不使用 -a)
		   --amend 追加提交(在不增加一个新的commid-id的情况下)
git log 查看提交日志
		   --pretty=online 一行展示
		   			short 简短展示
git log --graph --pretty=oneline --abbrev-commit
git reset HEAD^ 回退到上一个版本
		  HEAD^^ 上上一个版本
		  HEAD~100 上一百个版本
git reflog 查看每一次的commit命令(意味着查看到版本号就可以回到相应的版本去)
git checkout -- filename 撤销文件在工作区的修改
git rm filename 删除并且git add
		   
```

> 远程仓库

```shell
git remote add origin git@github.com:peapio/gittest.git
// 关联到远程仓库
git push origin master
master不存在,将会新建
$ git push origin :master
# 等同于
$ git push origin --delete master
表示删除master分支,相当于推送空的本地文件到远程分支
如果当前分支和远程分支存在追踪关系,则本地分支和远程分支都可以省略
git push -u origin master
上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。
```

## ssh key的添加

### 1.设置git的username和email

```sh	
git config --global user.name "peapio"
git config --global user.email  "aqiiii@yeah.net"	//github对应数据
git config -l查看当前配置
git config color.ui true 		git提示更明显
```



### 2.检查是否存在SSH Key

```sh
cd .ssh
ll
//查看是否有 id_rsa 和 id_rsa.pub 如果存在说明有SSH Key
```

### 3.生成SSH Key

```sh
ssh-keygen -t rsa -C "aqiiii@yeah.net"
enter
cat id_rsa.pub //复制密钥
```

### 4.GitHub添加SSH Key

设置->SSH

### 5.验证和修改

```sh
sh -T git@github.com
//运行结果出现类似如下
Hi peapio! You've successfully authenticated, but GitHub does not provide shell access.
```

> git支持多种协议,包括https,ssh,但ssh协议速度最快

## git分支管理

### 创建与合并

```sh
git checkout -b dev === git switch -c dev
创建并切换到dev分支
相当于
git branch dev
git checkout dev === git switch dev

git branch
查看当前分支
git meage dev 当前分支与dev分支合并(该分支变得和dev相同,在本分支没有改变之前时)
git merge --no-ff -m "merge with no-ff" dev
合并时保留信息,也就是多一个commit
git branch -d dev
删除dev分支
git branch -D dev
强制删除(适用于被删除的分支没有被merge)


```

团队合作时,分支应该看起来这样

![img](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)

### 修复bug分支

```sh
git stach 
储藏工作现场,以便于需要临时切换到别的分支,
git stach list 查看保存的工作现场
git stach apply		恢复
git stach drop	 	删除
或者
git stach pop 		恢复并删除
git stash apply stash@{0} 恢复指定
```

```sh
git cherry-pick 4c805e2
复制一次特定提交到当前分支(用与bug修复)
```

### Feature分支

> 每添加一个新功能可以新建一个Feature分支

```sh
git remote -v 		查看远程仓库的信息

```

### git标签

```sh
git tag <name>
git tag 		查看所有标签
git tag -d v1.0 删除标签
因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
git push origin <tagname>		推送某个标签到远程
git oush origin --tags			推送所有未推送到远程的本地标签
git push origin :refs/tags/<tagname> 删除一个远程标签
git tag <name> <commitid> 为忘记打标签的提交打标签
git show <tagname> 查看标签提交详细内容
git tag -a <tagname> -m "content" <commit_id
```

> :heavy_exclamation_mark:注意,标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

