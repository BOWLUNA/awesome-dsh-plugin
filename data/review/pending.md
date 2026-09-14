# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-14**
- 快照日期 / Snapshot date: **2026-09-14 (UTC)**
- 待审核 / Pending: **179**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **23**
- Star 异常增长 / Star-growth alerts: **1** — 先看下方告警节 / see the alert section first

审核决定记到数据文件后运行 `node scripts/merge.mjs` 生效：

- 通过 → 加入 [data/approved.json](../approved.json)（`"owner/name": "YYYY-MM-DD"`）
- 剔除 → 加入 [data/curated.json](../curated.json) 的 `excluded_repos`，理由只写「不是 DSH 插件 + 它是什么」，并同步从 `approved.json` 移除
- 只进目录、不进榜单 → 加入 `approved.json` + `curated.json` 的 `leaderboard_exclusions`
- desktop 客户端 / 桌面壳 / 启动器 → `leaderboard_exclusions`（TOP200 与下游市场都不出现）
- market 类（插件市场、商店、技能商城、内置市场的桌面端等）→ `leaderboard_exclusions` + `market_exclusions` 留底（市场不能包含市场）
- 其余非插件形态（手册教程、Docker、VS Code 扩展、配套工具等）与无安装路径的通用工具 → `excluded_repos` 整体剔除（同步从 `approved.json` 移除）
- 目录站 / awesome-list / 榜单站（如 `awesome-dsh-plugin*` 系列）→ `excluded_repos` 整体剔除，不留目录
- Star 异常增长（见告警节）→ 先做增强分析；热度并非来自 DSH 插件本身时，核准也加入 `leaderboard_exclusions`

完整约定见 [data/review/README.md](./README.md)。

Record decisions in the data files, then run `node scripts/merge.mjs`:

- Approve → add to [data/approved.json](../approved.json) (`"owner/name": "YYYY-MM-DD"`)
- Exclude → add to `excluded_repos` in [data/curated.json](../curated.json) — the reason just states "not a DSH plugin + what it is" — and remove it from `approved.json`
- Catalog-only (not in the board) → add to `approved.json` + `leaderboard_exclusions` in `curated.json`
- Desktop client / shell / launcher → `leaderboard_exclusions` (absent from both TOP200.md and the downstream market)
- Market class (plugin market, store, skill mall, desktop with a built-in market) → `leaderboard_exclusions` + a `market_exclusions` backstop entry (the market cannot include another market)
- Other non-plugin forms (handbooks, Docker, VS Code extensions, companion tooling) and generic tools without a DSH install path → `excluded_repos` outright (also removed from `approved.json`)
- Directory sites / awesome-lists / leaderboards (e.g. the `awesome-dsh-plugin*` family) → `excluded_repos` outright
- Star-growth alerts (see the section below) → extra analysis first; if the stars are not from the DSH plugin itself, approve into `leaderboard_exclusions` as well

See [data/review/README.md](./README.md) for the full convention.

## ⚠️ Star 异常增长 / Star-growth alerts

**审查员请先看本节。** 对照上一份快照，把「一天内 +100★」或「突然进入 / 大幅跃升榜单」的仓库单独列出。这些条目**必须做增强分析**后再决定，不要只看 README 就核准进榜。

**Reviewers: start here.** Repositories that gained ≥100 stars in one snapshot interval, or that would suddenly appear on / leap up the star board. Do extra analysis before approving them onto the board — a README check is not enough.

