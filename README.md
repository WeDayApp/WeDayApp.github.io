# WeDay 官网（wedayapp.cn）— 构建产物仓库

⚠️ **本仓库存放的是 Astro 站点的构建产物（`dist/`），不是源码。请勿手动编辑这里的 `index.html` / `assets/` 等文件 —— 下次部署会被整体覆盖。**

## 这是什么

- `https://wedayapp.cn` 的静态站点产物。
- 部署方式：WeDay 自家服务器 nginx 直挂本仓库目录当 document root（**不是 GitHub Pages**，仓库名仅历史遗留）。
- 服务器路径 `/root/WeDayApp.github.io`，nginx 容器内挂载到 `/var/www/wedayapp`（只读）。

## 源码在哪

源码是一个 Astro 项目，在 `weday-website/`（与本仓库同级的工作目录）。改动网站请改源码，然后重新构建产物覆盖本仓库。

## 部署流程

1. 本地构建源码：
   ```bash
   cd weday-website && ./node_modules/.bin/astro build
   ```
2. 用 `dist/` 产物替换本仓库内容（保留 `.git`），commit + push。
3. 服务器拉取并重启 nginx：
   ```bash
   cd /root/WeDayApp.github.io
   git pull origin main
   docker compose -f /root/UserSystemService/docker-compose.yml restart nginx
   ```
   注：服务器 git remote 必须是 SSH（HTTPS 会被墙）。

## 包含页面

- `/` 首页（看见 → 理解 → 靠近 → 记录 → 内测引导）
- `/privacy` 隐私政策
- `/terms` 用户服务协议
