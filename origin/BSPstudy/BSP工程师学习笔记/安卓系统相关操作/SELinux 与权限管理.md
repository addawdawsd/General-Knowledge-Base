# SELinux状态管理
# 临时关闭SELinux（设置为宽容模式）
setenforce 0
# 临时开启SELinux（设置为强制模式）
setenforce 1
# 查看SELinux当前状态
getenforce
# 查看SELinux详细状态信息
sestatus
# 永久禁用SELinux（需重启生效）
sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
# 永久启用SELinux（需重启生效）
sed -i 's/SELINUX=disabled/SELINUX=enforcing/g' /etc/selinux/config

# SELinux日志与排错
# 查看SELinux权限拒绝日志（avc: Access Vector Cache）
dmesg | grep avc
# 查看审计日志中的SELinux拒绝事件
ausearch -m avc
# 分析SELinux拒绝日志并提供解决方案
sealert -a /var/log/audit/audit.log
# 生成SELinux拒绝报告
aureport -m avc

# SELinux策略文件管理
# 转换策略文件格式（解决DOS格式导致的编译问题）
find vendor/lango/system/sepolicy/ -name "*.te" -exec dos2unix {} \;
# 恢复文件默认安全上下文
restorecon -Rv /path/to/directory
# 查看文件或目录的SELinux安全上下文
ls -Z /path/to/file
# 递归查看目录安全上下文
ls -laZ /path/to/directory

# SELinux权限规则添加
# 示例：修改触摸框权限文件（mw_default.te）
# 格式：allow 源类型 目标类型:目标类别 {权限};
allow hal_xbhhwmw_default boot_status_prop:file map;
# 添加文件上下文规则
semanage fcontext -a -t httpd_sys_content_t "/webdata(/.*)?"
# 应用文件上下文规则
restorecon -Rv /webdata

# SELinux策略工具
# 查看所有SELinux布尔值
getsebool -a
# 设置SELinux布尔值（-P选项使设置永久生效）
setsebool -P httpd_enable_homedirs on
# 查看SELinux端口标签
semanage port -l
# 添加SELinux端口标签
semanage port -a -