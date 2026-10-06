# assets/ —— 页面用的图片

> 用途：说明这 13 个文件各用在什么地方、哪些是背景纹样、删掉会怎样。

页面所有本地图片都在这里，共 13 个文件、593,956 字节（约 580 KB；本文件与下表里的「KB」
都是 1024 进制，复核：`find assets -type f ! -name 'README.md' -printf '%s\n' | awk '{s+=$1}END{print s}'`）。
引用方式有两种：`<img src="…">`
出现在页面内容里，CSS `url(…)` 出现在小节背景中。核对当前引用关系的命令写在
`docs/TESTING.md` 的「改动后的验证」里。

## 文件清单

| 文件 | 大小 | 用在哪 | 引用方式 |
|---|---|---|---|
| `portrait.jpg` | 10 KB | hero 区的个人照片 | `<img>` |
| `东南大学彩色校标.svg` | 89 KB | 页头/联系区的校标 | `<img>` |
| `东南大学彩色中英文字校标组合-左右.svg` | 137 KB | 联系小节的校名组合标 | `<img>` |
| `东南大学标准字-横排.svg` | 27 KB | 东南大学标准字 | `<img>` |
| `校训横排.svg` | 21 KB | 校训横排字 | `<img>` |
| `大礼堂-独立.svg` | 5 KB | 大礼堂线稿（独立成图） | `<img>` |
| `大礼堂-连续.svg` | 14 KB | 大礼堂线稿（可平铺） | `<img>` |
| `东南大学黑白校标.svg` | 76 KB | 小节背景水印 | CSS `url()` |
| `六朝松.svg` | 161 KB | 小节背景水印（页面里最大的一个文件） | CSS `url()` |
| `大礼堂-剪影-横向.svg` | 3 KB | 横向背景剪影 | CSS `url()` |
| `大礼堂-剪影-纵向.svg` | 3 KB | 纵向背景剪影 | CSS `url()` |
| `大礼堂-辅助-独立.svg` | 9 KB | 背景纹样变体 | CSS `url()` |
| `大礼堂-辅助-连续.svg` | 24 KB | 背景纹样变体（连续） | CSS `url()` |

13 个文件当前全部被 `index.html` 引用，没有多余文件。

## 命名与格式

- 文件名是中文。这在 `index.html` 里直接写没问题（浏览器会自动做百分号编码），
  但用命令行或某些脚本处理这些路径时要留意转义。
- 除照片是 `.jpg`，其余全是 `.svg`：线条类图形用 SVG 才能在深色/浅色背景上都不糊。

## 换图或加图

1. 把文件放进 `assets/`，然后加进 `index.html` 的引用。
2. 只放进来不引用，就会变成死文件 —— 本仓库没有任何构建流程会替你清理，
   核对命令见下面的「改这里之后要跑」。
3. 背景水印类图片建议控制在 100 KB 以内，整页目前是 580 KB 图片 + 56 KB HTML
   （复核：上面「共 13 个文件」那条 find 命令，以及 `wc -c < index.html` 得 57686）。

## 和谁打交道

- **上游**：没有生成脚本，也没有下载来源。13 个图片文件全是手工挑好放进仓库的静态素材，
  一次性随首个提交 `6d90a2f` 进仓，之后再没增删过。
- **下游**：只有 `index.html` 一份文件消费它们，两条路径：内容图写成 `<img src="assets/…">`
  进页面结构，背景图写成内联 `<style>` 里的 `url("assets/…")` 挂在 `<section>` 的 class 上。

计数与来源复核（在仓库根）：`ls assets | grep -v README.md | wc -l` 给 13；
`ls assets | grep -v README.md | grep -v jpg` 列出的 12 个就是全部的中文文件名，唯一的 ASCII
名是 `portrait.jpg` —— 所以命令行里处理这些路径要留意转义。
`git log --oneline --diff-filter=A -- assets` 只有两条（另一条 `2d6a95a` 加的是本说明页），
`git log --oneline --diff-filter=D -- assets` 无输出。

### 下游明细：哪一节用哪张

