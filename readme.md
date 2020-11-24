## Git的使用

> 最新更新：2020/11/24  git基本使用、关联远程分支
>
> 更新记录：

#### 简介

##### 分布式版本控制系统

- 从远程仓库克隆一份到本地仓库
- 在本地仓库进行版本更新

> 查看提交日志、提交、创建里程碑和分支、合并分支、回退等所有操作都在本地完成而不需要通过网络连接

#### 初始配置

##### 安装git，配置用户信息

```xml
$ git config --global user.name "用户名"
$ git config --global user.email "邮箱"
```

> 配置了全局的用户名和邮箱

##### 创建版本库

###### 本地仓库：

- 创建一个空目录

- 把目录变成git仓库

  ```yml
  git init
  #初始化的输出结果
  # Initialized empty Git repository in D:/JavaEEProject/MyGitRepository/.git/
  ```

###### 远程仓库

- 创建SSH Key

#### 关联远程仓库

##### 关联GitHub

- 创建`repository`

  登陆自己的github，右上角+号，New repository，填写相关信息

  ![image-20201124215540460](https://cdn.jsdelivr.net/gh/qinwant/Figurebed/img/20201124215542.png)

- 本地关联远程

```yml
# 初始化本地git仓库
git init
# 完本地仓库添加一个README.md的Markdown文件（非必须）
git add README.md
# 往本地仓库提交一次，提交内容说明:first commit
git commit -m "first commit"
# 与远程仓库关联
git remote add origin https://github.com/qinwant/MyGitRepository.git
# 同步推送本地仓库的提交到远程仓库mastet分支
git push -u origin master
```