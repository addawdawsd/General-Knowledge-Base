1. **核心用途**：防止 SSH 连接断开（如死机、网络中断）导致代码编译 / 执行中断，保持服务端持续运行。
2. **常用命令**

bash

运行

```bash
# 查看所有后台会话
tmux ls
# 新建会话（指定名称，如compile）
tmux new -s compile
# 隐藏会话（后台运行）：先按Ctrl+B，再按D
# 进入指定会话（如compile）
tmux a -t compile
# 删除指定会话（如compile）
tmux kill-session -t compile
```
