# 权限检查与初始化
# 确认是否有权限进入Gerrit仓库
# 创建代码目录并初始化Repo
mkdir am905D3
cd am905D3
repo init -u "http://pengguanzhen@192.168.1.182:8080/a/am905D3Adv/manifests"

repo init -u "http://luoyong@192.168.1.182:8080/a/AiTouch"

repo init -u  "http://luoyong@192.168.1.182:8080/a/rk3576_U/manifests"

git clone "http://luoyong@192.168.1.182:8080/a/AiTouch"
# 同步代码
repo sync


# 清代码
git clean -fd
git reset --hard aosp/develop-1.0