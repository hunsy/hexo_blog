---
title: 已存在项目上传github
date: 2018-02-28 18:54:45
tags:
categories: Git
---

#### 1. 打开命令行终端，进入项目所在的目录，将项目初始化为Git项目

```
git init
```
执行上述命令，会在当前目录生成.git隐藏文件夹

#### 2. 将本地文件添加到本地的git仓库中
	
```
git add .
```
如果目录中存在 `.gitignore`文件，会按照已有规则过滤不需要的文件。如果不需要添加所以文件，可以将`.`换成具体文件的名称。

#### 3. 将已添加的文件提交到本地仓库

```
git commit -m 'Inital commit'
```

#### 4. 在github上创建一个新的仓库

```
为了避免冲突，先不要勾选 `README` 和 `LICENSE` 选项
```

#### 5. 复制项目主页上的仓库地址

```	
例如： `https://github.com/hunsy/mc.git`
```

#### 6. 在命令行终端将本地仓库与远程仓库关联

```
git remote add origin https://github.com/hunsy/mc.git`
```

#### 7. 提交代码到git仓库

```
git push -u origin master
```

#### 参考：

![github](/images/img1.png)