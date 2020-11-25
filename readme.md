## Git的使用

> 最新更新：2020/11/25 基本开发规范，命令总结
>
> 更新记录：2020/11/24  git基本使用、关联远程分支

### 1. Git介绍

#### 1.1 分布式版本控制管理工具

#### 1.2 协同开发的利器

### 2. 配置git环境

#### 2.1 Windows下搭建git

- 下载安装git：[git地址](https://git-scm.com/downloads)

- 找到`Git`，运行`Git Bash`

- 全局配置用户名邮箱

  ```yml
  git config --global user.name "用户名"
  git config --global user.password "邮箱"
  ```

#### 2.2 Linux下搭建git

- 命令安装

  ```yml
  sudo apt-get install git
  ```

### 3. 创建本地仓库

- 新建一个文件夹作为git仓库

- git命令初始化化文件夹

  ```yml
  git init
  ```

##### 成功创建的情况

- 文件夹下出现`.git`的隐藏文件

- 控制台出现如下输出

  ```yml
  Initialized empty Git repository in D:/JavaEEProject/MyGitRepository/.git/
  # D:/JavaEEProject/MyGitRepository为你的文件夹所在路径
  ```

### 4. 创建远程仓库

#### 4.1 创建`github`远程仓库

##### New repository

登陆自己的github，右上角+号，New repository，填写相关信息

![image-20201124215540460](https://cdn.jsdelivr.net/gh/qinwant/Figurebed/img/20201124215542.png)

##### 说明

- Public：公开仓库
- Private：私有仓库
- Add a README file： 说明文档，可先不创建
- Add .gitignore：设置忽略一些特定的文件（git时不会提交）
- Choose a license：选择许可证（可不勾选）

#### 4.2 创建码云远程仓库

###5. 关联远程仓库

##### 关联方式

- SSH
- Git

> 注意：

### 6. 常见命令总结

#### 6.1 创建git仓库

- 克隆一个已存在的仓库

  ```yml
  git clone https://gitclone.com/github.com/qinwant/MyGitRepository.git
  ```

- 创建一个新的本地仓库

  ```yml
  git init
  ```

#### 6.2 本地操作

- 查看当前工作目录下改变的文件

  ```yml
  git status
  ```

- 跟踪改变的文件

  ```yml
  git diff
  ```

- 加入所有改变的文件到下次提交

  ```yml
  git add .
  ```

- 加入部分改变的文件到下次提交

  ```yml
  git add -p <file>
  ```

- 提交所有改变的文件

  ```yml
  git commit -a
  ```

- 提交

  ```yml
  git commit 
  ```

- 改变最后一次提交

  ```yml
  git commit --amend
  ```

#### 6.3 提交历史

- 显示所有的提交，从最新的提交开始

  ```yml
  git log
  ```

- 显示一个指定文件的改变记录

  ```yml
  git log -p <file>
  ```

- 显示谁在什么时候对指定的文件做了什么操作

  ```yml
  git blame <file>
  ```

#### 6.4 分支与标签

- 罗列所有分支

  ```yml
  git branch -av
  ```

- 切换分支

  ```yml
  git checkout <branch>
  ```

- 基于当前的HEAD创建一个新的分支

  ```yml
  git branch <branch-name>
  ```

- 基于一个远程分支创建一个新的分支

  ```yml
  git checkout --track <remote/branch>
  ```

- 删除一个本地分支

  ```yml
  git branch -d <branch>
  ```

- 在当前提交上打上标签

  ```yml
  git tag <tag-name>
  ```

#### 6.5 更新与发布

#### 6.6 merge和rebase

#### 6.7 撤销操作

### 7. 如何协同开发

### 8. 常见问题解决

### 9. 实际开发规范

#### 9.1 分支命名

##### mas ter分支

- 主分支，用于部署生成环境，确保master分支稳定性
- 一般由`develop`分支和`hotfix`分支合并
- 任何时间都不能直接修改代码

##### develop分支

- 开发分支，始终保持最新完成及bug修复后的代码
- 开发新功能时，feature分支一般都是基于develop分支创建

##### feature分支

- 分支命名：feature/模块，例如`feature/user_module`

##### release分支

- 预上线分支，一般在发布提测阶段

> 当feature分支开发完成，首先会合并到develop分支，进入提测阶段会创建release分支。测试阶段存在bug时，直接在release分支修复并提交，测试完成之后，合并release分支到master和develop分支，此时master为最新代码，用作上线。

##### hotfix分支

- 分支命名：hotfix/开头的为修复分支
- 线上出现紧急bug时，以master分支为基线，创建hotfix分支，修复完成后，合并到master和develop分支

####  9.2 常见任务

##### 增加新功能

```yml
(dev)$: git checkout -b feature/xxx  # dev建立特性分支
(feature/xxx)$: 增加功能
(feature/xxx)$: git add xxx
(feature/xxx)$: git commit -m "提交新功能"
(feature/xxx)$: git checkout dev
(dev)$: git merge feature/xxx --no-ff # 特性分支合并到dev
```

##### 修复紧急Bug

```yml
(master)$: git checkout -b hotfix/xxx
(hotfix/xxx)$: 修复bug
(hotfix/xxx)$: git add xxx
(hotfix/xxx)$: git commit -m "修复紧急bug"
(hotfix/xxx)$: git checkout master
(master)$: git merge hotfix/xxx --no-ff # hotfix分支合并到master,上线到生产环境
(dev)$: git merge hotfix/xxx --no-ff # hotfix分支合并到dev，同步代码
```

##### 测试环境代码

```yml
(release)$: git merge dev --no-ff # dev分支合并到release，并在测试环境拉取并测试
```

##### 生产环境上线

```yml
(master)$: git merge release --no-ff # 把测试好的release分支代码合并到master分支
(master)$: git tag -a v0.1 -m "部署包版本名" #给版本命名，打标签
```

#### 9.3 日志规范

##### 格式`<type>:<subject>`

- `type`：本次commit的类型
  - `feat`：添加新特性
  - `fix`：修复bug
  - `docs`：仅仅修改了文档
  - `style`：仅仅修改了空格、格式、缩进（不改变代码逻辑）
  - `refactor`：代码重构，没有加新功能或者修复bug
  - `perf`：增加代码进行性能测试
  - `test`：增加测试用例
  - `chore`：改变构建流程，增加依赖库、工具
- `subject`：简明扼要的阐述本次commit的主旨