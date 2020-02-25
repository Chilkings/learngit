# 起步

## git配置

Git 自带一个 `git config` 的工具来帮助设置控制 Git 外观和行为的配置变量。 这些变量存储在三个不同的位置：

1. `/etc/gitconfig` 文件: 使用带有 `--system` 选项的 `git config` 时，它会从此文件读写配置变量。
2. `~/.gitconfig` 或 `~/.config/git/config` 文件：只针对当前用户。 可以传递 `--global` 选项让 Git 读写此文件。
3. 当前使用仓库的 Git 目录中的 `config` 文件（就是 `.git/config`）：针对该仓库。

在 Windows 系统中，Git 会查找 `$HOME` 目录下（一般情况下是 `C:\Users\$USER`）的 `.gitconfig` 文件。 Git 同样也会寻找 `/etc/gitconfig` 文件，也就是在安装 Git 时所选的目标位置。

#### 用户信息

```console
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

#### 文本编辑器

```console
$ git config --global core.editor emacs
```

#### 检查配置信息

```console
$ git config --list
```

## 获取帮助

若你使用 Git 时需要获取帮助，有三种方法可以找到 Git 命令的使用手册：

```console
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```

例如，要想获得 config 命令的手册，执行

```console
$ git help config
```

# git基础

## 获取仓库

#### 初始化本地仓库

```console
$ git init
```

#### 克隆远程仓库

```console
$ git clone https://github.com/libgit2/libgit2 mylibgit  //克隆远程仓库并重命名为mylibgit
```

# 记录更新

![](https://raw.githubusercontent.com/Chilkings/blog_image/master/20200223152908.png)

#### **文件的四种状态**

1. 未跟踪
2. 未修改
3. 已修改
4. 已暂存

#### **常用操作**

```
git status 查看
git add . 将所有文件添加到暂存区
git commit -m "<message>" 进行一次提交

git commit --amend -m "message" 替换最新的一次提交
```

#### **从版本库删除文件**

```
git rm <file_name> = rm <file_name> + git add <file_name>
```

#### 恢复删除的文件

```
1. 将被删除的文件从暂存区恢复到工作区
   git reset HEAD test2.txt
2. 丢弃删除这一动作
   git checkout -- test2.txt
```
#### 忽略不需要的文件

自定义`.gitignore`文件：

1. ` *.txt  !error.txt 忽略所有txt文件除了error.txt`

2. `指定层级 /error.txt  /*/error.txt /**/error.txt `

3. `忽略文件夹的所有文件 build/

   > GitHub 有一个十分详细的针对数十种项目及语言的 `.gitignore` 文件列表，你可以在 https://github.com/github/gitignore 找到它。

#### 查看提交记录

```
git log -3  
git log --pretty=oneline
```

