# Git 配置

### 1. Terminal 选择
#### 在安装 Git 时需要选择命令行终端。Git 自带了的 MinTTY 和 系统默认终端两种选择。一般选择 MinTTY，一种 Cygwin（模拟Linux接口） 和 MSYS 环境下的虚拟终端。



---
### 2. 配置项目的 user.name 用户名和 user.email 邮箱
#### 需要注意的是 user.name 和 user.email 的必须要和 github 注册的账户名和邮箱地址完全相同，才能被统计进贡献次数。 所以在适配多个 Git 系统时，要注意全局的 user.name 和 user.email 的比项目的 config 配置优先级要低，所以要报清楚具体设置的生效值，以避免提交没有被统计的情况出现。
```
/* 如果使用 --global 参数配置，则在本机上提交 git 时都会以这个 usename 和 email 作为提交者的身份信息 */
$ git config --global user.name "yourname"
$ git config --global user.email "your@email.com"

/* 如果只希望为本项目添加用户信息，则去掉 --glabol 参数 */
$ git config user.name "yourname"
$ git config user.email "your@email.com"

/* 查看本项目的所有配置信息，包括全局的、项目级的都会显示 */
$ git config --list

/* 打开修改本项目的全局配置信息 */
$ git config --global -e
```



---
### 3. HTTPS & SSH
#### Git 中链接远程库的方式有两种：HTTPS 和 SSH。

HTTPS（改动时需要输入用户信息） | SSH（一劳永逸）
---|---
随意 clone | clone 之前需要配置 SSH Key
push 时需要输入用户名和密码 | 除非给 SSH 配置了密码，否则 push 时不需要输入





---
### 4. 配置 SSH
```
/* 检测本地是否有 public SSH key 存在 */
ls -al ~/.ssh t

/* 通过 ssh-keygen 生成 rsa key pair, 其中参数 [-t rsa] 代表加密类型，[-b bit]代表秘钥长度，[-C comment]代表注释帮助你记忆这对秘钥的用途 */
ssh-keygen -t rsa -b 4096 -C "comment"

/* 生成 SSH key pair 后会要求设置密码，这个密码也可以置空，如果置空，可以用回车直接登录。
如果设置了密码，则每次使用 SSH 密钥来连接远程仓库时都需要输入该密码 */

/* 生成 SSH key pair 后，将公钥 public key 拷入 gitHub 的 accunt 中 */

/* 以上步骤已经可以使用 SSH 的方式来连接远程库了，如果不、想每次连接都输入一遍密码
则应该配置 ssh-agent 来管理本地的私钥。有3个步骤如下： */
/* 1. start the ssh-agent */
eval $(ssh-agent -s)

/* 2. Add your SSH private key to the ssh-agent. 私钥地址名称都是默认的，可按需更改 */
ssh-add ~/.ssh/id_rsa

/* 3. 配置 ssh-agent 每次会自动运行，只需要在开启时输入一次密码即可 */
https://help.github.com/articles/working-with-ssh-key-passphrases/




/* 以上方式产生的 rsa 秘钥不适用于 tortoise，如果要兼容 tortoise，可以使用 PuTTYgen 来生成密钥对，并用 pageant 来管理本地私钥 */
http://blog.csdn.net/qq_15974389/article/details/50937862
```



---
### 5. 用 log 查看 commit 的历史记录（版本树内各个版本的差异）
#### 查看提交记录有好几种方式，最简单的就是通过 GUI 工具，图形化的展示历次 commit 情况。首先打开 Git GUI，然后选择 Repository ——> Visualize All Branch History

#### 另一种方法查看 cmmit 记录的方式就是利用 git log 命令。
```
/* 不加参数的 git log 会打印出当前分支所有的 commit 记录 */
$ git log

/* 添加参数 -p 会以补丁模式（patch）额外打印出每个 commit 相比于上一个 commit 的变动 */
$ git log -p

/* 添加参数 -n 只外打印出 n 条 commit 记录 */
$ git log -3

/* 打印最近一次的 commit 具体变动 */
$ git log -p -1
```




---
### 6. SSH 配置检查及常见问题
```
/* 通过以上步骤的 SSH 配置后，就可以无密码链接远程库。要检验是否配置成功，可以使用以下语句测试 */
ssh -T git@github.com


/* 如果出现 connect to host github.com port 22: Connection timed out 的错误 */
在秘钥存放的 .ssh 文件下新建一个名为 config 的文件，内容如下：
Host github.com
User 463215040@qq.com （注册 github 账号的邮箱，这里使用注册的用户名也行）
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443
```




---
### 7. push.default matching 和 push.default simple 的区别：

- #### push.default maching 的意思是：git push 会把你本地所有分支push到名称相对应的远程主机上。这意味着可能你会在不经意间push一些你原本没打算push的分支。

- #### push.default simple 的意思是：git push仅仅把当前所在分支push到从当初git pull pull下来的那个对应分支上，另外，这个过程也会同时检查各个分支的名称是否相对应。

