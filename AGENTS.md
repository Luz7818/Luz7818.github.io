# AGENTS.md —— 项目协作与代码开发规范（唯一权威入口）

> 用途：给 AI 编码助手与所有开发者。这里是规范入口与索引：目标、原则、流程、模块规则、
> 维护矩阵、阅读清单都在这份文件里。细则一律链接到对应文件，冲突时以细则文件为准并回改本文件。
> 被别的文档引用的事实（数字、命令、路径）以本文件的「当前状态」为准，其他文档只链接不复述。

## 项目目标

- 定位：中文单页个人主页，整页就是一个 `index.html`，由 GitHub Pages 从 `main` 分支根目录
  直接发布，没有构建、没有依赖、没有后端。
- 核心功能：8 个小节的静态展示（简介、科研、经历、论文、开源项目、荣誉、学生工作、联系）。
- 技术栈：纯 HTML/CSS/JS 单文件，零依赖零构建（复核：`grep -c "<script" index.html`）。
- 详情：[README.md](README.md)、[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)

## 开发原则

1. 正确性优先。
2. 可维护性优先。
3. 代码简洁、项目简洁。
4. 小步迭代。
5. 单模块开发。
6. 每个改动必须有明确设计与验收标准。
7. 禁止一次生成整个项目。
8. 禁止跳步开发。

执行口径：先想后写（假设与歧义先挑明）；最简优先（不加没要求的功能与抽象——对本仓尤其意味着
不加构建工具与 CI）；外科手术式改动（不动无关代码，每行改动可追溯到需求）；目标驱动（先有可
验证判据再动手，宣称完成前先跑通 [docs/TESTING.md](docs/TESTING.md) 的门禁）。

## 开发流程

**分析 → 设计 → 实现 → 测试 → 文档更新 → Git提交 → 等待确认**。不得跳过任何阶段。

| 阶段 | 产出物 | 放行标准 |
|---|---|---|
| 分析 | 影响面清单（动 `index.html` 哪一小节、是否涉及图片/锚点） | 影响面说全 |
| 设计 | 改动说明（改哪里、预期效果） | 验收标准已定义 |
| 实现 | `index.html` / `assets/` 改动 | 只含设计内改动 |
| 测试 | 门禁结果 | [docs/TESTING.md](docs/TESTING.md) 全过 |
| 文档更新 | 受影响文档 diff | 维护矩阵逐项过完 |
| Git提交 | 提交 | 符合 [docs/GIT.md](docs/GIT.md)，一批一提交 |
| 等待确认 | —— | 等人确认后推送 |

## 模块开发规则

- 一个智能体一次只开发一个模块；模块完成后才能进入下一模块。
- 如需同时开发，使用多个子智能体，每个子智能体同样一次只开发一个模块。

模块完成标准（全部满足才算完成）：

1. 功能完成：达到 [TODO.md](TODO.md) 中该任务的验收标准。
2. 测试通过：符合 [docs/TESTING.md](docs/TESTING.md)。
3. 最简原则：不引入本仓不需要的依赖与设施（本仓连测试框架都是有意不用的）。
4. [TODO.md](TODO.md) 更新：勾选完成项、明确下一项。
5. [HISTORY.md](HISTORY.md) 追加变更记录。
6. 受影响的 docs 更新（按需）。
7. [README.md](README.md) 更新（如有面向访客的变化）。
8. Commit message 符合 [docs/GIT.md](docs/GIT.md)。

## 文档维护规则

| 事件 | 需更新 |
|---|---|
| 模块完成 | `TODO.md`、`HISTORY.md`、受影响 docs |
| 结构性变化（新增小节、改导航、改发布链路） | `docs/ARCHITECTURE.md` + `HISTORY.md` 记录缘由 |
| 文案/图片/配色等访客可见变化 | `README.md` / 对应 docs / `assets/README.md` |
| 增删一级目录 | 仓根 `目录说明.md` + 本文件 |
| 数字（行数/字节数/图片数/锚点数）变化 | 本文件「当前状态」 |
| 新对话/新任务开始 | 按下方阅读清单阅读 |

## 开发前阅读清单

每个新对话/新任务，按顺序阅读：

1. 本文件（`AGENTS.md`）
2. [TODO.md](TODO.md)
3. [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)
4. [docs/GET-START.md](docs/GET-START.md)
5. [HISTORY.md](HISTORY.md)
6. 与任务相关的 [docs/CODE-STYLE.md](docs/CODE-STYLE.md)、[docs/TESTING.md](docs/TESTING.md)、[docs/GIT.md](docs/GIT.md)

