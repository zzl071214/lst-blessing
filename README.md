# LST · 藏在弹窗里的祝福

![HTML](https://img.shields.io/badge/HTML-单文件-e91e63)
![无依赖](https://img.shields.io/badge/依赖-零-ff69b4)
![License](https://img.shields.io/badge/license-MIT-brightgreen)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-在线-2ea44f)

一个纯前端的互动祝福页：点击 **「打开」**，300 份祝福气泡会一个接一个从屏幕各处弹出来；

点开其中那份特别的祝福（`平安喜乐`）右上角的 **×**，屏幕上所有气泡会缓缓移动、**拼成一颗心**；

心形停留片刻后，全屏出现最后的祝福 —— **天天开心**。

> 整个项目只有一个 HTML 文件，没有构建、没有依赖、没有后端。双击就能看，丢到任意静态托管上就能给所有人访问。

## 预览

| 300 份祝福弹出 | 拼成一颗心 | 最终祝福 |
| --- | --- | --- |
| ![祝福弹出](screenshots/1-popups.png) | ![心形](screenshots/2-heart.png) | ![最终祝福](screenshots/3-final.png) |

---

## 在线体验

- 演示地址：<https://zzl071214.github.io/lst-blessing/>

## 本地预览

直接双击 `index.html` 即可。

想用「服务器」的方式预览（推荐，行为和线上完全一致）：

```bash
# Python 3
python -m http.server 8080

# Node.js
npx serve .
```

然后打开 <http://localhost:8080>。

## 部署到 GitHub Pages

1. 新建仓库并推送本目录（仓库名例如 `lst-blessing`）：

   ```bash
   git init
   git add .
   git commit -m "feat: LST 祝福弹窗互动页面"
   git branch -M main
   git remote add origin https://github.com/<你的用户名>/lst-blessing.git
   git push -u origin main
   ```

2. 打开仓库 **Settings → Pages**；
3. **Source** 选 `Deploy from a branch`，**Branch** 选 `main` / `root`，保存；
4. 等 1 分钟左右，访问 `https://<你的用户名>.github.io/lst-blessing/`。

仓库里已经放了 `.nojekyll`，避免 GitHub Pages 的 Jekyll 处理干扰静态资源。

### 其他托管方式

因为只有一个静态文件，Vercel / Netlify / Cloudflare Pages / 对象存储都能直接部署，把仓库连上去、构建命令留空、输出目录填 `/` 即可。

## 自定义

打开 `index.html`，顶部 `<script>` 里的 `CONFIG` 是最常改的地方：

| 配置项 | 说明 | 默认值 |
| --- | --- | --- |
| `totalPopups` | 祝福气泡总数（含那 1 份特殊祝福） | `300` |
| `popupInterval` | 每个气泡出现的间隔（毫秒） | `70` |
| `specialBlessing` | 特殊祝福文案，点它的 × 触发心形 | `"平安喜乐"` |
| `finalBlessing` | 全屏最终祝福文案 | `"天天开心"` |
| `finalTip` | 最终祝福顶部的小标题 | `"💌 平安喜乐"` |
| `heartHoldMs` | 心形排好后停留多久再显示最终祝福（毫秒） | `12000` |

其他常见的改动：

- **换祝福语**：编辑 `normalBlessings` 数组，随便加多少条，会随机抽取。
- **换气泡颜色**：编辑 `popupBgColors` 数组。
- **换顶部日期和署名**：直接改 `<h1 class="main-title">` 和 `<p class="signature">`。
- **换背景音乐**：找到 `<audio id="bgMusic">`，把 `<source>` 的 `src` 换成你自己的直链或本地文件名（例如把 `music.mp3` 放进仓库后写 `src="music.mp3"`）。可以保留多个 `<source>` 作为回退。

> 音乐说明：浏览器会拦截「自动播放」，所以页面右上角有一个 🎵 按钮，点它（或点「打开」）才会开始播放。若外链音乐失效，页面其他功能不受影响。

## 兼容性与无障碍

- 移动端自适应：心形缩放跟随视口，文字过长自动放宽气泡，不会溢出。
- 支持系统「减弱动态效果」（`prefers-reduced-motion`）：会自动缩短动画。
- 关闭按钮带 `aria-label`，主按钮有可见焦点样式。
- 已在 Chromium 系（Edge / Chrome）与移动端浏览器实测。

## 目录结构

```
.
├── index.html      # 全部内容：结构、样式、逻辑
├── jumping.html    # 备用入口（在 iframe 里打开时重写父级地址）
├── .nojekyll       # 让 GitHub Pages 跳过 Jekyll
├── LICENSE         # MIT
└── README.md
```

## License

[MIT](LICENSE) © 2026 zzl
