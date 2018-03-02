---
title: Git基本操作
date: 2018-03-01 10:35:59
tags:
categories: Git
---
### 新建与获取项目命令

#### 1. git init

`git init`是在目录中创建Git的本地仓库。

例如：

```
$ mkdir demo
$ cd demo/
$ git init
Initialized empty Git repository in /home/hunsy/demo/.git/
```


#### 2. git clone
	
`git clone [url]`拷贝一个仓库到本地。url是想要拷贝项目的地址。

```
$ git clone https://github.com/hunsy/jzz.git
Cloning into 'jzz'...
remote: Counting objects: 7, done.
remote: Total 7(delta 0), reused 0 (delta 0),pack-reused 7
Unpacking objects: 100% (7/7),done.
Checking connectivity... done.
$cd jzz
$ ll
total 12
drwxrwxrwx 0 liuxindime liuxindime  4096 Mar  1 10:59 ./
drwxr-xr-x 0 liuxindime liuxindime  4096 Mar  1 10:58 ../
drwxrwxrwx 0 liuxindime liuxindime  4096 Mar  1 10:59 .git/
-rw-rw-rw- 1 liuxindime liuxindime   189 Mar  1 10:59 .gitignore
-rw-rw-rw- 1 liuxindime liuxindime 11357 Mar  1 10:59 LICENSE
-rw-rw-rw- 1 liuxindime liuxindime    21 Mar  1 10:59 README.md
```

### 基本快照命令

#### 1. git add

`git add [文件]` 将文件添加到缓存。

```
$ touch test.txt
$ ls
test.txt
$ git status -s
?? test.txt
```

`git status` 命令用于查看项目的当前状态。
使用 `git add` 命令将文件 `test.txt` 添加到缓存。

```
$ git add text.txt
```
再次使用 `git status -s` 查看项目。

```
$ git status -s
A test.txt
```

将项目中所有文件添加到缓存，用 `git add .` 命令。

修改 `test.txt`文件,添加内容：

```
$ vim test.txt
```

再次使用 `git status -s` 命令，查看项目状态：

```
$ git status -s
AM test.txt
```

`AM`状态的意思是，该文件已经添加到缓存之后又有改动。改动后的文件需要再次执行 `git add` 命令添加到缓存。

```
$ git add test.txt
$ git status -s
A test.txt 
```

#### 2. git status

`git status` 命令可以查看自上传提交后，项目是否有修改。

加上 `-s` 参数，为了获取简短的状态结果。 
完整的状态结果如下：

```
$ git status
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   test.txt
```

#### 3. git diff

执行 `git diff` 来查看执行 `git status` 的结果的详情。
`git diff` 命令显示已写入缓存与已修改但尚未写入缓存的改动的区别。`git diff` 有两个主要的应用场景。

+ 尚未缓存的改动： `git diff`
+ 查看已缓存的内容： `git diff --cached`
+ 查看已缓存与未缓存的所有改动： `git diff HEAD`
+ 显示摘要与非整个diff: `git diff --stat`

编辑 `test.txt`:

```
$ vim test.txt
```

```
$ git status -s
AM test.txt
$ git diff
diff --git a/test.txt b/test.txt
index d670460..4a44544 100644
--- a/test.txt
+++ b/test.txt
@@ -1 +1,2 @@
 test content
+add
```

`git status` 显示你上次提交更新后的更改或者写入缓存的改动， 而 `git diff` 一行一行地显示这些改动具体是啥。

`git diff --cached` 命令执行效果如下:

```
$ git diff
diff --git a/test.txt b/test.txt
new file mode 100644
index 0000000..d670460
--- /dev/null
+++ b/test.txt
@@ -0,0 +1 @@
+test content
```

#### 4. git commit

`git commit` 命令，是将写入缓存的文件提交到本地仓库。
Git为你的每一次提交都记录你的名字与电子邮箱，所以要首先配置用户名和邮箱地址。

```
$ git config --global user.name hunsy
$ git config --global user.email liuxindime1987@126.com
```

使用 `git commit` 命令提交所有缓存的文件。
`-m` 参数用于注释提交信息

```
$ git status -s
A test.txt
$ git commit -m '提交test.txt'
[master 9789be2] 提交test.txt
 1 file changed, 2 insertions(+)
 create mode 100644 test.txt
```

现在已经记录了快照。

```
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean
```

如果没有 `-m` 参数，Git会尝试打开编辑器，填写提交信息。默认会打开vim.

跳过 `git add` 命令，Git允许使用 `-a` 参数跳过这一步。

```
$ git commit -a
```

修改 `test.txt`

```
$ vim text.txt
```

执行直接提交:

```
$ git commit -am '测试-a提交'
[master 30ae2a3] 测试-a提交
 1 file changed, 1 insertion(+)
```

#### 5. git reset HEAD

`git reset HEAD` 命令用于取消已缓存的内容。

演示操作如下:

```
$ vim test.txt
$ vim test2.txt
$ git status -s
 M test.txt
?? test2.txt
$ git add .
$ git status -s
 M test.txt
A test2.txt
$ git reset HEAD test.txt
Unstaged changes after reset:
M       test.txt
$ git status -s
 M test.txt
A  test2.txt
$ git commit -m '修改'
[master 5af03ff] 修改
 1 file changed, 1 insertion(+)
 create mode 100644 test2.txt
```

#### 6. git rm 

`git rm` 命令，删除项目中的文件。如果手动删除文件，在运行 `git status ` 会报 `Changes not staged for commit`的提示。
要从Git中删除文件，就必须从跟踪清单中移除，然后提交。

```
$ git rm <file>
```

如果删除之前，文件修改过并且放到缓存区，则必须使用强制删除选中 `-f`

```
$ git rm -f <file>
```

如果只是从缓存区移除，仍保留文件在工作目录，就是将文件从跟踪清单中删除。 可以使用选项 `--cached`

```
$ git rm --cached <file>
```

如果删除一个目录，则需要递归删除 `-r`

```
$ git rm -r <文件夹>
$ git rm -r * 
```

#### 7. git mv

`git mv` 命令用于移动或重命名一个文件、目录、软连接。

```
$ git mv test.txt test.txt.bak
$ ls
test.txt.bak
```