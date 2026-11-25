# 我的小金库 🐷

一个只属于你自己的攒钱小账本：汇总所有银行卡余额，盯住攒钱目标，随时看进度。

- 纯静态：一个 HTML 文件 + 几张图，没有后端、没有账号、没有数据库
- 数据在本机浏览器（localStorage），打开就是上次的样子
- 可选「云同步」：数据加密后存进你自己的 GitHub 仓库，手机 / 电脑共用
- 可加到手机桌面（PWA），像 App 一样打开
- 余额自动每天记一笔，走势图看攒钱曲线；100% 达成撒彩纸 🎉

## 本地打开

双击 `index.html` 就行。或者：

```bash
python3 -m http.server 8000
# 浏览器打开 http://127.0.0.1:8000
```

> 云同步需要 https 页面（本地 `127.0.0.1` / `localhost` 也算安全环境）。

## 部署到 GitHub Pages

1. 在 GitHub 新建一个 **public** 仓库，例如 `xiaojinku`（不要勾选任何初始化文件）。
2. 在仓库页面的 **Settings → Pages**，Source 选 `Deploy from a branch`，分支 `main`、目录 `/ (root)`，保存。
3. 在本地这个目录里执行：

```bash
git remote add origin https://github.com/<你的用户名>/xiaojinku.git
git push -u origin main
```

4. 等 1～2 分钟，访问 `https://<你的用户名>.github.io/xiaojinku/`。

## 开启云同步（手机 + 电脑）

1. 在 GitHub 生成一个 fine-grained PAT：**Settings → Developer settings → Personal access tokens → Fine-grained tokens**。
   - Repository access：Only select repositories → 选 `xiaojinku`
   - Permissions → Contents：`Read and write`
2. 打开网页，点右上角 ☁️：
   - 仓库：`你的用户名/xiaojinku`
   - 访问令牌：刚生成的 PAT
   - 同步密码：自己定（至少 6 位，两台设备必须一样）
3. 手机打开同一个网址，☁️ 里填同样的三项。若提示云端已有数据，选「用云端」。

数据文件 `sync/data.json` 会提交在仓库里，但内容是用同步密码 AES-256-GCM 加密的，明文只在你的设备上。

## 数据说明

- 备份：底部「导出备份」下载 JSON；「导入备份」恢复。
- 清空数据会同时断开云同步，之前的数据仍留在 GitHub 仓库里（加密）。
- 手机和电脑各自有一份本地数据，靠云同步合并；同一时间两边都改时，以最后修改的为准。
