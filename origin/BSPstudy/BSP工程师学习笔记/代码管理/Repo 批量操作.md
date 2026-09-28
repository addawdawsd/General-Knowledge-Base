1. **全仓库分支与代码管理**

bash

运行

```bash
# 查看所有仓库分支状态
repo forall -c "git br -vv"
# 全仓库创建并切换分支
repo forall -c "git checkout -b 本地分支名 aosp/远程分支名"
# 示例：创建tcl-os5.1_9679_20250428分支
repo forall -c "git co -b tcl-os5.1_9679_20250428 aosp/tcl-os5.1_9679_20250428"
# 全仓库拉取最新代码并重置
repo forall -c 'git clean -xdf; git checkout .; git fetch; git reset --hard 远程分支; git pull'
# 示例1：拉取aosp/tcl-os5.1_9679_20250428
repo forall -c 'git clean -xdf; git checkout .; git fetch;git reset --hard aosp/tcl-os5.1_9679_20250428; git pull'
# 示例2：拉取aosp/iwb_develop-1.0.0-EDLA
repo forall -c 'git clean -xdf; git checkout .; git fetch; git reset --hard aosp/iwb_develop-1.0.0-EDLA; git pull'
# 全仓库回退到指定日期前的代码
repo forall -c 'ID=`git log --before="2025-01-21" -1 --pretty=format:"%H"`;git reset --hard $ID'
# 全仓库同步远程所有分支
repo forall -c 'git fetch --all'
```

2. **特殊仓库处理（xbh 仓库）**

bash

运行

```bash
# 全仓库拉取后，单独更新xbh仓库
cd vendor/xbh
git pull --force
```
