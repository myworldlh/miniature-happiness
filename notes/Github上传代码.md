# 这篇文章写得是windows下的使用方法。

### 第一步：创建Github新账户

### 第二步：新建仓库

### 第三步：填写名称，简介（可选），勾选Initialize this repository with a README选项，这是自动创建REAMDE.md文件，省的你再创建。

### 第四步：安装Github shell程序，地址：[http://windows.github.com/](http://windows.github.com/)如果下载不下来，可以把链接放到迅雷上下载

### 第五步：打开Git Shell，输入以下命令生成密钥来验证身份
```ssh-keygen -C 'github绑定的邮箱' -t rsa```
连续三个回车之后会在windows当前用户目录下生成.ssh文件夹，和linux一样。
把文件夹下的`id_rsa.pub`文件内容全部复制。
然后打开github账户设置
打开左侧`ssh keys`
右上角点击`add ssh key`
然后在title随便输入，key栏粘贴刚才的密钥。

### 第六步：在Git Shell下输入命令测试刚才的公钥是否认证正确。
`ssh -T git@github.com`
正确结果会显示：
```
Warning:Permanently added 'github.com,207.97.227.239' (RSA) to the list of known hosts.
Hi Flowerowl! You've successfully authenticated, but GitHub does not provide shell access.
warning 不用理会。
```

### 第七步：clone刚才新建的repository 到本地，输入命令：
```
git clone https://github.com/Flowerowl/stumansys.git
```
这时会在目录下生成对应的库文件

### 第八步：将想上传的代码目录拷贝到此库目录下

### 第九步：切换到Git shell 命令行下，输入命令：
```
先进入要commit文件的目录，这样才可以add 到（github上的项目其实就是一个个.git，必须进入.git下才可以进行操作）

可能需要配置用户名和邮箱
git config --global user.name "your name"
git config --global user.email "your_email@youremail.com"

初始化，生成.git文件（第一次需要生成，以后如果在对应分之下如master，则可以不进行init操作）
git init
可以add多个文件（包括文件夹，如果add的文件或文件夹名称中包含空格，则需要\进行转义）<br> 上传全部使用--all或者 .
git add '文件名'
本次提交的题目备注信息等，强烈建议填写，不填写则需要不填写的命令；a则是all，代表提交所有， m是备注信息
git commit -m 'test'
---
#### 关联Github仓库（上传单独的文件而不是提交整个项目，需要使用一下语句）
git remote add origin 库地址
git pull --rebase origin master  // 合并代码（pull=fetch+merge）
git push -u origin master  // 写了这句下面就不需要写了
---
将本地的文件上传到github的服务器上，这里不需要写库地址，因为就在当前的.git下，push就能够找到自己再github上的库路径，
而且，如果上传的库是主分支（master）的话，origin master也不需要写，直接git push就可以，如果是其他分支则需要写。
git push origin master
```

（注意：只有add的文件才能和库产生联系，只有commit后才能进行push，所以，操作的顺序为：add → commit → push）
```
如果执行git remote add origin https://github.com/Flowerowl/stumansys.git ，出现错误：
fatal: remote origin already exists
则执行以下语句：
git remote rm origin
再往后执行:
git remote add origin https://github.com/Flowerowl/stumansys.git

在执行git push origin master时，报错：
error:failed to push som refs to.......
则执行以下语句：<br>
git pull origin master
先把远程服务器github上面的文件拉先来，再push 上去。
```
最后，你可以去项目页面查看了~~代码上传成功！

```备注git常用语法：
1.添加文件       git add 文件名
2.删除文件       git rm 文件名
3.移动文件       git mv 文件名 目标目录
4.返回指定版本   git reset --hard 项目版本号（commit记录中可以找到，历史版本中的full SHA）
                git push -f origin master（强制提交）
```

#### 补充
* 可以clone的项目是远程仓库，clone或者init出来的是本地仓库。
* 对远程仓库进行修改需要clone库。

单独上传一个文件
```
git init
git add .
git commit -m 'test'
git remote add '仓库地址'
git pull --rebase origin master  --rebase合并分支代码
git push -u origin master
```

删除一个文件
```
git clone '库地地址
git pull origin master 下拉先来最新的项目，防止别人push冲突 
git rm -r --cached target  -r递归删除 --cached删除暂存区或分支上的文件, 但本地又需要使用, 只是不希望这个文件被版本控制
git commit -m '删除了target'
git push -u origin master
```

git中本地误删了文件，找回办法：
```
git status  // 查看工作区的变化（查看误删了的文件）
git reset HEAD 要恢复的文件
git checkout 要恢复的文件

这样就找回误删的文件了！
```

#### 再次补充
通常管理仓库是比较简单的，下载下来一直管理本地仓库即可：
* 将项目clone下来，在本地仓库管理，然后再commit到远程仓库中
* 本地仓库操作：文件的修改、删除可以直接commit到远程仓库中，而新增文件则需要add操作。
* 本地仓库管理的文件会有标记，修改的文件标记为M，删除的文件标记为D，新增的文件标记为A，
* 而修改和删除会自动生成标记，新增的文件则不会生成标记，所以库不能进行管理。
* 在一个文件夹下新增了文件，相当于修改了这个文件夹，所以不需要add，直接commit即可。

##### 命令如下

```
git commit -am 'message'  -a提交所有文件，必要参数，但是如果是新增文件，则需要先 git add .
git push
```

#### Tips

* 在clone项目的时候，如果使用了https路径下载，就会发生每次push都要输入用户名和密码的情况
* 如果使用了https方式则可以这样修改
```
git remote -v  查看当前git origin路径https://github.com/myworldlh/miniature-happiness.git
git remote rm origin 删除git origin
git remote add origin git@github.com:myworldlh/Chrome-Workspace.git
git remote -v 显示为git@github.com:myworldlh/Chrome-Workspace.git
```
* 这样下次再push的时候就不需要账号密码了



* 提交项目遇到问题:`warning: LF will be replaced by CRLF`
* 在add文件的时候，出现了关于换行的问题，可以用下面的代码解决警告
```
$git config --global core.autocrlf true
```


* 提交项目出现安全问题："potential security vulnerabilities"
```
解决办法是不上传package-lock.json
解决办法是在上传的项目中删除掉package-lock.json，然后再.gitignore文件中设置不上传到github的文件/package-lock.json
然后本地更新一下git，再push就可以了(就算本地再生成该文件也不会上传，就不会报这个安全警告了)
```
