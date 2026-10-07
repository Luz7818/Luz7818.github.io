# HISTORY —— 版本更新记录

> 用途：记录每次版本与规范变更的内容和缘由。只追加，禁止删除或改写既有条目；写错了就追加一条
> 更正。新条目写在文件末尾。

## 2026-10-05 · 文档规范体系落位

- 文档从"五件套"迁到九件体系：新增 `docs/ARCHITECTURE.md`、`docs/CODE-STYLE.md`、
  `docs/TESTING.md`、`docs/GIT.md`、`HISTORY.md`、`TODO.md`；`docs/getting-started.md`
  更名 `docs/GET-START.md`；`AGENTS.md` 重写为规范入口（原「当前真实状态」「已知坑」的事实
  原样保留，原「仓库地图」移入 ARCHITECTURE，原「改动后的验证」移入 TESTING）。
- 变更缘由：落位《项目整体规范.md》的九件必建。本仓此前无版本记录文件，更早历史未在此建档，
  可由 `git log --oneline` 追溯（复核：`git log --oneline | wc -l`）。

## 2026-10-06 · 文档核查修复（章节改名残引清理）

- **章节改名残引**：assets/README 两处指向 AGENTS 旧章节名——「改动后的验证」实际在
  `docs/TESTING.md`（九件迁移时移入），「当前真实状态」已更名「当前状态」，均回改。
- **杂项**：GET-START 加卡片示例的 `<仓库名>` 占位改真实示例 `zhishuxing` 并加注；
  目录说明树补 `.gitignore`（入库文件此前未画进树）、删去与 ARCHITECTURE 重复的
  规模数字职责短语；TODO「正在做」随迁移完成更新。

## 2026-10-07 · 分享元数据与首屏外图片懒加载

- `<head>` 补齐社交分享元数据：`og:title` / `og:description` / `og:image` / `og:url` /
  `og:type`、`twitter:card`（summary，头像 278×278 方图）与 `rel="canonical"`。og 文案逐字
  取自既有 `<title>` 与 `meta description`，不新造宣传语；`og:image` 用 Pages 根路径绝对
  URL `https://luz7818.github.io/assets/portrait.jpg`。核查报告连续三轮挂账的 P2 项，本轮清账。
- 首屏之外的 5 处 `<img>`（campus-band 连续剪影、#about 校徽与礼堂线稿、contact-lockup、
  footer-mark）加 `loading="lazy"`；侧边栏 5 处、顶栏 1 处与 hero 区 3 处首屏图保持即时
  加载，首屏渲染不变。CSS `::before` / `::after` 背景水印不受该属性作用，未动。
- AGENTS.md「当前状态」同步：行数 2105→2112、本地字节数；远程资源复核命令排除
  `rel="canonical"`（它是 `<link>` 声明，页面不加载它，不违反零远程资源约定）；新增
  分享元数据与图片懒加载两行及其复核命令。

## 2026-10-07 · LICENSE、行尾锁定与个人站外链修正

- 仓根补 `LICENSE`：MIT，版权人 Luz7818，年份 2026（与兄弟仓 Transportation_Harnesss、
  Marx_Cloud 同为 MIT）；README「许可」一节由"未附开源许可证文件"改写为如实描述。
- 仓根补 `.gitattributes`：`*.html -text` 锁定页面文件不做行尾转换，消除
  `core.autocrlf=true` 下 `index.html` 整文件 CRLF 翻转的持续风险；另加 `* text=auto`
  让其余文本入库归一 LF。验证：`git add --renormalize .` 后 `git status` 只出现两个新文件，
  无整仓 renormalize。
- `#contact` 的个人站外链由 `https://luzzz.me` 改为 `https://www.luzzz.me/`：裸域
  `luzzz.me` 无 A 记录、只有 www 有解析。AGENTS.md 已知坑与 GET-START 故障表同步改为
  如实描述（DNS 现状），不再表述为"网络不稳"。
- AGENTS.md「当前状态」本地字节数随外链改动更新；目录说明树补 `.gitattributes` 与
  `LICENSE`。

## 2026-10-07 · 最小校验工作流

- 新增 `.github/workflows/check.yml`：checkout → 逐字跑 AGENTS.md 的「资源核对」「锚点核对」
  两条命令 → 任一有输出即失败。核查报告"两条门禁命令完全靠人工"的 P2 项清账；命令正文仍以
  AGENTS.md 为唯一权威来源，工作流内加注防止两处口径漂移。
- 约定不破：工作流无构建、无依赖、无 lint，不影响零依赖单文件与双击可看。AGENTS / README /
  GIT / ARCHITECTURE / TESTING 五处"无 CI（有意选择）"的表述同步改为"CI 只有一条最小校验
  工作流"；目录说明树补 `.github/`。

## 2026-10-07 · 推送与线上复核（本日三批 + 工作流的收口记录）

- `a25b83f..e0b5663` 推送 `main`。线上复核：`curl -s https://luz7818.github.io/ | wc -c`
  = 58389，与本地一致；线上 og: 5 项 / `twitter:card` / `canonical` / 5 处
  `loading="lazy"` / `https://www.luzzz.me/` 外链逐一 grep 到位；LICENSE 线上 200，
  `.gitattributes` 已入库（API 确认）。
- check 工作流首跑（run 37592738597，e0b5663）结论 **success**。AGENTS「当前状态」
  同版本行更新为一致；TODO 任务 1/4/5 记完成。
