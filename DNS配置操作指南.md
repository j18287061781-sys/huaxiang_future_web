# 华享未来官网 · 自定义域名 DNS 配置操作指南

> 目标：把 `mvp.hxfz-group.com` 解析到 GitHub Pages（`j18287061781-sys.github.io`）
> 当前状态：GitHub 侧 CNAME 已配置完成（Pages 状态 built），仅缺域名注册商处的 DNS 记录。

---

## 一、域名在哪管理？（已查实）

`hxfz-group.com` 的 NS 记录为 `dns13.hichina.com` / `dns14.hichina.com`
→ **注册商 = 阿里云（万网），DNS 解析在「阿里云云解析 DNS」控制台。**

如果你实际用的是别的面板（如 DNSPod、Cloudflare、腾讯云），文末有对应写法。

---

## 二、必须添加的记录（网站能打开就靠它）

进入 **阿里云控制台 → 域名 → hxfz-group.com → 解析设置 → 添加记录**，填：

| 项目 | 填写值 |
|------|--------|
| 记录类型 | **CNAME** |
| 主机记录 | **mvp** |
| 记录值（指向） | **j18287061781-sys.github.io** （阿里云会自动补结尾的 `.`，直接粘这段即可） |
| TTL | 600（10 分钟）或保持默认 |
| 线路类型 | 默认 |

保存即可。**只需这一条网站就能访问**（http）。

---

## 三、可选的验证记录（推荐，防盗用）

GitHub Pages 允许别人把任意 GitHub 仓库指向你的域名。加一条 TXT 可锁定域名所有权：

1. 打开 GitHub 仓库 `j18287061781-sys/huaxiang_future_web` → **Settings → Pages**
2. 在 Custom domain 下方若显示 **Verify**，点开后会出现一个验证码（如 `1234abcd…`）
3. 回到阿里云，再「添加记录」：

| 项目 | 填写值 |
|------|--------|
| 记录类型 | **TXT** |
| 主机记录 | **_github-challenge-j18287061781-sys** |
| 记录值 | 上面 GitHub 给的验证码 |
| TTL | 默认 |

> 不加这条网站照样能开，只是域名理论上可被他人冒用，建议加上。

---

## 四、等解析生效（验证是否成功）

DNS 全球生效一般 **几分钟～最多 24 小时**（阿里云通常 10 分钟内）。用以下任一方式检查：

**方式 A：命令行（Windows PowerShell / 终端）**
```powershell
nslookup mvp.hxfz-group.com
```
预期看到：`mvp.hxfz-group.com` 是 `j18287061781-sys.github.io` 的别名，并最终解析到 GitHub 的 IP（如 185.199.108.x 等）。

**方式 B：在线工具**
打开 https://www.whatsmydns.net ，输入 `mvp.hxfz-group.com` 选 CNAME，看全球是否变绿。

---

## 五、DNS 生效后还要做一步（开 HTTPS）

GitHub 检测到 CNAME 后会**自动签发 SSL 证书**（约 15 分钟～数小时）：

1. 回到 GitHub 仓库 **Settings → Pages**
2. 看到「Your site is published at https://mvp.hxfz-group.com」且出现 **Enforce HTTPS** 勾选框时
3. ✅ 勾选 **Enforce HTTPS**（强制 https，避免浏览器报不安全）

至此，官网正式以 `https://mvp.hxfz-group.com` 对外访问。

---

## 六、其他注册商写法对照

**腾讯云 DNSPod / 腾讯云解析**
- 记录类型 CNAME，主机记录 `mvp`，记录值 `j18287061781-sys.github.io.`，TTL 600

**Cloudflare**
- Type CNAME，Name `mvp`，Target `j18287061781-sys.github.io`，Proxy 状态建议先设 **DNS only（灰云）** 再观察，TTL Auto

---

## 七、常见问题

- **加完还是打不开？** 多半是 DNS 还没生效（等 10~30 分钟再查）；或 CNAME 值拼错（应是 `j18287061781-sys.github.io`，不是仓库地址）。
- **打开是 http 不是 https？** 证书还在签发，等 GitHub 自动完成并在 Settings → Pages 勾 Enforce HTTPS。
- **GitHub 提示 "Domain does not resolve"？** 说明 CNAME 还没生效，确认阿里云记录已保存且主机记录是 `mvp`（不是 `@` 也不是 `www`）。

---

## 八、当前已完成的配置（备查）

- GitHub Pages 源分支：`main`，路径 `/`
- 仓库根目录 `CNAME` 文件内容：`mvp.hxfz-group.com`
- Pages 状态：`built`
- 待办：① 阿里云添加 CNAME（本指南第二步）② 生效后在 GitHub 勾 Enforce HTTPS
