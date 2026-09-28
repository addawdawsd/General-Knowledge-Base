# Git 仓库初始化与 SSH 推送流程

## 适用场景
把本地一个文件夹（例如知识库 / 学习笔记）初始化成 Git 仓库，并推送到 GitHub。本文基于一次真实操作整理。

## 一、初始化本地仓库
```bash
cd <你的文件夹路径>
git init -b main          # 初始化仓库并直接创建 main 分支
```
若本机尚未配置提交身份：
```bash
git config user.name  "你的名字"
git config user.email "你的邮箱"
```

## 二、整理仓库内容（推荐）
1. 新建 `.gitignore`，排除本地应用配置与杂项（以 Obsidian 笔记库为例）：
   ```
   # Obsidian 本地配置（非笔记内容）
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
2. 若目录里存在与主体完全相同的镜像副本（如 `origin/` 与 `BSPstudy/` 内容一致），先确认是镜像再将其移出仓库：
   ```bash
   git rm -r --cached origin/     # 取消追踪，不删磁盘文件
   # 在 .gitignore 末尾追加：origin/
   ```
   > 校验两目录是否逐文件一致（避免误删独有文件）：
   > 分别 `cd` 进两个目录，`find . -type f -exec md5sum {} \; | sort` 生成清单后 `diff`，无差异即为镜像。
   > 确认无误后，可把重复目录移入回收站彻底清理（非必须）。

## 三、暂存与首次提交
```bash
git add -A
git commit -m "Initial commit: ..."
```

## 四、添加远程仓库
```bash
git remote add origin https://github.com/<用户名>/<仓库名>.git
git branch -M main
```
> 若初始化时已用 `git init -b main`，`git branch -M main` 冗余但无害。

## 五、Git 凭证说明（关键）
GitHub 自 2021-08 起**不再支持用账号登录密码**做 HTTPS 推送，必须使用以下之一：
- **Personal Access Token (PAT)**：生成带 `repo` 权限的 token，推送时用户名填 GitHub 用户名、密码处粘贴 token。
- **SSH 密钥（推荐，一劳永逸）**：见下一节。

若 `git push` 卡在 `Username for 'https://github.com':` 并报 `Password authentication is not supported for Git operations`，说明在用登录密码，必须换成 PAT 或 SSH。

## 六、配置 SSH 密钥并推送（推荐方案）
1. 生成本地密钥（无 passphrase 最省事，也可设密码更安全）：
   ```bash
   ssh-keygen -t ed25519 -C "你的邮箱"
   # 一路回车用默认路径；若提示已存在，选 no 复用现有密钥
   ```
2. 复制公钥内容：
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   复制输出的整行（`ssh-ed25519 AAAA... 邮箱`）。
3. 到 GitHub → **Settings → SSH and GPG keys → New SSH key**：
   - Title：自取，如 `My-Laptop`
   - Key type：保持 `Authentication Key`
   - Key：粘贴第 2 步的公钥
   - 点 **Add SSH key**
4. 把 remote 改为 SSH 地址并推送：
   ```bash
   git remote set-url origin git@github.com:<用户名>/<仓库名>.git
   git push -u origin main
   ```
   首次连接会问 `Are you sure you want to continue connecting?`，输入 `yes`。之后免密。

> 关于页面上的 “Vigilant mode”：是 GPG 提交签名验证开关，与能否用 SSH 推送无关，无需理会。

## 七、验证
```bash
git ls-remote origin     # 看远端 main 的 SHA 是否等于本地 HEAD
ssh -T git@github.com    # 验证 SSH 连通，看到 Hi <用户名>! 即成功
```
推送成功后，本地 `git log` 应与 GitHub 仓库页面一致。

## 八、常见问题
- `fatal: Authentication failed`：凭证错误或用的是密码 → 改用 PAT 或 SSH。
- `repository not found`：仓库不存在或无 push 权限 → 先去 GitHub 建好同名空仓库。
- Git Credential Manager 退化成终端账号密码提示：可强制走浏览器登录
  ```bash
  git config --global credential.https://github.com.authModes "oauth"
  git push -u origin main
  ```
