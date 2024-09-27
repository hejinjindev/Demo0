### git(分布式版本控制工具)

#####    1.为什么需要版本控制

方便管理自己本地的各种版本的代码文件

![study](E:\study.png)

#####   2.工作机制与代码托管中心

​		2.1工作机制

​	![zhiji](E:\zhiji.png)

  	2.2代码托管中心

​		    	 2.2.1局域网:

​							GitLab

​			 	2.2.2互联网：

​							GitHub

​		  			  	Gitee

##### 3.常用命令

​	3.1设置用户签名	   

​			git config --global user.name 用户名：设置用户签名

​			git config --global user.email 邮箱：设置用户email地址

​			查看设置过用户签名：cat ~/.gitconfig

​	3.2初始化本地库

​			git init: *创建了一个名为.git非空隐藏文件夹*

​            初始化后的文件：

![image-20230404192331642](C:\Users\ROG\AppData\Roaming\Typora\typora-user-images\image-20230404192331642.png)

​	3.3查看本地库状态

​            （查看工作区和暂存区状态）：git status

​			git status:*vim hello.txt(在对应目录下创建hello.txt文件)*

​    3.4暂存区操作

​        3.4.1 添加暂存区

​			git add 文件名

​            git add 文件夹名称

​            git add --all （简写形式  git add .）把当前工作区里面所有没有添加到暂存区的内容全都添加进去

​        3.4.2 撤回暂存区的内容

​             git reset HEAD -- 文件名

​             git reset HEAD -- 文件夹名字

​             git reset HEAD --  .撤回暂存区里面的所有内容

​			*git rm --cached 文件名(在暂存区删除指定文件)*

​    3.5本地库（历史区）操作

​         3.5.1 提交历史版本（形成历史版本）

​            把暂存区的内容形成一个历史版本 ==>前提 暂存区有内容

​            切换到.git 所在的目录

​            输入指令：git commit -m "日志信息" 文件名 === 文件名是关键

​		 3.5.2 查看提交记录

​			git reflog![image-20211210155138461](C:\Users\ROG\AppData\Roaming\Typora\typora-user-images\image-20211210155138461.png)

​              git log（查看历史版本）：以倒叙的方式出现本地所保存的所有历史版本![image-20211210155349989](C:\Users\ROG\AppData\Roaming\Typora\typora-user-images\image-20211210155349989.png)

​          3.5.3 删除历史版本

​                git  rebase  -i  历史版本号

![image-20230404200220164](C:\Users\ROG\AppData\Roaming\Typora\typora-user-images\image-20230404200220164.png)

​    3.6修改文件

​			修改工作区的某个文件内容，`git status`会提示该文件，修改过之后再添加到暂存区之后提交到本地库

##### 4.版本穿梭

​	git reset --hard 版本号

​	*原理是master指向每个版本对应的版本号*

​    *Git 切换版本， 底层其实是移动的 HEAD 指针*

##### 5.分支

​	5.1什么是分支

    在版本控制过程中，同时推进多个任务，为每个任务，我们就可以创建每个任务的单独分支。使用分支意味着程序员可以把自己的工作从开发主线上分离开来， 开发自己分支的时候，不会影响主线分支的运行。对于初学者而言，分支可以简单理解为副本，一个分支就是一个单独的副本。（分支底层其实也是指针的引用）
![fenzhi](E:\fenzhi.png)

 	5.2分支的好处

​	同时并行推进多个功能开发，提高开发效率。各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可。

    5.3分支_查看&创建&切换

​			5.3.1查看分支

​					git branch 

​			5.3.2创建分支

​					git branch 分支名

​			5.3.3切换分支

​					git checkout 分支名

​             5.3.4 删除分支

​                    git branch -d 分支名 （如果分支上有些历史版本的临时文件还没有形成可能删不掉）

​			        git branch -D 分支名 （强力删除，不管分支历史版本有没有文件直接删除，一般不建议使用）

​            5.3.5分支合并

​					git merge 分支名 （站到自己分支上时只能合并其他的分支）

​			5.3.6把本地的分支提交到远程库

​					git push --set-upstream origin （分支名）

​					*冲突合并*

