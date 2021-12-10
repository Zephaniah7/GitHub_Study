Git教程--本地新建文件創建項目上传项目到远程仓库(最完整详细)

> 網上前輩整理：先看两个如果，再看第三点，动手能力强的可以用第三点(命令行)来解决，做一步要知道自己做的意义，比如：不要在错误的远程仓库上浪费精力等。所以检查好自己已有的环境。**这里以gitee为例子，别的牌子路数都是一样的**。
>
> 出錯的注意文章最末後的資料

### 1. 如果你已经搞乱了

将项目根目录下的`.git`删掉，然后再跟着做2或者3。

### 2. 如果你用的IDEA

IDEA可以利用插件`gitee`来快速的上传项目到gitee上。(github原生支持，不需要下载插件)

##### 1. 安装插件

> ~~~bash
> setting->plugins->搜索gitee 
> ~~~

##### 2. 使用插件

> ~~~bash
> VCS -> Import into Version Control -> Share Project on Gitee (or Share Project on GitHub)
> ~~~

然后就是傻瓜式的操作了。如果有错误，自己解决不了，返回第一点，重新来。如果git密码第一次输入错误后不再提示你输入而是一直用错误的密码，看第三点的第4小点的注意事项(`3.4`)。

### 3. 从头开始（命令行上传）

> ~~~bash
> 请按照自己进行到的步骤，结合自己的实际情况来选则继续下面的步骤。假设我的环境中没有`.git`,且我的远程仓库`https://gitee.com/xxx.git`已创建好。
> ~~~

##### 1. 初始化一个空的git本地仓库

```bash
git init
```

##### 2. 声明你的身份

```bash
git config --global user.name "Nahum"

git config --global user.email "565823537@qq.com"
```

##### 3. 声明你的远程仓库路径

```bash
git remote add origin https://gitee.com/gitnahum/django.git # (你的远程项目地址)

```

##### 查看远程仓库地址

`git remote -v` 应该要显示出你的远程仓库地址，如果不是对应的地址。先删除后添加。如果是正确的则跳过下面的代码。

```bash
$ git remote -v
origin  https://gitee.com/gitnahum/django.git (fetch)
origin  https://gitee.com/gitnahum/django.git (push)

# 如果结果是正确的则跳过下面的代码。# 
git remote rm origin
git remote add origin https://gitee.com/gitnahum/django.git

```

##### 查看全局配置信息

```bash
git config --global --list
sev@DESKTOP-SBEGI6U MINGW64 /d/django/venv (main)
$ git config --global --list
user.name=zhou
user.email=85286985@qq.com

```

##### 4. 检测是否成功连接上远程仓库

执行`git fetch`

```bash
$ git fetch
info: detecting host provider for 'https://gitee.com/'...
info: detecting host provider for 'https://gitee.com/'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), 1.12 KiB | 5.00 KiB/s, done.
From https://gitee.com/gitnahum/django
 * [new branch]      master     -> origin/master

sev@DESKTOP-SBEGI6U MINGW64 /d/django/venv (main)


```

~~~bash
**注意**： 如果出现上述，证明成功连接到远程仓库了，没有出现也没关系，证明你本地没有你的`gitee`账户信息，随便打个命令`git clone https://gitee.com/gitnahum/sev.git`或者`git pull origin master`就会让你输入密码，注意尽量一次性输正确，否则需要去win10 账户下修改(`控制面板->用户账户->管理凭据->寻找修改你的gitee密码`)。
~~~



##### 5. 拉取远程仓库

```bash
$ git pull origin master
info: detecting host provider for 'https://gitee.com/'...
info: detecting host provider for 'https://gitee.com/'...
From https://gitee.com/gitnahum/django
 * branch            master     -> FETCH_HEAD

```

如果这步有错请检查你的`gitee`密码是否正确。

##### 6. 准备上传工作

