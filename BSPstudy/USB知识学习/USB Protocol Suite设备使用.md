# USB篇
# 注意注意！
# 设备插入时会更新固件注意不要拔插，影响升级后果严重。
# 具体操作步骤
## 1.硬件的连接
1. 采集设备与USB Protocol Suite设备与电脑串联
2. 设备亮绿灯就表示正常连接。
## 2.USB采集的设置
![[设备设置位置.png]]
- 上图是设置在工具中的位置
![[USB默认设置.png]]
- 上图是2.0USB采集的设置图
- 在这个设置下如果没有采集到128MB数据前，需要手动停止保存。






# 3.数据分析
![[屏蔽界面.png]]
- 上图为屏蔽工具
- CC事件屏蔽（此事件为USB握手时的数据，可以不必看）
- SOF数据屏蔽（每次帧开始时传输的数据，也可以不必看）
- ![[Transfer事件.png]]
- 上图是屏蔽事件后的USB枚举过程中产生的传输事件
## USB数据的组成和分析可以看下面的这篇文章
- 【USB 协议分析（含基本协议和 USB 请求和设备枚举） - CSDN App】https://blog.csdn.net/zhoutaopower/article/details/82083043?sharetype=blog&shareId=82083043&sharerefer=APP&sharesource=m0_64276870