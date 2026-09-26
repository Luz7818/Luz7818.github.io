# 个人主页 上手手册

> 用途：给要改这个主页的人。每一步给做法、给验证方式、给出错时怎么办。
> 页面只有一个文件，不需要装任何东西。

## 1. 需要准备什么

| 项目 | 要求 |
|---|---|
| 编辑器 | 任意文本编辑器 |
| 运行时 | 无。想本地起服务器才需要 Python（`python -m http.server`） |
| 网络 | 读代码不需要；发布需要能访问 github.com |
| 依赖安装 | 无，没有 `package.json`，也没有构建步骤 |

## 2. 本地看一遍

两种方式，任选一种：

- 直接用浏览器打开仓库里的 `index.html`（双击即可，页面完全离线自包含）。
- 起一个本地静态服务器，路径解析与线上一致：

```bash
python -m http.server 8000
```

浏览器访问 `http://127.0.0.1:8000/`。看到带头像的中文单页、上方一条导航条即为正常。

## 3. 页面结构在哪

| 想改的东西 | 文件里的位置 |
|---|---|
| 姓名、英文名、引导语 | `<section>` 之前的 hero 区，含 `id="hero-title"` |
| 导航条 | `<nav>` 里的 8 个 `href="#…"` |
| 八个内容小节 | `<section … id="about|research|experience|publications|projects|honors|leadership|contact">` |
| 配色与字号 | 顶部 `<style>` 里 `:root` 的 14 个 CSS 自定义属性 |
| 项目卡片 | `id="projects"` 小节内的 `<article class="project">`，当前 5 张 |
| 邮箱 | 搜 `mailto:`，出现在 hero 与 `#contact` 两处 |
| 页脚与校标 | `#contact` 小节与 `<footer>` |

改文案时不要动 `id` 属性：导航靠它跳转。

## 4. 四种常见改动

### 4.1 加一条论文

在 `id="publications"` 的小节里，复制一条同级的列表项，改标题、作者、 venue、
年份与链接。加完在浏览器里确认这一节的排版没有错位。

### 4.2 加一个项目卡

在 `id="projects"` 的 `<div class="project-grid">` 内，仿照已有卡片加一段：

```html
<article class="project">
  <h3><a href="https://github.com/Luz7818/<仓库名>" target="_blank" rel="noreferrer">项目名</a></h3>
  <p>一句话说明这个项目在做什么。</p>
  <div class="stack"><span>语言</span><span>方向</span></div>
  <div class="project-links"><a href="https://github.com/Luz7818/<仓库名>" target="_blank" rel="noreferrer">GitHub 仓库</a></div>
</article>
```

三点注意：文案里的数字要能复核（例如"807 条术语"要来自该项目自己的校验命令）；
`target="_blank"` 要配 `rel="noreferrer"`；卡片是 3 列栅格，5 张会留两个空格子，属正常。

### 4.3 换头像或加图片

1. 把文件放进 `assets/`（图片逐个说明见 `assets/README.md`）。
2. 在 `index.html` 里引用：内容图用 `<img src="assets/文件名">`，背景用 CSS
   `url("assets/文件名")`。
3. 核对没有多余文件、没有引用缺失：

```bash
grep -oE 'assets/[^")]+' index.html | sort -u
ls assets | sed 's|^|assets/|' | sort
```

两条命令的差集应为空（第二条会多出 `assets/README.md`，那是文档）。

### 4.4 改配色

`:root` 里的 14 个变量是全站唯一的颜色来源（`--ink` 正文、`--muted` 次要文字、
`--teal` / `--teal-dark` 强调、`--paper` / `--white` 底色、`--line` 描边、
`--shadow` 阴影、`--mist` / `--sand` 浅底、`--gold` / `--coral` / `--blue` / `--gray` 点缀）。
改一处即可全站生效；不要在小节里另写十六进制色值，那会让下次统一改色漏掉它。

## 5. 发布与确认生效

```bash
git add index.html assets
git commit -m "说明这次改了什么"
git push
```

`main` 分支推上去就发布，不需要手动触发任何东西。确认线上确实更新了：

```bash
curl -s https://luz7818.github.io/ | wc -c
```

数字与本地 `index.html` 的字节数一致即为已生效。通常需要 1–2 分钟；浏览器仍显示旧版
是缓存，用 `curl` 判断，不要靠反复刷新。

## 6. 常见故障

| 现象 | 原因 | 怎么办 |
|---|---|---|
| 图片位置空白或图标裂开 | 路径写错，或文件名与实际不一致（`assets/` 里 12 个文件名是中文，一个字符都不能差） | 跑第 4.3 节的两条核对命令 |
| 点导航没反应 | 新增小节时 `id` 与导航里的 `href="#…"` 没对上 | 跑第 3 节末与 `AGENTS.md` 的锚点核对 |
| 本地打开一切正常，线上少一块 | 只改了工作区没提交，或提交没推 | `git status` 与 `git log origin/main..HEAD` |
| 线上半天不更新 | Pages 部署延迟或浏览器缓存 | 用 `curl -s … \| wc -c` 判断，别刷浏览器 |
| `git diff` 显示整个文件都改了 | `core.autocrlf=true`，行尾被从 LF 转成 CRLF | 不要把这次整文件翻转提交，先确认内容是否真的变了 |
| 手机上排版挤成一团 | 断点是 1100 / 920 / 640 px，新加的宽元素没参与响应式 | 在浏览器开发者工具里把宽度拖到 640 以下复现 |
| 本机打不开 `https://luzzz.me` 这条外链 | 那个域名在当前网络下解析不稳 | 不是本页问题，换网络再试 |

## 7. 术语小词典

| 词 | 在这里指什么 |
|---|---|
| GitHub Pages 用户站 | 仓库名恰好等于 `<用户名>.github.io` 时，GitHub 直接把该仓库根目录当作站点根，无需配置 |
| 项目页 | 同一域名下的子路径（如 `/marx-cloud/`），由另一个仓库发布，与本仓无关 |
| 锚点 | `href="#projects"` 这种页内跳转，靠页面上 `id="projects"` 的元素定位 |
| CSS 自定义属性 | `--ink` 这类以两个连字符开头的变量，写在 `:root` 里全站共享，改一处全站跟着变 |
| 断点 | 媒体查询（`@media`）里设定的屏幕宽度阈值，本页有 3 个 |
| `prefers-reduced-motion` | 操作系统里"减弱动态效果"的开关，页面读到它就不做平滑滚动 |
| LF / CRLF | 两种换行符。Windows 上 `core.autocrlf=true` 会在检出时转换，容易造成整文件假改动 |
