# 华享未来官网 · 山河长卷

华享未来（HUAXIANG FUTURE）官方网站的静态站点源码。设计方向为「山河长卷」——一座会呼吸的县域数字文化馆，既是 APP 的官网，也是品牌世界观的第一入口。C 端下载与 B 端政企合作兼顾。

## 在线访问

- **正式站点（GitHub Pages）**：https://j18287061781-sys.github.io/huaxiang_future_web/
- 临时测试环境（CloudStudio）：https://c8cc9afb72c04a69961dec4756e6b7c9.bj9.agentos-app.net

## 技术栈

- 纯静态单文件：`index.html`（HTML + CSS + JS 全内联，无构建步骤、无依赖）
- 中文排版：思源宋体（Noto Serif SC）标题 + 思源黑体（Noto Sans SC）正文，带系统兜底
- 动效：原生 IntersectionObserver 滚动渐显、数字计数动画、移动端汉堡菜单、咨询表单弹窗
- 响应式：980px / 560px 双断点

## 目录结构

```
huaxiang_future_web/
├── index.html     # 整站源码（单文件）
└── README.md
```

## 页面结构（共 8 段）

1. 页头（粘性导航 + 下载 APP / 合作咨询）
2. Hero 首屏 · 山河展卷（SVG 手绘远山、江呦呦数字人、百县印章）
3. 文化伙伴矩阵（9 位数字人 IP）
4. 精选县域橱窗（屏山 / 沙湾 / 射洪 / 兴文，左右交替）
5. 好物 · 研学（屏山风物 + 兴文石海研学营）
6. 百县火炬计划（深色 B 端段，数据 9 / 6 / 1866）
7. 下载 APP（双端入口）
8. 页脚（品牌区 + 导航 + 备案）

## 设计与内容源

- 设计稿（Ardot 在线）：fileId `712273310450760`
- 视觉规范：米白 `#F4EDDD`、墨黑 `#241B12`、朱砂红 `#9B4A32`、竹青 `#526B52`、金 `#AE8B45`
- 内容清单（Office）：`华享未来官网-山河长卷-内容清单.docx`

## 本地预览

直接用浏览器打开 `index.html` 即可；或：

```bash
python3 -m http.server 3000
# 访问 http://localhost:3000
```

## 部署（GitHub Pages）

源码推送到 `main` 分支根目录，已开启 GitHub Pages（`Settings → Pages → branch: main, path: /`），自动生成上方正式链接。

## 待办 / 后续

- [ ] 替换 AI 占位图为真实摄影 / 插画（数字人、县域山水、好物）
- [ ] 咨询表单对接真实后端或邮件
- [x] 绑定自定义域名（mvp.hxfz-group.com → 已在 GitHub Pages 设置 cname，待 DNS 生效）
- [ ] SEO / 分享卡片（OG 图、favicon）
- [ ] 埋点统计

## 自定义域名配置（mvp.hxfz-group.com）

已在 GitHub Pages 设置自定义域名 `mvp.hxfz-group.com`（仓库 Settings → Pages → Custom domain）。
要使域名真正可访问，需在你的域名 DNS 服务商（阿里云 / 腾讯云 DNSPod / Cloudflare 等）添加以下记录：

| 记录类型 | 主机记录 | 记录值（目标） | TTL |
|----------|----------|----------------|-----|
| CNAME    | mvp      | j18287061781-sys.github.io | 600（或默认） |

添加后 GitHub 会自动检测并签发 SSL 证书（强制 HTTPS）。DNS 全球生效通常需 5 分钟～24 小时，
生效前可继续用默认地址：https://j18287061781-sys.github.io/huaxiang_future_web/

> ⚠️ 冲突提示：`mvp.hxfz-group.com` 此前计划用于华享未来 MVP 后端。若它当前已服务于其他服务，
> 复用会使原服务失效。如需保留 MVP，请改用新子域名（如 `web.hxfz-group.com`、`www.hxfz-group.com`），
> 并在 GitHub Pages 改设对应 cname 后重新添加 DNS 记录。