阅读完成后**不要写代码**：先做架构评审，输出——项目理解 / 核心模块 / 模块依赖关系 / 潜在风险 /
建议优化项 / 推荐开发顺序 / 是否发现架构问题——然后等待确认。

## Git 索引

- Git 规范：[docs/GIT.md](docs/GIT.md)（提交身份、行尾陷阱、message 风格、一批一提交）

## 当前状态

| 项 | 值 | 复核命令 |
|---|---|---|
| 页面文件 | `index.html`，2112 行 | `wc -l index.html` |
| 仓库内与线上是否同版本 | 本地 58389 字节；线上为旧版，推送后用复核命令核对一致 | `curl -s https://luz7818.github.io/ \| wc -c` |
| 图片资源 | 13 个文件全部被引用，0 个多余 | `grep -oE 'assets/[^")]+' index.html \| sort -u` 与 `ls assets` 对差 |
| 页内锚点 | 全页 11 处 `href="#…"`，指向 8 个不同目标，8 个都有对应 `id` | 见下方「锚点核对」 |
| 样式 | 1 个内联 `<style>`，`:root` 下 14 个 CSS 自定义属性 | `grep -oE '^[[:space:]]+--[a-z-]+:' index.html \| sort -u \| wc -l` |
| 脚本 | 1 个内联 `<script>`，只做锚点平滑滚动 | `grep -c "<script" index.html` |
| 远程资源 | 0 个（不引 CDN、不加载远程字体；`rel="canonical"` 是声明，页面不加载它） | `grep -E '<(script\|link)[^>]*(src\|href)="https?:' index.html \| grep -v 'rel="canonical"'`（应无输出） |
| 分享元数据 | og: 5 项 + `twitter:card` + `rel="canonical"`，`og:image` 为 Pages 根路径绝对 URL | `grep -c 'property="og:' index.html`（= 5） |
| 图片懒加载 | 首屏之外的 5 处 `<img>` 带 `loading="lazy"`，首屏 9 处保持即时加载 | `grep -o '<img[^>]*loading="lazy"' index.html \| wc -l`（= 5） |
| 测试 / CI / lint | 无测试、无 lint；CI 只有跑两条核对的最小工作流（`.github/workflows/check.yml`），门禁就是它加下面两条核对 + [docs/TESTING.md](docs/TESTING.md) | — |

资源核对（在仓库根执行，`assets/README.md` 是目录说明页、不上页面，所以要滤掉）：

```bash
diff <(grep -oE 'assets/[^")]+' index.html | sort -u) \
     <(ls assets | sed 's|^|assets/|' | grep -v '^assets/README.md$' | sort)
```

输出为空即「页面引用到的」与「磁盘上的」完全一致。锚点核对（一条命令，输出为空即全部指得到）：

```bash
comm -23 <(grep -oE 'href="#[a-zA-Z0-9_-]+"' index.html | sed 's/href="#//;s/"//' | sort -u) \
         <(grep -oE 'id="[a-zA-Z0-9_-]+"'      index.html | sed 's/id="//;s/"//'      | sort -u)
```

不要直接 `diff` 那两条 grep 的原始输出——它们一个带 `href="#` 前缀一个不带，永远不相等；
上面的 `sed` 就是为了让两边口径一致。

## 已知坑

- 字体是系统栈（Inter → Segoe UI → 微软雅黑），页面不分发字体文件。没装 Inter 的机器上排版
  宽度与设计稿不同，这不是 bug，别去"修"。
- `assets/` 里 12 个文件名是中文，命令行处理要留意转义；浏览器会自动百分号编码。
- Pages 生效通常有 1–2 分钟延迟，浏览器还有缓存。核对线上用 `curl`，不要用刷新验证。
- 首页个人站外链指向 `https://www.luzzz.me/`：裸域 `luzzz.me` 没有 A 记录，只有 www 有解析
  （这是 DNS 现状，不是本页问题）。裸域生效前不要把链接改回裸域。
- `六朝松.svg` 161 KB 是页面最大的一张图，但它是可见背景水印，不是可删的重复素材。
- 不要为了"看起来正规"加打包、格式化配置，也不要往 CI 里堆构建与 lint——CI 只保留跑
  两条核对的最小工作流；不要新增住址、电话等更敏感字段。
- 不要因为两个「辅助」/两个「剪影」变体看着重复就删——它们分别被不同小节引用。
- 不要把本仓内容大段复制进 `luzzz.me`（那是另一个独立站点，数据各自维护）。
