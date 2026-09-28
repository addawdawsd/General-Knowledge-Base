---
name: git-init-push
description: 把本地任意文件夹初始化为 Git 仓库并推送到 GitHub。覆盖 .gitignore 整理、重复目录去重校验、HTTPS(PAT) 与 SSH 两种认证、以及常见推送报错（Authentication failed / repository not found / GCM 退化成密码提示）的排查与解决。当用户说"把这个文件夹变成 git 仓库""推送到 GitHub""git push 失败/要凭证/要 SSH"时使用。
---

# Git 仓库初始化与推送（GitHub）

通用流程：把任意本地文件夹变成 Git 仓库并推送到 GitHub。

## 触发场景
- "把这个文件夹变成 git 仓库并推送到 GitHub"
- "git push 提示要用户名密码 / Authentication failed"
- "配置 SSH 免密推送 GitHub"

## 执行步骤

### 1. 初始化本地仓库
```bash
cd <文件夹路径>
git init -b main            # 初始化并直接建 main 分支
# 若本机未配置提交身份：
git config user.name  "名字"
git config user.email "邮箱"
```

### 2. 整理内容（强烈推荐）
新建 `.gitignore`，排除本地应用配置与杂项（以下以 Obsidian 笔记库为例，按需增删）：
```
# Obsidian 本地配置（非内容）
.obsidian/
# OS / 编辑器垃圾
Thumbs.db
Desktop.ini
.DS_Store
*~
# IDE
.vscode/
.idea/
```
若目录里存在与主体**完全一致**的镜像副本（如 `origin/` 与 `main/` 内容相同），先校验再移出仓库：
```bash
git rm -r --cached origin/   # 取消追踪，不删磁盘文件
# 在 .gitignore 末尾追加：origin/
```
> 校验两目录是否逐文件一致（避免误删独有文件）：分别 `cd` 进两个目录，
> `find . -type f -exec md5sum {} \; | sort` 生成两份清单后 `diff`，无差异即为镜像。
> 确认无误后再决定是否把重复目录移入回收站彻底清理（非必须，且删除前需用户确认）。

### 3. 暂存与首次提交
```bash
git add -A
git commit -m "Initial commit: ..."
```

### 4. 添加远程仓库
```bash
git remote add origin https://github.com/<用户名>/<仓库名>.git
git branch -M main
```

### 5. 选择认证方式
GitHub 自 2021-08 起**不再支持用账号登录密码**做 HTTPS 推送。两种可行方式：

**方式 A ｜ Personal Access Token（HTTPS）**
1. GitHub 网页 → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token
2. 勾选 `repo`（完整仓库权限）→ Generate → 复制 token（只显示一次）
3. 推送时用户名填 GitHub 用户名、密码处**粘贴 token**
4. 或一次性写进 remote：`git remote set-url origin https://<TOKEN>@github.com/<用户名>/<仓库名>.git`
   （推完建议改回 `git remote set-url origin https://github.com/<用户名>/<仓库名>.git`，避免 token 明文留在 `.git/config`）

**方式 B ｜ SSH 密钥（推荐，一劳永逸）**
1. 生成本地密钥：
   ```bash
   ssh-keygen -t ed25519 -C "邮箱"
   # 一路回车用默认路径；若提示已存在则选 no 复用现有密钥
   ```
2. 复制公钥：`cat ~/.ssh/id_ed25519.pub`
3. GitHub → Settings → SSH and GPG keys → New SSH key → Title 自取、Key type 保持 Authentication Key、粘贴公钥 → Add SSH key
4. 改 remote 为 SSH 形式并推送：
   ```bash
   git remote set-url origin git@github.com:<用户名>/<仓库名>.git
   git push -u origin main
   ```
   首次连接输入 `yes` 接受 host key，之后免密。
   （关于页面上的 "Vigilant mode"：是 GPG 提交签名验证开关，与能否用 SSH 推送无关，无需理会。）

### 6. 验证
```bash
git ls-remote origin      # 远端 main 的 SHA 应等于本地 HEAD（权威确认已推送）
ssh -T git@github.com     # 看到 Hi <用户名>! 即 SSH 连通
```

## 常见问题

| 现象 | 原因 | 解决 |
|------|------|------|
| `fatal: Authentication failed` | 凭证错 / 用的是登录密码 | 改用 PAT 或 SSH |
| `repository not found` | 仓库不存在或无 push 权限 | 先去 GitHub 建好同名空仓库，并确认账号有写权限 |
| `git push` 卡在 `Username for 'https://github.com':` 且报 `Password authentication is not supported` | 在用登录密码做 HTTPS | 必须换 PAT 或 SSH |
| Git Credential Manager 退化成终端账号密码提示 | 默认 authMode 回退到 basic | 强制浏览器登录：`git config --global credential.https://github.com.authModes "oauth"` 后重推 |

## 注意事项
- 推送涉及外部认证：若当前运行环境无法弹窗/存凭据（如沙箱），完成本地配置后，请让用户**在本机终端**执行最后一步 `git push` / `git remote set-url` + `git push`。
- 删除个人目录文件前务必先 md5 校验，并优先移入回收站而非永久删除；删除前需向用户明确说明风险并取得确认。
- 远程仓库地址与用户名均为变量，执行时向用户确认，不要硬编码。
