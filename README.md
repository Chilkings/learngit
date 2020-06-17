**Notes for git！！！**



# git常用命令

| 获得版本库 | 查看信息            | 版本控制   | 远程协作 |
| ---------- | ------------------- | ---------- | -------- |
| git init   | git help            | git add    | git pull |
| git clone  | git log （--graph） | git commit | git push |
|            | git diff            | git rm     |          |

对于user.name和user.email有三个地方可以设置

* ```
  全部计算机用户  git config --system "value"
  ```

* ```
  当前计算机用户  git config --global      常用
  ```
  
* ```
  当前仓库       git config --local
  ```



# git文件操作

**直接删除**：只在工作区起作用，commit前需要手动git add

**`git rm`删除**：在工作区删除并提交到暂存区

**恢复删除的文件**：

1. 将被删除的文件从暂存区恢复到工作区

   `git reset HEAD test2.txt`

2. 丢弃删除这一动作

   `git checkout -- test2.txt`

**替换最新的一次提交**：

```git commit --amend -m "message"```

Replace the tip of the current branch by creating a new commit.

**自定义log输出**

``` git log -3          git log --pretty=oneline```

**忽略不需要的文件** ：

自定义`.gitignore`文件：

1. ` *.txt  !error.txt 忽略所有txt文件除了error.txt`
2.  `指定层级 /error.txt  /*/error.txt /**/error.txt `
3. `忽略文件夹的所有文件 build/`

# git分支

| 作用           | 命令                        |                       |                           |
| -------------- | --------------------------- | --------------------- | ------------------------- |
| 查看分支       | git branch                  | 创建新分支            | git branch new_branch     |
| 切换分支       | git checkout branch_name    | 删除分支(After merge) | git branch -d branch_name |
| 创建并切换分支 | git checkout -b new_branch  | 合并分支              | git merge branch_name     |
| 更改分支名称   | git branch -m name new_name | 查看远程分支           |  git remote -v               |
|                |                             |                       |                           |

**合并有冲突的分支**：

首先正常执行合并操作，git会在冲突区域给出选择，选择所需要的结果。使用git add name标记冲突已修改，最后使用git commit完成合并。

**禁用FF合并**：

`git merge --no-ff new_branch`

可以保留分支信息，合并时生成一个新的commit。



# git版本控制

#### **版本切换**

```
git reset --hard commit_id    
git reset --hard HEAD^（上一版本）   
git reset --hard HEAD^^（上两个版本） 
git reset --hard HEAD~x 回退到第x个版本 
```

**操作日志**：`用于查看id号  git reflog`



# checkout进阶与stash
#### **文件恢复**

```
git checkout -- file_name
将文件恢复至暂存区的状态，实际效果为修改工作区的文件
```

```
git reset HEAD file_name
将文件从暂存区移回工作区
```

#### **切换到游离状态**

```
git checkout commit_id
切换到commit_id这个版本，相当于创建一个未命名的分支。
如果要保存在commit_id这个版本下的修改，必须进行提交并创建一个新分支。
创建新分支时指向此次提交的commit_id2。
git branch new_branch_name commit_id2
```



#### **保存现场**

```
使用场景---当前分支未开发完成，需要切换的另一分支进行开发
git stash
git stash list
```

#### **恢复现场**

``` 
git stash pop 恢复并删除stash内容
git stash apply stash内容并不删除，单纯恢复，需要通过git stash drop stash@{0}删除
git stash apply stash@{0} 恢复到指定现场
```



# 标签与diff

|              |                                     |              |                        |
| ------------ | ----------------------------------- | ------------ | ---------------------- |
| 查看便签     | git tag                             | 打上轻量标签 | git tag <message>      |
| 打上附注标签 | git tag -a <message> -m "<message>" | 查找标签     | git tag -l '<message>' |
| 删除标签     | git tag -d <message>                |              |                        |

```
git blame file_name
查看文件的全部修改记录以及作者
```

|                           |                             |                           |                            |
| ------------------------- | --------------------------- | ------------------------- | -------------------------- |
| 暂存区与工作区比较        | git diff                    | 特定commit_id与工作区比较 | git commit commit_id(HEAD) |
| 特定commit_id与缓存区比较 | git diff --cached commit_id |                           |                            |



# 远程与GitHub

#### 新建远程仓库

**Creat a new repo**  

```
git init
echo "readme" > README.md
git add .
git commit -m "first commit"
git remote add origin https://github.com/Chilkings/learngit.git
git push -u origin master
```

**Push an existing repo**

```
git remote add origin https://github.com/Chilkings/learngit.git
git push -u origin master //将本地仓库与远程仓库绑定并提交，只执行一次
git remote remove origin //取消关联
git push  				//提交 
git remote show           		//查看所有远程仓库
git remote show origin         //查看远程origin仓库的详细信息
```

#### SSH证书配置

```
ssh-keygen       生成，密码可掠过
id_rsa   私钥              
id_rsa_pub 公钥
```




# git协作

#### 协作模型

```
master 分支
test 分支
dev 分支
bugfix 分支
```

#### 获取远程仓库

```
git clone <link> <new_name> 
```

#### 推送与拉取

```
git pull = git fetch + git merge  拉取远程分支并自动合并
git fetch  拉取远程分支
git push 推送到远程分支
```

#### 图形化界面

```
gitk        git自带的图形化软件
git gui
```

**获取fork仓库的更新**

```
git remote -v  查看现有的远程仓库
git remote add upstream git@github.com:xxx/xxx.git   添加被fork的远程仓库并命名为upstream
git fetch upstream        拉取远程仓库
git merge upstream/master 合并
git push                 提交到自己的远程仓库
```



#  git refspec

**别名配置：**

`git config --global alias.br "branch"		将branch的别名设置为br`

**拉取远程并创建本地同名同内容分支：**

```
git checkout -b dev origin/dev 
git checkout --track origin/dev
```

**新建分支推送到远程**

```
首先切换到新建分支
git push -u origin dev   -u参数为关联，只需使用一次
git push --set-upstream origin dev
运行此命令的含义就是关联分支并推送，没有关联是无法推送的
```

**删除远程分支**：

```
git push origin src:dev
git push origin  :dev   将空分支推送到远程分支，相当于删除
git push origin --delete dev 
```

**标签必须手动推送**：

```
git push origin tag_name
git push origin --tag  推送所有未推送的标签
git push origin :refs/tags/v1.0    删除远程v1.0标签
git push origin --delete tag v1.0  删除远程v1.0标签
git tag -d v1.0    删除本地v1.0标签
```



# 模块化开发

**submodul**

无法修改，只能拉取更新

**subtree**

可以修改，作为子仓库



# 官方手册

https://git-scm.com/book/zh/v2
