

## 一、 git配置
### 1、建立个人用户名称和邮件地址
```
git config --global user.name "wuwenchi"
git confit --global user.email "wuwenchihdu@hotmail.com"
```

### 2、更改git模式文本编辑器
```
git config --global core.editor vim
```

### 3、更改git默认差异分析工具
```
git config --global merge.too vimdiff
```

### 4、查看已有的配置信息
```
git config --list
```
或者
```
vim ~/.gitconfig
```

## 二、仓库
### 1、建立仓库
- ` git init ` 初始化仓库

- `git add .  ` 添加所有文件

- `git commit -m '初始项目版本'` 提交初始版本

- `git clone --bare <目录>` 会生成一个目录名+.git的文件夹，然后就可以去其他地方clone
- `git push origin master` 第一次push的时候可能会出错

### 2、克隆仓库
```
git clone <repo> <directory>
```
**其中**：
 - repo：git仓库
 - directory：本地目录

## 三、操作
` git reset --hard`

恢复到之前的仓库状态，如果之前暂存区有文件，则此文件会被清空
但是如果在工作区有新添加的文件，则此文件还会存在

`git status -s`

只看被更改的文件
红色的M：此文件被修改，但是没有被add
绿色的M：此文件被修改，并已经被add
红色的？？：此文件是新添加的文件，且没有被add
绿色的A：此文件为新添加的文件（即仓库中没有这个文件），且被add

`git rm --cached <文件>`

删除暂存区中的文件，就是把已经add的文件撤回，但此文件还存在于工作区
如果暂存区的文件和工作区的文件不一样，则会报错，如果要强制删除，则可以加-f

`git tag string ID`

给ID打上string标签

`git chechout <文件名>`

从暂存区中恢复此文件，如果暂存区没有，则会报错

`git checkout tag`

切换到标签为tag的分支上
这么做最好只用来查看代码和切换分支，因为使用checkout来切换，并不会改变master指针
如果要改变master指针，则应该使用 git reset --hard ID/tag
可以使用checkout master再切换到master上

` git diff`

查看工作区和和暂存区的差别
在diff后面也可以添加文件名称，查看固定文件的差别

` git diff --cache`
查看暂存区和仓库的区别
后面可以添加文件的名字

`git diff HEAD`
比较仓库和工作区之间的区别
后面可以添加文件名字

`git diff ID1 ID2`
比较两个ID的区别，也可以把ID换成tag标签

` git show ID`
查看此ID与上一次ID的区别，相当于默认ID2为上一次ID

## 四、设置git差异对比软件（文件对比）
1、 新建文件，并写入参数：
```
mkdir ~/bin/
vim ~/bin/git_xxx.sh
```
2、 写入以下内容
```
#!/bin/sh
xxx $2 $5
```
3、  添加可执行权限
```
chmod +x ~/bin/git_xxx.sh
```
4、 配置git
```
git config --global diff.external ~/bin/git_xxx.sh
```

## 五、.gitconfig 配置
```
[user]
	email = wuwenchi@hotmail.com
	name = wuwenchi
[alias]
	st = status
	co = checkout
	ci = commit
	br = branch
	lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
[core]
	editor = vim
[merge]
	too = vimdiff
[diff]
    external = /home/rst012/bin/git_diffuse.sh
```
