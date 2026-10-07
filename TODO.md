# TODO —— 开发计划与当前进度

> 用途：给开发者与 AI。当前在做哪个任务、每个任务按什么标准验收、接下来做什么。
> 完成一项就勾一项并写明下一项；历史性记录写进 [HISTORY.md](HISTORY.md)，这里只留计划。

## 当前进度

- 正在做：最小校验工作流（任务 5）
- 下一个：移动端 3 断点真机走查

## 任务计划

| # | 任务 | 验收标准（可验证） | 状态 |
|---|---|---|---|
| 1 | 补 `og:` 与 `canonical` 元标签 | `grep -cE 'og:\|canonical' index.html` ≥ 1；推送后线上 `curl -s https://luz7818.github.io/ \| grep -c 'og:'` ≥ 1 | 待确认（本地已验，推送后线上复核） |
| 2 | 决定是否附 LICENSE 文件 | 仓根出现 LICENSE，或本条以"决定不加"注销并记入 HISTORY 缘由 | 完成（2026-10-07，MIT，见仓根 LICENSE） |
| 3 | 移动端 3 断点真机走查 | 1100 / 920 / 640 三档各留一张截图，存档路径登记进本表备注 | 待开始 |
| 4 | 首屏之外的 `<img>` 加 `loading="lazy"` | `grep -o '<img[^>]*loading="lazy"' index.html \| wc -l` > 0，首屏 9 处不受影响 | 待确认（本地已验，推送后线上复核） |
| 5 | 加最小校验工作流 | `.github/workflows/check.yml` 跑 AGENTS.md 两条核对，有输出即失败；推送后 Actions 结论 passing | 进行中 |

状态取值：待开始 / 进行中 / 待确认 / 完成。

## 完成记录

- [x] 文档九件体系迁移 —— 2026-10-05（见 HISTORY.md 对应条目）
