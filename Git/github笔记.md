# Git笔记

#### 首次安装Git需要提交自己的用户签名和邮箱(无需验证真实性)，否则可能无法提交代码。

```
 git config --global user.name//用户名
 git config --global user.email//邮箱
```





## Git工作机制

![image-20220625110446511](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625110446511.png)



------



## 基本语法：

### 1.初始化本地库:git init(会生成一个.git隐藏文件)

![image-20220625093948423](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625093948423.png)

------



#### 查看本地库状态:git status( 显示文件实在那个分支  是否有新增文件或者修改)

##### 	①有新增而且没上传暂存区(未使用git add)：

![image-20220625094804711](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625094804711.png)

##### （红色text.xt表示文件中未上传更新到暂存区的文件，提示用git add 上传到暂存区）

##### 	②新文件已经上传暂存区：

![image-20220625095853093](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625095853093.png)

​	

------



### 2.添加暂存区：git add(添加文件到暂存区)

##### 	初始化文件后需要使用git add 文件名或者 git add . 将文件添加至暂存区

​					![image-20220625095723026](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625095723026.png)	

##### 	注意：上传暂存区只是在中间的一个暂存阶段，可删除已经上传暂存区文件（远程库无法显示暂存区文件）



#### 删除暂存区文件：git rm -cached 文件名 

##### 	该命令可删除暂存区指定文件，用git status可以查看相关状态

##### 						![image-20220625100403334](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625100403334.png)



#### 从暂存去恢复工作台已删除文件：git restore 文件或文件夹

##### 	暂存区已有文件但是自己本地已经删除

![image-20220625101526061](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625101526061.png)

 

------



### 3.提交本地库：git commit -m "日志信息" 文件名

##### 	①-m ""是将你提交本库的文件提交日志信息，即使写程序也会要求你填写日志信息

##### 	②不填写文件名则会将文件中未提交本地库的文件或者已经修改后的文件全部上传

![image-20220625102617991](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625102617991.png)

##### 	

##### 上传后在使用git status查看本地库状态：

![image-20220625102751134](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625102751134.png)

##### 	显示该工作树已经干净(暂存区文件或修改后的文件已经全部上传本地库)



#### 	删除工作区文件(删除后需要将修改后的添加暂存区,提交本地库,然后上传到远程残酷)： git rm 文件名

![image-20220625163142700](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625163142700.png)



------



### 4.历史版本

#### :star:查看引用日志信息：git reflog

![image-20220625103217975](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625103217975.png)

##### 前面的993e0b0是版本号(版本号前7位) text是git commit -m后的版本



#### 查看详细日志：git log

![image-20220625103440711](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625103440711.png)

##### commit后的字符串是完整的版本号

##### Anthor：提交该版本的用户信息

------



#### ！！    版本穿梭：git reset --hard 版本号      ！！

##### 	使用git reflog查看历史版本查看其版本号和现在所指向的版本

##### 	使用git reset --hard 版本号回到历史版本并修改文件

##### 	可以在使用git reflog查看具体信息

![image-20220625105535920](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625105535920.png)

------



#### 修改文件信息：vim 文件名：(进入修改页面修改文件信息)

![image-20220625104014000](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625104014000.png)

##### esc后使用   :wq  保存并退出编辑

------



### 5.Git分支操作

#### 	查看分支：git branch -v 

![image-20220625111626931](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625111626931.png)

​	

#### 	创建分支：git branch 分支名

![image-20220625111828199](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625111828199.png)

​	

#### 	切换分支：git checkout 分支名

![image-20220625112012572](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625112012572.png)



#### 	合并分支：git merge  分支名（将分支名合并到当前分支内 ）

##### 		正常合并：

![image-20220625112648506](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625112648506.png)



##### 		冲突合并：

![image-20220625113539865](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625113539865.png)

​		**master|MERGING：正在合并中即合并冲突系统无法合并**



​		**产生冲突原因：合并分支时，两个分支在同一个文件的同一个位置有两套完全不同的修改，    	  Gti无法决定使用哪个。必须人为决定。**

#### 		合并冲突解决方法：(修改后的内容只是合并到的分支的内容，合并进来的分支内容不做改变 )

##### 		①git status查看哪些文件冲突

![image-20220625135407877](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625135407877.png)

​	

##### 		②vim命令进入冲突文件

![image-20220625135520288](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625135520288.png)

​	**<<<<HEAD 与====之间:当前分支代码**

​	**>>>>newmaster 与===之间：合并的分支代码**

​	

##### 	③把不要的代码和 <<<<  ==== >>> 行删除并保存



##### 	④用git add 文件名 将其上传暂存区

