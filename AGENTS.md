# 给 AI 的项目说明

> 用途：给 AI 编码助手。这里是事实与约束,不含介绍性文字。改动本仓库前先读这份。
> README.md 与 docs/getting-started.md 里被引用的事实以本文件为准,它们只链接不复述。

## 一句话

一个中文单页个人主页,整页就是一个 `index.html`,由 GitHub Pages 从 `main` 分支根目录
直接发布,没有构建、没有依赖、没有后端、没有测试。

## 当前真实状态

| 项 | 值 | 复核命令 |
|---|---|---|
| 页面文件 | `index.html`,2105 行 | `wc -l index.html` |
| 仓库内与线上是否同版本 | 一致(均 57686 字节) | `curl -s https://luz7818.github.io/ \| wc -c` |
| 图片资源 | 13 个文件全部被引用,0 个多余 | `grep -oE 'assets/[^")]+' index.html \| sort -u` 与 `ls assets` 对差 |
| 页内锚点 | 全页 11 处 `href="#…"`,指向 8 个不同目标,8 个都有对应 `id` | 见下方「锚点核对」 |
| 样式 | 1 个内联 `<style>`,`:root` 下 14 个 CSS 自定义属性 | `grep -oE '^[[:space:]]+--[a-z-]+:' index.html \| sort -u \| wc -l` |
| 脚本 | 1 个内联 `<script>`,只做锚点平滑滚动 | `grep -c "<script" index.html` |
| 远程资源 | 0 个(不引 CDN、不加载远程字体) | `grep -E '<(script\|link)[^>]*(src\|href)="https?:' index.html`(应无输出) |
| 测试 / CI / lint | 都没有;门禁就是下面两条核对 | — |

资源核对(在仓库根执行,`assets/README.md` 是目录说明页、不上页面,所以要滤掉):

```bash
diff <(grep -oE 'assets/[^")]+' index.html | sort -u) \
     <(ls assets | sed 's|^|assets/|' | grep -v '^assets/README.md$' | sort)
```

输出为空即「页面引用到的」与「磁盘上的」完全一致。锚点核对(一条命令,输出为空即全部指得到):

```bash
comm -23 <(grep -oE 'href="#[a-zA-Z0-9_-]+"' index.html | sed 's/href="#//;s/"//' | sort -u) \
         <(grep -oE 'id="[a-zA-Z0-9_-]+"'      index.html | sed 's/id="//;s/"//'      | sort -u)
```

不要直接 `diff` 那两条 grep 的原始输出——它们一个带 `href="#` 前缀一个不带,
永远不相等;上面的 `sed` 就是为了让两边口径一致。

## 仓库地图

| 路径 | 职责 |
|---|---|
| `index.html` | 页面全部内容:结构、样式、脚本、文案都在这一份文件里 |
| `assets/` | 13 个图片资源,逐个说明见 `assets/README.md` |
| `docs/getting-started.md` | 给人跟做的上手手册 |

## 关键约定(违反会出问题的才列)

1. **保持零依赖单文件**。不要引入 npm/构建工具/CDN 资源/远程字体 —— 这个页面的
   一个目的就是双击本地文件也能看。违反后果:离线打开白屏或字体错位。
2. **锚点与 `id` 必须成对**。主导航 7 处 `href="#…"`(品牌 `#top` + 6 个栏目),正文另有
   4 处指向 `#publications`/`#honors`/`#experience`。新增小节必须同时给 `section` 加
   `id` 并在导航登记。漏了不会报错,只会点了没反应。
3. **平滑滚动要尊重系统减弱动效偏好**。脚本里用 `matchMedia("(prefers-reduced-motion: reduce)")`
   判断后才决定用不用 `behavior:"smooth"`。改成无脑 smooth 会让这部分用户体验变差。
4. **不要在本仓建 `marx-cloud/` 等子目录**。用户站占根路径,`/marx-cloud/` 由
   `marx-cloud` 那个仓的 Pages 提供,本仓同名目录会与它冲突。
5. **提交身份是本仓仓库级覆盖成学校邮箱**(`git config user.email` = 213230392@seu.edu.cn),
   与其余仓库用的 noreply 身份不同,是有意保留的,不要"统一"掉。
6. **行尾**:`core.autocrlf=true` 且仓库内没有 `.gitattributes`。当前 `index.html` 工作区与
   仓库内都是 57686 字节(LF,无 CR)。若某次操作后 `git diff` 显示整文件改动,先怀疑是
   LF→CRLF 翻转,不要把它当内容改动提交。

## 改动后的验证

| 动了什么 | 必须做 |
|---|---|
| 文案/样式/结构 | `python -m http.server 8000` 打开看一眼;移动端宽度(≤640px)也看一眼 |
| 新增或替换图片 | 跑「资源核对」命令,输出为空 |
| 新增小节或改导航 | 跑「锚点核对」命令,输出为空 |
| 任何改动 | `git push` 后用 `curl -s https://luz7818.github.io/ \| wc -c` 确认线上字节数已变 |

## 已知坑

- 字体是系统栈(Inter → Segoe UI → 微软雅黑),页面不分发字体文件。没装 Inter 的机器上
  排版宽度与设计稿不同,这不是 bug,别去"修"。
- `assets/` 里 12 个文件名是中文,命令行处理要留意转义;浏览器里浏览器会自动百分号编码。
- Pages 生效通常有 1–2 分钟延迟,浏览器还有缓存。核对线上请用 `curl`,不要用刷新验证。
- 首页里 `https://luzzz.me` 这个外链指向另一个仓的站点。它在本机当前网络下解析不稳,
  那是网络与域名解析的问题,不是本页的问题。
- `六朝松.svg` 161 KB 是页面最大的一张图,但它是可见背景水印,不是可删的重复素材。

## 不要做的事

- 不要为了"看起来正规"给它加 CI、打包、格式化配置。
- 不要新增住址、电话、身份证号一类更敏感的字段。
- 不要因为两个「辅助」/两个「剪影」变体看着重复就删 —— 它们分别被不同小节引用。
- 不要把这里的内容大段复制进 `luzzz.me`(那是另一个独立站点,数据各自维护)。
