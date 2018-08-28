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

如果执行git remote add origin https://github.com/Flowerowl/stumansys.git ，出现错误：<br>
```fatal: remote origin already exists```
则执行以下语句：
`git remote rm origin`
再往后执行:
`git remote add origin https://github.com/Flowerowl/stumansys.git`<br>

在执行git push origin master时，报错：<br>
`error:failed to push som refs to.......`
则执行以下语句：<br>
`git pull origin master`
先把远程服务器github上面的文件拉先来，再push 上去。<br>

最后，你可以去项目页面查看了~~代码上传成功！<br>

```备注git常用语法：
1.添加文件       git add 文件名
2.删除文件       git rm 文件名
3.移动文件       git mv 文件名 目标目录
4.返回指定版本   git reset --hard 项目版本号（commit记录中可以找到，历史版本中的full SHA）
                git push -f origin master（强制提交）
```