```
/* 一般设置成更加保守的策略 simple */
$ git config --global push.default simple
```





---
### 8. GUI 查看中文乱码
#### 打开 GUI，选择 Edit ——> Options ——> Default File Contents Endoding ——> change 改成 utf-8

http://blog.csdn.net/h3c4lenovo/article/details/17091811





```
```
# Git 常用命令
### 1. Help
#### 1. 打开命令的说明文档
```
$ git help <命令名>
```



---
### 2. Init
#### 1. 将当前文件夹初始化为 Git 仓库
```
$ git init
```




---
### 3. Clone
#### 1. 克隆整个远程仓库
```
/* clone 出来的远程仓库和本地仓库会自动关联 */
$ git clone <远程仓库地址> <可以指定本地仓库名>
```
#### 支持多种类型的远程仓库地址协议，例如：
```
$ git clone http[s]://userName:password@XXXXXX.git
$ git clone ssh://userName@XXXXXX.git myRepositoryName
```





---
### 4. Remote
#### 1. 查看远程仓库名(-v 可以显示对应远程仓库地址)
```
$ git remote -v
```
#### 2. 管理远程仓库名
```
$ git remote add <远程仓库名> <远程仓库地址>    // 手动关联当前库与远程库
$ git remote rm <远程仓库名>
$ git remote rename <原远程仓库名> <新远程仓库名>
```
#### ==一般情况都取 origin 作为远程仓库名。== 例如在clone操作时，就默认用 origin 作为远程仓库名。




