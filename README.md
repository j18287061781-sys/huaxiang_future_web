# 华享未来官网 · 正式简洁版

华享未来（HUAXIANG FUTURE）官方网站的静态站点源码。设计方向为**正式、简洁、机构感**的官网风格（参考汇丰 HSBC 等国际机构站点）：红 + 白 + 灰主色、大量留白、无衬线字体、结构化卡片与导航。既是 APP 的官网，也是品牌与县域合作的第一入口。C 端下载与 B 端政企合作兼顾。

> 旧版「山河长卷」水墨风已弃用并移除。

## 在线访问

- **正式站点（GitHub Pages）**：https://j18287061781-sys.github.io/huaxiang_future_web/
- 自定义域名（待 DNS 生效）：https://mvp.hxfz-group.com

## 技术栈

- 纯静态单文件：`index.html`（HTML + CSS + JS 全内联，无构建步骤、无依赖）
- 中文排版：思源黑体（Noto Sans SC），标题与正文统一无衬线，带系统兜底
- 动效：原生 IntersectionObserver 滚动渐显、数字计数动画、移动端汉堡菜单、咨询表单弹窗
- 响应式：980px / 560px 双断点

## 目录结构

```
huaxiang_future_web/
├── index.html              # 整站源码（单文件）
├── README.md
├── CNAME                   # 自定义域名 mvp.hxfz-group.com
└── DNS配置操作指南.md        # 域名 DNS 添加步骤
```

## 页面结构（共 7 段）

1. 顶部工具条 + 粘性主导航（下载 APP / 县域登录）
2. Hero 首屏（标题 + 副文案 + 双 CTA + 数据条 9 / 6 / 1866 + 数字人矩阵预览卡）
3. 业务板块（4 张核心业务卡：AI 数字人 / 县域好物 / 研学旅行 / 百县计划）
4. 数字人矩阵（9 位数字人 IP）
5. 县域文化（6 个县域橱窗：屏山 / 沙湾 / 射洪 / 兴文 / 崇州 / 井研）
6. 合作伙伴（红色 B 端段，3 项合作权益 + 申请县域合作）
7. 下载 APP + 关于我们 + 页脚

## 设计令牌

- 主色（机构红）：`#C8102E`，深红 `#A50E26`
- 文字：墨黑 `#1A1A1A` / 正文 `#333` / 辅助灰 `#6B6B6B`
- 背景：白 `#FFFFFF` / 浅灰 `#F5F5F3`
- 分割线：`#E4E4E1`
- 字体：Noto Sans SC

## 本地预览

直接用浏览器打开 `index.html` 即可；或：

```bash
python3 -m http.server 3000
# 访问 http://localhost:3000
```

## 部署（GitHub Pages）

源码推送到 `main` 分支根目录，已开启 GitHub Pages（`Settings → Pages → branch: main, path: /`），自动生成上方正式链接。

## 待办 / 后续

- [ ] 替换数字人/县域头像占位（首字母色块）为真实肖像或品牌插画
- [ ] 咨询表单对接真实后端或邮件
- [ ] 自定义域名 DNS 生效 + 强制 HTTPS（见 DNS配置操作指南.md）
- [ ] SEO / 分享卡片（OG 图、favicon）
- [ ] 埋点统计

## 自定义域名配置（mvp.hxfz-group.com）

已在 GitHub Pages 设置自定义域名 `mvp.hxfz-group.com`（仓库 Settings → Pages → Custom domain）。
要使域名真正可访问，需在域名 DNS 服务商（阿里云 / 腾讯云 DNSPod / Cloudflare 等）添加 CNAME 记录：

| 记录类型 | 主机记录 | 记录值（目标） | TTL |
|----------|----------|----------------|-----|
| CNAME    | mvp      | j18287061781-sys.github.io | 600（或默认） |

添加后 GitHub 会自动检测并签发 SSL 证书（强制 HTTPS）。DNS 全球生效通常需 5 分钟～24 小时，
生效前可继续用默认地址：https://j18287061781-sys.github.io/huaxiang_future_web/

> ⚠️ 冲突提示：`mvp.hxfz-group.com` 此前计划用于华享未来 MVP 后端。若它当前已服务于其他服务，
> 复用会使原服务失效。如需保留 MVP，请改用新子域名（如 `web.hxfz-group.com`、`www.hxfz-group.com`），
> 并在 GitHub Pages 改设对应 cname 后重新添加 DNS 记录。
