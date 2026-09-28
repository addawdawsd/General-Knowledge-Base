##  查看文件格式命令

bash

```bash
file device/xxxx/common/sepolicy/vendor/system_suspend.te
```

**执行结果**：

plaintext

```plaintext
device/xxxx/common/sepolicy/vendor/system_suspend.te: ASCII text, with CRLF line terminators
```

## 2. 转换文件格式命令

bash

```bash
dos2unix device/xxxx/common/sepolicy/vendor/system_suspend.te
```

## 3. 再次查看转换后格式命令

bash

```bash
file device/xxxx/common/sepolicy/vendor/system_suspend.te
```

**执行结果**：

plaintext

```plaintext
device/xxxx/common/sepolicy/vendor/system_suspend.te: ASCII text
```