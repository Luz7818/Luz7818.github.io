# 个人主页 代码风格

> 用途：给改 `index.html` 的人与 AI。本仓唯一源文件是 HTML，约定围绕它；无 lint 工具（有意），
> 格式跟随现状。

## 代码风格

- 不引入格式化/lint 配置（保持零依赖）；改动跟随现有缩进与命名风格。
- 单文件内分区：`<style>` 在前、`<script>` 在后，均为内联，不拆文件。

## 命名与结构约定

- 小节 = `<section id="…">`。8 个小节的 id 固定：`about` / `research` / `experience` /
  `publications` / `projects` / `honors` / `leadership` / `contact`。新增小节必须同时给
  `section` 加 `id` 并在导航登记 `href="#…"`——锚点与 id 成对，漏了不报错、只是点了没反应。
- 配色只用 `:root` 的 14 个 CSS 自定义属性（`--ink` 正文、`--teal` 强调、`--paper` 底色等）；
  不在小节里另写十六进制色值，否则下次统一改色会漏掉它。
- 外链一律 `target="_blank"` 配 `rel="noreferrer"`。
- 文案里的数字要能复核（如"807 条术语"须来自该项目自己的校验命令），不给页面写无法核实的数。

## 错误处理与交互

- 脚本只用 `matchMedia("(prefers-reduced-motion: reduce)")` 判断后才启用平滑滚动；
  不许改成无脑 `behavior:"smooth"`（会让开启"减弱动态效果"的用户体验变差）。
- 不引远程资源、不加载远程字体与 CDN 脚本（复核命令见 `AGENTS.md`「当前状态」）。

## 日志

无日志设施（静态页、无后端）。