对比上一份快照 **2026-09-13** / vs previous snapshot **2026-09-13**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **1**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [reactive-resume/reactive-resume](https://github.com/reactive-resume/reactive-resume) | 已核准 / approved | 42853 | +145 | 4737 | 2363d | 日增百星 | 日增 +145★；已不进榜单 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [ZSeven-W/rish-app](https://github.com/ZSeven-W/rish-app) | 64 | 2026-08-25 | 2026-09-14 | Your pocket agent. Local-first AI agents on iOS and Android — real workspaces, tool execution with approvals, and your choice of model (DSH · Claude Code · Codex · GLM). |
| 2 | [KongFangXun/sofagent](https://github.com/KongFangXun/sofagent) | 44 | 2026-06-18 | 2026-09-14 | Audit-first governance layer for AI coding agents — 24 git-diff rules, HMAC tamper-evident chain, snapshot rollback (95 tools, 14 plugins) |
| 3 | [WestFox-AwA/dsh-prompt-optimizer](https://github.com/WestFox-AwA/dsh-prompt-optimizer) | 38 | 2026-09-11 | 2026-09-14 | DSH Web 插件：在输入框按回车时，先由『传话 AI』把你的话改写成一条可直接发给工作 AI 的命令——档位/权限/上下文可调，并按任务难度自行决定编排强度，确认后再发送 |
| 4 | [miuzel/dsh-graph](https://github.com/miuzel/dsh-graph) | 7 | 2026-08-21 | 2026-09-14 | 把工作组织成目标看板的 DeepSeek Harness (dsh) 插件：目标 / 判据 / 上下文卡片 / 执行 attempt 的二维泳道看板，数据以文件+事件流落在 .dsh-graph · Goal-kanban plugin for DeepSeek Harness |
| 5 | [Guzhou2002/Fairy-DSH-Optimized](https://github.com/Guzhou2002/Fairy-DSH-Optimized) | 4 | 2026-09-12 | 2026-09-14 | Chengzhibense/Fairy-DSH 的非官方整理分支（孤舟版）；与云朵版 addsas222/Fairy-DSH-Exp 是两套独立分发，只装一个 |
| 6 | [MoonGlassKitty/dsh-tailscale-sync](https://github.com/MoonGlassKitty/dsh-tailscale-sync) | 4 | 2026-08-14 | 2026-09-14 | Zero-config Tailscale sync for DeepSeek Harness (dsh-plugin). 零配置：在手机上继续电脑端 DeepSeek Harness 的工作。 |
| 7 | [drscrewdriver/dsh-search-index](https://github.com/drscrewdriver/dsh-search-index) | 3 | 2026-08-19 | 2026-09-14 | 给 DeepSeek Harness 侧边栏加一个会话内容检索——标题/内容一键切换，还能按用户/回复/工具筛选 |
| 8 | [huashenglian/dsh-livechat](https://github.com/huashenglian/dsh-livechat) | 3 | 2026-09-14 | 2026-09-14 | 给 dsh 对话区叠加 B 站风格吐槽弹幕，可接入 LLM 生成弹幕。/Bilibili-style live-chat danmaku overlay for DeepSeek Harness Web — preset packs, optional LLM quips, drag ball, per-session pools.  |
| 9 | [lemonxiny55/dsh-code-index](https://github.com/lemonxiny55/dsh-code-index) | 3 | 2026-08-21 | 2026-09-14 | Structural code index for DeepSeek Harness (dsh): tree-sitter symbol index, ranked lexical search, a bounded auto-injected repo map, and call-graph tracing. |
| 10 | [NakamuraIA/dsh-plugin-speech](https://github.com/NakamuraIA/dsh-plugin-speech) | 3 | 2026-09-13 | 2026-09-14 | Read assistant replies aloud in DeepSeek Harness: text-to-speech providers with streaming playback. |
| 11 | [claudejaune/OmaSeek](https://github.com/claudejaune/OmaSeek) | 2 | 2026-09-13 | 2026-09-14 | OmaSeek: the Omarchy spirit and aesthetic. Now in DeepSeek Harness |
| 12 | [Momonaka/commandcode-dash](https://github.com/Momonaka/commandcode-dash) | 2 | 2026-09-11 | 2026-09-14 | Unofficial DeepSeek Harness settings panel for Command Code: credits, usage windows, and model-catalog sync. |
| 13 | [NeoXider/neoxider-agent-deck](https://github.com/NeoXider/neoxider-agent-deck) | 2 | 2026-08-25 | 2026-09-14 | Animated desktop companion for DeepSeek Harness — live agent deck, mini-chat, streaming replies, model routing, context pressure and native commands, in a widget that docks to your screen edge. |
| 14 | [Phant0Meow/femo-plugin](https://github.com/Phant0Meow/femo-plugin) | 2 | 2026-08-28 | 2026-09-14 | FEMO插件版 — 可接入dsh的多智能体引擎，差不多能做所有事：我已经用femo和我的主agent玩了好几局狼人杀了，他抽到狼他还刀我！ 我在b站的宣传视频也是用femo剪的。 coding的时候，特别难找的bug、代码重构，我都会用femo来做。 我甚至用femo模式给我的主agent养了只宠物，她很开心。 |
| 15 | [RUO-MO/dsh-deepseek-web](https://github.com/RUO-MO/dsh-deepseek-web) | 2 | 2026-09-13 | 2026-09-14 | DeepSeek Harness 插件：侧边栏内嵌[chat.deepseek.com](https://chat.deepseek.com)网页版对话，无需 API Key，不消耗 DSH 会话 Token，支持 Web 与 Electron 桌面端。 |
| 16 | [better-er/dsh-notify-ding](https://github.com/better-er/dsh-notify-ding) | 1 | 2026-09-13 | 2026-09-14 | dsh·通知叮咚插件。agent 提问或跑完一轮时，弹浏览器系统通知并让宿主进程播放 Windows 内置提示音，人跑去别的窗口时也能被叫回来；纯插件自包含，不改 DSH 源码。 |
| 17 | [better-er/dsh-remote-file-system](https://github.com/better-er/dsh-remote-file-system) | 1 | 2026-09-13 | 2026-09-14 | dsh·远程文件系统插件。给模型提供 read_remote、write_remote、edit_remote 三个工具，经 ssh 读写远程主机文件，不用再在 PowerShell 里套 bash 命令；write_remote 只允许新建。纯插件自包含，不改 DSH 源码。 |
| 18 | [dragonTalon/dsh-browser-assistant](https://github.com/dragonTalon/dsh-browser-assistant) | 1 | 2026-09-04 | 2026-09-14 | 将dsh转成谷歌插件 |
| 19 | [DZQJOKER/dsh-plugin-local-model](https://github.com/DZQJOKER/dsh-plugin-local-model) | 1 | 2026-09-12 | 2026-09-14 | "DeepSeek Harness 本地模型插件：设置里独立的「本地模型」页，首条对话自动拉起 llama.cpp，空闲 5 分钟自动卸载释放资源。" |
| 20 | [Emck/tirol-dsh-language-set](https://github.com/Emck/tirol-dsh-language-set) | 1 | 2026-09-14 | 2026-09-14 | [DeepSeek Harness] dsh plugin, that controls AI's reply language and thinking language separately via system prompt injection. |
| 21 | [GuidoMaxier/dsh-locale-es](https://github.com/GuidoMaxier/dsh-locale-es) | 1 | 2026-09-13 | 2026-09-14 | Spanish (es) language pack for the DeepSeek Harness Web UI — a community DSH client plugin adding Espanol to Settings > General > Language. |
| 22 | [HakureiMonika/dsh-browser-scope](https://github.com/HakureiMonika/dsh-browser-scope) | 1 | 2026-09-09 | 2026-09-14 | Agent-native browser DevTools workbench for DeepSeek Harness. / 让你的DSH获得非常强大的 Chromium DevTools 能力 |
| 23 | [hoyyang/dsh-improve-prompt](https://github.com/hoyyang/dsh-improve-prompt) | 1 | 2026-09-14 | 2026-09-14 | 输入框一键增强提示词：直接替换 + 一键撤回，带保真闸（硬事实零丢失）与长度闸（防膨胀）。DSH plugin. |
| 24 | [KannaKuron/dsh-ide-git](https://github.com/KannaKuron/dsh-ide-git) | 1 | 2026-09-14 | 2026-09-14 | DSH plugin: an IDE-grade Git tool window as a native dsh-better-sidebar tab — branch tree, commit graph, changes, commit details, JetBrains-style actions, in the right sidebar and the bottom panel. \| DSH 插件:IDE 级 Git 工具窗口,以 dsh-better-sidebar 原生 Tab 挂载——分支树 / 提交图谱 / 变更与提交详情 / JetBrains 风格操作,右侧栏与底部面板双布局自适应。 |
| 25 | [liceses/dsh-showme-html](https://github.com/liceses/dsh-showme-html) | 1 | 2026-09-14 | 2026-09-14 | DSH 插件：把工作区里写好的 HTML 页展示在对话里，并让用户在页面上的表态快速回到 agent 手里。含四套预设样式。 |
| 26 | [liyixuan201211/dsh-rewind](https://github.com/liyixuan201211/dsh-rewind) | 1 | 2026-09-14 | 2026-09-14 | Undo what an agent did to a directory: content-addressed snapshots, one-command rewind, and an undo you can undo. Works in any folder — git or not. DSH plugin + skill, zero dependencies. |
| 27 | [liyixuan201211/mcp-cap](https://github.com/liyixuan201211/mcp-cap) | 1 | 2026-09-14 | 2026-09-14 | What can this MCP server actually do — and has it changed since you trusted it? Inspect its declared capabilities, seal them in a lock file, and get told when a later version can do more. Never invokes a tool; gives the server a minimal environment. |
| 28 | [lyd123qw2008/pi-control-chrome](https://github.com/lyd123qw2008/pi-control-chrome) | 1 | 2026-08-17 | 2026-09-14 | Chrome and Edge browser control for Pi, Codex and DSH. Drives your real browser profile, login state and tabs through an MV3 extension and a local loopback Bridge - native CDP, AX-first semantics, no separate browser. |
| 29 | [lzhhhhc/Arknights-flavor-theme](https://github.com/lzhhhhc/Arknights-flavor-theme) | 1 | 2026-09-14 | 2026-09-14 | Arknights theme skin for DeepSeek Harness. 适用于 DeepSeek Harness 的明日方舟主题皮肤。 |
| 30 | [MarcSierszen/dsh-specify-lite](https://github.com/MarcSierszen/dsh-specify-lite) | 1 | 2026-09-12 | 2026-09-14 | A light version of Githubs spec-kit as DSH plugin |
| 31 | [meimiaoji-creator/meow-dsh-task](https://github.com/meimiaoji-creator/meow-dsh-task) | 1 | 2026-08-31 | 2026-09-14 | meow-dsh-task 是 DeepSeek Harness 的一款研发任务项目管理插件，解决跨上下文研发任务执行的问题。标准化研发任务拆解。规范化研发执行流程。包含 研发计划、研发任务、研发评审、issue等管理可视化功能，同时所有研发环节均可以是人或者AI参与 |
| 32 | [meimiaoji-creator/meow-file-view](https://github.com/meimiaoji-creator/meow-file-view) | 1 | 2026-09-14 | 2026-09-14 | meow-file-view 解决「AI 改完文件，我却要切到 VS Code 才能看它到底改了什么」的问题。它把一个轻量文件查看器直接嵌进 DSH 对话窗：左侧目录树懒加载浏览工作区，右侧预览 Markdown（含 TOC / mermaid / 图片）、源码高亮、甚至直接编辑保存；模型每回合产出/修改的文件会以 chips 行挂在回合尾部，点一下直达该文件，命中 git 变更还能一键看 diff。  零 DSH 源码改动——独立 bundle，经 dsh 插件 --profile web add 装进 web profile，与官方插件平级共存。 |
| 33 | [NeoXider/neoxider-mcp-hub](https://github.com/NeoXider/neoxider-mcp-hub) | 1 | 2026-08-25 | 2026-09-14 | One MCP tool instead of every schema you own — a lazy capability broker that cuts resident tool context by a measured 94.4%. Search, inspect, enable and call MCP servers and skills on demand. |
| 34 | [NoodleStormno/dsh-plugin-tic80](https://github.com/NoodleStormno/dsh-plugin-tic80) | 1 | 2026-09-14 | 2026-09-14 | DeepSeek Harness (dsh) plugin for TIC-80 fantasy console: full console capabilities, conversational code, music, map, and sprite generation by LLM, with native & live web execution. |
| 35 | [qtaik/dsh-noname-kit](https://github.com/qtaik/dsh-noname-kit) | 1 | 2026-09-13 | 2026-09-14 | DeepSeek Harness无名杀插件  无名杀扩展开发工坊:AI 按规范写武将技能与卡牌(确认协议/校验门禁/区块化写入) |
| 36 | [RavenWangChina/yuanzhu](https://github.com/RavenWangChina/yuanzhu) | 1 | 2026-09-09 | 2026-09-14 | 元铸工坊 SOSOFAST——企业 AI 人效平台：把最佳实践铸成可治理的工作流资产（AI 提议，人拍板） |
| 37 | [samuelrubiodev/dsh-hyper-tools](https://github.com/samuelrubiodev/dsh-hyper-tools) | 1 | 2026-09-13 | 2026-09-14 | DSH plugin: keeps Charm Hyper model requests under the gateway's 10 MiB body cap by replacing the oldest images (newest survive) and retrying when the gateway rejects the body. |
| 38 | [Sun-L1/DSH-WhaleMaid-Companion](https://github.com/Sun-L1/DSH-WhaleMaid-Companion) | 1 | 2026-09-14 | 2026-09-14 | DeepSeek Harness：鲸鱼妹抖桌宠！ |
| 39 | [tq04qom/dsh-multirole](https://github.com/tq04qom/dsh-multirole) | 1 | 2026-09-14 | 2026-09-14 | DSH 多角色协作模式插件——人/顾问/总控/执行者四层架构，任务单制度 + 写入域互斥 + 授权模式 + 裁决日志，让大模型协作开发可控、可复用。DSH multi-role collaboration plugin — human/advisor/orchestrator/executor four-layer architecture with task manifests, write-set isolation, authorization modes, and audit logging for controllable, reusable LLM team development. |
| 40 | [weibaohui/dsh-fde-tools](https://github.com/weibaohui/dsh-fde-tools) | 1 | 2026-09-12 | 2026-09-14 | dsh 插件全家桶：装一个插件带一批插件（Git 服务器/WebDAV 挂载盘/知识库/定时任务/自动续跑/界面微调/自动复盘） |
| 41 | [YpipaQ/dsh-s-m-c-center](https://github.com/YpipaQ/dsh-s-m-c-center) | 1 | 2026-09-14 | 2026-09-14 | Skills, MCP and CLI manager for the DeepSeek Harness (dsh) web GUI — one page, real connections. |
| 42 | [zeyu-j/centricmem-skill](https://github.com/zeyu-j/centricmem-skill) | 1 | 2026-07-06 | 2026-09-14 | Cross-agent workspace memory for AI agents |
| 43 | [zp2921060653/dsh-plugins](https://github.com/zp2921060653/dsh-plugins) | 1 | 2026-08-31 | 2026-09-14 | DeepSeek Harness (DSH) plugins: agent bridge (Claude Code/Codex/Marvis) + Ghidra reverse engineering bridge |
| 44 | [zzy6-a/dsh-prompt-enhance](https://github.com/zzy6-a/dsh-prompt-enhance) | 1 | 2026-09-14 | 2026-09-14 | DSH 输入框旁的一键提示词增强：把口语化的一句话改写成目标明确、细节完整的任务说明，可一键撤销；五种改写风格、模型可跟随或固定，含 @引用/命令芯片时自动置灰保护。 |
| 45 | [1921622004/dsh-command-palette](https://github.com/1921622004/dsh-command-palette) | 0 | 2026-09-09 | 2026-09-14 | ⌘K 命令面板插件，为 DeepSeek Harness Web GUI 提供：会话切换、设置直达、侧边栏页签与插件集成入口，支持自定义快捷键，手不离键盘完成大部分操作。 |
| 46 | [776138506/pinpoint](https://github.com/776138506/pinpoint) | 0 | 2026-08-21 | 2026-09-14 | 指哪打哪：在任意网页标记元素并评论，截图+结构化文本直达 dsh 会话（dsh 插件 + 浏览器扩展） |
| 47 | [Aclguh/dsh-web-close](https://github.com/Aclguh/dsh-web-close) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek-Harness插件，用于关闭dsh的web进程 |
| 48 | [advance-lion/dsh-lan-link](https://github.com/advance-lion/dsh-lan-link) | 0 | 2026-09-14 | 2026-09-14 | Persistent token-gated LAN access for DeepSeek Harness Web |
| 49 | [alexhegit/dsh-plugin-h3-hip](https://github.com/alexhegit/dsh-plugin-h3-hip) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness Host plugin for h3-hip.c (--serve, protocol v1alpha) |
| 50 | [almazom/dsh-almazom-approve-escalate](https://github.com/almazom/dsh-almazom-approve-escalate) | 0 | 2026-09-14 | 2026-09-14 | DSH web plugin: one-click Approve & escalate on the approval card — approves the pending request and switches the live session to a permission preset |
| 51 | [AmigaMeow/dsh-asset-library](https://github.com/AmigaMeow/dsh-asset-library) | 0 | 2026-09-14 | 2026-09-14 | DSH (DeepSeek Harness) 素材库插件：会话内容一键保存 + 自动采集，按时间/类型/会话/项目四轴归纳，本地 Markdown 存储，零运行时依赖。 |
| 52 | [aoripus/dsh-optimize](https://github.com/aoripus/dsh-optimize) | 0 | 2026-09-14 | 2026-09-14 | Long-session resource control for DeepSeek Harness: measures the context every request carries, warns at configurable thresholds, can run the harness compaction engine over budget, and contains offscreen chat rows behind a toggle. |
| 53 | [azazo1/dsh-limit-timeout](https://github.com/azazo1/dsh-limit-timeout) | 0 | 2026-09-14 | 2026-09-14 | Cap how long one DSH tool call may wait: a global default wait limit in Settings, plus a per-session raise the model can request from the user. |
| 54 | [baixianger/dsh-codex-adapter](https://github.com/baixianger/dsh-codex-adapter) | 0 | 2026-09-14 | 2026-09-14 | ChatGPT-powered coding, image generation and web search for DeepSeek Harness. |
| 55 | [ch1bug/dsh-voice-mimo](https://github.com/ch1bug/dsh-voice-mimo) | 0 | 2026-08-14 | 2026-09-14 | Xiaomi MiMo-powered voice for DeepSeek Harness: browser 🎤/🧠/🔊 UI, voice_transcribe/voice_understand/voice_speak tools, configurable voice map (preset/voicedesign/voiceclone). Fork of zhuiyueya/dsh-voice (MIT), Settings pattern from Anionex/dsh-vision-toolkit (MIT). |
| 56 | [ChenneyZhuang/agent-skills-cn](https://github.com/ChenneyZhuang/agent-skills-cn) | 0 | 2026-09-14 | 2026-09-14 | Bilingual (EN/CN) agent skills: email deliverability audit, competitor recon, resume localization CN→EN, delivery checklist — battle-tested domain workflows as open SKILL.md files. |
| 57 | [ChenneyZhuang/ask-batch](https://github.com/ChenneyZhuang/ask-batch) | 0 | 2026-09-14 | 2026-09-14 | Ask-batch skill: park piecemeal questions with context, group by decision, ask once per group with proposed defaults in a numbered format, and apply defaults visibly — true blockers still ask immediately. |
| 58 | [ChenneyZhuang/backlog-triage](https://github.com/ChenneyZhuang/backlog-triage) | 0 | 2026-09-14 | 2026-09-14 | Backlog triage skill: sweep every source into one inventory, classify items into six dispositions with reasons, archive drops, and batch commitment changes into one approval — a list that only grows is not a plan. |
| 59 | [ChenneyZhuang/changelog-capture](https://github.com/ChenneyZhuang/changelog-capture) | 0 | 2026-09-14 | 2026-09-14 | Changelog capture skill: user-facing entries at change time in who/what/upgrade shape, Added/Changed/Fixed with breaking changes leading, verified against the actual diff at release. |
| 60 | [ChenneyZhuang/competitor-recon](https://github.com/ChenneyZhuang/competitor-recon) | 0 | 2026-09-14 | 2026-09-14 | Competitor research skill: complaint-driven recon with cited evidence from reviews, forums, and issue trackers — comparison table plus copy-worthy and skip lists. CN/EN. |
| 61 | [ChenneyZhuang/context-budget](https://github.com/ChenneyZhuang/context-budget) | 0 | 2026-09-14 | 2026-09-14 | Context budget skill: graduated file reads (head, section, search), a working notes file that survives compaction, and three-line checkpoints at phase boundaries — long tasks finish on notes, not fumes. |
| 62 | [ChenneyZhuang/delivery-checklist](https://github.com/ChenneyZhuang/delivery-checklist) | 0 | 2026-09-14 | 2026-09-14 | Delivery checklist skill: verify deliverables by opening the real file — row/dedup counts, placeholder scan, baseline diff — and log every batch. CN/EN. |
| 63 | [ChenneyZhuang/email-deliverability-audit](https://github.com/ChenneyZhuang/email-deliverability-audit) | 0 | 2026-09-14 | 2026-09-14 | Email deliverability audit skill: four sequential DNS gates classify addresses as sendable/risky/dead — every verdict traces to a query run that session. CN/EN. |
| 64 | [ChenneyZhuang/estimate-before-build](https://github.com/ChenneyZhuang/estimate-before-build) | 0 | 2026-09-14 | 2026-09-14 | Estimate-before-build skill: bounded task list, S/M/L/XL band estimates with uncertainty drivers named, scope-vs-budget options surfaced to the user, and estimates recorded for finish-line calibration. |
| 65 | [ChenneyZhuang/expense-capture](https://github.com/ChenneyZhuang/expense-capture) | 0 | 2026-09-14 | 2026-09-14 | Expense capture skill: receipts to ledger-ready rows without invention — transcribe as shown, flag unclear fields, read tax never derive it, and reconcile count and total before any write. |
| 66 | [ChenneyZhuang/onboarding-pack](https://github.com/ChenneyZhuang/onboarding-pack) | 0 | 2026-09-14 | 2026-09-14 | Onboarding pack skill: the day-one doc — what & why, exact run commands, a map naming the authoritative source, the unwritten rules, and who decides — ten minutes to read, updated with the change that invalidates it. |
| 67 | [ChenneyZhuang/project-handoff](https://github.com/ChenneyZhuang/project-handoff) | 0 | 2026-09-14 | 2026-09-14 | Project handoff skill: a dated handoff.md per project — current state, decisions with reasons, pitfalls as symptom/cause/fix — so any fresh session resumes without archaeology. CN/EN. |
| 68 | [ChenneyZhuang/report-link-verification](https://github.com/ChenneyZhuang/report-link-verification) | 0 | 2026-09-14 | 2026-09-14 | Link verification skill: fetch every URL in a deliverable for real, retry bot walls, fix or cut failures — links in file must equal links in table. CN/EN. |
| 69 | [ChenneyZhuang/resume-localize-cn2en](https://github.com/ChenneyZhuang/resume-localize-cn2en) | 0 | 2026-09-14 | 2026-09-14 | Resume localization skill (CN to EN): demographic fields stripped, duties become quantified outcomes, one spelling variant, ATS-parsable, full change log. CN/EN. |
| 70 | [ChenneyZhuang/template-instantiator](https://github.com/ChenneyZhuang/template-instantiator) | 0 | 2026-09-14 | 2026-09-14 | Template instantiator skill: inventory every placeholder and example block, fill from stated data inventing nothing, delete unrequested optional sections, and show the zero-hit residue scan with the delivery. |
| 71 | [ChenneyZhuang/web-cliplibrary](https://github.com/ChenneyZhuang/web-cliplibrary) | 0 | 2026-09-14 | 2026-09-14 | Web clip library skill: save research as markdown clips with URL, fetch date, verbatim quotes, and separated agent notes — greppable per project and citable after the source page dies. |
| 72 | [ChenneyZhuang/weekly-review](https://github.com/ChenneyZhuang/weekly-review) | 0 | 2026-09-14 | 2026-09-14 | Weekly review skill: reconcile last week's logged commitments against outcomes with evidence, bank wins, carry items forward only with a fresh reason, and commit to a small checkable set — logged for next week to compare. |
| 73 | [chenqg618/compliance-skills](https://github.com/chenqg618/compliance-skills) | 0 | 2026-09-13 | 2026-09-14 | Mechanical-check AI agent skills for contracts, invoices, tender/bidding documents and ad copy: every finding is recomputable evidence, fully offline, no model, no network. 合同、票据、招投标与广告文案的机械核对型 AI 技能（免费版源码）。 |
| 74 | [ciceroyang/dsh-topic-audit](https://github.com/ciceroyang/dsh-topic-audit) | 0 | 2026-09-14 | 2026-09-14 | Audit the GitHub dsh-plugin topic: which repos are real DSH plugins, which are companions, which are pollution. |
| 75 | [cnkids/dsh-session-reattach](https://github.com/cnkids/dsh-session-reattach) | 0 | 2026-09-13 | 2026-09-14 | DSH 宿主插件：把游离（未分组）会话按 cwd 归位到匹配的工作区 —— 只改工作区归属记录，不碰会话文件；支持拖拽与 /reattach 命令（默认 dry-run）｜ DSH host plugin: re-attach ungrouped sessions to their matching workspace by cwd — ownership bookkeeping only, never rewriting session logs |
| 76 | [daha1216/dsh-better-display](https://github.com/daha1216/dsh-better-display) | 0 | 2026-09-13 | 2026-09-14 | DeepSeek Harness 沉浸式阅读视图（fork）：执行步骤自动折叠 + MCP-App 交互沙箱，深度适配 dsh-retrace 撤回/重发节点展示 |
| 77 | [daha1216/dsh-pocket](https://github.com/daha1216/dsh-pocket) | 0 | 2026-09-08 | 2026-09-14 | 把 DeepSeek Harness 装进口袋：手机扫码同步操控电脑端 DSH（局域网/公网直连 + 移动端抽屉布局），基于上游 v2.10.3 安全加固版 |
| 78 | [daha1216/dsh-retrace](https://github.com/daha1216/dsh-retrace) | 0 | 2026-09-09 | 2026-09-14 | DeepSeek Harness 会话时光机（fork）：消息撤回/编辑重发/重新生成 + 产物版本化，适配 DSH 0.1.5+ 与插件服务机制 |
| 79 | [damlys99/dsh-queue-reorder](https://github.com/damlys99/dsh-queue-reorder) | 0 | 2026-09-14 | 2026-09-14 | Reorder queued messages inside the DeepSeek Harness Web GUI queue dock: grip-and-drag plus move buttons, without taking over the official dock. |
| 80 | [danhcng3822f/dsh-upload-plugin](https://github.com/danhcng3822f/dsh-upload-plugin) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness plugin providing Add photos, Add files, and Uploaded files in chat UI with vision validation and session isolation |
| 81 | [duanyunlun/dsh-session-actions](https://github.com/duanyunlun/dsh-session-actions) | 0 | 2026-09-12 | 2026-09-14 | Sidebar Conversation actions for DeepSeek Harness: double-click to rename, copy the session ID, and permanently delete a Conversation with its storage. |
| 82 | [eiainano/agpa-dsh-plugin](https://github.com/eiainano/agpa-dsh-plugin) | 0 | 2026-09-14 | 2026-09-14 | AGPA (Agent Player Achievements) for DeepSeek Harness: native achievement_* tools bridging the AGPA engine, plus automatic event tracking from dsh session events. |
| 83 | [exoticknight/dsh-just-chat](https://github.com/exoticknight/dsh-just-chat) | 0 | 2026-09-14 | 2026-09-14 | One-click native conversations with independent workspaces for DeepSeek Harness |
| 84 | [fan56/dsh-profile-switch](https://github.com/fan56/dsh-profile-switch) | 0 | 2026-09-11 | 2026-09-14 | dsh plugin: switch named model profiles (default model, think level, per-subagent models) interactively via the host ask-user flow — one implementation for the TUI and web surfaces |
| 85 | [FengHuoLinShan/novelAssist-dsh](https://github.com/FengHuoLinShan/novelAssist-dsh) | 0 | 2026-08-14 | 2026-09-14 | novelAssist DSH 插件重写 (M4) |
| 86 | [fuguier001/dsh-imgnav](https://github.com/fuguier001/dsh-imgnav) | 0 | 2026-09-13 | 2026-09-14 | Click-to-zoom lightbox with arrow-key paging for DSH conversation images: ← prev / → next / Esc close, edge hints |
| 87 | [fuguier001/dsh-procguard](https://github.com/fuguier001/dsh-procguard) | 0 | 2026-09-12 | 2026-09-14 | DSH 进程看护管家：launchd 保活 + preflight 启动闸 + 内存哨兵 + 断链自愈的四层防御插件（macOS 实测 / Linux 骨架 / 不支持 Windows） |
| 88 | [fuguier001/dsh-progress](https://github.com/fuguier001/dsh-progress) | 0 | 2026-09-12 | 2026-09-14 | DSH web GUI 浮动水球进度指示器：莫兰迪色带水位、光晕联动、抓取感拖动（附可复用拖动模板） |
| 89 | [fyisgod/dsh-selection-tools](https://github.com/fyisgod/dsh-selection-tools) | 0 | 2026-09-13 | 2026-09-14 | DSH 插件：任意 Windows 应用里划词，用 DeepSeek Harness 自己的 agent 解释/翻译，结果落在原生置顶浮窗（GDI+，零依赖、零额外进程）。安装：dsh plugin --profile web add "github:fyisgod/dsh-selection-tools" |
| 90 | [GooDAnDReaDY/dsh-issue-reporter](https://github.com/GooDAnDReaDY/dsh-issue-reporter) | 0 | 2026-09-14 | 2026-09-14 | DSH plugin that turns installed plugin problems into safe, reviewable GitHub issues. |
| 91 | [guytogay/dsh-addon-kit](https://github.com/guytogay/dsh-addon-kit) | 0 | 2026-09-03 | 2026-09-14 | DSH addon kit: reusable MCP servers (desktop/browsers), A2A agent bridge, skill, plugins and mobile-remote kit - sanitized for public reuse |
| 92 | [hatsuyuki0103/dsh-fight-scene-director](https://github.com/hatsuyuki0103/dsh-fight-scene-director) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness ??:? Codex ?? fight-scene-director(??? AI ????????????)??? DSH ????,???? Seedance 2.0 / 2.5?MiniMax H3 ?????????? |
| 93 | [Haven-hvn/deepseek-harness-web3-agent-stack](https://github.com/Haven-hvn/deepseek-harness-web3-agent-stack) | 0 | 2026-08-19 | 2026-09-14 | web3 extensions for the deepseek harness where everything is a plugin |
| 94 | [he-yufeng/dsh-tool-radar](https://github.com/he-yufeng/dsh-tool-radar) | 0 | 2026-09-14 | 2026-09-14 | Repo health radar for DeepSeek Harness: score a GitHub repo's contribution-friendliness from live evidence |
| 95 | [he-yufeng/dsh-tool-reading-map](https://github.com/he-yufeng/dsh-tool-reading-map) | 0 | 2026-09-14 | 2026-09-14 | Repo reading-map tool for DeepSeek Harness: a structured, priority-ranked map of any codebase before the agent edits it |
| 96 | [Hoshino910/REMI](https://github.com/Hoshino910/REMI) | 0 | 2022-10-17 | 2026-09-14 | Adaptive memory for AI. A DeepSeek Harness plugin prototype for selective recall, configurable context budgets, and history compaction, designed to reduce token usage while preserving conversational continuity. |
| 97 | [hoyin-law/dsh-notify-plus](https://github.com/hoyin-law/dsh-notify-plus) | 0 | 2026-09-13 | 2026-09-14 | Context-rich native notifications for DSH Desktop: the toast title is the live conversation title, and the body is a deterministic 10–20 character distillation of what the turn produced. Replaces the built-in notifications row and reuses its settings namespace. |
| 98 | [icanotcode/dsh-feishu-bot](https://github.com/icanotcode/dsh-feishu-bot) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness 社区飞书插件：Webhook、长连接、可视化配置与消息自动回复 |
| 99 | [imroc/dsh-browser-panel](https://github.com/imroc/dsh-browser-panel) | 0 | 2026-09-14 | 2026-09-14 | A shared browser inside the DeepSeek Harness host: the AI drives it with browser_panel_* tools, and you watch or take over the same tab in the DSH Web UI — logins, 2FA, QR codes included. |
| 100 | [ivanearisty/dsh-plugin-cmdk](https://github.com/ivanearisty/dsh-plugin-cmdk) | 0 | 2026-09-14 | 2026-09-14 | Command palette for DeepSeek Harness (Cmd+K) — new chat, jump to session, switch model, permissions, slash commands, settings, all from one fuzzy bar |
| 101 | [ivanearisty/dsh-session-search](https://github.com/ivanearisty/dsh-session-search) | 0 | 2026-09-14 | 2026-09-14 | Full-text search across every DeepSeek Harness conversation — MiniSearch host index, Option+K palette, jump straight to the message |
| 102 | [jasonjiang9527/dsh-plugins](https://github.com/jasonjiang9527/dsh-plugins) | 0 | 2026-09-14 | 2026-09-14 | 自研 dsh 插件合集 · dsh-btw: 划选引用 / btw 临时会话 / 新上下文 / Provider 高级配置 |
| 103 | [jerryxugit-2026/dsh-web-companion](https://github.com/jerryxugit-2026/dsh-web-companion) | 0 | 2026-09-13 | 2026-09-14 | Chrome side panel that puts the DeepSeek Harness (DSH) agent next to the page you are reading — read it, or let the agent work it. Built on DeepSeek Harness; not affiliated with or endorsed by DeepSeek. |
| 104 | [jonah791/dsh-agent-cluster](https://github.com/jonah791/dsh-agent-cluster) | 0 | 2026-09-14 | 2026-09-14 | DSH 多实例通讯底座：文件总线 + 在线名册 + 点对点/广播 + 收件箱 + 会话注入（多智能体工作台的 L0 层） |
| 105 | [jonah791/dsh-plugin-bootreport](https://github.com/jonah791/dsh-plugin-bootreport) | 0 | 2026-09-14 | 2026-09-14 | DSH 启动自报账本：web 启动时落一行「本进程加载了哪些插件构建」，判据 lib mtime vs 进程起点，一条命令答全生态「构建是否生效 / 谁需重启」 |
| 106 | [KhalilYamber/yammory-system](https://github.com/KhalilYamber/yammory-system) | 0 | 2026-09-13 | 2026-09-14 | Cross-session user-profile memory for DeepSeek Harness: remembers who you are and how much you know, so the agent speaks at your level. Approval-gated, auditable, local SQLite. |
| 107 | [kiiiiile/dsh-approval-ai-review](https://github.com/kiiiiile/dsh-approval-ai-review) | 0 | 2026-09-14 | 2026-09-14 | AI-reviewed auto-approval for DeepSeek Harness: safe tool asks granted automatically, risky ones escalated with the review attached |
| 108 | [laym0nd/dsh-labrador](https://github.com/laym0nd/dsh-labrador) | 0 | 2026-09-14 | 2026-09-14 | A Labrador virtual pet for deepseek harness |
| 109 | [liyixuan201211/ctx-budget](https://github.com/liyixuan201211/ctx-budget) | 0 | 2026-09-14 | 2026-09-14 | What will your agent's context cost before it runs? Audit instruction files, skills, MCP tool schemas and memory per source — with duplication, always-on versus on-demand costs, and a budget you can enforce in CI. Reads files and nothing else. |
| 110 | [LLYlab/DLT](https://github.com/LLYlab/DLT) | 0 | 2026-09-14 | 2026-09-14 | DLT (DeepSeek Light Tool) - a permanent DeepSeek Harness (DSH) plugin: per-turn CNY cost, DeepSeek account balance, native PDF/Word/Excel/CSV read-write tools and right-sidebar previews, a hardcoded compiler/runtime registry with direct run/build tools, and a runtime master switch (DLT manager). |
| 111 | [lnsdlszsqxxx/dsh-courseware](https://github.com/lnsdlszsqxxx/dsh-courseware) | 0 | 2026-09-14 | 2026-09-14 | create pptx file based on template.pptx and a outline file  |
| 112 | [loeissu/dsh-plugin-mobile-ui](https://github.com/loeissu/dsh-plugin-mobile-ui) | 0 | 2026-09-11 | 2026-09-14 | Mobile-first UI for the DeepSeek Harness web client — an official slot client plugin. 让 DSH 在手机上好用：抽屉导航、命中区、键盘适配、横屏。不改宿主源码，不 fork tether，不接管 sidebar。 |
| 113 | [lucyTrump/dsh-runninghub-api](https://github.com/lucyTrump/dsh-runninghub-api) | 0 | 2026-09-14 | 2026-09-14 | A plugin that integrates runninghub cloud ComfyUI workflows: a settings card for your API key and workflow library, seven `runninghub_*` tools for agents, a sha256 media upload cache, a local concurrency gate with FIFO queueing and timeouts, background tasks with completion notifications, and a durable task ledger with automatic restart recovery. |
| 114 | [LyaxZ/dsh-fonttune](https://github.com/LyaxZ/dsh-fonttune) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness 字体插件：正文/代码字体族、全局字号偏移、字重，以及西文/中文分栏选择。 |
| 115 | [ManoloRemiddi/dsh-steering](https://github.com/ManoloRemiddi/dsh-steering) | 0 | 2026-09-14 | 2026-09-14 | Responsive steering during model output in DeepSeek Harness; preserves queued follow-ups and running tools. |
| 116 | [MARIOMLY/dsh-desktop-app](https://github.com/MARIOMLY/dsh-desktop-app) | 0 | 2026-09-12 | 2026-09-14 | Open the DeepSeek Harness Web UI as a standalone desktop app window (Chromium --app mode) — a DSH host plugin. / 把 DSH Web 界面变成独立桌面应用窗口的 DSH 插件。 |
| 117 | [MARIOMLY/dsh-schedule-panel](https://github.com/MARIOMLY/dsh-schedule-panel) | 0 | 2026-09-14 | 2026-09-14 | 日程面板——一个可以提醒你的小插件 |
| 118 | [MARIOMLY/dsh-window-pin](https://github.com/MARIOMLY/dsh-window-pin) | 0 | 2026-09-14 | 2026-09-14 | 一个小巧且轻量的置顶工具 |
| 119 | [Meaple-SFKY/dsh-model-orchestrator](https://github.com/Meaple-SFKY/dsh-model-orchestrator) | 0 | 2026-09-13 | 2026-09-14 | Model routing for DeepSeek Harness, with a standing capability-to-model assignment table, per-route reasoning levels, and a user-triggered sync that researches public model prices. 为 DeepSeek Harness 提供模型路由：可持久化的「能力→模型」分工表、按路由的推理档位，以及手动触发、由模型联网核对公开价格的同步。 |
| 120 | [Missher12/dsh-missher-brain](https://github.com/Missher12/dsh-missher-brain) | 0 | 2026-09-14 | 2026-09-14 | Shared, bounded recall coordination for DeepSeek Harness Memory and MSE providers. |
| 121 | [Missher12/dsh-missher-enhance](https://github.com/Missher12/dsh-missher-enhance) | 0 | 2026-09-14 | 2026-09-14 | Independent enhancement bundle for DeepSeek Harness: usage, sessions, model helpers, documents and piano navigation. |
| 122 | [moonbowterfly/dsh-bio-graft](https://github.com/moonbowterfly/dsh-bio-graft) | 0 | 2026-09-14 | 2026-09-14 | 基因编辑设计域插件（dsh-bio-genie 生态）：sgRNA 候选/评分向量/切割位点 + 声明式排名 + Cas-OFFinder 脱靶语义层 + 碱基编辑（CBE/ABE）+ EditPlan 可审计账本 \| CRISPR / gene-editing design plugin for dsh (dsh-bio family) |
| 123 | [MrTomTao/dsh-token-billing](https://github.com/MrTomTao/dsh-token-billing) | 0 | 2026-09-14 | 2026-09-14 | 给DeepSeek Harness Web GUI用的会话token计费插件：在会话标题栏显示本次会话的实时花费，点开可以看输入 / 缓存命中 / 缓存写入 / 输出 / 推理的分项、按模型的账单，以及当前用的是高峰还是空闲时段价。 |
| 124 | [MrWeiCodes/dsh-fs-encoding](https://github.com/MrWeiCodes/dsh-fs-encoding) | 0 | 2026-09-14 | 2026-09-14 | 为 DeepSeek Harness（DSH）提供文件编码守护：让 AI 读写 GBK 等非 UTF-8 文件和带 BOM 的文件时不会弄坏编码 |
| 125 | [n0pe-sled/clear-session-history](https://github.com/n0pe-sled/clear-session-history) | 0 | 2026-09-13 | 2026-09-14 | dsh plugin: clear session history from disk (workspace/all/session) with scoped, confirmed deletes |
| 126 | [n0pe-sled/configurable-subagents](https://github.com/n0pe-sled/configurable-subagents) | 0 | 2026-09-13 | 2026-09-14 | dsh plugin: default sub-agent provider, model, and reasoning effort plus per-delegation overrides |
| 127 | [n0pe-sled/context-before-user](https://github.com/n0pe-sled/context-before-user) | 0 | 2026-09-13 | 2026-09-14 | dsh plugin: keep injected runtime context and skill context as user-role turns before the human request |
| 128 | [n0pe-sled/herdr-themes](https://github.com/n0pe-sled/herdr-themes) | 0 | 2026-09-13 | 2026-09-14 | dsh plugin: the 18 herdr themes as Settings > Themes with live swatch cards and persistent selection |
| 129 | [n0pe-sled/skill-mcp-manager](https://github.com/n0pe-sled/skill-mcp-manager) | 0 | 2026-09-13 | 2026-09-14 | dsh plugin: manage dsh skills and MCP servers from Settings > Skills & MCP, hot-reloaded without restarting the GUI |
| 130 | [n0pe-sled/subscription-logins](https://github.com/n0pe-sled/subscription-logins) | 0 | 2026-09-13 | 2026-09-14 | dsh plugin: store and switch ChatGPT/Claude OAuth and Z.AI Coding Plan credentials in a Logins settings page |
| 131 | [n0pe-sled/system-prompt-editor](https://github.com/n0pe-sled/system-prompt-editor) | 0 | 2026-09-13 | 2026-09-14 | dsh plugin: edit the assembled system prompt of every new session (custom text, persona, tool guidance) with live preview |
| 132 | [n0pe-sled/web-search-searxng](https://github.com/n0pe-sled/web-search-searxng) | 0 | 2026-09-13 | 2026-09-14 | dsh plugin: SEARXNG-backed web search provider for the dsh web_search tool (host-only, no Settings UI) |
| 133 | [naitoupi/dsh-outbound-proxy](https://github.com/naitoupi/dsh-outbound-proxy) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness (DSH) plugin: set a global outbound proxy from Settings |
| 134 | [new-Beginner/dsh-cliproxyapi](https://github.com/new-Beginner/dsh-cliproxyapi) | 0 | 2026-09-14 | 2026-09-14 | Native Codex and Antigravity subscription accounts inside DeepSeek Harness, based on CLIProxyAPI |
| 135 | [new-Beginner/dsh-default-prompt](https://github.com/new-Beginner/dsh-default-prompt) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness 基础默认系统提示词插件，紧跟在系统提示词之后注入，像 Codex 一样提供核心指导与全局指令 |
| 136 | [new-Beginner/dsh-diff-review-likecodex](https://github.com/new-Beginner/dsh-diff-review-likecodex) | 0 | 2026-09-14 | 2026-09-14 | Codex-like diff review plugin for DeepSeek Harness Web: interactive side-by-side diffs, compact floating dock, and turn-scoped deliverable change tracking. |
| 137 | [nguyenduclong-ict/dsh-better-uiux](https://github.com/nguyenduclong-ict/dsh-better-uiux) | 0 | 2026-09-14 | 2026-09-14 | Better UIUX for DeepSeek Harness: one Settings section with switches for live terminal output streaming and custom CSS injection |
| 138 | [nuaaweixinye/dsh-gme-workflow](https://github.com/nuaaweixinye/dsh-gme-workflow) | 0 | 2026-09-14 | 2026-09-14 | GME Test Agent workflow tools for DeepSeek Harness (dsh): pick interfaces, generate and repair tests autonomously in a local Python backend, poll until review, decide with consent. |
| 139 | [pilahito/dsh-locale-es](https://github.com/pilahito/dsh-locale-es) | 0 | 2026-09-13 | 2026-09-14 | Paquete de idioma español para la GUI web de DeepSeek Harness (DSH): 42 namespaces y 1257 cadenas traducidas |
| 140 | [PolinniZhong/dsh-visual-acceptance](https://github.com/PolinniZhong/dsh-visual-acceptance) | 0 | 2026-08-26 | 2026-09-14 | DSH 视觉验收｜AI 生成 Web 页面与 UI 原型的本地验收与复验工作台：检查页面是否按声明范围真实打开、记录可追溯的浏览器异常、按原条件复验，不替用户做最终审美判断。Local-first acceptance & retest workbench for AI-generated web UI. |
| 141 | [pureexe/dsh-vision-3090-fix](https://github.com/pureexe/dsh-vision-3090-fix) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness LLM adapter that caps images per request to 1, for self-hosted vLLM backends that reject prompts with more than one image |
| 142 | [rex178178/dsh-turnbar](https://github.com/rex178178/dsh-turnbar) | 0 | 2026-08-16 | 2026-09-14 | A progress bar for your agent conversations — in-session turn navigation with hover previews, scrub, playhead, Esc-return and ⌘K search for DeepSeek Harness |
| 143 | [Riderich/self-evolving-router-dsh](https://github.com/Riderich/self-evolving-router-dsh) | 0 | 2026-09-14 | 2026-09-14 | Self-evolving deterministic rule objects before DeepSeek Harness model calls |
| 144 | [ryanxie113/dsh-solpi](https://github.com/ryanxie113/dsh-solpi) | 0 | 2026-09-14 | 2026-09-14 | Four harness efficiency mechanisms (Action Fusion, ObservationPack, Evidence-Preserving Reducer, Online Context Compact) as a DeepSeek Harness bundle |
| 145 | [ryukirin/dsh-momo-learning](https://github.com/ryukirin/dsh-momo-learning) | 0 | 2026-09-14 | 2026-09-14 | 墨墨背单词的 DeepSeek Harness 插件：本地学习镜像 MCP 工具 + 每日出题 Skill |
| 146 | [s867968286/dsh-memory-md](https://github.com/s867968286/dsh-memory-md) | 0 | 2026-09-14 | 2026-09-14 | 简单的纯依赖MD文件的记忆插件，实现思路参考CodeBuddy和WorkBuddy的实现 |
| 147 | [sangning-h/dsh-farm-dispatch](https://github.com/sangning-h/dsh-farm-dispatch) | 0 | 2026-09-14 | 2026-09-14 | 子代理派发规范（吝啬农场主模式）全局化插件 for DeepSeek Harness — syncs cordis-async preset + AGENTS.md dispatch rules. dsh plugin add ready. |
| 148 | [sdegongzuo/dsh-webops-plugin](https://github.com/sdegongzuo/dsh-webops-plugin) | 0 | 2026-09-12 | 2026-09-14 | DeepSeek Harness 客户端网页操作与调试插件：多会话、新窗口、多标签页调试和操作网页 |
| 149 | [sdoygb/dsh-geometry-knowledge](https://github.com/sdoygb/dsh-geometry-knowledge) | 0 | 2026-09-14 | 2026-09-14 | 几何论（共扼谱几何 CSG）知识库插件 for DeepSeek Harness：纯离线 BM25 检索 251 篇文章 + 869 条真理，31 个 geo_* 工具，开箱即用。Conjugate Spectral Geometry knowledge base plugin for DSH. |
| 150 | [shengyvself/dsh-prompt-only-forge](https://github.com/shengyvself/dsh-prompt-only-forge) | 0 | 2026-09-14 | 2026-09-14 | dsh-prompt-only-forge — 点输入框右座 ✨ 把「打磨提示词」写进输入栏（当前草稿自动嵌进 <内容> 位置），不发送、不联网、不调模型 |
| 151 | [simikangtao/dsh-storyboard](https://github.com/simikangtao/dsh-storyboard) | 0 | 2026-09-14 | 2026-09-14 | Doubao-style end-of-chat storyboard card for DeepSeek Harness: lightweight, zero-dependency HTML/SVG visual summary at the end of substantive chats |
| 152 | [sueccku/dsh-plugin-wps-office-next](https://github.com/sueccku/dsh-plugin-wps-office-next) | 0 | 2026-09-12 | 2026-09-14 | 在 DeepSeek Harness（DSH）里用中文对话操作 WPS 表格 / 文字 / 演示：读写数据、排版、公式图表、批量转 PDF。自带 MCP server 与常驻 COM 宿主，免装加载项、免配环境变量。 |
| 153 | [sxylvlv/dsh-weixin-channel](https://github.com/sxylvlv/dsh-weixin-channel) | 0 | 2026-09-14 | 2026-09-14 | 微信通道插件 for DSH：把微信消息接成 DSH 会话（文本/图片/文件/语音/视频双向，出站可推文档） |
| 154 | [tabilet/tabilet-skills](https://github.com/tabilet/tabilet-skills) | 0 | 2026-09-13 | 2026-09-14 | Agentic Engineering Harness for Small to Large Projects |
| 155 | [Teow9/dsh-isolation-pod](https://github.com/Teow9/dsh-isolation-pod) | 0 | 2026-09-14 | 2026-09-14 | 隔离舱：在 DSH 主会话之外运行受沙箱约束的隔离任务；主会话默认完全无感，结果返回与文件导出都要手动确认。 |
| 156 | [thezavtrak-a11y/dsh-cost-stats](https://github.com/thezavtrak-a11y/dsh-cost-stats) | 0 | 2026-09-13 | 2026-09-14 | Money on the screen for the DeepSeek Harness web GUI: per-turn USD cost in the chat, a Cost tab with charts, ratings and an interactive spend timeline, and a local price table you control. |
| 157 | [virgoC0der/dsh-plugins](https://github.com/virgoC0der/dsh-plugins) | 0 | 2026-09-11 | 2026-09-14 | Plugins for DeepSeek Harness (DSH): a work dashboard with GitHub PRs, Jira, Calendar, and local git state |
| 158 | [vv5v5/dsh-memory-archive](https://github.com/vv5v5/dsh-memory-archive) | 0 | 2026-09-14 | 2026-09-14 | Session memory archive + prompt viewer for DeepSeek Harness: read back what compaction folded away, and inspect the prompt each turn actually sent. |
| 159 | [wangzhanchao883/dsh-lost-and-found](https://github.com/wangzhanchao883/dsh-lost-and-found) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness plugin: local file recall - watch the folders you choose, index what appeared (name/type/size/appeared-at/location/origin) into a local SQLite database, then search by keyword/time/type/folder with a live read-only fallback scan. 文件快速寻回:DSH 本地文件记忆索引,忘了文件放哪问一句就能找回;每个目录各有独立增量锚点,新加入的目录首扫回填历史;只读,绝不修改、移动或删除你的文件。 |
| 160 | [wei125775-lab/whalegirl-deskpet](https://github.com/wei125775-lab/whalegirl-deskpet) | 0 | 2026-09-14 | 2026-09-14 | 鲸鱼娘桌宠，dsh 和 Claude Code（PetPet）两个版本 —— 待机由分层 PSD 烘焙，其余动作由 AI 视频转序列帧 |
| 161 | [xby-skill/xby-audio-tag](https://github.com/xby-skill/xby-audio-tag) | 0 | 2026-09-14 | 2026-09-14 | 识别音频中的声音事件，譬如：笑声、打响指、狗叫声等。 |
| 162 | [xby-skill/xby-audio-tools](https://github.com/xby-skill/xby-audio-tools) | 0 | 2026-09-14 | 2026-09-14 | 音频处理工具集，包括：常用的语音识别，中文文字转语音、音频格式转换、降噪、为文本添加标点符号、识别音频中的声音事件。 |
| 163 | [xby-skill/xby-denoise](https://github.com/xby-skill/xby-denoise) | 0 | 2026-09-14 | 2026-09-14 | 降噪，噪声抑制。 |
| 164 | [xby-skill/xby-mp3](https://github.com/xby-skill/xby-mp3) | 0 | 2026-09-14 | 2026-09-14 | 音频文件转MP3格式。 |
| 165 | [xby-skill/xby-punctuation](https://github.com/xby-skill/xby-punctuation) | 0 | 2026-09-14 | 2026-09-14 | 为文本添加标点符号。通过语音转文本从语音获取的文本，经常不包含标点符号，可以使用此功能。 |
| 166 | [xby-skill/xby-tts-cn](https://github.com/xby-skill/xby-tts-cn) | 0 | 2026-09-14 | 2026-09-14 | 中文文字转语音。 |
| 167 | [xby-skill/xby-wav](https://github.com/xby-skill/xby-wav) | 0 | 2026-09-14 | 2026-09-14 | 音频文件转WAV格式。 |
| 168 | [Xian-JL/dsh-Kinich-theme](https://github.com/Xian-JL/dsh-Kinich-theme) | 0 | 2026-09-01 | 2026-09-14 | A Kinich-themed UI plugin for DeepSeek Harness 0.1.1-rc.2. |
| 169 | [xinghaix/deepseek-harness-desktop](https://github.com/xinghaix/deepseek-harness-desktop) | 0 | 2026-09-07 | 2026-09-14 | Minimal cross-platform desktop wrapper for DeepSeek Harness (DSH) CLI |
| 170 | [xingheyewang-1/dsh-whale-rod-cursor](https://github.com/xingheyewang-1/dsh-whale-rod-cursor) | 0 | 2026-09-14 | 2026-09-14 | 🎣 鱼竿鲸鱼娘光标 —— DSH Web 的鱼竿光标：弹性绳吊着 Q 版鲸鱼娘，随鼠标甩飞/回弹，悬停变色，甩猛了尖叫，停下演「钓鱼佬又空军了」小剧场。A fishing-rod cursor companion for the DSH Web UI. |
| 171 | [xinyang920/dsh-caps-beacon](https://github.com/xinyang920/dsh-caps-beacon) | 0 | 2026-09-14 | 2026-09-14 | Caps Lock LED status beacon for DeepSeek Harness — solid while agents work, blinking when your approval or answer is needed |
| 172 | [Yagami0502/dsh-composer-pause](https://github.com/Yagami0502/dsh-composer-pause) | 0 | 2026-09-14 | 2026-09-14 | Codex-style pause/continue button for the DeepSeek Harness web composer: stop a running turn and resume it with one click. |
| 173 | [yiyunet/dsh-dingtalk-connector](https://github.com/yiyunet/dsh-dingtalk-connector) | 0 | 2026-09-14 | 2026-09-14 | 把钉钉 AI 表格接入 DeepSeek Harness ｜ 10 个工具 + 设置面板 + 定时导出 ｜ Read & write DingTalk AI Tables from DeepSeek Harness |
| 174 | [yunxiyang/dsh-loop-continue](https://github.com/yunxiyang/dsh-loop-continue) | 0 | 2026-09-10 | 2026-09-14 | Continue a DeepSeek Harness agent turn whose model narrated its next action but called no tool. |
| 175 | [yunxiyang/dsh-wide-conversation](https://github.com/yunxiyang/dsh-wide-conversation) | 0 | 2026-09-13 | 2026-09-14 | DSH web client plugin: pins the conversation column to a configurable percentage of its width (default full width) instead of the built-in 680-920px reading measure. |
| 176 | [yuu1111/dsh-ui-cost-meter](https://github.com/yuu1111/dsh-ui-cost-meter) | 0 | 2026-09-13 | 2026-09-14 | DeepSeek Harness Web GUI plugin: real-time spend for the current session, priced from per-model token rates and shown as a pill under the composer |
| 177 | [zhang-guo-wen/dsh-drawio](https://github.com/zhang-guo-wen/dsh-drawio) | 0 | 2026-09-14 | 2026-09-14 | Standalone DeepSeek Harness plugin: preview .drawio (mxGraph XML) diagrams in the Web Sidebar.侧边栏预览流程图  .drawio文件 |
| 178 | [zhang-guo-wen/dsh-drawioedit](https://github.com/zhang-guo-wen/dsh-drawioedit) | 0 | 2026-09-14 | 2026-09-14 | DeepSeek Harness plugin: edit .drawio diagrams in the Web Sidebar ,侧边栏编辑流程图  .drawio文件 |
| 179 | [zhangzhangco/dsh-llm-antigravity](https://github.com/zhangzhangco/dsh-llm-antigravity) | 0 | 2026-09-14 | 2026-09-14 | Antigravity route for DeepSeek Harness: local Antigravity CLI (agy) as an LLM provider |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- cyanseek/dsh-landscape
- cyanseek/dsh-native-playbook
- cyanseek/dsh-tool-chaos
- drscrewdriver/dsh-session-search-toggle
- duanjiangDJ/dsh-gui
- GalaxyBatMan111/dsh-plugins
- goldgish/dsh-agent-trace
- goldgish/dsh-gamepad-approval
- huey1in/reef
- levi52/dsh-appearance
- levi52/dsh-pet
- Makoveli89/dsh-swarm
- modelbus/deepseek-harness-pro
- Phant0Meow/dsh-femo
- Robin1987China/dsh-plugin-preset-default-guard
- sdoygb/geometry-knowledge
- shinzarou-eng/dsh-codebase-chat
- tangjunyi1/dsh-remote-workspace
- weibaohui/dsh-xiuxian
- YpipaQ/dsh-skills-mcp-cli-manager
- yuu1111/dsh-cost-meter
- zhuiyueya/dsh-visionary
- zhuiyueya/dsh-voice
