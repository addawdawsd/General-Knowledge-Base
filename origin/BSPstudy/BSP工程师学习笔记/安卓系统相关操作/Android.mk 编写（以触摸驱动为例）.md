makefile

```makefile
LOCAL_PATH := $(call my-dir)
include $(CLEAR_VARS) 

# 模块名称
LOCAL_MODULE := k2_ir_touch 
# 源文件（此处为可执行文件）
LOCAL_SRC_FILES := k2_ir_touch 
# 模块类型（可执行文件）
LOCAL_MODULE_CLASS := EXECUTABLES
# 标记为私有模块
LOCAL_PROPRIETARY_MODULE := true
# 依赖库（按需添加，此处注释示例）
# LOCAL_SHARED_LIBRARIES := libasound libc++ libc libcutils libdl libhardware liblog libm libutils
# 跳过ELF文件检查（解决无法复制问题）
LOCAL_CHECK_ELF_FILES := false

include $(BUILD_PREBUILT)

# 将模块添加到产品打包列表
PRODUCT_PACKAGES += k2_ir_touch
```
