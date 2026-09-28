# 1. 查看系统所有 I2C 总线 
- ls /dev/i2c-*

# 2. 查看已注册的 I2C 设备（按总线）                                                
- ls /sys/bus/i2c/devices/  
# 3. 查看具体总线上的设备（如总线1）
- ls /sys/bus/i2c/devices/i2c-1/
# 4. 用 i2c-tools 扫描总线上的设备地址（如果设备上有 i2cdetect）
- i2cdetect -y <bus_number>    # 如 i2cdetect -y 1 