​				    *合并分支时，两个分支在同一个文件的同一个位置有两套完全不同的修改。 Git 无法替我们决定使用哪一个，因此，必须人为决定新代码内容。*

​     5.4 分支的远程操作

​           当建立了其他分支以后，默认是不会上传到远程的（默认是上传的master）

​           当上传的时候：

​                =>git push -u origin（origin是远程仓库的别名） master

​                =>把当前分支和远程的master分支建立连接

​        5.4.1 把自定义的分支的内容上传

​            切换到你要上传内容的分支

​             切换到.git所在的目录

​             输入指令git push origin 分支名称

​        5.4.2 删除远程分支

​             打开命名行，切换到.git所在的目录

​             输入指令git push origin  --delete 你要删除的分支名称

​         5.4.3 拓展

​               gh-pages（git特殊分支）

![image-20230407194716395](C:\Users\ROG\AppData\Roaming\Typora\typora-user-images\image-20230407194716395.png)

​     5.5 分支的命名规范

![Snipaste_2024-09-23_11-32-15](C:\Users\何金京\Desktop\Snipaste_2024-09-23_11-32-15.png)

![Snipaste_2024-09-23_11-32-55](C:\Users\何金京\Desktop\Snipaste_2024-09-23_11-32-55.png)

![Snipaste_2024-09-23_11-33-50](C:\Users\何金京\Desktop\Snipaste_2024-09-23_11-33-50.png)

##### 6.团队协作![team](E:\team.png)

##### 7.跨团队协作![kua-team](E:\kua-team.png)

##### 8.创建远程库(基于github)

![create1](E:\create1.png)

![create2](E:\create2.png)

##### 9.远程仓库操作

​		9.1创建别名

​				git remote -v ：查看当前所有远程地址别名

​				git remote add 别名 远程地址：添加远程库并创建别名

​        9.2推送本地库到远程库

​				git push -u 远程库地址或其别名 分支名(第一次上传的时候)

​				git push 远程库地址或其别名 分支名（第2次以及2次以后的时候）

​		9.3拉取远程库到本地库

​				git pull  远程库地址或其别名 （远程仓库已有的分支名）

​                 如果本地仓库和远程仓库实际上是独立的两个仓库，–allow-unrelated-history选项来解决

​		9.4克隆远程库到本地

​                9.4.1第一次克隆的时候：

​                    =>复制远程仓库的地址

​                    =>在本地找到一个你需要存放这个文件夹的位置(该文件夹是被git初始化后的)

​                    =>在git hash窗口里面 输入  git clone 远程地址

​			    9.4.2 第2到n次克隆时：

​                     =>直接在第一次克隆下来的文件夹里打开git窗口输入**git pull**

​				clone 会做如下操作：

​					1.拉取代码。2.初始化本地仓库。3.创建别名。

​		9.5团队内协作

​				gitee使用组织功能邀请其他账户

​				github在项目的settings选项中邀请

​		9.6跨团队合作

​				谁想要用别人的项目就点击别人项目的fork按钮，这样就把别人的项目导入到自己的本地仓库了

​				fork的一方可以修改里面的内容等等，修改成功后点击pull requests并创建新的请求，然后被fork的一方可以收到pull请求如果没问题就可以点击 Merge pull reque 合并代码

##### 10.git相关的三个文件

​       git占位文件 

​          =>由于git不会管理空文件夹但有时为了提前搭建项目结构又得使用文件夹

​          =>直接在空文件家里面添加一个**.gitkeep**的文件夹

​          =>没有实际意义只是为了占位

​       git 忽略文件

​          =>在实际开发中可能会下载一些三方文件

​          =>node_modules 文件夹里面的文件过于繁琐，一般不上传

​          =>只要在初始化项目时生成package.json文件，把package.json文件上传即可

​          =>所有就不需要管理node_modules文件了

​          =>git 有一个.gitignore 文件（只有后缀没有文件名）

​          =>.gitignore 文件在文件同级目录创建

​          =>在文件里面 写下 node_modules/  这种格式就代表Git不会管理该文件夹了

​      git说明文件

​          => readme.md

​          =>按照md规则书写你要说明的信息

##### 11.github密钥上传（ssh）

![image-20230407200345429](C:\Users\ROG\AppData\Roaming\Typora\typora-user-images\image-20230407200345429.png)