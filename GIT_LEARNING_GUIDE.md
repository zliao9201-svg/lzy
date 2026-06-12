# Git 教程

这不是概念介绍，这是按顺序操作的教程。

你照着做，就能把本地 Git、远程仓库、`push`、`pull` 跑通。

---

## 1. 先回答你最关心的几个问题

### 1.1 你电脑上为什么会有 Git

因为 Git 已经被安装到你的电脑里了。

你这台机器上的 Git 可执行文件位置是：

```text
D:\lzy tool\Git\cmd\git.exe
```

这说明：

- Git 不是我临时给你变出来的
- 是你电脑里本来就已经装好的程序
- 只要终端里能执行 `git --version`，就说明环境可用

你自己验证：

```powershell
git --version
where.exe git
```

---

## 2. 第一步：确认 Git 能用

执行：

```powershell
git --version
```

你应该能看到类似：

```text
git version 2.53.0.windows.1
```

这一步是干嘛的：

- 确认 Git 已安装
- 确认终端能找到 Git

如果这一步报错，后面所有 Git 命令都不能继续。

---

## 3. 第二步：配置用户名和邮箱

Git 每次提交都要记录“是谁提交的”，所以必须先配身份。

执行：

```powershell
git config --global user.name "lzy"
git config --global user.email "你的邮箱"
```

例如：

```powershell
git config --global user.name "lzy"
git config --global user.email "lzy@example.com"
```

查看配置结果：

```powershell
git config --global user.name
git config --global user.email
```

这一步是干嘛的：

- `user.name`：提交记录里显示的名字
- `user.email`：提交记录里显示的邮箱

注意：

- 这是 Git 配置，不是 GitHub 账号登录
- 配了这个，不代表你已经连上 GitHub
- 它只是告诉 Git：“以后提交时写谁的名字和邮箱”

你这台电脑现在已经配置过：

```text
user.name = lzy
user.email = lzy@example.com
```

如果要改，重新执行一次即可，后执行的值会覆盖前面的。

---

## 4. 第三步：进入项目目录

如果你要在某个项目里用 Git，先进入那个目录。

例如你现在的练习目录：

```powershell
cd C:\Users\82791\git-training
```

这一步是干嘛的：

- 告诉 Git：你要操作的是哪个项目
- Git 的很多命令都依赖当前目录

---

## 5. 第四步：初始化本地仓库

如果这个目录还不是 Git 仓库，执行：

```powershell
git init
```

这一步是干嘛的：

- 在当前目录创建 `.git` 隐藏目录
- 从这一刻起，这个文件夹就变成“Git 仓库”

你可以理解成：

- 普通文件夹：只是放文件
- Git 仓库：除了放文件，还能记录历史

检查是否初始化成功：

```powershell
git status
```

如果能看到分支、文件状态等信息，说明仓库已经可用。

---

## 6. 第五步：第一次提交

这是本地 Git 最基础的一套流程。

### 6.1 查看状态

```powershell
git status
```

这一步是干嘛的：

- 看哪些文件改了
- 看哪些文件还没被 Git 跟踪
- 看哪些文件已经放进暂存区

### 6.2 添加到暂存区

```powershell
git add .
```

这一步是干嘛的：

- 把当前改动加入“准备提交的清单”

注意：

- `git add .` 不是提交
- 只是先把内容放进暂存区

### 6.3 正式提交

```powershell
git commit -m "第一次提交"
```

这一步是干嘛的：

- 生成一次本地历史记录
- 把暂存区内容正式保存下来

### 6.4 查看提交历史

```powershell
git log --oneline
```

这一步是干嘛的：

- 查看你刚才的提交是否已经生成

---

## 7. 第六步：以后每次改代码的固定顺序

以后你平时写代码，就按这个顺序：

```powershell
git status
git add .
git commit -m "本次改动说明"
```

如果想看历史：

```powershell
git log --oneline --graph --all
```

记住这个最小流程就够了：

1. 先看 `status`
2. 再 `add`
3. 再 `commit`

---

## 8. 第七步：检查有没有远程仓库

本地仓库和远程仓库不是一回事。

先检查当前有没有远程：

```powershell
git remote -v
```

如果有输出，例如：

