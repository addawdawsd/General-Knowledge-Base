# 基础配置与设备管理
# 查询已连接设备
adb devices
# 重启设备到bootloader模式
adb reboot bootloader
# 软重启系统
adb shell stop; start
# 硬重启设备
adb reboot
# 获取root权限（部分设备需解锁）
adb root
# 重新挂载系统分区为可写
adb remount

# 文件传输与应用管理
# 推送文件到设备
adb push
# 示例：推送中间件APK
adb push D:\code\first\MiddleWare5.0\out\release\XbhPlatformMiddleWare_rk3588_5.2.0.80_9e5ff794.apk /system/app/XbhPlatformMiddleWare/XbhPlatformMiddleWare.apk
# 安装应用（强制覆盖安装）
adb install -r
# 示例：安装教学应用
adb install -r .\ls\prowise_app_teach.apk
# 获取已安装应用列表
adb shell pm list packages
# 清除应用缓存（以中间件为例）
pm clear xbh.platform.middleware
# 查看应用版本（以中间件为例）
dumpsys package xbh.platform.middleware | grep version



# 抓内核日志
logcat -b kernel -v time > /sdcard/kernel.log


# 抓USER报告
