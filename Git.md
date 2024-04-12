# Git的基本操作

## 创建账号--查询

设置用户信息

```l
git config --global user.name "messi"
git config --global user.email "barca10messi@163.com"
```

查询用户信息

```
git config --global user.name
git config --global user.email
```

## 创建文件

在用户目录下创建一个.bashrc的文件

```
touch ~/.bashrc
```

## 获取本地仓库

1. 在需要进行代码控制的仓库进行右键点击gitbash

2. 进行初始化

   ```
   git init
   ```

   

## 仓库操作

1. 获取仓库状态

   ```
   git status
   ```

2. 添加工作区进仓库暂存区(index)

   ```
   git add .  //这个.代表添加当前文件夹中所有文件
   ```

3. 提交暂存区进入本地仓库

   ```
   git commit -m "add file01"//这个file01是自定义的
   ```

4. 查看提交信息

   ```
   git log
   ```

5. 版本回退

   ```
   git reset -
   ```


## 分支

几乎所有的版本控制系统都以某种形式支持分支,使用分支意味你可以把你的工作从主线上分离开来进行重大bug修改,开发新的功能,以免影响开发主线

### 分支操作

- 查看本地分支

```
git branch
```

- 创建本地分支

```
git branch 分支名
```

- **切换分支**

```
git checkout -b 分支名
```

- 合并分支

一个分支上的提交可以合并到另一个分支

```
git merge 分支名称
```

