1. **分支管理**

bash

运行

```bash
# 查看本地分支（含关联远程分支）
git br -vv
# 查看所有分支（本地+远程）
git br -a
# 创建并切换到本地分支（关联远程分支）
git checkout -b 本地分支名 origin/远程分支名
# 示例：创建vs_9679g_edla_250224分支
git checkout -b develop-1.0 origin/develop-1.0  origin/develop-1.0
# 设置本地分支关联远程分支
git br --set-upstream-to=aosp/远程分支名 本地分支名
# 示例：关联develop-1.0.0-EDLA分支
repo forall -c "git br --set-upstream-to=aosp/develop-1.0.0-EDLA"


repo forall -c 'git clean -xdf; git reset --hard HEAD~1; git pull aosp iiyama_revC:iiyama_revC --force'

repo forall -c 'git clean -xdf . && git checkout -- . && git fetch && git reset --hard @{u} && git pull'

repo forall -c 'git clean -xdf; git reset --merge; git fetch aosp;'

repo forall -c 'git clean -xdf; git reset --hard HEAD^; git pull'

repo forall -c 'git fetch && git reset --hard @{u} && git clean -xdf'

```

2. **代码提交与回退**

bash

运行

```bash
# 添加修改文件到暂存区
git add .
# 提交修改（修改最近一次提交）
git commit --amend
# 查看提交日志
git log
# 拉取远程代码
git fetch
# 回退到上一次提交（保留修改）
git reset HEAD^
# 强制回退到指定版本（丢弃所有修改）
git reset --hard 版本号/HEAD/远程分支
# 示例1：回退到当前HEAD
git reset --hard HEAD
# 示例2：回退到远程develop-1.0
git reset --hard remotes/aosp/develop-1.0.0-EDLA
# 回退某一笔提交
git revert 提交ID
# 代码清理（删除未跟踪文件和目录）
git clean -fd
# 彻底清理（删除所有未跟踪文件，含.gitignore中的）
git clean -xdf
```

3. **代码推送**

bash

运行

```bash
# 推送到Gerrit（格式：refs/for/目标分支）
git push aosp HEAD:refs/for/目标分支

git push origin HEAD:refs/for/develop-android14_edla_311D2

git push origin HEAD:refs/for/develop-common

git push origin HEAD:refs/for/develop-2.1.6-311d2-iiyama

git push origin HEAD:refs/for/master

git push origin HEAD:refs/for/develop-6.1

git push origin HEAD:refs/for/RB_Public_G520_1.0.0-20260617

git push aosp HEAD:refs/for/develop

git push origin HEAD:refs/for/develop-main

git push aosp HEAD:refs/for/RB_Public_G520_1.0.0-20260617

git push aosp HEAD:refs/for/Sorbet_3576_Android16_developer_branch

git push aosp HEAD:refs/for/develop-1.0.0

git push aosp HEAD:refs/for/Sorbet_3576_developer_branch

git push aosp HEAD:refs/for/develop-1.0.0-EDLA

git push aosp HEAD:refs/for/iiyama_revC
git push aosp HEAD:refs/for/xbh-production-android16_os6.1_3576_20260313

aosp/Benq_EDLA_A311D2_Release_MP_20250715
# 示例1：推送到vs_9679g_edla_250224分支
git push origin HEAD:refs/for/iiyama_3576b_EDLA_20250730
# 示例2：推送到aosp的develop分支
git push aosp develop:refs/for/develop

git push origin HEAD:refs/for/develop_5.3

git push origin HEAD:refs/for/iiyama_9679b_edla_20250215

git push origin HEAD:refs/for/RB_aple_android16 

git push aosp develop-1.0.0-EDLA_20260105:refs/for/develop-1.0.0-EDLA_20260105

git push origin HEAD:refs/for/xbh-production-android16_os6.1_3576_410_20260414


git push origin HEAD:refs/for/RB_iiyama_3576b_EDLA_20250730
```

创建并切换到本地develop-1.0分支：
```bash
git checkout -b develop-1.0
将本地分支关联到远程aosp/develop-1.0分支：（如果远程分支已存在）
bash
git branch --set-upstream-to=aosp/develop-1.0 develop-1.0
（如果远程分支不存在，需先推送本地分支到远程）
```
要删除当前仓库中下面的 develop-1.1 分支，需注意当前不能处于该分支（从截图看当前在 develop-1.0，符合条件），执行以下 Git 命令：
```bash
git branch -d develop-1.1
```
切完分支后拉代码
- repo forall -c "git clean -xdf;git reset --hard HEAD^;git pull"

### 1. 强制使用传入的代码（合进来的分支）

确保你在项目的根目录（即 `MiddleWare3.0` 目录下），运行以下命令：

Bash

```
git checkout --theirs .
```

_(注意末尾有一个 `.`，这代表将当前目录下所有产生冲突的文件，全部替换为你要 cherry-pick 进来的那个版本。)_

### 2. 将修改标记为已解决

把这些刚刚替换好的文件添加到暂存区：

Bash

```
git add .
```

### 3. 继续并完成 cherry-pick

最后，告诉 Git 冲突已经解决，继续完成操作：

Bash

```
git cherry-pick --continue
```

此时如果弹出一个文本编辑器让你确认提交信息，直接保存并关闭即可（通常在 Vim 中是输入 `:wq` 然后回车）。



# 合错分支了

```
git reset --mixed HEAD@{1}
```





git pull --rebase origin <你的分支名>
# 例如：git pull --rebase origin main












# 拉取远端最新代码
git fetch aosp 
# 变基同步到远端 develop-1.0，
不会产生合并提交 git rebase aosp/develop-1.0