```text
origin  https://github.com/你的用户名/项目名.git (fetch)
origin  https://github.com/你的用户名/项目名.git (push)
```

说明已经绑定了远程。

如果没有任何输出，说明：

- 当前只有本地仓库
- 还没有远程仓库地址

---

## 9. 没有远程时，为什么不能 pull

因为 `pull` 的意思是：

“从远程仓库拉取最新内容到本地”

所以必须先满足两个条件：

1. 你得有远程仓库
2. 本地仓库得知道远程仓库地址

如果你连远程都没配置，`git pull` 就没有目标可拉。

所以顺序一定是：

1. 先建远程仓库
2. 再把本地和远程绑定
3. 然后才能 `push` / `pull`

---

## 10. 第八步：先去 GitHub 或 GitLab 新建远程仓库

### 如果你用 GitHub

去 GitHub 网站，新建一个空仓库。

### 如果你用 GitLab

去 GitLab 网站，新建一个空仓库。

创建完后，你会拿到一个远程地址，通常长这样：

```text
https://github.com/你的用户名/git-training.git
```

或者：

```text
https://gitlab.com/你的用户名/git-training.git
```

这一步是干嘛的：

- 在云端准备一个仓库
- 给本地仓库一个上传目标

---

## 11. 第九步：把本地仓库绑定到远程仓库

拿到远程地址后，在本地执行：

```powershell
git remote add origin <远程仓库地址>
```

例如：

```powershell
git remote add origin https://github.com/你的用户名/git-training.git
```

这一步是干嘛的：

- `origin` 是远程仓库的默认名字
- 把你的本地仓库和那个网址关联起来

执行完后检查：

```powershell
git remote -v
```

如果看到远程地址，说明绑定成功。

---

## 12. 第十步：第一次 push

第一次上传前，先看当前分支名：

```powershell
git branch --show-current
```

你当前练习仓库现在所在分支是：

```text
feature/login-note
```

这不是适合第一次上传到远程的主分支名。

正常教程里，第一次上传一般发生在：

- `master`
- 或 `main`

所以你自己以后要先确认分支名，再决定 push 哪个分支。

### 如果当前分支是 `master`

执行：

```powershell
git push -u origin master
```

### 如果当前分支是 `main`

执行：

```powershell
git push -u origin main
```

### 如果你就是要上传当前功能分支

执行：

```powershell
git push -u origin feature/login-note
```

这一步是干嘛的：

- 把本地提交上传到远程
- `-u` 表示以后记住默认上游分支

---

## 13. 第十一步：以后怎么 pull 和 push

当远程已经配好以后，日常顺序通常是：

### 开始工作前

```powershell
git pull
```

作用：

- 把远程最新代码拉到本地

### 改完代码后

```powershell
git add .
git commit -m "本次改动说明"
git push
```

作用：

- `add`：准备提交
- `commit`：生成本地提交
- `push`：把本地提交传到远程

---

## 14. 最短操作清单

如果你不想看解释，只想照着做，就按这个顺序。

### 本地第一次使用 Git

```powershell
git --version
git config --global user.name "lzy"
git config --global user.email "你的邮箱"
cd 你的项目目录
git init
git status
git add .
git commit -m "第一次提交"
```

### 绑定远程

```powershell
git remote -v
git remote add origin <远程仓库地址>
git remote -v
```

### 第一次上传

```powershell
git branch --show-current
git push -u origin master
```

如果不是 `master`，就把最后一个参数改成当前分支名。

### 以后日常使用

```powershell
git pull
git add .
git commit -m "修改说明"
git push
```

---

## 15. 你现在最该怎么做

你现在不要急着背所有命令。

先按这个顺序做就行：

1. `git --version`
2. `git config --global user.name`
3. `git config --global user.email`
4. `git remote -v`
5. 去 GitHub 或 GitLab 创建空仓库
6. `git remote add origin <url>`
7. `git branch --show-current`
8. `git push -u origin <当前分支名>`

只要这 8 步跑通，你的“本地 + 远程”链路就通了。

---

## 16. 你下一步如果还要继续

下一份教程可以继续写成纯操作版：

- `GitHub / GitLab 建仓库到 push 成功`
- `分支怎么创建、切换、合并`
- `怎么撤销错误提交`
- `怎么解决 pull / push 冲突`
