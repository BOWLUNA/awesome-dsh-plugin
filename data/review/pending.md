# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-15**
- 快照日期 / Snapshot date: **2026-09-15 (UTC)**
- 待审核 / Pending: **114**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **22**
- Star 异常增长 / Star-growth alerts: **2** — 先看下方告警节 / see the alert section first

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

对比上一份快照 **2026-09-14** / vs previous snapshot **2026-09-14**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **2**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [reactive-resume/reactive-resume](https://github.com/reactive-resume/reactive-resume) | 已核准 / approved | 42958 | +105 | 4748 | 2364d | 日增百星 | 日增 +105★；已不进榜单 |
| ⚠️ [MeteorNOX/DeepSeek-Balance-Whale-Widget](https://github.com/MeteorNOX/DeepSeek-Balance-Whale-Widget) | 已核准 / approved | 2460 | +104 | 98 | 27d | 日增百星 | 日增 +104★；已不进榜单 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [wushi2333/dsh-computer-use_codex-style](https://github.com/wushi2333/dsh-computer-use_codex-style) | 14 | 2026-09-15 | 2026-09-15 | Codex-style Computer Use for DeepSeek Harness: the official window2 13-method desktop surface plus Chromium automation, a visible overlay with Esc interrupt, per-app approvals and bundled skills. Windows, MIT, no Codex required. |
| 2 | [meto-ventus/dsh-deepseek-usage](https://github.com/meto-ventus/dsh-deepseek-usage) | 9 | 2026-08-17 | 2026-09-15 | DeepSeek API 用量监测 DSH 插件：悬浮球 + 展开面板，展示开放平台真实余额、累计消费、今日消费、请求次数、Tokens 与分模型用量，支持手动登录获取 userToken。 |
| 3 | [meto-ventus/dsh-ventus-whale](https://github.com/meto-ventus/dsh-ventus-whale) | 7 | 2026-08-15 | 2026-09-15 | 🐳 蓝色大肥鱼 · DeepSeek 虎鲸 3D 桌宠插件 — 由 DeepSeek 虎鲸 logo 轮廓重建，悬浮于 Web GUI 角落：拖拽旋转、360° 转圈、爱心互动、悬停工具栏、大小/灵敏度/文字设置，配置本地持久化 / A 3D whale desktop pet rebuilt from the DeepSeek whale logo for DeepSeek Harness — drag to rotate, 360° spin, heart bursts, hover toolbar, size/sensitivity/caption settings, and local persistence. |
| 4 | [twoyoung91/dsh-memoknow](https://github.com/twoyoung91/dsh-memoknow) | 4 | 2026-09-15 | 2026-09-15 | Local personal memory and knowledge management for DeepSeek Harness. It supports local FTS, CPU-embedding or OpenAI-Compatible Embedding API. |
| 5 | [x102201/dsh-helper](https://github.com/x102201/dsh-helper) | 4 | 2026-08-25 | 2026-09-15 | 🖥️ 一台电脑并行无限 DeepSeek Harness 实例 · 🔀 每个 dsh 一个专职实例 · 🪟 同一工作区并行 · 📦 .dshpack 配置交付 |
| 6 | [Zoria-Lind/dsh-ecolink](https://github.com/Zoria-Lind/dsh-ecolink) | 4 | 2026-09-10 | 2026-09-15 | Memory ecosystem bridging the DeepSeek web app and local DSH — one local memory pool shared by a browser extension (harvest/inject), a zero-dependency local service (sole writer), and a DSH adapter (pre-step injection). |
| 7 | [huguangyu666/open-source-first-skill](https://github.com/huguangyu666/open-source-first-skill) | 2 | 2026-09-15 | 2026-09-15 | Pragmatic Anti-Wheel-Reinvention Protocol for AI Coding Agents: Research First, Open-Source Ethics, and Tokenomics Advantage. |
| 8 | [id7869/dsh-security](https://github.com/id7869/dsh-security) | 2 | 2026-09-14 | 2026-09-15 | 在 DeepSeek Harness (DSH) 内等价重建 OpenAI codex-security 安全审计能力的原生插件 |
| 9 | [meto-ventus/dsh-ventus-search](https://github.com/meto-ventus/dsh-ventus-search) | 2 | 2026-08-19 | 2026-09-15 | 🔍 Ventus 搜索 · DeepSeek Harness 多引擎搜索与正文抓取插件 — Bing/360/Bilibili 并发搜索、评分去重、正文抽取、总开关与测试按钮 / Multi-engine web search and fetch providers for DeepSeek Harness (Bing, 360, Bilibili) with scoring, dedup, readability extraction, master switch and test button. |
| 10 | [nomicore-ai/nomicore](https://github.com/nomicore-ai/nomicore) | 2 | 2026-08-18 | 2026-09-15 | A self-describing, governed data core for AI agents—schemas, authority, validation, and semantic context travel with the data. |
| 11 | [RUO-MO/DSH-Plugin](https://github.com/RUO-MO/DSH-Plugin) | 2 | 2026-09-13 | 2026-09-15 | DeepSeek Harness (DSH) 插件仓库：侧边栏内嵌网页版 DeepSeek 聊天 + Token 用量仪表盘。零侵入，本地 127.0.0.1 数据桥/反代，浏览器与桌面端通用。 |
| 12 | [sailoumili/dsh-sidebar-plus](https://github.com/sailoumili/dsh-sidebar-plus) | 2 | 2026-09-15 | 2026-09-15 | 基于 DSH 官方侧边栏的文件视图增强插件，提供源码视图、原位编辑、行号显示、搜索和字体缩放功能。  A file-view enhancement plugin that extends the official DSH sidebar, providing source view, in-place editing, line number display, search, and font zoom. |
| 13 | [0x7A7A6572/dsh-forge-studio](https://github.com/0x7A7A6572/dsh-forge-studio) | 1 | 2026-09-10 | 2026-09-15 | Aggregated dsh plugins for daily use — a dsh-plugin rewrite of Forge Studio. |
| 14 | [173787247/dsh-wsl-im](https://github.com/173787247/dsh-wsl-im) | 1 | 2026-09-14 | 2026-09-15 | dsh plugin: Feishu / WeCom aibot / DingTalk Stream / QQ Gateway bridge into dsh agents (WSL) |
| 15 | [2754LM/dsh-theme-newsprint](https://github.com/2754LM/dsh-theme-newsprint) | 1 | 2026-09-15 | 2026-09-15 | 报纸衬线 · Newsprint Serif — DSH 主题插件：暖白报纸 + 纯黑中性灰 + 衬线正文 + 报纸排版笔画 |
| 16 | [a1435473620/dsh-web-search-nokey](https://github.com/a1435473620/dsh-web-search-nokey) | 1 | 2026-09-15 | 2026-09-15 | 给 DeepSeek Harness 的免 key 搜索插件，也可以修复接 Trae / WorkBuddy 积分时 web_search 恒 401。 |
| 17 | [ArtlexYoung/dsh-super-agent](https://github.com/ArtlexYoung/dsh-super-agent) | 1 | 2026-09-12 | 2026-09-15 | 面向 DeepSeek Harness 的场景化 Agent 预设，覆盖单人交付、团队委派、方案调研和优化实验。Scenario-focused DeepSeek Harness agent presets for solo delivery, team delegation, evidence-based research, and optimization experiments. |
| 18 | [CkEFFAF/dsh-plugin-devkit](https://github.com/CkEFFAF/dsh-plugin-devkit) | 1 | 2026-09-15 | 2026-09-15 | DevKit for DeepSeek Harness plugins — runtime inspector (/debug), isolated debug-boot, host contract tests without a browser, and client slot preview. |
| 19 | [CosmoSail/DSH_Launch_Console](https://github.com/CosmoSail/DSH_Launch_Console) | 1 | 2026-09-15 | 2026-09-15 | DSH Launch Console是Deepseek Harness的桌面外壳，无需终端命令即可静默启动 DSH 服务，固定窗口显示 Web UI。DSH Launch Console is the desktop shell for Deepseek Harness. It silently starts the DSH service without terminal commands and displays the Web UI in a fixed window. |
| 20 | [destr-z/dsh-web-portable](https://github.com/destr-z/dsh-web-portable) | 1 | 2026-09-15 | 2026-09-15 | 非官方的 DSH（DeepSeek Harness）Web 界面 Windows 便携版，面向 AI 短剧/AI 视频的剧本工作流：自带「剧本批注」（小说→剧本）与「提示词对照」（剧本→视频提示词）两个成对的改稿工作台，划词写批注交给 AI 改稿。主程序走 Releases。 |
| 21 | [godv61/dsh-task-engine](https://github.com/godv61/dsh-task-engine) | 1 | 2026-09-15 | 2026-09-15 | Engineering workflow plugin for DeepSeek Harness: task stages, verification records, commit checks, and skill and rule management. |
| 22 | [JeremyWangCY/dsh-pc-pilot](https://github.com/JeremyWangCY/dsh-pc-pilot) | 1 | 2026-09-01 | 2026-09-15 | Windows computer-use runtime, CLI, and DeepSeek Harness host plugin: UIA accessibility targeting, occlusion-immune per-window capture, background synthetic input, and a persistent Chromium CDP session. |
| 23 | [MasterZ9286/dsh-plugin-followup](https://github.com/MasterZ9286/dsh-plugin-followup) | 1 | 2026-09-14 | 2026-09-15 | 划词追问：选中回答文字右键追问，问答留在按会话独立的右侧面板，并从主对话隐藏该轮（DeepSeek Harness 插件） |
| 24 | [NoMindSama/dsh-launcher](https://github.com/NoMindSama/dsh-launcher) | 1 | 2026-09-15 | 2026-09-15 | dsh web的桌面快捷启动方式 |
| 25 | [OMSociety/dsh-fishpai](https://github.com/OMSociety/dsh-fishpai) | 1 | 2026-09-14 | 2026-09-15 | 公众号排版工作台，长在 DeepSeek Harness 的右侧栏里。 人在侧栏改字、加批注与占位；模型用块级 diff 看懂你改了什么、想要什么；成品仍由你复制粘贴进公众号编辑器。 |
| 26 | [polaris-smart/dsh-agent-mailbox](https://github.com/polaris-smart/dsh-agent-mailbox) | 1 | 2026-09-15 | 2026-09-15 | dsh (DeepSeek Harness) 跨 agent 信箱插件：mailbox_send/check/reply/list/done/broadcast + task_create/list，桥接 agent-mailbox，零依赖 Node 22 |
| 27 | [PolinniZhong/dsh-knit](https://github.com/PolinniZhong/dsh-knit) | 1 | 2026-09-15 | 2026-09-15 | Agent 一天产出 20 篇文档，你找不到刚才那篇。 Knit 把它们放到对话旁边 —— 你正在聊什么，相关的那篇就在最上面。 |
| 28 | [qingli-sketch/dsh-preset-agent-manager](https://github.com/qingli-sketch/dsh-preset-agent-manager) | 1 | 2026-09-15 | 2026-09-15 | Preset agent manager for DeepSeek Harness: a sidebar admin panel and the preset_agent_dispatch tool, with strict per-agent plugin whitelists and isolated child sessions. |
| 29 | [siruignaw-sys/dsh-tool-bandit-search](https://github.com/siruignaw-sys/dsh-tool-bandit-search) | 1 | 2026-08-16 | 2026-09-15 | A DeepSeek Harness plugin that replaces the standard web_search tool with a search tool that learns which search strategy to use through a contextual multi-armed bandit, instead of relying on a single hardcoded approach. |
| 30 | [snhna-a/dsh-reactor](https://github.com/snhna-a/dsh-reactor) | 1 | 2026-09-09 | 2026-09-15 | Event-Condition-Action (ECA) automation plugin for DeepSeek Harness: turns your agent into a proactive watchdog with polling/push event sources, condition evaluation, and composable actions. |
| 31 | [trynewthin/dsh-left-panel](https://github.com/trynewthin/dsh-left-panel) | 1 | 2026-09-15 | 2026-09-15 | Git worktree-aware workspace browser for the DeepSeek Harness Web sidebar: repositories group their worktrees, and worktree workspaces are registered and unregistered automatically. |
| 32 | [yeastcloud/dsh-anchor](https://github.com/yeastcloud/dsh-anchor) | 1 | 2026-09-15 | 2026-09-15 | ⚓ 定锚 · Anchor — DeepSeek Harness 会话指令定锚插件：为会话注入可自由组合的指令，并在压缩或长会话后自动重锚同一段原文 |
| 33 | [1998moye/dsh-plugin-usage](https://github.com/1998moye/dsh-plugin-usage) | 0 | 2026-09-15 | 2026-09-15 | DSH（DeepSeek Harness）Web 用量与费用看板插件：余额、今日/本周/本月/累计消费、API 请求次数、token 明细与趋势图，按 DeepSeek 官方峰谷价估算，数据从本地会话日志全量重建 |
| 34 | [Acoder416/dsh-plugin-workbuddy-gateway](https://github.com/Acoder416/dsh-plugin-workbuddy-gateway) | 0 | 2026-09-15 | 2026-09-15 | Use a WorkBuddy subscription as a model provider in DSH: supervises the local OpenAI-compatible gateway and manages it from the settings page. |
| 35 | [Alfred-Lau/OPC-Fellows](https://github.com/Alfred-Lau/OPC-Fellows) | 0 | 2026-09-15 | 2026-09-15 | OPC-Fellows — local-first workbench for a one-person company. Kernel + occupation plugins on DeepSeek Harness / Cordis. |
| 36 | [amwangfan/dsh-privacy-guard](https://github.com/amwangfan/dsh-privacy-guard) | 0 | 2026-09-15 | 2026-09-15 | DSH Web 隐私脱敏守护插件：状态监控看板、出网泄密探测沙箱与网关路由管理（配合 Privacy Gateway） |
| 37 | [antonio-mastropaolo/dsh-anthropic-membership](https://github.com/antonio-mastropaolo/dsh-anthropic-membership) | 0 | 2026-09-15 | 2026-09-15 | DeepSeek Harness plugin: Sign in with Claude Pro/Max (no API key). Caps Anthropic images at 2000px and slims /compact for 1M context. |
| 38 | [anweat/dsh-substrate](https://github.com/anweat/dsh-substrate) | 0 | 2026-08-25 | 2026-09-15 | A conflict-resolution substrate for the DeepSeek Harness plugin ecosystem, with the measurements it is built on. |
| 39 | [ArcaneOrion/dsh-tavily-web](https://github.com/ArcaneOrion/dsh-tavily-web) | 0 | 2026-09-14 | 2026-09-15 | DSH Tavily plugin: key-pooled web search (tavily_search) + page fetch (web_fetch) |
| 40 | [ArcaneOrion/dsh-teaching-board](https://github.com/ArcaneOrion/dsh-teaching-board) | 0 | 2026-09-05 | 2026-09-15 | DSH in-session panel view: agent HTML projected into a sandboxed iframe |
| 41 | [Aztech-Lab/dsh-3301](https://github.com/Aztech-Lab/dsh-3301) | 0 | 2026-09-13 | 2026-09-15 | LAN entry for the DSH Web GUI on port 3301. |
| 42 | [bobobo2026/dsh-workspace-promote](https://github.com/bobobo2026/dsh-workspace-promote) | 0 | 2026-09-15 | 2026-09-15 | DSH host plugin: promote the workspace you just submitted a task in to the top of the sidebar — once per submission, never during task execution. \| 提交任务时把该工作区置顶，任务执行期间不重排。 |
| 43 | [BreakFree003/dsh-clinepass-deepseekv4.1](https://github.com/BreakFree003/dsh-clinepass-deepseekv4.1) | 0 | 2026-09-15 | 2026-09-15 | Cline Pass for DeepSeek Harness (dsh): one pi-ai provider route pinned to the DeepSeek upstream channel, key entered on Settings → Models. Share-only snapshot — 分享性质，非长期维护。 |
| 44 | [bycall/dsh-engineer-tools](https://github.com/bycall/dsh-engineer-tools) | 0 | 2026-09-15 | 2026-09-15 | Engineering work-tools for DeepSeek Harness: a scoped git runner and a package-manager (npm/pnpm/yarn/bun) runner with structured output, plus an easy template to add more tools. |
| 45 | [citisen/dsh-font](https://github.com/citisen/dsh-font) | 0 | 2026-09-15 | 2026-09-15 | DeepSeek Harness plugin: customize the Web GUI fonts (interface font, code font, and font sizes) from Settings |
| 46 | [dangxinxing090-svg/dsh-plugin-plain-slides](https://github.com/dangxinxing090-svg/dsh-plugin-plain-slides) | 0 | 2026-09-15 | 2026-09-15 | A DeepSeek Harness plugin that turns each agent reply into a short slide deck in plain language — for people who use the harness but do not read code. |
| 47 | [davidekingsss/dsh-screen-eye](https://github.com/davidekingsss/dsh-screen-eye) | 0 | 2026-09-15 | 2026-09-15 | Autonomous screen vision for DeepSeek Harness on macOS: the agent captures the screen and receives the image itself in one call. |
| 48 | [DYF-zs/dsh-qboson-ising-solver](https://github.com/DYF-zs/dsh-qboson-ising-solver) | 0 | 2026-09-15 | 2026-09-15 | A DeepSeek Harness Agent Tool for solving Ising problems with QBoson Kaiwu/SPQC. |
| 49 | [EmotionG/dsh-llm-config](https://github.com/EmotionG/dsh-llm-config) | 0 | 2026-09-13 | 2026-09-15 | 为解决dsh导入订阅后配置模型的思考强度等问题而创建的插件 |
| 50 | [enterhalf/dsh-session-colorful-unread-pin-jobs](https://github.com/enterhalf/dsh-session-colorful-unread-pin-jobs) | 0 | 2026-09-15 | 2026-09-15 | Colors every session title in the DSH sidebar by state — unread (blue running / green done), pinned (yellow), live background shell jobs (purple) — composed into one gradient; plus a "Model updated" sort mode and an unread settings section. |
| 51 | [EPCN-fla/dsh-custom-headers](https://github.com/EPCN-fla/dsh-custom-headers) | 0 | 2026-09-15 | 2026-09-15 | Per-model custom request headers for DeepSeek Harness: define named header profiles in Settings → Plugins → Plugin configuration, pick one per model in the provider's model catalog, and every call to that model carries those headers. |
| 52 | [Eray114514/dsh-find-plugins](https://github.com/Eray114514/dsh-find-plugins) | 0 | 2026-09-15 | 2026-09-15 | Find DSH plugins across several community catalogs, ranked by relevance × trust × freshness instead of stars alone. 跨多个社区目录查找 DeepSeek Harness 插件，按相关度 × 可信度 × 新鲜度排序，而不是只看 star。 |
| 53 | [ewoowe/dsh-session-messages-plugin](https://github.com/ewoowe/dsh-session-messages-plugin) | 0 | 2026-09-12 | 2026-09-15 | Searchable message overlay for DSH sessions: jump to any loaded message with the keyboard. |
| 54 | [ewoowe/dsh-session-usage-plugin](https://github.com/ewoowe/dsh-session-usage-plugin) | 0 | 2026-09-15 | 2026-09-15 | Session usage view: tokens, wall time and cache share per model and per turn, as a conversation view. |
| 55 | [FireOpalus/dsh-laa](https://github.com/FireOpalus/dsh-laa) | 0 | 2026-09-12 | 2026-09-15 | LAA：峰时停止运行，谷时继续运行的开关 |
| 56 | [GIN0076/dsh-bg-changer](https://github.com/GIN0076/dsh-bg-changer) | 0 | 2026-09-15 | 2026-09-15 | DeepSeek Harness 背景图插件：上传图片 + 布局裁剪 + 不透明度/模糊/暗化 + 界面半透明；零依赖零构建，含一键装回脚本 |
| 57 | [GooDAnDReaDY/dsh-model-search](https://github.com/GooDAnDReaDY/dsh-model-search) | 0 | 2026-09-03 | 2026-09-15 | DSH web plugin: searchable model selector for DeepSeek Harness WebUI |
| 58 | [hoyyang/dsh-plan-board](https://github.com/hoyyang/dsh-plan-board) | 0 | 2026-09-15 | 2026-09-15 | 思维导图式项目规划可视 + 最强防跑偏：计划→模块→任务树/DAG、执行序号、Agent GPS 站位、改图人审门、git 交叉核对、阻断级漂移防护（DeepSeek Harness 插件） |
| 59 | [huguangyu666/dsh-plugin-ai-gateway](https://github.com/huguangyu666/dsh-plugin-ai-gateway) | 0 | 2026-09-13 | 2026-09-15 | DeepSeek Harness 插件：AI 聚合网关可视化控制台——集成 Google Antigravity 与 OpenAI Codex 反代、多账号轮换池、5h/周额度看板与故障转移。 |
| 60 | [imchangchang/dsh-llm-provider](https://github.com/imchangchang/dsh-llm-provider) | 0 | 2026-09-15 | 2026-09-15 | dsh LLM provider plugin: self-maintained pi-ai bridge, model selector, provider quota/billing and settings UI for DeepSeek Harness |
| 61 | [jackchen13755/dsh-memory-core](https://github.com/jackchen13755/dsh-memory-core) | 0 | 2026-09-15 | 2026-09-15 | DSH 记忆插件：零依赖免构建，SQLite 事实源 + Markdown 快照 |
| 62 | [jiumengya/dsh-knowledge-suite](https://github.com/jiumengya/dsh-knowledge-suite) | 0 | 2026-09-15 | 2026-09-15 | English: DeepSeek Harness knowledge (document library) capability plugin suite - six packages, install/uninstall individually, idempotent, offline verification scripts and fixtures. Chinese: DeepSeek Harness 资料库知识能力插件套件 - 六个包可单独装卸，install/uninstall 幂等，含离线验证脚本与夹具 |
| 63 | [jonah791/computer-use](https://github.com/jonah791/computer-use) | 0 | 2026-09-15 | 2026-09-15 | DSH computer-use 插件：让 agent 自己看屏幕、自己操作鼠标键盘（截屏/窗口/鼠标/键盘 6 工具），用于自主开发-验证-迭代闭环 |
| 64 | [jonah791/dsh-prompt-defense](https://github.com/jonah791/dsh-prompt-defense) | 0 | 2026-09-15 | 2026-09-15 | DSH 提示词注入防御：外部内容标记 + 注入特征检测 + 危险动作人审门控 + 审计侧车 |
| 65 | [kevin9327/dsh-hwp](https://github.com/kevin9327/dsh-hwp) | 0 | 2026-09-15 | 2026-09-15 | DeepSeek Harness plugin: read Korean Hangul .hwp (HWP 5.x) and .hwpx documents as Markdown or text, with no native binaries |
| 66 | [kiterunner1/dsh-attention-beep](https://github.com/kiterunner1/dsh-attention-beep) | 0 | 2026-09-15 | 2026-09-15 | DSH 插件：任务结束或命令卡死时用本机人声提醒，自动中断卡住的 pwsh 调用并把「怎么继续」写回工具结果，并在 spawn 之前拦掉已知的性能陷阱写法。仅 Windows。 / Beeps + stuck-command watchdog + command guard for DeepSeek Harness. Windows only. |
| 67 | [kiterunner1/dsh-plugin-audit](https://github.com/kiterunner1/dsh-plugin-audit) | 0 | 2026-09-15 | 2026-09-15 | Agent Skill for DeepSeek Harness (DSH)：装第三方插件前的静态安全审计 —— 扫出 eval、patch 层 !!js、安装期脚本、开机自启、凭据复制、出网域名与提示词注入面。Audit third-party DSH plugins before installing. Works with DSH, Claude Code, Codex, Cursor & any Agent Skills compatible agent. |
| 68 | [kovey/dsh-memory](https://github.com/kovey/dsh-memory) | 0 | 2026-09-15 | 2026-09-15 | Layered memory plugin for DeepSeek Harness: strictly separated project/global memory, host-driven recall before tasks and continuous learning after them. |
| 69 | [lau4tin1/dsh-skill-router](https://github.com/lau4tin1/dsh-skill-router) | 0 | 2026-09-14 | 2026-09-15 | An automatic skill router for deepseek harness |
| 70 | [LAwLi3tCoding/dsh-approval-review](https://github.com/LAwLi3tCoding/dsh-approval-review) | 0 | 2026-09-15 | 2026-09-15 | Codex-style agent auto-approval for DeepSeek Harness: an independent reviewer model decides allow/deny on the approval answerer chain, fail-closed, with a rationale for every decision (refusals and allows) in a dedicated Approvals tab. · 替我审批：独立复核模型裁决，fail-closed，每次审批留详细理由。 |
| 71 | [LeeLee592/dsh-obsidian-plugin](https://github.com/LeeLee592/dsh-obsidian-plugin) | 0 | 2026-09-12 | 2026-09-15 | Provides DeepSeek Harness (DSH) agents with Obsidian plugin development capabilities: scaffolding, validation, version syncing, plus a development-guidelines skill. |
| 72 | [leolee9086/dsh-computer-use](https://github.com/leolee9086/dsh-computer-use) | 0 | 2026-09-15 | 2026-09-15 | Independent cross-platform desktop computer-use plugins for DeepSeek Harness (region capture via a bundled native helper) |
| 73 | [Li-Mingshuang/dsh-audio-control](https://github.com/Li-Mingshuang/dsh-audio-control) | 0 | 2026-08-22 | 2026-09-15 | DSH(DeepSeek Harness)插件:在 Web 界面直接控制 Windows 音频 —— 播放/暂停/切歌/音量/静音 \| DSH plugin: control Windows audio from the Web UI (play/pause/next/volume/mute) |
| 74 | [liangz2210-lgtm/dsh-openclaude-ecosystem](https://github.com/liangz2210-lgtm/dsh-openclaude-ecosystem) | 0 | 2026-09-15 | 2026-09-15 | Register OpenClaude as a named subagent provider on DeepSeek Harness: task graph, exit-code classification, stall watchdog with auto-resume. Experimental — no real delegation has completed yet. |
| 75 | [liceses/dsh-ds-tts](https://github.com/liceses/dsh-ds-tts) | 0 | 2026-09-15 | 2026-09-15 |  用 DeepSeek 官方朗读音色朗读 / 导出 / 接口化 |
| 76 | [lin-strive/deepseek-harness-enterprise](https://github.com/lin-strive/deepseek-harness-enterprise) | 0 | 2026-09-14 | 2026-09-15 | Enterprise deployment template for DeepSeek Harness |
| 77 | [liujuntao123/dsh-mobile-keys](https://github.com/liujuntao123/dsh-mobile-keys) | 0 | 2026-09-15 | 2026-09-15 | DSH 移动端热键模式插件：自动检测移动端，Ctrl+Enter 发送 / Enter 换行；设置面板开关。Mobile hotkey mode plugin for DeepSeek Harness. |
| 78 | [liyixuan201211/dsh-audio-read](https://github.com/liyixuan201211/dsh-audio-read) | 0 | 2026-09-15 | 2026-09-15 | 让 AI Agent 听懂音频：转写、鸟种识别、语音情感、环境声与音乐分析。全部本地运行，不用大模型。DeepSeek Harness 技能。 |
| 79 | [lizhuangCoding/dsh-chicken-pet](https://github.com/lizhuangCoding/dsh-chicken-pet) | 0 | 2026-09-15 | 2026-09-15 | 🐔 A pixel chicken desktop pet for DeepSeek Harness — naps, paces, pecks and spins a basketball on its own, and reacts to your agent's work. Original procedurally-generated pixel art, no third-party assets. |
| 80 | [masknull/dsh-delete-session](https://github.com/masknull/dsh-delete-session) | 0 | 2026-09-15 | 2026-09-15 | DSH 插件：在侧栏会话行的 ⋯ 菜单中增加「删除会话」（永久删除，不可恢复），不接管也不禁用任何官方插件行。 \| DSH plugin: add a permanent "delete session" action to the sidebar session row menu, with zero official-row takeover. |
| 81 | [masknull/dsh-sidebar-ratio](https://github.com/masknull/dsh-sidebar-ratio) | 0 | 2026-09-15 | 2026-09-15 | DSH 插件：侧边栏按窗口比例打开（左栏默认 14%、右栏可选），同一父会话组内共享右侧栏面板。 \| DSH plugin: sidebar widths as a window ratio, plus one shared right panel across a parent session group. |
| 82 | [Moleitau-WorldSaver/dsh-strata-custom](https://github.com/Moleitau-WorldSaver/dsh-strata-custom) | 0 | 2026-09-15 | 2026-09-15 | 在长对话里找回你问过的每一句话：历史提问面板 + 等比会话地图，鼠标一停列出全部提问，点一下跳回那一轮。Prompt-history minimap for the DeepSeek Harness Web GUI. Customized derivative of jsdvjx/dsh-strata (MIT). |
| 83 | [MoriTang/dsh-neubrutalism-theme](https://github.com/MoriTang/dsh-neubrutalism-theme) | 0 | 2026-09-06 | 2026-09-15 | Neubrutalism Web UI theme plugin for DeepSeek Harness |
| 84 | [Nerdless-ship-it/dsh-adversarial-roundtable](https://github.com/Nerdless-ship-it/dsh-adversarial-roundtable) | 0 | 2026-09-12 | 2026-09-15 | 多模型圆桌会议编排：四席协作 + 独立验收，开会前先向用户确认阵容（DeepSeek Harness 插件） |
| 85 | [nmhwsygxb/dsh-tools](https://github.com/nmhwsygxb/dsh-tools) | 0 | 2026-09-13 | 2026-09-15 | DeepSeek Harness 工具包：自选组件一键安装（远程执行/执行前自动审核/GitHub/联网研究/本地git发布/沙箱逃生/Bug知识库/Blender/上下文压缩/自愈启动器）。组件独立、无个人信息、凭据安装时输入。 |
| 86 | [OoJae/dsh-technocore-watch](https://github.com/OoJae/dsh-technocore-watch) | 0 | 2026-09-14 | 2026-09-15 | Unofficial DeepSeek Harness plugin that watches Technocore rooms and wakes sessions (flop-labs/technocore-chat#765). Not affiliated with FLOP Labs. |
| 87 | [Paloma966/dsh-thesis](https://github.com/Paloma966/dsh-thesis) | 0 | 2026-08-16 | 2026-09-15 | 毕业论文全流程 DSH 插件 |
| 88 | [pgjh/dsh-model-metadata](https://github.com/pgjh/dsh-model-metadata) | 0 | 2026-09-15 | 2026-09-15 | DSH plugin: match custom-gateway models to the model metadata they should have (context window, output cap, reasoning levels, vision) by bare model name — nothing written to your settings |
| 89 | [raphael-y7/dsh-desktop-statusbar](https://github.com/raphael-y7/dsh-desktop-statusbar) | 0 | 2026-09-15 | 2026-09-15 | 把 DSH 桌面端底部的统计行换成可配置状态栏：10 个字段可选可排序，按 DeepSeek 官方峰谷口径估算费用，支持自定义模型单价与账户余额。非商业许可。 |
| 90 | [Saretheya/dsh-settings-nav-order](https://github.com/Saretheya/dsh-settings-nav-order) | 0 | 2026-09-15 | 2026-09-15 | Long-press and drag to reorder the DeepSeek Harness settings panel nav. Order is saved in the plugin's own folder; nothing is written to settings.yaml, and uninstalling restores the original order. |
| 91 | [saya-ch/dsh-amadeus](https://github.com/saya-ch/dsh-amadeus) | 0 | 2026-08-30 | 2026-09-15 | Amadeus — DSH Galgame Mode + 独立移动端 APP |
| 92 | [SiriusWJ/dsh-skill-manager](https://github.com/SiriusWJ/dsh-skill-manager) | 0 | 2026-09-15 | 2026-09-15 | DSH Web 本地技能管理插件：在设置的插件配置页启用或禁用技能 |
| 93 | [sra-research/self-evolving-router-dsh](https://github.com/sra-research/self-evolving-router-dsh) | 0 | 2026-09-14 | 2026-09-15 | Self-evolving deterministic rule objects before DeepSeek Harness model calls |
| 94 | [tearslee/dsh-workbuddy2api](https://github.com/tearslee/dsh-workbuddy2api) | 0 | 2026-09-15 | 2026-09-15 | DeepSeek Harness (dsh) plugin: supervise a workbuddy2api gateway process and auto-register its models as an LLM provider |
| 95 | [TiChuXiXi/dsh-git-vcs](https://github.com/TiChuXiXi/dsh-git-vcs) | 0 | 2026-09-14 | 2026-09-15 | DSH Web GUI 的 Git 版本管理插件：右侧栏新增「版本管理」页，功能与界面参照 IntelliJ IDEA 的 Version Control 工具窗（本地变更 / 提交 / 历史 / 分支 / 命令 / 贮藏）。 |
| 96 | [Tisitan/dsh-tool-guard](https://github.com/Tisitan/dsh-tool-guard) | 0 | 2026-09-15 | 2026-09-15 | Preset-agnostic global tool masking for DeepSeek Harness — presentation-layer filtering, execution-layer guard veto, self-protection gate and a WebUI editor. |
| 97 | [turnwire/turnwire](https://github.com/turnwire/turnwire) | 0 | 2026-09-09 | 2026-09-15 | Self-hosted agent sessions across terminal, browser and phone. Continue tasks and handle approvals remotely through local access, temporary or named tunnels, or your own encrypted Relay. Powered by DeepSeek Harness; model credentials stay on your host. |
| 98 | [u9521/dsh-cust-search](https://github.com/u9521/dsh-cust-search) | 0 | 2026-09-15 | 2026-09-15 | Custom Web Search plugin for DeepSeek Harness (DSH), replacing web-search-deepseek with multi-engine sequential fallback. |
| 99 | [udisyue/dsh-update](https://github.com/udisyue/dsh-update) | 0 | 2026-09-15 | 2026-09-15 | a plugin for update deepseek harness by one click |
| 100 | [unsiscon/dsh-novel-launcher](https://github.com/unsiscon/dsh-novel-launcher) | 0 | 2026-09-15 | 2026-09-15 | 在 DSH 界面放一个悬浮球：点开本地书单，用你自己的阅读器打开，窗口自动归位。 |
| 101 | [Webificio/dsh-deepseek-cost-watch](https://github.com/Webificio/dsh-deepseek-cost-watch) | 0 | 2026-09-15 | 2026-09-15 | DeepSeek off-peak alert, account balance and live Session cost estimate for the DeepSeek Harness Web UI |
| 102 | [weimingyu9312/DSHSwitch](https://github.com/weimingyu9312/DSHSwitch) | 0 | 2026-09-14 | 2026-09-15 | DSH 插件 — 在 DSH Web GUI 聊天输入框左侧添加可自定义的 switch 快捷按钮。 |
| 103 | [windrover/dsh-minimal-UI-panels](https://github.com/windrover/dsh-minimal-UI-panels) | 0 | 2026-08-28 | 2026-09-15 | Four right-Sidebar panels for the DeepSeek Harness web client — artifacts, long-term memory, terminal and notes — paired two per tab with a draggable split. |
| 104 | [wyzh0117/dsh-notebook](https://github.com/wyzh0117/dsh-notebook) | 0 | 2026-09-13 | 2026-09-15 | DSH sidebar notebook: titles + bodies, inline images (videos rejected), click a title to copy its body, @-reference notes from the composer, and a per-session auto-open sidebar. |
| 105 | [wyzh0117/dsh-port-manager](https://github.com/wyzh0117/dsh-port-manager) | 0 | 2026-09-15 | 2026-09-15 | Native DSH sidebar app: every listening port on this machine, the app behind it, and one-click port actions. |
| 106 | [xiazhi88/dsh-lan](https://github.com/xiazhi88/dsh-lan) | 0 | 2026-09-15 | 2026-09-15 | 把只监听 127.0.0.1 的 dsh web 暴露到局域网，并带上移动端适配 —— 一个包，手机连上就能用（DeepSeek Harness 插件） |
| 107 | [xoykor/dsh-searxng](https://github.com/xoykor/dsh-searxng) | 0 | 2026-09-15 | 2026-09-15 | Unofficial DSH context guard and SearXNG search adapter maintained by xoykor |
| 108 | [xrn1997/dsh-novel](https://github.com/xrn1997/dsh-novel) | 0 | 2026-09-14 | 2026-09-15 | 嵌入一个小说阅读功能，防止打瞌睡 |
| 109 | [Xstone1129/dsh-model-search](https://github.com/Xstone1129/dsh-model-search) | 0 | 2026-09-15 | 2026-09-15 | dsh-plugin |
| 110 | [yeruizhi/dsh-ask-user-timeout](https://github.com/yeruizhi/dsh-ask-user-timeout) | 0 | 2026-08-18 | 2026-09-15 | Guard plugin for DeepSeek Harness: bounded lifetime for ask_user_question — stops the no-tab-renders-question infinite hang |
| 111 | [yixiuzhemu/MCP-Manager](https://github.com/yixiuzhemu/MCP-Manager) | 0 | 2026-09-11 | 2026-09-15 | MCP-Server管理 |
| 112 | [YJLTF/dsh-animation-studio](https://github.com/YJLTF/dsh-animation-studio) | 0 | 2026-09-14 | 2026-09-15 | 给 DeepSeek Harness（DSH）做的教学动画制作工作台插件：一套内置在教学会话里的"教学视频 agent"。 |
| 113 | [youdotcom-oss/dsh-plugin-youcom](https://github.com/youdotcom-oss/dsh-plugin-youcom) | 0 | 2026-09-14 | 2026-09-15 | You.com search + fetch provider plugin for DeepSeek Harness (dsh), plus a research-focused agent preset |
| 114 | [zhitiaojun/dsh-auto-git](https://github.com/zhitiaojun/dsh-auto-git) | 0 | 2026-09-14 | 2026-09-15 | dsh profile bundle: git init every newly registered DSH workspace, with one empty commit, so git-aware plugins have a repository to attach to. |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- ArcaneOrion/dsh-stage-panel
- EmotionG/model-import
- ewoowe/session-messages-plugin
- freedomkk-qfeng/dsh-mail-assistant
- freedomkk-qfeng/dsh-oidc
- haiyoucuv/dsh-model-provider-label
- HanzhiOvO/deepseek-harness-shell
- hyperion2144/dsh-subagent-pro
- ismoss/dsh-harness-zh-l10n
- Lee-Si-Yoon/dsh-llm-friendli
- liangyou09/lyshell
- mmzm0808/dsh-deepseek-usage
- mmzm0808/dsh-ventus-search
- mmzm0808/dsh-ventus-whale
- Paloma966/dsh-paper
- qingli-sketch/dsh-ui-kit
- RUO-MO/dsh-deepseek-web
- VviLliAm-qwq/dshtui-format-setting
- welltop-jim-wang/nomicore
- wendou-chen/dsh_image-modlens-bridge
- x102201/deepseek-harness-helper
- Y1fe1Zh0u/dsh-doudizhu