| 页面位置 | 文件 | 方式 |
|---|---|---|
| 左侧信息栏 `<aside class="profile-sidebar">` | `portrait.jpg`、`东南大学彩色中英文字校标组合-左右.svg`、`校训横排.svg`、`东南大学彩色校标.svg`、`六朝松.svg` | `<img>` |
| 顶部导航 `.brand` 与 `<section class="hero">` | `东南大学彩色校标.svg`、`大礼堂-剪影-横向.svg`、`大礼堂-剪影-纵向.svg`、`东南大学黑白校标.svg` | `<img>` |
| hero 与 `#about` 之间的通栏 `.campus-band`，以及 `#about` 小节内部 | `大礼堂-连续.svg`、`东南大学彩色校标.svg`、`大礼堂-独立.svg` | `<img>` |
| `#contact` 小节与 `<footer>` | `东南大学彩色中英文字校标组合-左右.svg`、`东南大学标准字-横排.svg` | `<img>` |
| 各小节背景水印（CSS 伪元素 `::before` / `::after`） | `.campus-mark` → `东南大学黑白校标.svg`；`.campus-pattern` → `大礼堂-辅助-连续.svg`；`.pine-mark` 与 `.pine-mark-right` → `六朝松.svg`；`.hall-horizontal` → `大礼堂-剪影-横向.svg`；`.hall-vertical` → `大礼堂-剪影-纵向.svg`；`.contact-campus` → `大礼堂-辅助-独立.svg` | CSS `url()` |

水印挂在 class 上，所以一张图通常同时服务多个小节，换它等于一次改若干节的背景：
`.campus-pattern` 用在 `#research`、`#experience`、`#projects`、`#honors`、`#leadership` 五处；
`.campus-mark` 与 `.hall-horizontal` 用在 `#about` 和 `#publications`；`.pine-mark` 用在
`#research` 和 `#projects`，`.pine-mark-right` 用在 `#experience`、`#leadership`、`#contact`；
`.hall-vertical` 用在 `#honors` 与夹在它前面的「近期亮点」小节（那一个 `<section>` 没有 `id`）。
复核：`grep -n '<section class' index.html` 看 class 与 `id` 的配对，
`grep -n 'url("assets' index.html` 看每条背景规则挂在哪。

### 改这里之后要跑

本仓库没有构建、没有依赖、也没有测试，可执行的核对就是 `AGENTS.md`「当前状态」下面的
那两条（原文照抄，都在仓库根执行）。动过图片必跑第一条：

```bash
diff <(grep -oE 'assets/[^")]+' index.html | sort -u) \
     <(ls assets | sed 's|^|assets/|' | grep -v '^assets/README.md$' | sort)
```

`diff` 无输出即「页面引用到的」与「磁盘上的」完全一致。看不一致时读它的行就够：`<` 那侧多出来的
一行是引用了不存在的图（只表现为裂图或背景空白，不报错），`>` 那侧多出来的一行是没被引用的
死文件。第二条锚点核对在换图的同时动了小节或导航时才需要跑（这两件事常一起做）：

```bash
comm -23 <(grep -oE 'href="#[a-zA-Z0-9_-]+"' index.html | sed 's/href="#//;s/"//' | sort -u) \
         <(grep -oE 'id="[a-zA-Z0-9_-]+"'      index.html | sed 's/id="//;s/"//'      | sort -u)
```

同样是无输出为过。两条都空之后再 `python -m http.server 8000` 开浏览器看一眼，移动端宽度
（≤640px）也看一眼 —— 背景水印的位置与浓淡只有肉眼能判，命令只能证明引用关系没断。
哪些文件看着像重复其实各有归属，见下面的「别动」，这里不再列一遍。

## 别动

- `六朝松.svg`（161 KB）看着最大、最像可以压缩，但它同时是某个小节的可见水印，
  压缩或替换后需要目视复核背景层次，不要只按体积判断它多余。
- 两个「辅助」变体与两个「剪影」方向版本是不同小节各自在用的，不是重复文件。
