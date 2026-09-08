# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-08**
- 快照日期 / Snapshot date: **2026-09-08 (UTC)**
- 待审核 / Pending: **100**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **7**
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

对比上一份快照 **2026-09-07** / vs previous snapshot **2026-09-07**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **1**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [Ayuilos/Miffan](https://github.com/Ayuilos/Miffan) | 待审 / pending | 112 | — | 0 | 22d | 待审高星 | 核准即榜 #95；高星零 fork |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [Ayuilos/Miffan](https://github.com/Ayuilos/Miffan) ⚠️ | 112 | 2026-08-16 | 2026-09-08 | RikkaHub fork，Android AI 客户端。支持 ChatGPT 订阅登录使用、跨应用划词悬浮翻译、助手工作区文件隔离、工作区 Skills 自动发现、文档与 HTML 预览、可定制动态角色。 |
| 2 | [sugarforever/dsh-plugins](https://github.com/sugarforever/dsh-plugins) | 6 | 2026-08-20 | 2026-09-08 | DeepSeek Harness Plugins |
| 3 | [FylarOpen/dsh-fylar-office-editor](https://github.com/FylarOpen/dsh-fylar-office-editor) | 4 | 2026-09-02 | 2026-09-08 | Office document preview, editing, and DOCX generation for DeepSeek Harness, powered by Fylar Office SDK. |
| 4 | [easyv-ai/dsh-jumpserver](https://github.com/easyv-ai/dsh-jumpserver) | 3 | 2026-08-20 | 2026-09-08 | JumpServer asset lookup and management plugin for DeepSeek Harness, with HTTP Signature auth. |
| 5 | [lucasx001/dsh-skin-claude-code](https://github.com/lucasx001/dsh-skin-claude-code) | 3 | 2026-08-14 | 2026-09-08 | Claude Code-inspired skin for the DeepSeek Harness web GUI |
| 6 | [edisontaisite/codex-harness-control](https://github.com/edisontaisite/codex-harness-control) | 2 | 2026-09-07 | 2026-09-08 | Open-source multi-model coordinator connecting Codex with DeepSeek Harness for automatic dispatch, review, and progress reporting. |
| 7 | [1014029855/dsh-codevault](https://github.com/1014029855/dsh-codevault) | 1 | 2026-09-06 | 2026-09-08 | Records what you understood while reading open-source code — quick notes and deep notes grouped into one card per repo/file/symbol, stored as Markdown you can open in Obsidian. |
| 8 | [54shitaimzf/dsh-price-less](https://github.com/54shitaimzf/dsh-price-less) | 1 | 2026-09-07 | 2026-09-08 | DeepSeek Harness 的上下文管家：替你记住“现在在干嘛”，自动整理送进模型的上下文——该留的留、该删的删、拿不准的不动，让 AI 编程长会话不跑偏，每个 token 都花在刀刃上。 |
| 9 | [agent-mobile/dsh-mobile-gateway](https://github.com/agent-mobile/dsh-mobile-gateway) | 1 | 2026-09-08 | 2026-09-08 | LAN access plugin for the DeepSeek Harness (dsh) web host: token-gated /m/api for the companion mobile app |
| 10 | [agent-mobile/dsh-speech](https://github.com/agent-mobile/dsh-speech) | 1 | 2026-09-08 | 2026-09-08 | Speech plugin for the DeepSeek Harness (dsh) web host: ASR, TTS and realtime transcription over pluggable providers |
| 11 | [azazo1/dsh-reject-message](https://github.com/azazo1/dsh-reject-message) | 1 | 2026-09-08 | 2026-09-08 | DSH web plugin: take over the native approval window so a reject can carry a description the model will see. |
| 12 | [azazo1/dsh-think-window](https://github.com/azazo1/dsh-think-window) | 1 | 2026-09-08 | 2026-09-08 | DSH web plugin: cap expanded thinking blocks with a bounded scroll window. |
| 13 | [azazo1/dsh-write-protect](https://github.com/azazo1/dsh-write-protect) | 1 | 2026-09-07 | 2026-09-08 | 防止模型改写工作区里的指定路径. 同时支持放开某些外部目录的写入而不必放开沙箱. |
| 14 | [blauerberg/dsh-web-push-notification](https://github.com/blauerberg/dsh-web-push-notification) | 1 | 2026-09-05 | 2026-09-08 | Web Push notifications for DeepSeek Harness tasks, approvals, and questions. |
| 15 | [careyourcake/dsh-plugin-litsearch-zotero](https://github.com/careyourcake/dsh-plugin-litsearch-zotero) | 1 | 2026-09-08 | 2026-09-08 | DeepSeek Harness plugin: literature/related-work search + one-shot Zotero import |
| 16 | [chihy525/dsh-mcp-skill-manager](https://github.com/chihy525/dsh-mcp-skill-manager) | 1 | 2026-08-30 | 2026-09-08 | MCP & Skills management panel for DeepSeek Harness — manage MCP servers and the skill library from the Settings page. |
| 17 | [goatliamia/dsh-trajectory-query](https://github.com/goatliamia/dsh-trajectory-query) | 1 | 2026-09-05 | 2026-09-08 | 把 DSH 已保存的会话轨迹重新可达:3 个查询工具 + 1 条纪律的极薄历史查询层(不是 Memory) |
| 18 | [HarrisXiu/WinWIKIAgent-dsgplugin](https://github.com/HarrisXiu/WinWIKIAgent-dsgplugin) | 1 | 2026-09-01 | 2026-09-08 | WINWIKI的dsh插件版 |
| 19 | [iptton-ai/dsh-plugin-session-notes](https://github.com/iptton-ai/dsh-plugin-session-notes) | 1 | 2026-09-08 | 2026-09-08 | Highlight & annotate DeepSeek Harness (DSH) conversations with sticky notes — dynamic Cordis plugin |
| 20 | [jarvan1/dsh-aiops](https://github.com/jarvan1/dsh-aiops) | 1 | 2026-09-07 | 2026-09-08 | DSH AIOps 是一套面向 Kubernetes 的智能运维系统，集成告警接入、故障诊断、Prometheus 数据发现、路由策略与可观测能力，帮助团队快速定位并处理集群异常。   |
| 21 | [kakajun/dsh-web-recorder](https://github.com/kakajun/dsh-web-recorder) | 1 | 2026-09-08 | 2026-09-08 | Browser-recording tools for DSH: records real browser operations and network requests, then exports a Markdown timeline report for the model to analyze and reproduce.      🥇DSH 的浏览器录制工具：记录真实浏览器操作和网络请求，然后导出 Markdown 时间线报告供模型分析和重现。 |
| 22 | [Kalospacer/dsh-model-capabilities](https://github.com/Kalospacer/dsh-model-capabilities) | 1 | 2026-08-15 | 2026-09-08 | 给 DSH 的设置里加一页：模型能力。  解决一件事：你接的自定义模型，DSH 不认它的思考档位和视觉能力。 |
| 23 | [kk112222/dsh-chat-index](https://github.com/kk112222/dsh-chat-index) | 1 | 2026-09-04 | 2026-09-08 | DSH (DeepSeek Harness) web plugin: per-session question index — rail + chain panel over main & branch sessions, click to jump & highlight. |
| 24 | [LBurny/deepseek-harness-desktop](https://github.com/LBurny/deepseek-harness-desktop) | 1 | 2026-08-15 | 2026-09-08 | Windows desktop shell for DeepSeek's agent harness CLI (dsh). The installer bundles Node.js and dsh, so the official Web UI runs as a native app with tray, notifications, and theme following. No prerequisites. |
| 25 | [linshuangb347/dsh-memory-fortress](https://github.com/linshuangb347/dsh-memory-fortress) | 1 | 2026-09-08 | 2026-09-08 | Memory Fortress for DeepSeek Harness: 5-track layered memory, self-evolution, knowledge graph (SQLite+FTS5), status pill. 本地记忆堡垒：五轨记忆·自我进化·知识图谱·状态灯。 |
| 26 | [LiweiDonVee/dsh-cherry-provider-bridge](https://github.com/LiweiDonVee/dsh-cherry-provider-bridge) | 1 | 2026-09-08 | 2026-09-08 | Synchronize a Cherry Studio provider and model catalog into DeepSeek Harness without model discovery. |
| 27 | [LiweiDonVee/dsh-preset-library](https://github.com/LiweiDonVee/dsh-preset-library) | 1 | 2026-09-08 | 2026-09-08 | Search, tag and organize DeepSeek Harness agent presets with compact views and affiliations. |
| 28 | [LiweiDonVee/dsh-prompt-presets](https://github.com/LiweiDonVee/dsh-prompt-presets) | 1 | 2026-09-08 | 2026-09-08 | Content-free prompt profile editor, versioned compiler and import/export framework for DSH. No bundled prompt packs. |
| 29 | [LiweiDonVee/dsh-tavern-renderer](https://github.com/LiweiDonVee/dsh-tavern-renderer) | 1 | 2026-09-08 | 2026-09-08 | Independent DSH message renderer with sanitized HTML/CSS, macros and eight immersive document templates. |
| 30 | [marcosmmjr2023/dsh-h-v1](https://github.com/marcosmmjr2023/dsh-h-v1) | 1 | 2026-09-05 | 2026-09-08 | FreeDSH — free-first multi-model routing, automatic fallback, safe updates and pt-BR support for DeepSeek Harness. |
| 31 | [mo-n/dsh-provider-qoder](https://github.com/mo-n/dsh-provider-qoder) | 1 | 2026-09-08 | 2026-09-08 | DSH provider plugin for Qoder subscriptions. |
| 32 | [PlxloYzb/dsh-context-management](https://github.com/PlxloYzb/dsh-context-management) | 1 | 2026-09-08 | 2026-09-08 | Windowed, reversible context management for DeepSeek Harness (DSH): compression, historical retrieval, and native compaction integration. |
| 33 | [swenbo1-web/dsh-web-search-button](https://github.com/swenbo1-web/dsh-web-search-button) | 1 | 2026-09-05 | 2026-09-08 | Direct web search button and /search slash command plugin for DeepSeek Harness |
| 34 | [TIREEDMAN/dsh-mulanci](https://github.com/TIREEDMAN/dsh-mulanci) | 1 | 2026-09-08 | 2026-09-08 | 木兰辞 · MulanCi — 多 Agent 编排与逐 Agent 认证管理；DeepSeek Harness 第三方源码预览 / multi-agent orchestration source preview |
| 35 | [WongYuYe/dsh-diff-card](https://github.com/WongYuYe/dsh-diff-card) | 1 | 2026-09-07 | 2026-09-08 | Codex-style per-turn file-change card for DSH Desktop |
| 36 | [Yelloooooow/dsh-shutdown-button](https://github.com/Yelloooooow/dsh-shutdown-button) | 1 | 2026-09-08 | 2026-09-08 | DeepSeek Harness 关机按钮插件：左下角弹窗确认后安全结束 DSH 进程 (dsh-shutdown-button) |
| 37 | [Yelloooooow/dsh-whale-pet](https://github.com/Yelloooooow/dsh-whale-pet) | 1 | 2026-09-08 | 2026-09-08 | DeepSeek Harness 鲸鱼娘余额桌宠插件:右下角常驻,气泡显示 DeepSeek 余额,可拖动,单击刷新/双击打开用量页 |
| 38 | [16512354554/dsh-chat-navigator](https://github.com/16512354554/dsh-chat-navigator) | 0 | 2026-09-08 | 2026-09-08 | Right-edge chat-history navigator plugin for DeepSeek Harness Web. |
| 39 | [Anduin9527/dsh-document-evidence](https://github.com/Anduin9527/dsh-document-evidence) | 0 | 2026-09-08 | 2026-09-08 | Native PDF library for DeepSeek Harness Web: bounded evidence retrieval, page images and source citation highlighting. |
| 40 | [AtWhuhu/dsh-devin-cli](https://github.com/AtWhuhu/dsh-devin-cli) | 0 | 2026-09-07 | 2026-09-08 | dsh devin cli插件 |
| 41 | [better-er/dsh-pause](https://github.com/better-er/dsh-pause) | 0 | 2026-09-07 | 2026-09-08 | DSH Web 暂停插件：agent 完成一轮工具交互、正要发出下一次模型请求之前在 agent/pre-step 处拉门暂停，保持 composer 输入框可用，人类在主输入框按回车放行，空草稿为无感继续、带字作为插话一并放行；此暂停不打断任何在途 API 调用，模型上下文完整、无感知。纯插件自包含，不改 DSH 源码。 |
| 42 | [boogoo619/dsh-noteboard](https://github.com/boogoo619/dsh-noteboard) | 0 | 2026-09-08 | 2026-09-08 | 便签画布 / Noteboard canvas for DeepSeek Harness (DSH)：框选会话内容一键存为便签（可 AI 提炼），便签以结构化引用再次发回 AI；工作区级无限画布。 |
| 43 | [CaffeineOddity/dsh-plugins](https://github.com/CaffeineOddity/dsh-plugins) | 0 | 2026-09-07 | 2026-09-08 | Deepseek harness plugins. |
| 44 | [chen704290901chen/dsh-newapi-video](https://github.com/chen704290901chen/dsh-newapi-video) | 0 | 2026-09-08 | 2026-09-08 | Call a new-api (one-api style) relay station's video model from the conversation, with @-referenced image/video materials plus a prompt. Supports Seedance 2.0 and Happyhorse text-to-video / image-to-video, four relay protocols, task ledger and a visual generation panel. |
| 45 | [chensenmiao/DeepSeek-Harness-Principles-and-Practice](https://github.com/chensenmiao/DeepSeek-Harness-Principles-and-Practice) | 0 | 2026-08-31 | 2026-09-08 | DeepSeek Harness 插件开发实战 —— 从零到一编写 Harness 插件的结构化教程，基于官方 65+ 篇文档整理而成，包含完整代码示例与实战案例。插件经理prd模式可以让agent先生成需求文档，随后进行插件生成 |
| 46 | [Choi-Peng/dsh-tenancy](https://github.com/Choi-Peng/dsh-tenancy) | 0 | 2026-08-27 | 2026-09-08 | 为 DeepSeek Harness(DSH)打造的单实例多租户插件:借助 Caddy + Authelia 认证前置提取用户身份,通过会话级 owner/access ACL、影子路由门控与事件流过滤实现会话/工作区的可见性隔离,并以工作区围栏与共享、邀请码注册、公开站点发布等能力,让互信团队安全共用一个 dsh 实例。 |
| 47 | [chromoany/dsh-notify-me](https://github.com/chromoany/dsh-notify-me) | 0 | 2026-09-08 | 2026-09-08 | DSH 桌面消息提醒插件 / desktop notification and message alerts for DeepSeek Harness web：需要你操作（可操作提醒）与回复完成提醒，系统通知+提示音+标签页标题，设置页开关 + 中英通知语言 |
| 48 | [DAAMAAO/datatally](https://github.com/DAAMAAO/datatally) | 0 | 2026-09-08 | 2026-09-08 | DataTally — usage records for data assets.     The first data-asset plugin for DeepSeek Harness.     Official domain: datatally.xyz |
| 49 | [dearbld/dsh-living-memory](https://github.com/dearbld/dsh-living-memory) | 0 | 2026-09-07 | 2026-09-08 | Living memory for DeepSeek Harness — self-tending local knowledge base: nightly patrol, temporal decay, RRF hybrid recall, knowledge graph. Built by 暖暖 (NuanNuan). |
| 50 | [dpskk2/dsh-sync-plugin](https://github.com/dpskk2/dsh-sync-plugin) | 0 | 2026-09-01 | 2026-09-08 | DeepSeek Harness 一键同步插件:页面⟳同步按钮,会话/设置/API密钥/插件/技能全量同步到私有 GitHub 仓库,支持会话删除 \| One-click sync plugin for DeepSeek Harness |
| 51 | [DshHunt/community](https://github.com/DshHunt/community) | 0 | 2026-09-08 | 2026-09-08 | Community submissions, evidence corrections, and methodology feedback for DSH Hunt |
| 52 | [dusbin/dsh-memory-view](https://github.com/dusbin/dsh-memory-view) | 0 | 2026-09-08 | 2026-09-08 | 查看 dsh 的 memory |
| 53 | [easyv-ai/dsh-pve](https://github.com/easyv-ai/dsh-pve) | 0 | 2026-09-07 | 2026-09-08 | Proxmox VE control plugin for DeepSeek Harness, with API token and password auth. |
| 54 | [EIGHTfs/dsh-skill-scoreboard](https://github.com/EIGHTfs/dsh-skill-scoreboard) | 0 | 2026-09-01 | 2026-09-08 | DSH skill 使用记分板：监听 tools/result，按会话去重自动累计 skill 加载次数。 |
| 55 | [Fishsb/dsh-project-nav](https://github.com/Fishsb/dsh-project-nav) | 0 | 2026-09-07 | 2026-09-08 | Anti-drift project governance plugin for DSH — bidirectional feature-map, mainline vector, architecture-first protocol \| DSH 项目反漂移治理插件 |
| 56 | [Flan246/dsh-plugin-litmus](https://github.com/Flan246/dsh-plugin-litmus) | 0 | 2026-09-08 | 2026-09-08 | Automated acceptance testing for DeepSeek Harness plugins: declarative scenarios, isolated headless runs, assertions and LLM judging. |
| 57 | [Ghpt6/dsh-system-prompt](https://github.com/Ghpt6/dsh-system-prompt) | 0 | 2026-09-08 | 2026-09-08 | 在 DeepSeek Harness 设置页编辑系统提示词，支持恢复默认与撤销修改 |
| 58 | [goatliamia/dsh-capability-facade](https://github.com/goatliamia/dsh-capability-facade) | 0 | 2026-09-08 | 2026-09-08 | Model Capability Facade for DeepSeek Harness: declare one semantic capability, get typed model-facing operations that run a deterministic pipeline of existing tools. |
| 59 | [IYIcode/dsh-ctx-probe](https://github.com/IYIcode/dsh-ctx-probe) | 0 | 2026-09-08 | 2026-09-08 | 自动探测本地模型上下文 dsh-ctx-probe — DSH plugin: auto-sync llm-pi-ai contextWindow with the real runtime window of local llama.cpp/Ollama servers (probe n_ctx per request; tighten before overflow, widen when the server grows). |
| 60 | [john-walks-slow/dsh-hybrid-notify](https://github.com/john-walks-slow/dsh-hybrid-notify) | 0 | 2026-09-08 | 2026-09-08 | Multi-channel notification plugin for DeepSeek Harness — in-page toast, PWA, and browser notifications with sound |
| 61 | [JRNitre/dsh_deepseekapi_quota](https://github.com/JRNitre/dsh_deepseekapi_quota) | 0 | 2026-09-08 | 2026-09-08 | Deepseek Harness Deepseek API Balance Display Plugins |
| 62 | [jtt0001/dsh-progress-overlay](https://github.com/jtt0001/dsh-progress-overlay) | 0 | 2026-09-08 | 2026-09-08 | Windows always-on-top task progress overlay for DeepSeek Harness (DSH): live phase/tool/command, real todo progress, multi-task list, approvals from the overlay. |
| 63 | [lffrom0303/dsh-window98-theme](https://github.com/lffrom0303/dsh-window98-theme) | 0 | 2026-09-08 | 2026-09-08 | A faithful Windows 98 skin for the DeepSeek Harness web GUI, derived from the classic 98.css design system. |
| 64 | [link-fgfgui/dsh-shutup](https://github.com/link-fgfgui/dsh-shutup) | 0 | 2026-09-08 | 2026-09-08 | Quiet DSH web bundle: no token gate, inverted --no-open, --host 0.0.0.0 allowed |
| 65 | [linxsy-code/dsh-plugin-window-input](https://github.com/linxsy-code/dsh-plugin-window-input) | 0 | 2026-09-08 | 2026-09-08 | Windows input plugin for deepseek harness |
| 66 | [lnyuqian/dsh-quick-prompts](https://github.com/lnyuqian/dsh-quick-prompts) | 0 | 2026-08-27 | 2026-09-08 | DSH Web 插件：输入框快捷输入（闪电笔），权限切换旁一键选预设提示词直接发送，提示词可增删改并持久化到项目根目录 |
| 67 | [lnyuqian/dsh-restart-plugin](https://github.com/lnyuqian/dsh-restart-plugin) | 0 | 2026-08-22 | 2026-09-08 | DSH Web 插件：一键重启 DSH Web 宿主（10 秒倒计时、自检探针、状态文件回写），支持静默计划任务触发 |
| 68 | [loommii/dsh-input-history](https://github.com/loommii/dsh-input-history) | 0 | 2026-09-07 | 2026-09-08 | DeepSeek Harness Web 输入历史插件:↑/↓ 终端式翻查本会话消息,/history 可搜索面板;纯客户端,按会话隔离。 |
| 69 | [lsdt45/dsh-plan-plus](https://github.com/lsdt45/dsh-plan-plus) | 0 | 2026-09-08 | 2026-09-08 | DeepSeek Harness 计划评审增强插件：评审弹窗内直接提意见修改计划，随时回看、对比、编辑每一版计划 |
| 70 | [lumoping/dsh-todo-inbox](https://github.com/lumoping/dsh-todo-inbox) | 0 | 2026-09-07 | 2026-09-08 | DSH web static plugin: global cross-session todo inbox (merge MR / approve work orders / reviews) with sidebar panel |
| 71 | [MikotoMyWife/dsh-mcp-loader](https://github.com/MikotoMyWife/dsh-mcp-loader) | 0 | 2026-09-08 | 2026-09-08 | Lazy-loading MCP tools for DeepSeek Harness (DSH): one loader tool per multi-tool MCP server, per-agent tool masking, description presets |
| 72 | [MncStudio/dsh-prompt-star](https://github.com/MncStudio/dsh-prompt-star) | 0 | 2026-09-08 | 2026-09-08 | DSH plugin: ⭐ button beside the input reads your draft + project doc files and generates a fuller prompt |
| 73 | [msn233/dsh-keymouse-use](https://github.com/msn233/dsh-keymouse-use) | 0 | 2026-09-08 | 2026-09-08 | A project that allow dsh to control your Windows. |
| 74 | [Nanmu-del/dsh-plan-toggle](https://github.com/Nanmu-del/dsh-plan-toggle) | 0 | 2026-09-08 | 2026-09-08 | DSH web client plugin: a persistent plan-mode toggle button in the composer tool row. |
| 75 | [Paul090515/dsh-system-cleanup](https://github.com/Paul090515/dsh-system-cleanup) | 0 | 2026-09-08 | 2026-09-08 | DSH skill：保守地自动清理系统缓存与垃圾文件（macOS / Linux / Windows）。可恢复删除、白名单制、不影响用户工作。 |
| 76 | [Rainflowers686/deepseek-harness-minimal-omni](https://github.com/Rainflowers686/deepseek-harness-minimal-omni) | 0 | 2026-09-04 | 2026-09-08 | DeepSeek Harness Minimal Omni Developer Preview: minimal-by-default runtime with on-demand capabilities and model-invisible governance |
| 77 | [RedMaple96/dsh-plugin-safety](https://github.com/RedMaple96/dsh-plugin-safety) | 0 | 2026-09-08 | 2026-09-08 | Install-time safety gate for the DSH plugin market: scans npm/GitHub plugins before install, passes safe ones silently, opens a review dialog for risky ones. |
| 78 | [Ricardo-WJP/dsh-signal](https://github.com/Ricardo-WJP/dsh-signal) | 0 | 2026-09-08 | 2026-09-08 | DSH Signal: tidal branding, verified resource quotas and local Token analytics for DeepSeek Harness |
| 79 | [RuyiAI-Stack/dsh-osc](https://github.com/RuyiAI-Stack/dsh-osc) | 0 | 2026-09-08 | 2026-09-08 | A deepSeek harness plugin for open-source collaboration |
| 80 | [ShawnKung/dsh-balance-monitor](https://github.com/ShawnKung/dsh-balance-monitor) | 0 | 2026-09-08 | 2026-09-08 | DSH Web 侧边栏余额与用量监控插件，支持 DeepSeek 官方 API 和 TeamoRouter。 |
| 81 | [shengyvself/dsh-reading-pad](https://github.com/shengyvself/dsh-reading-pad) | 0 | 2026-09-08 | 2026-09-08 | Immersive read-only reading panel for DeepSeek Harness: model delivers pre-formatted Markdown via reading_pad_send; 3 low-blue-light themes, 30em measure, progress bar, chapter browsing. better-sidebar tab plugin. Apache-2.0. |
| 82 | [softspark/dsh-web-search-searxng](https://github.com/softspark/dsh-web-search-searxng) | 0 | 2026-09-08 | 2026-09-08 | Web-search provider for DeepSeek Harness backed by a SearXNG instance: metasearch with no vendor API key and no account tying the queries together. |
| 83 | [sousike/dsh-faxin-search](https://github.com/sousike/dsh-faxin-search) | 0 | 2026-09-08 | 2026-09-08 | DSH client plugin: login your Faxin(faxin.cn) account and give AI structured legal search tools (law provisions / judicial interpretations / adjudication rules) |
| 84 | [techflag/dsh-plugin-ssh](https://github.com/techflag/dsh-plugin-ssh) | 0 | 2026-09-08 | 2026-09-08 | SSH/SFTP workspace and host-model server assistant for DeepSeek Harness. |
| 85 | [teethyachi/dsh-usage-mini](https://github.com/teethyachi/dsh-usage-mini) | 0 | 2026-09-07 | 2026-09-08 | USEAGE WINDOW \| DeepSeek Harness usage plugin. Currently supports Claude/Codex subscriptions and DeepSeek API only. |
| 86 | [tr1v3r/dsh-proxy](https://github.com/tr1v3r/dsh-proxy) | 0 | 2026-09-07 | 2026-09-08 | Runtime-switchable outbound proxy plugin for the DeepSeek Harness — hot-reload HTTP(S)/SOCKS5 routing via one settings section |
| 87 | [TT-Wang/dsh-agent-swarm](https://github.com/TT-Wang/dsh-agent-swarm) | 0 | 2026-09-08 | 2026-09-08 | #dsh-plugin Durable agent swarms for DeepSeek Harness: one-command planning, peer collaboration, independent verification, and an embedded sidebar. |
| 88 | [twilightt1/dsh-llm-chatgpt-web](https://github.com/twilightt1/dsh-llm-chatgpt-web) | 0 | 2026-09-08 | 2026-09-08 | ChatGPT Web as a DeepSeek Harness provider — owned Chromium daemon driving Temporary Chat, no API key |
| 89 | [TYEclipse/dsh-linalg](https://github.com/TYEclipse/dsh-linalg) | 0 | 2026-09-07 | 2026-09-08 | Linear algebra toolbox for DeepSeek Harness (dsh): matrix multiply, determinant, inverse, RREF, linear system solver, vector ops — zero runtime dependencies |
| 90 | [violetdream/dsh-officecli](https://github.com/violetdream/dsh-officecli) | 0 | 2026-09-07 | 2026-09-08 | dsh插件-结合officecli命令实现在Deepseek Harness中操作office文档 |
| 91 | [wangzhanchao883/dsh-resume-screening](https://github.com/wangzhanchao883/dsh-resume-screening) | 0 | 2026-09-08 | 2026-09-08 | Resume screening plugin for DeepSeek Harness (HR): ingest up to 100k resumes into one library, rule pre-filter + LLM fine-judge, auto-ingest & dedupe with ingest time. DeepSeek Harness 简历筛选插件:批量收简历建档,大白话下指令,库内规则粗筛+LLM精判,自动入库去重、可导出。 |
| 92 | [weibaohui/dsh-smart-title](https://github.com/weibaohui/dsh-smart-title) | 0 | 2026-09-08 | 2026-09-08 | dsh 插件 · 会话智能标题：LLM 总结改写会话标题，每轮对话后自动更新 |
| 93 | [Xingkong42/dsh-open-workspace](https://github.com/Xingkong42/dsh-open-workspace) | 0 | 2026-09-08 | 2026-09-08 | DSH (DeepSeek Harness) plugin: add "打开工作区 / Open workspace" entries to the workspace sidebar session-row menu and the session header actions slot; opens the session's workspace folder with the system file manager. |
| 94 | [yingtianlan/dsh-tauri-turnrewind](https://github.com/yingtianlan/dsh-tauri-turnrewind) | 0 | 2026-08-30 | 2026-09-08 | 每次 Agent 改动自动建私有快照，/undo 一键预览红绿 diff 并回滚本轮文件——卡内确认、冲突检测、不动你的 git历史 |
| 95 | [ystyle/dsh-harmonyos](https://github.com/ystyle/dsh-harmonyos) | 0 | 2026-09-07 | 2026-09-08 | dsh-harmonyos |
| 96 | [YuChuanhui3/dsh-plugin-attention-chime](https://github.com/YuChuanhui3/dsh-plugin-attention-chime) | 0 | 2026-09-08 | 2026-09-08 | 🔔 macOS sound + system notification whenever a DeepSeek Harness (dsh) agent needs your reply, answer, or approval — click the notification to jump to the session's browser tab. 后台任务守卫 / 升级递进提醒 / 设置页卡片配置。 |
| 97 | [yzxxy010/dsh-workspace-write-plus](https://github.com/yzxxy010/dsh-workspace-write-plus) | 0 | 2026-09-07 | 2026-09-08 | DSH 第四档权限 工作区修改++：文件仍锁工作区，通配符放行 Git Bash 等进程沙箱。 |
| 98 | [Zh1rV/dsh-web-search-tavily](https://github.com/Zh1rV/dsh-web-search-tavily) | 0 | 2026-08-24 | 2026-09-08 | DeepSeek Harness 的 Tavily 搜索插件 |
| 99 | [zhaoxuejie/dsh-plugin-tool-guard](https://github.com/zhaoxuejie/dsh-plugin-tool-guard) | 0 | 2026-09-08 | 2026-09-08 | DeepSeek Harness 工具调用安全守卫（防火墙）插件：危险命令拦截、路径白名单、敏感文件黑名单、人工审批与审计 |
| 100 | [zhengmz/dsh-wecom-plugin](https://github.com/zhengmz/dsh-wecom-plugin) | 0 | 2026-09-08 | 2026-09-08 | DSH 的企业微信插件 |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- chiphoton/DeepSeek-Harness-Video-Director
- FuRongJun-1999/CommonTrustProtocol
- FylarOpen/fylar-deepseek-harness-office-editor
- goatliamia/dsh-runtime-react
- HZ-JasonLin/dsh-todolist
- riesbri/dsh-plugins
- Shyboy0499/dsh-web-search