![image-20220625140424253](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625140424253.png)



##### 	⑤提交本地库（使用git commit 时不要再带文件名）

![image-20220625140638783](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625140638783.png)

​	

------



# GitHub操作



### 1.进入GitHub，在右上角创建仓库

![image-20220625155436967](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625155436967.png)

------



### 2.给仓库创建别名

#### 	创建远程地址别名：git remote add 别名 远程仓库地址

![image-20220625155857792](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625155857792.png)



![image-20220625155932594](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625155932594.png)

#### 	

#### 	查看当前所有远程地址别名：git remote -v

![image-20220625155958872](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625155958872.png)

​	

​	

------



### 3.将本地库代码上传到GitHub上

#### 	本地库代码上传(必须本地库有代码，详情在Git操作里面)：git push 别名(或者远程仓库地址) 分支

​							![image-20220625161329425](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625161329425.png)		

​	

------



#### 	常见问题和解决方案:

​		问题1：![image-20220625161546604](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625161546604.png)

​		原因：一般是因为服务器的[SSL](https://so.csdn.net/so/search?q=SSL&spm=1001.2101.3001.7020)证书没有经过第三方机构的签署，所以才报错。

​		解决：使用 git config --global http.sslVerify “false”再git push即可

​		

​		问题2：![image-20220625161657169](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625161657169.png)		

​		原因：再解决问题1的时候 .gitconfig文件中的false赋值的时候加上了”“

​		解决：在C盘的用户文件夹下找到.gitconfig文件  将sslverify的值false



------

### 4.将远程库的代码拉取到本地库(拉取远程库更新内容)

#### 	拉取远程库代码： git pull 别名(或者远程仓库地址) 分支 

![image-20220625162405970](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625162405970.png)

#### 	

#### 	常见问题和解决方案:

​		问题：![image-20220625164250718](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625164250718.png)	

​		原因(个人认为)：pull代码将代码从远程仓库拉取到本地库时只能拉取到master主分支，其他分支无法拉取成功。

​		解决：将 git pull 别名 分支  中的  分支  改为 主分支 即newmaster改为master

------



### 5.克隆远程仓库到本地

#### 	①在需要的克隆文件的文件夹下面右键git bash here

#### 	② 克隆远程仓库代码：git clone 远程仓库地址

​		![image-20220625165452148](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625165452148.png)	

​	**克隆执行的步骤：克隆代码  初始化本地仓库(代码的.git文件)  创建别名(但是别名为origin)**

------



### 6.GitHub团队合作

#### 	①创建仓库者进入仓库Settings 在collaborators中点击 Add people

![image-20220625170620194](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625170620194.png)

​	

#### 	②在弹出框输入需加入成员的用户名或者邮箱

​						![image-20220625170907770](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625170907770.png)		

​		

#### 	③复制所得的邀请凭证(Pending invite)发送给成员，成员打开并接受

![image-20220625171017666](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625171017666.png)

​		

#### 	④成员可以使用链接进行push等相关操作

------



### 7.跨团队合作(未加入团队且修改代码 )

#### 	①未加入用户A通过搜索或者链接进入远程仓库，点击右上角Fork

#### 			![image-20220625171922320](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625171922320.png)		

​	

#### 	②用户A在自己的代码仓库列表找到Fork的仓库并进入

![image-20220625172038967](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625172038967.png)

​	

#### 	③用户A修改代码后点击左上角Pull requests请求

![image-20220625172207345](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625172207345.png)



#### 	④点击New pull requsets按钮并点击Create pull request按钮

![image-20220625172355455](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625172355455.png)



#### 	⑤在该远程仓库创建者的账号中点击Pull requsets，查看详情信息并同意合并

------



### 8.SSH免密登录

#### 	①进入C盘用户下的用户名文件夹右键Git Bash Here



#### 	②输入 ssh-keygen -t -rsa -C 邮箱地址(GitHub的邮箱地址)然后三次回车(如果已经有.ssh文件的删除在操作即可)

![image-20220625173441870](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625173441870.png)



#### 	③进入.ssh文件打开id_rsa.pub文件并复制公钥代码

![image-20220625173701420](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625173701420.png)



#### 	④进入仓库创建者的个人信息，右上角头像点击Settings，点击SSH and GPG keys添加SSH keys。

![image-20220625173925646](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625173925646.png)

​	

#### 	⑤将公钥复制进去然后 Add SSH key即可

![image-20220625174017931](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625174017931.png)

​	![image-20220625174044359](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625174044359.png)

​	

#### 	⑤之后就可以用SSH链接进行pull push操作免密登录

​									![image-20220625174139729](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220625174139729.png)

------