---
### 5. 本地 Git 仓库
- #### 工作区是除 .git 外的文件
- #### 版本库是指 .git 文件
- #### stage 是暂存区

  ![本地 Git 仓库](https://github.com/StRothschild/Tools/blob/master/Git%20%E2%80%94%20%E6%A6%82%E5%BF%B5.jpg?raw=true)




---
### 6. Status
#### 查看当前有哪些改动，以及这些改动的状态

```
$ git status      // 显示有哪些改动，有没有被add，红色没表示没有被暂存，绿色表示已被暂存
```




---
### 7. diff（本地修改与当前版本库的差异）
#### 查看改动的具体内容
```
/* 显示还在工作区的改动（working directory）与暂存区的区别（stage）*/
$ git diff

/* 显示已经被暂存的改动（stage）与版本库的区别（repository）*/
$ git diff --cached/--staged

/* 显示当前的所有的改动（working directory + stage）与版本库的区别（repository） */
$ git diff HEAD
```






---
### 8. Add
#### 1. 添加到修改暂存区（stage）
```
/* 将指定的文件变化提交到暂存区（stage）*/
$ git add <file>

/* 监控工作区的状态树，并把工作区的所有变化提交到暂存区（stage），
包括文件内容修改（modified）以及新文件（new），但不包括被删除的文件 */
$ git add .     // . 代表当前目录及其子孙目录

/* 不会提交新文件（untracked file），但会更新已有文件的修改和文件的删除 */
git add -u

/* 不但提交新文件（untracked file），并会更新已有文件的修改和文件的删除 */
$ git add -A
```
![三种add指令的区别](http://image.codeweblog.com/upload/4/c5/4c5c187f4b7b6af1_thumb.jpg)

#### 注意：Git 2.0 以后，需要显示指定目录不然就是整个目录树。并且git add .和git add -A .没有区别。




---
### 9. Commit
#### 1. 将暂存区（stage）的所有内容提交到分支中
```
$ git commit                     // 自动打开 vim 来编辑提交信息
$ git commit -m "commit info"    // 提交同时添加提交信息
```





---
### 10. 撤销
#### 1. 将当前工作区的改动撤销
```
/* 撤销工作区（尚未 add）的改动*/
$ git checkout -- <file>
例如：
$ git checkout -- 'test.md'
```

#### 2. 将已经add到暂存区的改动撤销（unstage）
```
/* 撤销已添加到暂存区的改动，改动会返回工作区 */
$ git reset HEAD <file>
例如：
$ git reset HEAD 'test.md'
```

#### 3. 将已经commit到版本库的改动撤销（版本回退）
```
/* 查看版本库,获取 commitId（版本号） */
$ git log

/* 通过 commitId，强制选择版本库中的版本 */
$ git reset --hard commitId

/* 返回之前版本 */
$ git reset HEAD^     // 回退版本,一个^表示一个版本
$ git reset HEAD~1    // HEAD~n,表示回退到之前n个版本
$ git reset HEAD~3

/* reset 的三种参数 */
--hard 版本库、暂存区（storage）和工作区全部被指定的提交版本所替换
--mixed 或者不使用参数，版本库和暂存区（storage）会被替换，而工作区不会被替换，老版本和新版本之间的差异会被当成 local change 保存在工作区中
--soft 版本库被替换，而暂存区（storage）和工作区不会被替换，老版本和新版本之间的差异会被保存在暂存区（storage）中
```





---
### 12. Branch
#### 1. 查看分支
```
$ git branch      查看本地分支
$ git branch -a   查看所有分支
$ git branch -r   查看远程分支
```

#### 2. 创建新分支，但是==不切换到新分支==
```
$ git branch <新分支名>
```


#### 3. 建立本地分支与远程分支的====追踪关系====
```
git branch --set-upstream-to=<远程仓库名>/<远程分支名>
```


#### 4. 切换分支
```
$ git checkout <分支名>         切换本地分支，如果存在远程同名分支，则会自动追踪
$ git checkout -b <新分支名>    创建本地新分支并且切换到该新分支
```

#### 5. 删除本地分支
```
$ git branch -d <分支名>    删除本地分支
$ git branch -D <分支名>    强制删除本地分支，用于删除没有被merge到当前分支的本地分支
```





---
### 13. Fetch
#### 1. 获取特定的远程仓库下的某一分支
```
$ git fetch <远程仓库名> <分支名>
```


####  2. 如果==省略分支名==，则将所有分支取回
```
$ git fetch <远程仓库名>
```





---
### 14. Merge
#### 1. 合并分支
```
$ git merge <分支名>

```
#### 例如： $ git merge origin/test  把本地的origin/test分支合进了==当前分支==。
#### ==如果合并出现冲突，则修改冲突文件后，再次 commit 即可完成合并。==






---
### 15. Pull
#### 1. 获取远程分支==并且合并==
```
$ git pull <远程仓库名> <远程分支名>:<本地分支名>
```


#### 2. 如果远程分支是与当前分支合并，则==本地分支名（冒号后面的部分）可以省略==
```
$ git pull origin test = ($ git fetch origin  + $ git merge origin/next)
```


#### 3. 如果当前分支与远程分支之间存在追踪关系，则==本地分支和远程分支都可以省略==
```
$ git pull origin
```


#### 4. 如果当前分支==只有一个追踪分支，那么主机名都可以省略==
```
$ git pull
```






---
### 16. Push
#### 1. 提交分支
```
$ git push <远程仓库名> <本地分支名>:<远程分支名>
```


#### 2. 提交未关联的分支
#### Git2.0之后的版本，git push 操作的默认模式从 matching 变成了 simple。matching 意味着 push 的本地仓库和远程仓库存在的同名分支即可。simple 则必须保证本地分支和它的远程 upstream 分支同名，否则会拒绝 push 操作。
#### ==--set-upstream 可以指定远程分支为本地分支的 upstream 分支（关联分支）。==
```
$ git push --set-upstream <远程仓库名> <本地分支名>
```
#### 如上，设置了 upstream 分支后，下次提交就只需要 git push。



#### 3. 新建分支
#### 如果==省略远程分支名==，则表示将本地分支推送到与之存在”追踪关系”的远程分支(通常两者同名)，如果该远程分支不存在，则会被==新建==
```
$ git push origin test  =  $ git push origin test:test
```


#### 4. 删除分支
#### 如果==省略本地分支名==，则表示==删除指定的远程分支==，因为这等同于推送一个空的本地分支到远程分支
```
$ git push origin :test  =  $ git push origin --delete test
```


#### 5. 如果当前分支与远程分支之间存在追踪关系，则==本地分支和远程分支都可以省略==
```
$ git push origin
```


#### 6. 如果当前分支==只有一个追踪分支，那么远程仓库名都可以省略==
```
$ git push
```



---
### 17. Stash
#### 1. 存储当前未 commit 的代码
```
$ git stash [save "可以添加备注"]
```

#### 2. 显示存储列表
```
$ git stash list

结果如下：
stash@{0}: On master: 可以添加备注
```

#### 3. 恢复到某一存储状态。如果没有指定存储列表中的序号，则默认恢复到暂存列表中的最后一个存储状态。==同时，会删除存储表中的该条记录。==
```
$ git stash pop [存储列表序号]

例如：
git stash pop stash@{0}
```

#### 4. 也可以恢复到某一存储状态。==但是不会删除存储表中的该条记录。==
```
$ git stash apply [存储列表序号]
```



---
### 18. Git 代码统计
```
/* 统计当前用户的代码提交量，包括增加，删除 */
git log --author="$(git config --get user.name)" --pretty=tformat: --numstat | gawk '{ add += $1 ; subs += $2 ; loc += $1 - $2 } END { printf "added lines: %s removed lines : %s total lines: %s\n",add,subs,loc }' -

/* 仓库提交者排名前 5（如果看全部，去掉 head 管道即可）*/
git log --pretty='%aN' | sort | uniq -c | sort -k1 -n -r | head -n 5

/* 贡献者统计 */
git log --pretty='%aN' | sort -u | wc -l

/* 提交数统计 */
git log --oneline | wc -l

/* 添加或修改的代码行数 */
git log --stat|perl -ne 'END { print $c } $c += $1 if /(\d+) insertions/
```

---
### Git流程简图
![Git流程简图](http://image.beekka.com/blog/2014/bg2014061202.jpg)
