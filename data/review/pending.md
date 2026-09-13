# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-13**
- 快照日期 / Snapshot date: **2026-09-13 (UTC)**
- 待审核 / Pending: **136**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **18**
- Star 异常增长 / Star-growth alerts: **3** — 先看下方告警节 / see the alert section first

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

对比上一份快照 **2026-09-12** / vs previous snapshot **2026-09-12**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **3**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [Tiger3807861189/J-Space-Cognition-Suite](https://github.com/Tiger3807861189/J-Space-Cognition-Suite) | 待审 / pending | 3011 | +0 | 219 | 52d | 待审高星 | 核准即 Top 4 |
| ⚠️ [sopaco/deepwiki-rs](https://github.com/sopaco/deepwiki-rs) | 待审 / pending | 2650 | — | 262 | 372d | 待审高星 | 核准即 Top 5 |
| ⚠️ [reactive-resume/reactive-resume](https://github.com/reactive-resume/reactive-resume) | 已核准 / approved | 42708 | +182 | 4728 | 2362d | 日增百星 | 日增 +182★；已不进榜单 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [Tiger3807861189/J-Space-Cognition-Suite](https://github.com/Tiger3807861189/J-Space-Cognition-Suite) ⚠️ | 3011 | 2026-07-22 | 2026-09-13 | J-Space Cognition Suite V3.7 - AI cognitive-enhancement Skills based on Anthropic's J-space global workspace research. \| 哔哩哔哩：Tiger380 (UID 3494375382321675) — https://space.bilibili.com/3494375382321675 |
| 2 | [sopaco/deepwiki-rs](https://github.com/sopaco/deepwiki-rs) ⚠️ | 2650 | 2025-09-05 | 2026-09-13 | Turn code into clarity. Generate accurate technical docs and AI-ready context in minutes—perfectly structured for human teams and intelligent agents. |
| 3 | [Nyasers/DSHana](https://github.com/Nyasers/DSHana) | 48 | 2026-08-14 | 2026-09-13 | DSHana: DeepSeek Harness as a subagent for HanaAgent |
| 4 | [ManoloRemiddi/augmentor-dsh-extension-plugin](https://github.com/ManoloRemiddi/augmentor-dsh-extension-plugin) | 21 | 2026-08-24 | 2026-09-13 | Chromium side panel and browser control for DeepSeek Harness. Includes the plugin, extension and native host. |
| 5 | [startnewlabs/dsh-history](https://github.com/startnewlabs/dsh-history) | 15 | 2026-08-17 | 2026-09-13 | Quickly view, search, and jump to all the messages you sent in a long conversation. |
| 6 | [YanKaFei/kitten-punch-screenwriting](https://github.com/YanKaFei/kitten-punch-screenwriting) | 4 | 2026-08-18 | 2026-09-13 | kitten-punch-screenwriting，是生产级中文编剧创作与剧本诊断系统，覆盖概念超短片、短片、电影长片、剧集/连续剧与竖屏短剧/微短剧。内置主角驱动因果、场景价值转折、潜台词、中文去AI味、故事状态机、人物知识边界、关系连续性、承诺-兑现机制、14道证据式QC、单调修复与长篇记忆快照，支持从零开发、续写、改戏、对白打磨与剧本医生诊断。 |
| 7 | [corrinehu/dsh-buddy-checkin](https://github.com/corrinehu/dsh-buddy-checkin) | 2 | 2026-09-12 | 2026-09-13 | DSH 启动时自动为 WorkBuddy 国内版账号完成每日签到。Automatic daily check-in for all WorkBuddy CN accounts on this machine, every time DSH starts. |
| 8 | [dugujun3-cloud/dsh-wallpaper](https://github.com/dugujun3-cloud/dsh-wallpaper) | 2 | 2026-09-02 | 2026-09-13 | DSH web plugin: whole-app background wallpaper - local library, wallhaven online search, local import, right-click actions |
| 9 | [ManoloRemiddi/dsh-model-picker-augmented](https://github.com/ManoloRemiddi/dsh-model-picker-augmented) | 2 | 2026-08-30 | 2026-09-13 | Search, pin and hide models in DeepSeek Harness; refresh provider catalogues. |
| 10 | [Phant0Meow/dsh-femo](https://github.com/Phant0Meow/dsh-femo) | 2 | 2026-08-28 | 2026-09-13 | dsh-FEMO (Flow Emerges Opus) — dsh 插件版多智能体剧本引擎：Femo 会话、聊天窗口角色气泡、剧本控制（含完整引擎，整个文件夹搬走即用）。Private until scrub review. |
| 11 | [vlln/dsh-autofork](https://github.com/vlln/dsh-autofork) | 2 | 2026-09-13 | 2026-09-13 | Agent 忙时自动分叉会话：你新发的指令立刻在新会话里得到响应，旧会话留在后台跑完并把结果回注（DeepSeek Harness 插件） |
| 12 | [wwwangzilin/dsh-character-presets](https://github.com/wwwangzilin/dsh-character-presets) | 2 | 2026-09-12 | 2026-09-13 | DSH 角色预设集：10 个角色共用一套六层情感引擎——露娜 / 小喵 / 绯音 / 凛 / 芽衣 / 白夜 / 阿尔玛 / 小铃 / 三千代 / 灰 |
| 13 | [Across2005/harness-self-evolution-plugin](https://github.com/Across2005/harness-self-evolution-plugin) | 1 | 2026-09-04 | 2026-09-13 | DeepSeek Harness 全盘自进化升级插件 v2.4.0: 扫描/监控/识别/提案/审批/执行六段闭环 + DSH subagent 真实集成（task DAG 编排协议）; MoonBit native 重写, 422 测试全过（347 MoonBit + 75 legacy-ts）。 |
| 14 | [cq-guojia/dsh-session-title-pattern](https://github.com/cq-guojia/dsh-session-title-pattern) | 1 | 2026-09-12 | 2026-09-13 | 自动管理 dsh 会话标题，统一成「日期｜类型｜主题」的格式：类型与主题由模型对整段对话总结。 |
| 15 | [eteced/memoplus4dsh](https://github.com/eteced/memoplus4dsh) | 1 | 2026-08-31 | 2026-09-13 | 一个 Agent，一整份记忆——不拆散，不分割，如人的记忆一般完整连续。One agent, one whole memory — undivided, unbroken, as memory was meant to be. memoplus4dsh 是 deepseek-harness 的统一长期记忆插件。memoplus4dsh is the unified long-term memory plugin for deepseek-harness.  |
| 16 | [liuliyisui/dsh-background](https://github.com/liuliyisui/dsh-background) | 1 | 2026-09-13 | 2026-09-13 | DeepSeek Harness Web GUI 的自定义背景插件：图片 / 动图 / 视频 / 内置极光渐变，磨砂玻璃质感，配浮动控制面板 |
| 17 | [MarchLiu/dsh-graft](https://github.com/MarchLiu/dsh-graft) | 1 | 2026-09-02 | 2026-09-13 | DSH session grafting plugin: read, export, fork and forward DSH session log slices as agent tools (graft_sessions/graft_read/graft_export/graft_fork/graft_forward/graft_search) |
| 18 | [MichengAI/dsh-codex-pet](https://github.com/MichengAI/dsh-codex-pet) | 1 | 2026-09-09 | 2026-09-13 | DSH Codex Pet — 为 DeepSeek Harness 提供宠物陪伴、多任务提醒与交互，以及 Skill 自定义宠物 · A pet companion with multi-task notifications, interactions, and Skill-based custom pets for DeepSeek Harness |
| 19 | [moluyao/dsh-minimax-asr](https://github.com/moluyao/dsh-minimax-asr) | 1 | 2026-09-12 | 2026-09-13 | MiniMax 语音识别（asr-1.0）的 DeepSeek Harness 全局插件：transcribe_audio 工具 + 设置卡片 + 输入框语音输入 |
| 20 | [RyanZeeee/dsh-chattree](https://github.com/RyanZeeee/dsh-chattree) | 1 | 2026-09-12 | 2026-09-13 | A visual, non-linear conversation canvas for DeepSeek Harness (DSH) — every turn is a node, every question grows a branch. DSH 插件：把线性聊天记录变成一张可以看、可以点的对话地图，每轮问答是一个节点，每次提问都是一条新分支。 |
| 21 | [troytse/dsh-plugin-subagent-roles](https://github.com/troytse/dsh-plugin-subagent-roles) | 1 | 2026-09-13 | 2026-09-13 | DeepSeek Harness - Subagent Roles Plugin |
| 22 | [Vergil-long/dsh-email-notify](https://github.com/Vergil-long/dsh-email-notify) | 1 | 2026-09-13 | 2026-09-13 | DeepSeek Harness 邮件通知插件：任务完成 / 工具等你授权 / 助手在等你回答时发邮件给你，配一个「离开模式」开关。设置全部集成在 harness 设置界面里。 |
| 23 | [VviLliAm-qwq/dsh-open-path](https://github.com/VviLliAm-qwq/dsh-open-path) | 1 | 2026-09-07 | 2026-09-13 | dsh-TUI /open command: open files and folders by path or fuzzy workspace search (v0.15 manifest, MIT) |
| 24 | [wjingshan/dsh-dock-launcher](https://github.com/wjingshan/dsh-dock-launcher) | 1 | 2026-09-10 | 2026-09-13 | 常驻程序坞的 DeepSeek Harness 开关：左键回到/启动 dsh 网页界面，右键菜单（停止服务、动画开关），图标实时显示服务与任务状态并在完成/需确认时发光提醒。 \| Always-on macOS Dock toggle for DeepSeek Harness: left-click to open/start the dsh web UI, right-click menu (stop service, animation toggle); live state icon with glow alerts. |
| 25 | [xarleyn/dsh-plugins](https://github.com/xarleyn/dsh-plugins) | 1 | 2026-08-29 | 2026-09-13 | Community plugins, developer tooling, and shared utilities for extending DeepSeek Harness — built as an Nx + pnpm monorepo. |
| 26 | [zlZayn/dsh-zhihu-search](https://github.com/zlZayn/dsh-zhihu-search) | 1 | 2026-09-12 | 2026-09-13 | DSH 插件：基于知乎开放平台官方 API 的站内搜索、全网索引搜索与直答三个工具，结果带可引用的来源。（原生嵌入设置-插件-插件配置） |
| 27 | [778672151/dsh-session-turn-eta](https://github.com/778672151/dsh-session-turn-eta) | 0 | 2026-09-13 | 2026-09-13 | Live remaining-time prediction and once-per-turn wall-time record for DeepSeek Harness turns, with a Web UI progress bar. |
| 28 | [99galaxy/dsh-plugin-market](https://github.com/99galaxy/dsh-plugin-market) | 0 | 2026-09-12 | 2026-09-13 | 在 DeepSeek Harness 设置面板里浏览并一键安装社区插件 \| A plugin market inside the DeepSeek Harness settings panel |
| 29 | [9Ashwin/dsh-session-rename](https://github.com/9Ashwin/dsh-session-rename) | 0 | 2026-09-13 | 2026-09-13 | DSH plugin: a model-facing rename_session tool, so the agent can retitle a session from inside the conversation. |
| 30 | [AllenLogo/dsh-restart-button](https://github.com/AllenLogo/dsh-restart-button) | 0 | 2026-09-13 | 2026-09-13 | DSH 设置 → General 一键重启按钮:重启宿主进程并自动刷新页面。One-click restart row for the DeepSeek Harness Web GUI (DSH 0.1.5+). |
| 31 | [Amer-CN/zcode-usage-stats](https://github.com/Amer-CN/zcode-usage-stats) | 0 | 2026-09-13 | 2026-09-13 | 非官方 DSH 插件：在 DeepSeek Harness 设置页渲染全量会话的 Token 用量统计——日历点阵热力图、多模型趋势折线、刻度环仪表盘，支持深浅主题与自定义时间范围。 |
| 32 | [Animal2404/dsh-axia-cachebilling](https://github.com/Animal2404/dsh-axia-cachebilling) | 0 | 2026-09-10 | 2026-09-13 | 虾算账：DSH 缓存账单插件 —— 上下文弹层实时算账（三档账单 + 真实事件计数 + Token 统计 + 实时汇率统一币种），价目目录自动填价（Open Code / Command Code / GLM / Kimi / MiniMax / MiMo） |
| 33 | [Aone2233/dsh-router-sci](https://github.com/Aone2233/dsh-router-sci) | 0 | 2026-09-13 | 2026-09-13 | 科研计算 Agent 预设 — 核工程粉体/多相流仿真（LAMMPS + Fluent DPM + LaTeX）的 dsh agent preset |
| 34 | [ArimaKana-Akane/dsh-sakurafrp](https://github.com/ArimaKana-Akane/dsh-sakurafrp) | 0 | 2026-09-11 | 2026-09-13 | dsh-mobile satellite: manage the SakuraFrp phone-desktop link from DSH UI (status, gateway toggle, pairing QR, devices, self-heal). Vibe-coded. |
| 35 | [ArimaKana-Akane/dsh-wallpaper-position](https://github.com/ArimaKana-Akane/dsh-wallpaper-position) | 0 | 2026-09-11 | 2026-09-13 | dsh-dream-skin satellite: per-image wallpaper position (X/Y px) settings row. Vibe-coded. |
| 36 | [ArimaKana-Akane/dsh-whale-tools](https://github.com/ArimaKana-Akane/dsh-whale-tools) | 0 | 2026-09-11 | 2026-09-13 | dsh-whale-widget satellite: replace the whale mascot with any image (auto cutout) + restart button + heartbeat. Vibe-coded. |
| 37 | [AsILAnn/dsh-update-checker](https://github.com/AsILAnn/dsh-update-checker) | 0 | 2026-08-21 | 2026-09-13 | dsh (DeepSeek Harness) 插件：在设置页检查并更新 dsh 官方版本 |
| 38 | [Astervolans/dsh-literature-search](https://github.com/Astervolans/dsh-literature-search) | 0 | 2026-09-13 | 2026-09-13 | Literature search for DeepSeek Harness: PubMed NCBI E-utilities + Google Scholar, unified paper output. Zero runtime dependencies. |
| 39 | [BaihaWhite/dsh-plugins-list](https://github.com/BaihaWhite/dsh-plugins-list) | 0 | 2026-09-13 | 2026-09-13 | 个人 DSH（DeepSeek Harness）插件清单：记录 web profile 已安装插件、版本与一键恢复提示词 |
| 40 | [BaihaWhite/dsh-web-search-scrape](https://github.com/BaihaWhite/dsh-web-search-scrape) | 0 | 2026-09-13 | 2026-09-13 | DSH 六档分级抓取式网页检索插件（web-scrape provider + web_search 工具，无需 API key） |
| 41 | [BeiWay1145/dsh-download-guard](https://github.com/BeiWay1145/dsh-download-guard) | 0 | 2026-09-13 | 2026-09-13 | DeepSeek Harness plugin: force every large-file download through the local aria2 engine by denying shell download commands at the tool pre-execute hook. 强制下载统一走 aria2 的 DSH 插件。 |
| 42 | [BeiWay1145/dsh-sidebar-downloads](https://github.com/BeiWay1145/dsh-sidebar-downloads) | 0 | 2026-09-13 | 2026-09-13 | DeepSeek Harness plugin: move download progress out of the floating overlay and into a dsh-better-sidebar page. 把下载进度从悬浮窗搬进侧边栏的 dsh-better-sidebar 附属插件。 |
| 43 | [Better-Rain/dsh-plugin-photoshop](https://github.com/Better-Rain/dsh-plugin-photoshop) | 0 | 2026-09-12 | 2026-09-13 | 让 DeepSeek Harness 的 AI 直接驱动你本机的 Photoshop：批量抠图、批量处理、任意 PS 脚本。7 个工具、93 个操作、零依赖。 |
| 44 | [cardclown/dsh-sims-agent](https://github.com/cardclown/dsh-sims-agent) | 0 | 2026-09-13 | 2026-09-13 | DSH SIMS 单工具助手：连接配置、凭据管理与用户模板（开发候选） |
| 45 | [chaochaokongbai/dsh-beginner-hub](https://github.com/chaochaokongbai/dsh-beginner-hub) | 0 | 2026-09-11 | 2026-09-13 | 🧭 DSH新手台：大白话输入需求 → 路由成可直接用的方案（话术/技能/进阶玩法），一键填入新会话 |
| 46 | [clevebitr/dsh-base16-skins](https://github.com/clevebitr/dsh-base16-skins) | 0 | 2026-09-13 | 2026-09-13 | 配色方案，作为 DSH Web GUI 皮肤（ 的 v2 纯资产皮肤目录）。 |
| 47 | [cnkids/dsh-palimpsest](https://github.com/cnkids/dsh-palimpsest) | 0 | 2026-09-13 | 2026-09-13 | DSH 宿主插件：让 AI 智能体在新会话里按需检索同一工作目录下的历史会话记忆（只读、不落盘、不注入）｜ DSH host plugin: on-demand recall of past sessions in the same working directory for AI agents |
| 48 | [ddowbnac/dsh-claude-auth-proxy](https://github.com/ddowbnac/dsh-claude-auth-proxy) | 0 | 2026-09-11 | 2026-09-13 | LLM provider plugin for the DeepSeek Harness (dsh): streams Claude through your Claude Code subscription (claude.ai OAuth credentials), no Anthropic API key required. |
| 49 | [ddowbnac/dsh-web-search-local](https://github.com/ddowbnac/dsh-web-search-local) | 0 | 2026-09-08 | 2026-09-13 | A web-search provider for the DeepSeek Harness, fully local no API key needed. |
| 50 | [devacc8/dsh-billing-badge](https://github.com/devacc8/dsh-billing-badge) | 0 | 2026-09-13 | 2026-09-13 | Billing season and account balance chip for the DeepSeek Harness web GUI: a native-looking pill after the cache-hit stat, with a panel on click. DeepSeek Harness 计费时段与余额插件 |
| 51 | [DoctorxPriestess/dsh-cache-safe-tool-result](https://github.com/DoctorxPriestess/dsh-cache-safe-tool-result) | 0 | 2026-09-13 | 2026-09-13 | A DeepSeek Harness (DSH) plugin that keeps tool results cache-prefix safe: truncate a result before it first enters the session surface, and never rewrite a tool result a provider request has already delivered. |
| 52 | [du-u-uck/DSH-Prompt-Optimization](https://github.com/du-u-uck/DSH-Prompt-Optimization) | 0 | 2026-09-12 | 2026-09-13 | DSH的提示词优化插件，帮助优化对话框中输入的提示词与项目要求 |
| 53 | [EmotionG/model-import](https://github.com/EmotionG/model-import) | 0 | 2026-09-13 | 2026-09-13 | 为解决dsh导入订阅后配置模型的思考强度等问题而创建的插件 |
| 54 | [firestige/crystra-dsh](https://github.com/firestige/crystra-dsh) | 0 | 2026-08-29 | 2026-09-13 | The single dsh-crystra plugin for DeepSeek Harness: workflow execution, analysis and deterministic initialization. |
| 55 | [FOX4096/dsh-custom-css](https://github.com/FOX4096/dsh-custom-css) | 0 | 2026-09-12 | 2026-09-13 | DSH Web GUI 扩展：在 设置 → 通用 → 外观 下方增加一行自定义 CSS 编辑器（DevTools 风格编辑体验：补全 / 校验 / 规则面板） |
| 56 | [gezi-wen/dsh-repair](https://github.com/gezi-wen/dsh-repair) | 0 | 2026-09-13 | 2026-09-13 | DSH plugin that ships a skill for diagnosing and repairing a broken DeepSeek Harness install: boot failures, dead plugins, broken dependency bridges, upgrades. |
| 57 | [gezi-wen/dsh-skill-authoring](https://github.com/gezi-wen/dsh-skill-authoring) | 0 | 2026-09-13 | 2026-09-13 | DSH plugin that ships a skill for writing, reviewing and verifying DSH skills: SKILL.md frontmatter, trigger surface, length rules, and an A/B check. |
| 58 | [gezi-wen/dsh-subagent-delegation](https://github.com/gezi-wen/dsh-subagent-delegation) | 0 | 2026-09-13 | 2026-09-13 | DSH plugin that ships a skill on when to delegate to subagents, how many to fan out in parallel, and how to verify what they returned. |
| 59 | [gurio-wine/dsh-fold-it-up](https://github.com/gurio-wine/dsh-fold-it-up) | 0 | 2026-09-13 | 2026-09-13 | DeepSeek Harness Web 插件：强制折叠每一轮的工作过程，答案照常显示，历史轮次与上下文注入行一并折叠。 |
| 60 | [Harzva/dsh-wemedia-workbench](https://github.com/Harzva/dsh-wemedia-workbench) | 0 | 2026-09-13 | 2026-09-13 | Local-first media workbench for DeepSeek Harness: AI-assisted workflows, revision-bound reviews, native approvals and persistent jobs. |
| 61 | [hasan-aghayev/dsh-session-resilience](https://github.com/hasan-aghayev/dsh-session-resilience) | 0 | 2026-09-12 | 2026-09-13 | Safe DSH restart, token-aware reconnect, and policy-based session recovery |
| 62 | [hmr-BH/dsh-round-rightclick](https://github.com/hmr-BH/dsh-round-rightclick) | 0 | 2026-09-13 | 2026-09-13 | 为 DeepSeek Harness 提供圆盘式右键菜单 |
| 63 | [hnmrxz/deepseek-harness-desktop-HarmonyOS](https://github.com/hnmrxz/deepseek-harness-desktop-HarmonyOS) | 0 | 2026-09-10 | 2026-09-13 | Deepseek Harness HarmonyOS 多端客户端 |
| 64 | [ice5kysl/dsh-msg9-kit](https://github.com/ice5kysl/dsh-msg9-kit) | 0 | 2026-09-13 | 2026-09-13 | 给每个 dsh workspace 一个 msg9.io 收件箱：Agent 用工具收发，GUI 点 ✉ 看同一份邮件 \| one msg9.io inbox per dsh workspace |
| 65 | [idoall/dsh-notify](https://github.com/idoall/dsh-notify) | 0 | 2026-09-13 | 2026-09-13 | In-page task notifications for DeepSeek Harness: toast, bell history, WebAudio cue, flashing background tab title. No web push, no OS notification matrix. |
| 66 | [igormel81/dsh-chat-cost](https://github.com/igormel81/dsh-chat-cost) | 0 | 2026-09-12 | 2026-09-13 | DeepSeek Harness (dsh) plugin: live token cost of every chat, its subagents and the whole session tree — DeepSeek, OpenAI, Anthropic, Gemini, Kimi, Grok and Mistral prices from a bundled catalog, plus an append-only JSONL cost log in your project folder. |
| 67 | [iii993/computer-use-advance](https://github.com/iii993/computer-use-advance) | 0 | 2026-09-13 | 2026-09-13 | 一个DSH的电脑操作插件，专门为近视眼ds添加光标放大镜等功能 |
| 68 | [iimaguest/dsh-browser-annotate](https://github.com/iimaguest/dsh-browser-annotate) | 0 | 2026-09-13 | 2026-09-13 | Browser tools, Chrome DevTools Protocol, and right-click annotation for the DeepSeek Harness agent — plus the desktop shell that owns the real Chromium beside your session |
| 69 | [iwinoid/dsh-kde-tint](https://github.com/iwinoid/dsh-kde-tint) | 0 | 2026-09-13 | 2026-09-13 | Tint the DSH web UI with the KDE system accent color. |
| 70 | [iwinoid/fakeip-compat](https://github.com/iwinoid/fakeip-compat) | 0 | 2026-09-13 | 2026-09-13 | Fake-IP-aware web.fetch provider for TUN (Mihomo/Clash) DNS environments plus pinned LAN CIDR access |
| 71 | [janewas/dsh-image-annotate](https://github.com/janewas/dsh-image-annotate) | 0 | 2026-09-13 | 2026-09-13 | Annotate a pending composer image in place (pen / box / arrow / typed text) and insert the PNG back next to the original. Minimal footprint: nothing in DSH UI is restyled, no host routes, no dependencies. |
| 72 | [jianghuifr/dsh-feishu-auth](https://github.com/jianghuifr/dsh-feishu-auth) | 0 | 2026-09-13 | 2026-09-13 | Feishu (Lark) OAuth login gate for the DeepSeek Harness web GUI — a signed session cookie in front of every HTTP request. |
| 73 | [JIUYUE-SEP/dsh-plugin-archive-shelf](https://github.com/JIUYUE-SEP/dsh-plugin-archive-shelf) | 0 | 2026-09-13 | 2026-09-13 | 随手做的一个dsh归档架，可以查看，还原，彻底清除已归档的会话 |
| 74 | [jonah791/dsh-agent-toolface](https://github.com/jonah791/dsh-agent-toolface) | 0 | 2026-09-13 | 2026-09-13 | 工具面分档（DSH agent preset 行）：按证据化的 deny 集在 agent 作用域收窄模型可见工具，lean/full 一键切换 + 审计留痕，降低工具 schema 的固定上下文成本与工具选择稀释。 |
| 75 | [jonah791/dsh-semantic-docs](https://github.com/jonah791/dsh-semantic-docs) | 0 | 2026-09-13 | 2026-09-13 | DSH 本地语义文档系统工具面：semantic_list/get/check/register + D1–D6 drift 判据（单一真源、文档随代码、未验证显式、留白诚实）。 |
| 76 | [KasenRi/dsh-browser](https://github.com/KasenRi/dsh-browser) | 0 | 2026-09-13 | 2026-09-13 | Installable GitHub release mirror for @kasenri/dsh-browser. Canonical source: KasenRi/dsh-orbit-browser-plugins. |
| 77 | [KasenRi/dsh-orbit](https://github.com/KasenRi/dsh-orbit) | 0 | 2026-09-13 | 2026-09-13 | Installable GitHub release mirror for @kasenri/dsh-orbit. Canonical source: KasenRi/dsh-orbit-browser-plugins. |
| 78 | [lcohvne-tomorin/dsh-context-dashboard](https://github.com/lcohvne-tomorin/dsh-context-dashboard) | 0 | 2026-09-13 | 2026-09-13 | Sidebar context/billing dashboard for DeepSeek Harness: live context ring, per-session usage & spend, account balance and token-plan quota readouts across configured LLM channels. |
| 79 | [lengmoXXL/dsh-remote-workspace](https://github.com/lengmoXXL/dsh-remote-workspace) | 0 | 2026-09-11 | 2026-09-13 | A DeepSeek Harness (DSH) plugin that runs the harness's file, shell, and terminal tools inside a git worktree on a remote machine over SSH. The remote agent installs itself: it ships as a static Rust binary from GitHub Releases, listens on a random loopback port, and updates when the plugin does. |
| 80 | [liangl1985/work-personal-secretary](https://github.com/liangl1985/work-personal-secretary) | 0 | 2026-09-11 | 2026-09-13 | DSH（DeepSeek Harness）插件集合 · 工作秘书集成体：强记忆 + 强文档处理（Word/Excel/PPT/PDF）+ 20 位专家库 + 桌宠定制层。安装：git clone 后 dsh plugin --profile desktop add <克隆目录>/modules/work-personal-secretary，重启 DSH 后在「设置 → 工作秘书 → 安装与检查」装子模块。MIT。 |
| 81 | [liyiersan/dsh-usage-monitor](https://github.com/liyiersan/dsh-usage-monitor) | 0 | 2026-09-12 | 2026-09-13 | DSH plugin: show DeepSeek API pricing, token usage/cost and account balance inside DeepSeek Harness |
| 82 | [liyixuan201211/dsh-deadend](https://github.com/liyixuan201211/dsh-deadend) | 0 | 2026-09-13 | 2026-09-13 | A refutation ledger for coding agents: remember what did not work, and expire it automatically when the code it depended on changes. DSH plugin + CLI, no build step. |
| 83 | [liyixuan201211/dsh-skillnotary](https://github.com/liyixuan201211/dsh-skillnotary) | 0 | 2026-09-13 | 2026-09-13 | DSH plugin: lock, verify and govern AI agent skills. Tells you what a skill can do before you install it — and when it silently gains a capability after your review. Ships no boot-time code. |
| 84 | [lsjspl/dsh-reel](https://github.com/lsjspl/dsh-reel) | 0 | 2026-09-12 | 2026-09-13 | dsh插件: 基于dsh的端口，实现的一个本地视频、图片等多媒体库，兼容移动端，可以使用刷视频模式。 |
| 85 | [maci0/dsh-ponytail](https://github.com/maci0/dsh-ponytail) | 0 | 2026-09-13 | 2026-09-13 | Ponytail (lazy senior dev mode) for DeepSeek Harness: six skills, an always-on anti-over-engineering ruleset, and a Plugin configuration card. |
| 86 | [ManoloRemiddi/deepseek-harness-plugins](https://github.com/ManoloRemiddi/deepseek-harness-plugins) | 0 | 2026-09-13 | 2026-09-13 | DeepSeek Harness plugins by Manolo Remiddi: downloads, installation guides and compatibility notes. |
| 87 | [ManoloRemiddi/dsh-adaptive-reasoning](https://github.com/ManoloRemiddi/dsh-adaptive-reasoning) | 0 | 2026-09-13 | 2026-09-13 | Automatic per-request reasoning for DeepSeek Harness, without extra model calls or GPU keep-alive. |
| 88 | [ManoloRemiddi/dsh-prompt-library](https://github.com/ManoloRemiddi/dsh-prompt-library) | 0 | 2026-09-05 | 2026-09-13 | Reusable prompts in DeepSeek Harness Settings, with standalone SQLite storage or an existing Augmentor service. |
| 89 | [MichengAI/dsh-code-review](https://github.com/MichengAI/dsh-code-review) | 0 | 2026-09-13 | 2026-09-13 | DSH Code Review — 为 DeepSeek Harness 提供 Codex 风格代码审查、原生独立子 Agent、灵活范围选择和中英文报告 · Codex-style code review with native independent agents, flexible scope selection, and bilingual reports for DSH |
| 90 | [minghuo/dsh-github-sync](https://github.com/minghuo/dsh-github-sync) | 0 | 2026-09-13 | 2026-09-13 | 把 dsh 会话、插件清单与设置备份到私有 GitHub 仓库（纯 REST，无需 git 二进制），每台机器一个独立目录，可在另一台机器按整机 / 工作区 / 单会话恢复。 |
| 91 | [MirrMeur/dsh-tavily-provider](https://github.com/MirrMeur/dsh-tavily-provider) | 0 | 2026-09-12 | 2026-09-13 | Tavily-backed web_search / web_fetch providers for DeepSeek Harness — replaces the built-in DeepSeek search backend (0.1.1-rc.x and 0.1.5 compatible) |
| 92 | [MirrMeur/dsh-workspace-colors](https://github.com/MirrMeur/dsh-workspace-colors) | 0 | 2026-09-12 | 2026-09-13 | DSH Web 外观增强：侧边栏工作区专属颜色 + 页面背景 tint（含设置页与内存回收面板） |
| 93 | [Neptune810/dsh-model-router](https://github.com/Neptune810/dsh-model-router) | 0 | 2026-09-13 | 2026-09-13 | Flash-only reasoning-effort routing for DeepSeek Harness, setting the DeepSeek flash model reasoning effort per step. The model never changes; effort max is opt-in. |
| 94 | [nina27486486/dsh-prompt-forge](https://github.com/nina27486486/dsh-prompt-forge) | 0 | 2026-09-13 | 2026-09-13 | ⚒ 点词成金 — Zero-config streaming prompt optimizer for DeepSeek Harness (dsh): reuse session model, file-based prompt library, one-click skills. 提示词流式优化 + 文件词库 + 一键存技能 |
| 95 | [pureexe/dsh-windows-remote-ssh](https://github.com/pureexe/dsh-windows-remote-ssh) | 0 | 2026-09-12 | 2026-09-13 | Control a remote Windows desktop over SSH from DeepSeek Harness |
| 96 | [qxcool/dsh-usage-plus](https://github.com/qxcool/dsh-usage-plus) | 0 | 2026-09-13 | 2026-09-13 | DSH Desktop plugin: usage stats, plan quotas, custom HTTPS balance, 26-week heatmap |
| 97 | [RBkreb/dsh-console-hub](https://github.com/RBkreb/dsh-console-hub) | 0 | 2026-09-12 | 2026-09-13 | 一个Deepseek Harness Telnet/Raw TCP连接控制插件，典型场景为串口服务器和网络设备 |
| 98 | [Rex16200513/dsh-lifecycle-inspector](https://github.com/Rex16200513/dsh-lifecycle-inspector) | 0 | 2026-09-13 | 2026-09-13 | Diagnose DSH plugin Fiber lifecycles, live Cordis Effects, and teardown outcomes |
| 99 | [RINGOLINK/dsh-desktop-shell](https://github.com/RINGOLINK/dsh-desktop-shell) | 0 | 2026-09-13 | 2026-09-13 | 把 DeepSeek Harness 的 WebUI 爆改成真正的桌面应用（DSH 插件）：WebView2 独立窗口 + 托盘常驻 + 无痕启动 + 就绪门控 + 调试模式；零 Electron 依赖，载荷仅 1.2MB。 \| Turn the DSH Web UI into a real desktop app from inside DSH: WebView2 window, tray residency, silent start, debug console. No Electron. |
| 100 | [rootkiller6788/dsh-flow](https://github.com/rootkiller6788/dsh-flow) | 0 | 2026-09-12 | 2026-09-13 | dsh-flow —— DeepSeek Harness 的统一智能体画布：把需求会话、多智能体团队、成员任务与发言、依赖 DAG 编织进同一张可交互时间轴，让 Agent 从“后台运行”变成“可视化协作”。 |
| 101 | [satan9394/dsh-usage-unified](https://github.com/satan9394/dsh-usage-unified) | 0 | 2026-09-12 | 2026-09-13 | Machine-wide DeepSeek Harness (dsh) token usage statistics — trends, a custom date range, per-model bucket splits, call details, CSV/JSON export. 全机 DSH 用量统计：趋势 / 自定义区间 / 模型四桶 / 调用明细 / 导出，中英双语、浅深色。 |
| 102 | [slatinwine/dsh-sentience-audit](https://github.com/slatinwine/dsh-sentience-audit) | 0 | 2026-09-13 | 2026-09-13 | Audit a DeepSeek Harness session against the 14 consciousness indicator properties (Butlin/Long/Bengio 2023), scored L1-L5. |
| 103 | [succlz123/dsh-model-switch](https://github.com/succlz123/dsh-model-switch) | 0 | 2026-09-12 | 2026-09-13 | DSH (DeepSeek Harness) 全局插件：用任意按键（含 spare 键、蓝牙小键盘、遥控器 HID 键盘等）**一键切换模型与思考强度**。 |
| 104 | [syroezhkin/dsh-routerai](https://github.com/syroezhkin/dsh-routerai) | 0 | 2026-09-12 | 2026-09-13 | RouterAI plugins for the DeepSeek Harness: web search and a session-cost meter |
| 105 | [TEGONG00/dsh-plugin-browser](https://github.com/TEGONG00/dsh-plugin-browser) | 0 | 2026-09-13 | 2026-09-13 | Built-in browser panel for the DeepSeek Harness web client: live screencast, element picker → composer attachments, Playwright-driven model tools |
| 106 | [thanhdz235123-commits/nyx-dsh-plugins](https://github.com/thanhdz235123-commits/nyx-dsh-plugins) | 0 | 2026-09-12 | 2026-09-13 | Nyx plugins for DeepSeek Harness — a right-side file panel and true edit-message, both drawn with the harness's own UI. |
| 107 | [ThinkForge-core/dsh-upgrade-tools](https://github.com/ThinkForge-core/dsh-upgrade-tools) | 0 | 2026-09-12 | 2026-09-13 | Keep your DSH profile current: six compatibility checks against any core version, inspect a plugin before installing it, snapshot and restore the whole profile, update only what has a newer release, recheck the deferred list, and probe what really loads and answers — imports, apply(), route handlers, shadowed UI, dead endpoints. Menu, CLI, JSON. |
| 108 | [tippykafuu/dsh-client-ui-wallpaper](https://github.com/tippykafuu/dsh-client-ui-wallpaper) | 0 | 2026-09-13 | 2026-09-13 | Changes the wallpaper of the dsh Web GUI. |
| 109 | [ttmouse/dsh-model-picker](https://github.com/ttmouse/dsh-model-picker) | 0 | 2026-09-13 | 2026-09-13 | Enhanced model picker for the dsh web GUI — replaces the composer's model seat |
| 110 | [vansonffff/dsh-kdocs-sidebar](https://github.com/vansonffff/dsh-kdocs-sidebar) | 0 | 2026-09-12 | 2026-09-13 | 金山文档 (WPS 云文档) 接入 DeepSeek Harness：侧边右栏面板 / 预览文件 / 引用文件和文件夹到对话 / 编辑器打开 |
| 111 | [vecnode/vn-harness](https://github.com/vecnode/vn-harness) | 0 | 2026-09-08 | 2026-09-13 | vn-harness 🤖 |
| 112 | [Volta-ln/dsh-quick-ask](https://github.com/Volta-ln/dsh-quick-ask) | 0 | 2026-09-12 | 2026-09-13 | A quick ask in the side windows（if there are any problems, please tell me.） |
| 113 | [VviLliAm-qwq/dsh-console-utf8](https://github.com/VviLliAm-qwq/dsh-console-utf8) | 0 | 2026-09-13 | 2026-09-13 | Keep the Windows console on code page 65001 (UTF-8) for the dsh host and its bash tool commands, so output from Windows-native child processes stops being decoded as mojibake |
| 114 | [VviLliAm-qwq/dsh-git-bash](https://github.com/VviLliAm-qwq/dsh-git-bash) | 0 | 2026-09-13 | 2026-09-13 | Make a Git for Windows installation resolvable as bash inside the dsh host process, so the official bash shell stack can run on Windows |
| 115 | [VviLliAm-qwq/dsh-mama-cheer](https://github.com/VviLliAm-qwq/dsh-mama-cheer) | 0 | 2026-09-13 | 2026-09-13 | Keyboard shortcut that injects an encouraging message into the running dsh-TUI conversation: steer when a tool is in flight, interrupt-and-deliver when only text is streaming |
| 116 | [VviLliAm-qwq/dsh-web-tavily](https://github.com/VviLliAm-qwq/dsh-web-tavily) | 0 | 2026-09-13 | 2026-09-13 | Tavily-backed search provider for dsh: registers the tavily provider on the ctx.web seam so the web_search tool runs against the Tavily Search API |
| 117 | [VviLliAm-qwq/dshtui-format-setting](https://github.com/VviLliAm-qwq/dshtui-format-setting) | 0 | 2026-09-13 | 2026-09-13 | Lightweight window settings for dsh-tui: maximize on startup, native Window settings section, bilingual zh/en |
| 118 | [webkubor/dsh-llm-hub](https://github.com/webkubor/dsh-llm-hub) | 0 | 2026-09-13 | 2026-09-13 | DSH 官方直连的 LLM 配置补强：模型发现（Models 页「获取可用模型」对 deepseek-official 生效）+ provider 卡片上的 DeepSeek 余额与可用性。零依赖，不改动 DSH 安装。 |
| 119 | [whiskey1993/dsh-thermal-monitor](https://github.com/whiskey1993/dsh-thermal-monitor) | 0 | 2026-09-13 | 2026-09-13 | DSH Web 左侧栏硬件温度看板：CPU / 内存 / GPU / 固态实时温度，提权失败自动降级。Sidebar hardware temperature panel for DeepSeek Harness. |
| 120 | [WsTe47/dsh-tab-status](https://github.com/WsTe47/dsh-tab-status) | 0 | 2026-09-13 | 2026-09-13 | 把 DeepSeek Harness 网页版的会话进度同步到浏览器标签：标题状态前缀 + favicon 计数徽章。 |
| 121 | [wwwangzilin/dsh-role-cards](https://github.com/wwwangzilin/dsh-role-cards) | 0 | 2026-09-13 | 2026-09-13 | DSH Web 插件：新建会话界面上的角色卡 + 工作区卡选择器（毛玻璃卡片墙 / 横向滚动 / 角色主题色 / 入场动画） |
| 122 | [Xiaobai01/dsh-tool-ths](https://github.com/Xiaobai01/dsh-tool-ths) | 0 | 2026-09-13 | 2026-09-13 | DSH的同花顺插件 |
| 123 | [xie129716/computer-user-vision](https://github.com/xie129716/computer-user-vision) | 0 | 2026-09-13 | 2026-09-13 | Unofficial fork of computer-user: fixes the silent load failure on DSH >= 0.1.2, and returns screenshots as real images to vision models with an exact image->screen coordinate mapping. |
| 124 | [y2zyyr/smart-session-title](https://github.com/y2zyyr/smart-session-title) | 0 | 2026-09-13 | 2026-09-13 | Automatic session titles for DeepSeek Harness, using the conversation model. English and Chinese documentation. |
| 125 | [yangzhe1991/dsh-proxy-router](https://github.com/yangzhe1991/dsh-proxy-router) | 0 | 2026-09-12 | 2026-09-13 | DSH plugin: local routing proxy with a Web settings page — only blocked domains use the upstream proxy, everything else goes direct. 上游地址等参数在设置页里改，热生效。 |
| 126 | [YanKaFei/art-aesthetic-vault](https://github.com/YanKaFei/art-aesthetic-vault) | 0 | 2026-09-12 | 2026-09-13 | 147 art movements decomposed into 7 swappable AI prompt layers — style, lighting, color, composition, medium, mood, camera. CLI + MCP server. Obsidian vault with public-domain artworks. |
| 127 | [Yezery/dsh-image-download](https://github.com/Yezery/dsh-image-download) | 0 | 2026-09-13 | 2026-09-13 | Hover-to-download buttons for images in DeepSeek Harness conversations. |
| 128 | [yknBugs/dsh-balance-status](https://github.com/yknBugs/dsh-balance-status) | 0 | 2026-09-13 | 2026-09-13 | 自用的轻量级Deepseek余额查询插件 |
| 129 | [YMRwithNoworry/dsh-nushell-only](https://github.com/YMRwithNoworry/dsh-nushell-only) | 0 | 2026-09-10 | 2026-09-13 | DeepSeek Harness (dsh) bundle: Nushell as the only shell executor + Nushell syntax teaching. Install with: dsh plugin --profile web add github:YMRwithNoworry/dsh-nushell-only |
| 130 | [yoursc/dsh-siyuan](https://github.com/yoursc/dsh-siyuan) | 0 | 2026-09-12 | 2026-09-13 | 把思源笔记（SiYuan）接入 DeepSeek Harness：17 个 siyuan_* 工具（检索/读写/日记/删除）+ 独立设置页。SiYuan notes integration for dsh: 17 siyuan_* tools plus a Web settings page. |
| 131 | [yuu1111/dsh-cost-meter](https://github.com/yuu1111/dsh-cost-meter) | 0 | 2026-09-13 | 2026-09-13 | DeepSeek Harness Web GUI plugin: real-time spend for the current session, priced from per-model token rates and shown as a pill under the composer |
| 132 | [zengqingsong/dsh-sidebar-frog](https://github.com/zengqingsong/dsh-sidebar-frog) | 0 | 2026-09-03 | 2026-09-13 | 可弹出侧边栏 · Popout Sidebar — an artifacts + file-tree sidebar for DeepSeek Harness: offline previews (code / Markdown with math & Mermaid / PDF / HTML / images / CSV tables / Word·Excel·PowerPoint / audio-video), CodeMirror editing with Ctrl+S, a read-only Git slice, and a one-click pop-out into a second-monitor tab. |
| 133 | [zhangzhangco/dsh-llm-codex](https://github.com/zhangzhangco/dsh-llm-codex) | 0 | 2026-09-13 | 2026-09-13 | Codex route for DeepSeek Harness: local Codex CLI first, OpenAI-compatible API fallback |
| 134 | [zhengjy01/dsh-updater](https://github.com/zhengjy01/dsh-updater) | 0 | 2026-09-13 | 2026-09-13 | Track DeepSeek Harness's own releases and update in one click: npm dist-tags + GitHub changelog, risk-graded, with an atomic-rename backup and automatic rollback |
| 135 | [zhitiaojun/dsh-anysearch](https://github.com/zhitiaojun/dsh-anysearch) | 0 | 2026-09-01 | 2026-09-13 | AnySearch 实时搜索的 DeepSeek Harness 原生插件：web/垂直域搜索、批量并行、网页提取 + API key 设置面板，优先于内置 web_search |
| 136 | [Zhuang-A/dsh-go-sensei](https://github.com/Zhuang-A/dsh-go-sensei) | 0 | 2026-09-12 | 2026-09-13 | dsh-go-sensei —— DeepGo Sensei 围棋复盘教练 DSH（DeepSeek Harness）插件：把围棋 AI 的数学判断（胜率、目差、候选点、变化图）翻译成老师级口头讲解，供自学棋手复盘； 讲解与多轮追问由 DSH 会话原生完成 |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- ankhishtar2-lang/dsh-sakurafrp
- ankhishtar2-lang/dsh-wallpaper-position
- ankhishtar2-lang/dsh-whale-tools
- bottledkzk/dsh-search-router
- chen6896qqwee/dsh-workflow-console
- chenproton/dsh-history
- firestige/wsr-dsh
- firestige/wsr-execution
- geeklei/dsh-plugins
- kllilizxc/dsh-worka
- lengmoXXL/dsh-remote-ssh-worktree
- Luoji-Yuli/dsh-turn-rail
- Nyasers/dsh-hanako
- shengmk/godsh
- twelvecarbon/dsh-conversation-toc
- vansonffff/dsh-kdocs
- vecnode/dsh-vn-plugins
- wwwangzilin/dsh-luna-preset
