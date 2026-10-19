# 可以成为我的恋人吗？

一个纯静态、单文件的表白互动页。发一个链接给对方，剩下的交给「不要」按钮。

> 在线体验：<https://daniu.dpdns.org/>

## 玩法

- 打开页面，看到「可以成为我的恋人吗？」
- 点 **不要**：按钮会躲、会变文案、表情会从震惊 → 思考 → 生气 → 哭
- 点 **可以**：进入表白成功页，爱心爆发 + 拥抱表情

### 带上对方的名字

在链接后面加 `?name=`，名字会自动接在问题后面：

```
https://daniu.dpdns.org/?name=小美
```

> 名字按「字符」截断到 20 个，emoji 不会被切成乱码；注入使用 `textContent`，不存在 XSS。

## 特性

| 能力 | 说明 |
| --- | --- |
| 零依赖 | 没有框架、没有 CDN、没有外部字体，全部内联 |
| 响应式 | `clamp()` + `100dvh`，手机 / 平板 / 桌面都居中不抖 |
| 图片优化 | WebP 优先、PNG 回退，183 KB → 48 KB（-74%） |
| 分享卡片 | Open Graph / Twitter Card，微信、QQ、Twitter 有预览图 |
| 无障碍 | `aria-live`、`focus-visible`、尊重 `prefers-reduced-motion` |
| 懒加载音频 | 首次点击才请求 `Hello.mp3`，首屏不背 70 KB |
| 结果页操作 | 「分享给她」（Web Share API，降级为复制链接）、「再玩一次」 |

## 本地预览

任选其一，然后打开 <http://localhost:8000>：

```bash
python3 -m http.server 8000
# 或
npx serve .
```

## 目录结构

```
.
├── index.html          # 主页面（内联 CSS + JS）
├── 404.html            # 自定义 404
├── CNAME               # 自定义域名：daniu.dpdns.org
├── images/
│   ├── *.webp          # 优先加载
│   ├── *.png           # 旧浏览器回退
│   ├── Hello.mp3       # 点击音效
│   ├── og-cover.png    # 分享封面 1200×630
│   └── favicon.svg     # 站点图标
├── robots.txt
└── sitemap.xml
```

## 部署

仓库就是 GitHub Pages 的站点源：推送到 `main` 后自动构建（`Settings → Pages` 已指向 `main` / 根目录）。

```bash
git add .
git commit -m "feat: 优化表白页"
git push origin main
```

## 自定义

- **换文案**：`index.html` 里的 `noTexts`、`<h1>`、成功页文案
- **换表情**：替换 `images/` 下同名文件（保持 240×240，透明 PNG），WebP 用同样的文件名
- **换配色**：改 `:root` 里的 `--pink-*`、`--ink`、`--blue`

## License

[MIT](./LICENSE)
