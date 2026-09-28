1. **9679U 解锁指令**

bash

运行

```bash
adb shell
avb init 0
avb set-devicestate 0
avb set-verity disable
```

2. **3576 解锁与刷写**

bash

运行

```bash
# 重启到bootloader
adb reboot bootloader
# 解锁vboot
fastboot oem at-unlock-vboot
# 重启到fastbootd模式
fastboot reboot fastboot
# 刷写镜像
fastboot flash misc misc.img
fastboot flash vendor_boot vendor_boot-debug.img
fastboot flash system system.img（需从谷歌服务器下载）
# 重启设备
fastboot reboot
```

3. **9950 Remount 权限**

bash

运行

```bash
set devicestate unlock
avbab disable-verity
delboot androidboot.selinux
saveenv
reset
# 手动挂载为可写
mount -o rw,remount /
```