```bash
git add .

git commit -m "first commit"

git push origin master
Compressing objects: 100% (75/75), done.

Writing objects: 100% (82/82), 4.10 MiB | 1.73 MiB/s, done.

Total 82 (delta 6), reused 0 (delta 0)

remote: Powered by Gitee.com

```

出现上面则为上传成功。

------

------



~~~bash
 git push 时发生错误 error: src refspec master does not match any. error: failed to push some refs to
很多相关解决办法都是最后要 push 到远端的 master 上，但很多其实要求不能把个人的修改内容直接 push 到 master 主分支。
因此，当我想将本地 feature/work 分支的修改内容 push 到远端 develop 分支时，执行了：
git push origin develop
但却发生了错误，提示为 error: src refspec master does not match any. error: failed to push some refs to ...
最后发现问题是 git push 指令的格式为：git push [remote-name（通常为 origin）] [branch-name]
当将本地分支 push 到远端同名的分支时，branchname 只需要写一个分支名就可以（如直接克隆远程分支后修改再push）；
但当要 push 到的远端分支名不同于本地分支名时，需要使用 git push origin [本地分支名：远端分支名]，因此，在上述出错情况下，改为执行
git push origin feature/work1：develop
然后，就发现可以正确执行了。

# 使用命令查看狀態
git remote -v
git branch
$ git branch
* main # 發現只有一個分支
# 再次push
git push repos main --force
# 教程  注意細節 main <本地分支名>:master<远程分支名>
sev@DESKTOP-SBEGI6U MINGW64 /d/django/djvenv (main)
$ git push origin main:master
info: detecting host provider for 'https://gitee.com/'...
info: detecting host provider for 'https://gitee.com/'...
Everything up-to-date

sev@DESKTOP-SBEGI6U MINGW64 /d/django/djvenv (main)
---------------------------------------------------------------------------
# 教程  注意細節 main <本地分支名>:master<远程分支名>
git push 命用于从将本地的分支版本上传到远程并合并。
命令格式如下：
git push <远程主机名> <本地分支名>:<远程分支名>
如果本地分支名与远程分支名相同，则可以省略冒号：
git push <远程主机名> <本地分支名>
实例
以下命令将本地的 master 分支推送到 origin 主机的 master 分支。
$ git push origin master
相等于：
$ git push origin master:master
如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数：
git push --force origin master
删除主机的分支可以使用 --delete 参数，以下命令表示删除 origin 主机的 master 分支：
git push origin --delete master
以我的 https://github.com/tianqixin/runoob-git-test 为例，本地添加文件：
$ touch runoob-test.txt      # 添加文件
$ git add runoob-test.txt 
$ git commit -m "添加到远程"
master 69e702d] 添加到远程
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 runoob-test.txt
$ git push origin master    # 推送到 Github
将本地的 master 分支推送到 origin 主机的 master 分支。
重新回到我们的 Github 仓库，就可以看到文件已经提交上来了；
------------------------------------------------------------------------
不懂原因 本地新建倉庫初始化后分支為main：
sev@DESKTOP-SBEGI6U MINGW64 /d/django/djvenv
$ git init
Initialized empty Git repository in D:/django/djvenv/.git/
sev@DESKTOP-SBEGI6U MINGW64 /d/django/djvenv (main)
------------------------------------------------------------------------
github上传代码的默认分支master。但本地分支分支為main，这就出現有两个分支
我這新手實在不懂咋弄，查找無數資料，試了很多方法，找到上面的分析
選擇使用命令：
git push origin main:master
将本地main分支的推送至远程分支
git push origin main # 推送至main分支
-------------------------------------------------------------------------


~~~

--------------------

~~~bash
git@github.com:Zephaniah7/GitHub_Study.git
https://github.com/Zephaniah7/GitHub_Study.git

在GitHub上新建仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。
现在，我们根据GitHub的提示，在本地的testgit仓库下运行命令：
git remote add origin https://github.com/Zephaniah7/GitHub_Study.git
~~~

