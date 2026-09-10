# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-10**
- 快照日期 / Snapshot date: **2026-09-10 (UTC)**
- 待审核 / Pending: **137**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **26**
- Star 异常增长 / Star-growth alerts: **0**

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

对比上一份快照 **2026-09-09** / vs previous snapshot **2026-09-09**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **0**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| — | — | — | — | — | — | — | 本次无异常 / no alerts this snapshot |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [v587d/capital-generation](https://github.com/v587d/capital-generation) | 8 | 2026-08-16 | 2026-09-10 | 面向中国股市散户的金融投资智能体。Next-Gen AI-Driven Capital Generation. |
| 2 | [Cyning12/SpecWave](https://github.com/Cyning12/SpecWave) | 7 | 2026-08-16 | 2026-09-10 | SpecWave — multi-host coding CLI + P0 gates/Harness (Cursor/Claude/DSH). Formerly SpecGate / dsh-coding-kit. npx spec-wave |
| 3 | [grelvan/dsh-ocr-local](https://github.com/grelvan/dsh-ocr-local) | 6 | 2026-08-17 | 2026-09-10 |  DeepSeek Harness 本地 OCR 插件：粘贴图片，PP-OCRv5 + ONNX Runtime   识别文字，完全离线，支持 TUI 与 Web \| Local OCR plugin for DeepSeek Harness — paste an image, get its text via PP-OCRv5 + ONNX Runtime, fully offline.   Supports TUI and Web.  |
| 4 | [SiriusNEO/d.sh](https://github.com/SiriusNEO/d.sh) | 4 | 2026-09-10 | 2026-09-10 | Minimal agent harness in one Bash file. One-line quick start. Bootloader agent for bare-metal servers. |
| 5 | [xlennart/dsh-goal-mode-enhance](https://github.com/xlennart/dsh-goal-mode-enhance) | 4 | 2026-08-13 | 2026-09-10 | 为 DeepSeek Harness 提供可视化 goal 模式：Goal 栏 / 头部入口 / 设置页（历史+多会话总览）/ goal_overview 模型工具 |
| 6 | [shiningsprk-arch/dsh-context-viewer](https://github.com/shiningsprk-arch/dsh-context-viewer) | 3 | 2026-08-13 | 2026-09-10 | DeepSeek Harness (DSH) 上下文查看器 — 浏览思考链、shell 命令、工具调用与原始事件日志（Electron + React） |
| 7 | [xlennart/dsh-side-chat](https://github.com/xlennart/dsh-side-chat) | 3 | 2026-08-14 | 2026-09-10 | DeepSeek Harness native parallel side chat with hidden child sessions and on-demand parent context |
| 8 | [honghuachen/deepseekharness-desktop](https://github.com/honghuachen/deepseekharness-desktop) | 2 | 2026-09-04 | 2026-09-10 | 一键安装的跨平台桌面容器(macOS / Windows),完整运行官方 DeepSeek Harness Web 壳,内置兼容性守护机制,支持第三方插件管理、更新与移除,并自动拉取官方内核最新版本。 \| One-click cross-platform desktop container (macOS / Windows) running the official DeepSeek Harness Web shell, with built-in compatibility safeguards, third-party plugin management (update & remove), and automatic updates to the official runtime. |
| 9 | [kaelorvyn/dsh-archived-sessions](https://github.com/kaelorvyn/dsh-archived-sessions) | 2 | 2026-09-09 | 2026-09-10 | DSH 设置面板新增「已归档会话」页：列出全部已归档会话并一键恢复。Settings page listing archived sessions with one-click restore. |
| 10 | [pn1024/dsh-skill-market](https://github.com/pn1024/dsh-skill-market) | 2 | 2026-09-01 | 2026-09-10 | dsh plugin - skill marketplace (SkillHub + ClawHub) with sidebar entry, overlay panel, and chat input quick-pick |
| 11 | [benz-ai-x/dsh-research-graph](https://github.com/benz-ai-x/dsh-research-graph) | 1 | 2026-08-28 | 2026-09-10 | DSH Research Graph · 研图 — DeepSeek Harness plugin for research topics, traceable knowledge cards, and reusable AI discussions. |
| 12 | [CAI-MH/dsh-gpt-image](https://github.com/CAI-MH/dsh-gpt-image) | 1 | 2026-09-09 | 2026-09-10 | 控制已登录的网页版 ChatGPT 生成图片并下载到本地 — DSH bundle 插件。 |
| 13 | [domitor-syh/dsh-rollback](https://github.com/domitor-syh/dsh-rollback) | 1 | 2026-09-09 | 2026-09-10 | TRAE-style conversation rollback plugin for DeepSeek Harness |
| 14 | [dsh-cc/dsh-cc](https://github.com/dsh-cc/dsh-cc) | 1 | 2026-09-05 | 2026-09-10 | A batteries-included coding agent for DeepSeek Harness — Claude Code-style workflows, your choice of models, TUI, skills, subagents, hooks, MCP, memory, and worktrees. |
| 15 | [Enosensu/dsh-fork-relink](https://github.com/Enosensu/dsh-fork-relink) | 1 | 2026-09-10 | 2026-09-10 | DSH fork 伴随插件:fork 后自动重链子 agent 记录到新会话 / Auto-relink subagent records to a forked DSH session. Co-developed with AI. |
| 16 | [Grove-ovo/dsh-stack](https://github.com/Grove-ovo/dsh-stack) | 1 | 2026-09-10 | 2026-09-10 | Enforced safety rails for stacked PRs in DeepSeek Harness — every sync, land, and cleanup is guarded, and "tests passed" is proven per commit with SHA-bound validation records. |
| 17 | [HCY7757/dsh-lexiforge](https://github.com/HCY7757/dsh-lexiforge) | 1 | 2026-09-10 | 2026-09-10 | DeepSeek Harness 语言模组（LangPack）框架插件：以 ZIP 配置包提供 A/B/C 三种处理引擎与复合管线、术语检索增强、流拦截与安全安装机制，内置市场分发与风险免责闸门。LexiForge is a community LangPack framework plugin for DeepSeek Harness. |
| 18 | [idoall/dsh-quick-replies](https://github.com/idoall/dsh-quick-replies) | 1 | 2026-09-09 | 2026-09-10 | dsh-quick-replies |
| 19 | [idoall/dsh-update-status](https://github.com/idoall/dsh-update-status) | 1 | 2026-09-09 | 2026-09-10 | Read-only DeepSeek Harness Web version status and release-channel guidance plugin |
| 20 | [master1Sun/dsh-QQbot](https://github.com/master1Sun/dsh-QQbot) | 1 | 2026-09-08 | 2026-09-10 | dsh-QQbot |
| 21 | [mrSutivu/plugin-effort-slider](https://github.com/mrSutivu/plugin-effort-slider) | 1 | 2026-09-09 | 2026-09-10 | Notched reasoning-effort slider grouped with the model picker for DeepSeek Harness — native styling, themeable, i18n |
| 22 | [nagatoquin33/dsh-villager-hmm](https://github.com/nagatoquin33/dsh-villager-hmm) | 1 | 2026-09-10 | 2026-09-10 | Play a Minecraft villager hmm whenever the model hums inside its reasoning chain. DeepSeek Harness plugin. |
| 23 | [noteflowai/dsh-skills-anywhere](https://github.com/noteflowai/dsh-skills-anywhere) | 1 | 2026-09-10 | 2026-09-10 | Your skills, anywhere. Live Agent Skills provider for DeepSeek Harness (dsh): every agent's skill dirs (Claude Code, Codex, Cursor, 60+ more), Claude Code plugin marketplaces, and any GitHub skill repo. Zero copies, zero symlinks. |
| 24 | [phuongddx/jarvis](https://github.com/phuongddx/jarvis) | 1 | 2026-07-25 | 2026-09-10 | JARVIS is an intelligent layer that gives agents access to their code, knowledge, context, memory, tools, and runtime — starting locally on your machine, with the ability to extend into the cloud. |
| 25 | [Rabbit-bot-No-002/dsh-chat-avatar](https://github.com/Rabbit-bot-No-002/dsh-chat-avatar) | 1 | 2026-09-10 | 2026-09-10 | 轻量级DSH聊天头像插件 |
| 26 | [sss-1012/DeepSeek-Harness-Manager](https://github.com/sss-1012/DeepSeek-Harness-Manager) | 1 | 2026-08-21 | 2026-09-10 | Windows control center for DeepSeek Harness — manage plugins, profiles, diagnostics, updates and rollback. |
| 27 | [suomir1995/dsh-link-collect](https://github.com/suomir1995/dsh-link-collect) | 1 | 2026-09-10 | 2026-09-10 | DSH bundle（DeepSeek Harness 插件）：链接收藏 —— 把收藏的链接（标题/简介/图标/标签/正文）持久化为本地 Markdown 收藏夹，带 Web 侧栏页面。 |
| 28 | [tangjunyi1/dsh-remote-workspace](https://github.com/tangjunyi1/dsh-remote-workspace) | 1 | 2026-09-10 | 2026-09-10 | Remote workspaces for DeepSeek Harness: run the agent on your server over SSH stdio. Zero file mirroring. |
| 29 | [toustifer/dsh-harvest](https://github.com/toustifer/dsh-harvest) | 1 | 2026-08-25 | 2026-09-10 | DSH 原生多平台调研流水线插件：scout/extract/verify/audit 四件套，零依赖 |
| 30 | [ZhiGangCai/dsh-header-injection](https://github.com/ZhiGangCai/dsh-header-injection) | 1 | 2026-09-08 | 2026-09-10 | 请求头注入插件：DSH 插件，按 host 规则注入 HTTP 请求头（多条规则各自独立头集合，同名头覆盖原值），默认对 agentrouter.org 注入 User-Agent: RooCode/0.15.0 绕过其客户端 WAF；其余请求零影响 |
| 31 | [120777190/dsh_plugin](https://github.com/120777190/dsh_plugin) | 0 | 2026-09-10 | 2026-09-10 | 用Harmess搞的自用插件合集 |
| 32 | [2021Heei/dsh-tts-flash](https://github.com/2021Heei/dsh-tts-flash) | 0 | 2026-09-09 | 2026-09-10 | 给 DeepSeek Harness 的语音朗读插件：AI 回复流式 TTS 朗读，思考等待期还有趣味语音短语反馈。Edge TTS 开箱即用，支持任意 OpenAI 兼容云端引擎。 |
| 33 | [AcidGr/dsh-web-whale-maid](https://github.com/AcidGr/dsh-web-whale-maid) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness (dsh) Web plugin — Anime maid whale desktop pet with satiety system and real-time LLM interaction |
| 34 | [acryldev/cordis-plugin-graph](https://github.com/acryldev/cordis-plugin-graph) | 0 | 2026-09-10 | 2026-09-10 | DSH/Cordis Web plugin: a zoomable relation graph of every loaded plugin (dependencies, resolved providers, Loader-tree nesting) as a Settings tab next to 'Plugin list'. |
| 35 | [advance-lion/dsh-brand](https://github.com/advance-lion/dsh-brand) | 0 | 2026-09-10 | 2026-09-10 | 方便魔改作者轻量化自定义商标 |
| 36 | [ALIWUER/dsh-process-panel](https://github.com/ALIWUER/dsh-process-panel) | 0 | 2026-09-10 | 2026-09-10 | dsh 侧栏「进程任务」面板：启动/停止/重启长时后台进程 + 实时日志，AI 侧配 sv_* 工具。A process panel plugin for DeepSeek Harness. |
| 37 | [Arborsm/dsh-memory-plugin](https://github.com/Arborsm/dsh-memory-plugin) | 0 | 2026-09-10 | 2026-09-10 | Cross-session long-term memory plugin for DeepSeek Harness |
| 38 | [awol2005ex3/dsh-wecom](https://github.com/awol2005ex3/dsh-wecom) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness (dsh) plugin: WeCom (WeChat Work) smart-robot integration over the long-connection (WebSocket) API. Per-session agents, idempotent msgid dedup, stream/markdown replies, media download/upload, whitelist, welcome/feedback events. |
| 39 | [azizemreozturk/dsh-locale-tr](https://github.com/azizemreozturk/dsh-locale-tr) | 0 | 2026-09-10 | 2026-09-10 | Turkish language pack for DeepSeek Harness web UI (42 namespaces, 1278 strings) |
| 40 | [biubiu23333333/dsh-memorix-panel](https://github.com/biubiu23333333/dsh-memorix-panel) | 0 | 2026-09-10 | 2026-09-10 | Memorix memory panel for the DSH Web GUI: browse every project and memory, read full details, archive/restore and create memories — writes go through the official memorix CLI. |
| 41 | [CAI-MH/dsh-agent-bridge](https://github.com/CAI-MH/dsh-agent-bridge) | 0 | 2026-09-09 | 2026-09-10 | 飞书机器人 → DSH 会话桥：在指定工作区开真会话，用 DSH 现有模型+插件执行任务并回传结论 — DSH bundle。 |
| 42 | [CAI-MH/dsh-agent-group-panel](https://github.com/CAI-MH/dsh-agent-group-panel) | 0 | 2026-09-09 | 2026-09-10 | 飞书多助手机器人控制台：开启/关闭/重连守护进程、状态与最近动态、直达任务工作区 — DSH bundle。 |
| 43 | [CAI-MH/dsh-plugin-forge](https://github.com/CAI-MH/dsh-plugin-forge) | 0 | 2026-09-09 | 2026-09-10 | 插件工坊：在任意工作区按 dph 格式快速脚手架 DSH 本地插件，并维护踩坑经验库持续修正开发 — DSH bundle。 |
| 44 | [CAI-MH/dsh-sysbrief](https://github.com/CAI-MH/dsh-sysbrief) | 0 | 2026-09-09 | 2026-09-10 | 系统理解简报工作流：解析 PRD/PDF、分批追问澄清目标系统并沉淀 BRIEF.md，最终打包可上传交付物 — DSH bundle。 |
| 45 | [catsenior507/dsh-context-assembler](https://github.com/catsenior507/dsh-context-assembler) | 0 | 2026-09-10 | 2026-09-10 | Assembled context for DeepSeek Harness: a context tree over the session surface with per-node assemble modes (full / key / off), agent-authored presets, and a panel that decides what the model actually sees. |
| 46 | [catsenior507/dsh-policy-strict-gate](https://github.com/catsenior507/dsh-policy-strict-gate) | 0 | 2026-09-10 | 2026-09-10 | Enforce strict checks as dsh harness policy: repeated-failure intervention, a glob-protected critical-path gate that blocks with diagnostics, and an automatic post-write check. |
| 47 | [catsenior507/dsh-tool-failure-journal](https://github.com/catsenior507/dsh-tool-failure-journal) | 0 | 2026-09-10 | 2026-09-10 | Durable failure journal for dsh tool calls: every abnormal exit appended to JSONL on disk, folded by error signature, readable back by the agent. |
| 48 | [catsenior507/dsh-tool-strict-check](https://github.com/catsenior507/dsh-tool-strict-check) | 0 | 2026-09-10 | 2026-09-10 | Strict checker for dsh: verify code and commands with real checkers - Lean 4 kernel checking, language compilers, and harness-shell hazard rules. |
| 49 | [converk/dsh-tweaks](https://github.com/converk/dsh-tweaks) | 0 | 2026-09-10 | 2026-09-10 | 让 DSH（DeepSeek Harness）更顺手的一套小改动：prompt-history / model-capabilities / turn-file-revert 三个独立插件 |
| 50 | [dat-lequoc/dsh-notifications](https://github.com/dat-lequoc/dsh-notifications) | 0 | 2026-09-10 | 2026-09-10 | Desktop notifications and chimes for DeepSeek Harness Web |
| 51 | [Daviszhou212/dsh-cost-pill](https://github.com/Daviszhou212/dsh-cost-pill) | 0 | 2026-09-10 | 2026-09-10 | DSH web plugin: session API cost + account balance, as a pill merged into the official composer stats row (费用 · 余额 · 缓存命中). |
| 52 | [dboycht/dsh-cooldown-retry](https://github.com/dboycht/dsh-cooldown-retry) | 0 | 2026-09-10 | 2026-09-10 | Patient auto-retry for DeepSeek Harness — reads the retry delay out of an upstream 429 capacity-cooldown message and waits it out, instead of giving up after two fast retries. |
| 53 | [EmmanuelMartinez/tolten-image-attach](https://github.com/EmmanuelMartinez/tolten-image-attach) | 0 | 2026-09-10 | 2026-09-10 | Attach an image to the DeepSeek Harness composer and the session model switches itself to a vision model — then restores your previous model when the image is removed. Material Design 3 button, native file picker, thumbnails. MIT. |
| 54 | [f-infinite-z/dsh-plugin-ops](https://github.com/f-infinite-z/dsh-plugin-ops) | 0 | 2026-09-09 | 2026-09-10 | DeepSeek Harness plugin operations: pre-boot health gate, failure attribution, dependency governance, and a web panel — the startup-lifecycle guard for the dsh plugin ecosystem. |
| 55 | [fishOfOUC/dsh-price-monitor](https://github.com/fishOfOUC/dsh-price-monitor) | 0 | 2026-09-10 | 2026-09-10 | Session cost monitor for DeepSeek Harness — a dsh-better-sidebar tab (that sidebar is required; this package ships no UI of its own) showing per-turn, per-attempt token cost priced by official or manual plans |
| 56 | [FitBBC/dsh-plugin-tokensmarket](https://github.com/FitBBC/dsh-plugin-tokensmarket) | 0 | 2026-09-10 | 2026-09-10 | Token Market provider bundle for DeepSeek Harness |
| 57 | [genen-s/dsh-plugins](https://github.com/genen-s/dsh-plugins) | 0 | 2026-09-10 | 2026-09-10 | Personal dsh plugins for the DeepSeek Harness web profile (agent-monitor, quick-notes) |
| 58 | [Harris-Logic/dsh-resume-turn](https://github.com/Harris-Logic/dsh-resume-turn) | 0 | 2026-09-10 | 2026-09-10 | DSH 断点续接插件：模型回复因网络中断/超时半途失败时，自动把已生成的部分输出带进下一轮，让模型从中断处继续，而不是从零全量重跑。DSH plugin: on a mid-stream network failure, auto-resume the turn from its partial output instead of restarting from scratch. |
| 59 | [HDNRAY/dsh-plugin-colorguess](https://github.com/HDNRAY/dsh-plugin-colorguess) | 0 | 2026-09-01 | 2026-09-10 | 等结果时换换脑筋 |
| 60 | [huangyuheng/dsh-token-usage](https://github.com/huangyuheng/dsh-token-usage) | 0 | 2026-09-09 | 2026-09-10 | 实时 Token 用量仪表盘 · Real-time token usage dashboard for DeepSeek Harness — live totals, filters by model/day/month/project, smooth trend chart. |
| 61 | [hutao562/dsh-remote-dsh](https://github.com/hutao562/dsh-remote-dsh) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness plugin: a sidebar tab that takes over the whole page with another DSH instance's Web GUI, plus a remote session-state badge. 在侧边栏顶部加一个「远程」标签，整页切到另一台主机上的 DSH。 |
| 62 | [ice5kysl/dsh-why](https://github.com/ice5kysl/dsh-why) | 0 | 2026-09-09 | 2026-09-10 | dsh (DeepSeek Harness) failure diagnostics CLI — why a plugin crashes the loader (missed the module table), engines.dsh mismatch, known official breaking points, ecosystem cross-check. Zero-dep, read-only, offline-capable. 失败诊断 CLI，零依赖只读离线可用。 |
| 63 | [Imnotndesh/dsh-peak-pricing-warning](https://github.com/Imnotndesh/dsh-peak-pricing-warning) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness plugins: peak/off-peak pricing warning with live countdown, plus a session cost estimator priced from real DeepSeek billing buckets and published rates. |
| 64 | [jiekesu967/dsh-markitdown](https://github.com/jiekesu967/dsh-markitdown) | 0 | 2026-09-10 | 2026-09-10 | Microsoft MarkItDown as a DeepSeek Harness tool: convert PDF, Word, Excel, PowerPoint, HTML, CSV, EPUB, or a URL into Markdown the model can read. |
| 65 | [jonah791/dsh-video-studio](https://github.com/jonah791/dsh-video-studio) | 0 | 2026-09-10 | 2026-09-10 | DSH 视频工作台插件：把视频工厂（TTS/配乐/混音/Remotion 渲染/多级质检/主题脚手架）封装为工具面，支撑创作任意视频 |
| 66 | [JularDepick/dsh-wakatime-plugin](https://github.com/JularDepick/dsh-wakatime-plugin) | 0 | 2026-08-15 | 2026-09-10 | A plugin for dsh: quantify every dsh Agent interaction as a visualized performance metric and automatically sync it to WakaTime -- use data to showcase your productivity with Agent. |
| 67 | [kovey/dsh-chat-interaction](https://github.com/kovey/dsh-chat-interaction) | 0 | 2026-09-10 | 2026-09-10 | Abstract interaction layer between DeepSeek Harness (DSH) and IM platforms (Feishu, WeCom, ...). Channel-agnostic hub with proven interaction patterns (dedupe, instant ack, wait-reply, followup wakeup, scoring-based model routing, approval gate) plus pluggable adapters for Feishu and WeCom. |
| 68 | [LeeGuanWei-a/dsh-mini-games-lee](https://github.com/LeeGuanWei-a/dsh-mini-games-lee) | 0 | 2026-09-10 | 2026-09-10 | 🎮 DeepSeek Harness Web 端小游戏合集：俄罗斯方块 / 贪吃蛇 / 2048 / 扫雷，一个可拖动毛玻璃悬浮窗，支持深浅色主题与各游戏独立排行榜，一条命令安装。实测 @deepseek-ai/dsh 0.1.2-rc.1。 |
| 69 | [leeyoung1/dsh-web-search-opencode-go](https://github.com/leeyoung1/dsh-web-search-opencode-go) | 0 | 2026-09-10 | 2026-09-10 | Fix DSH web_search through OpenCode Go / Zen: auto-inject x-opencode-session. Drop-in patched fork of @deepseek-ai/dsh-web-search-deepseek. |
| 70 | [lide4144/dsh-tidewatch](https://github.com/lide4144/dsh-tidewatch) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness 动态插件：悬浮面板显示 DeepSeek API 高峰/低谷时段、倒计时与账户余额 |
| 71 | [Lin-A1/dsh-workbench](https://github.com/Lin-A1/dsh-workbench) | 0 | 2026-09-04 | 2026-09-10 | DeepSeek Harness 的协同工作台插件：在对话旁的右侧栏里，人与 AI 共写同一把真实 PTY Shell、共读同一份网页预览，另有 Git 变更面板与输入归属审计。 |
| 72 | [liooil/dsh-files-pane](https://github.com/liooil/dsh-files-pane) | 0 | 2026-09-10 | 2026-09-10 | In-browser files pane for the DeepSeek Harness Web GUI: a Session View tab that browses the host's files and reads them in place. · DSH 网页「文件」视图标签：两栏目录导航 + 就地阅读文件 |
| 73 | [lmr233/dsh-git-update-notifier](https://github.com/lmr233/dsh-git-update-notifier) | 0 | 2026-09-10 | 2026-09-10 | 每天首次启动 dsh 时用 git 检测上游提交并在 Web GUI 中询问是否更新（适配源码 checkout，不改 npm 依赖） |
| 74 | [looeton/dsh-plugin-proxy-env](https://github.com/looeton/dsh-plugin-proxy-env) | 0 | 2026-09-10 | 2026-09-10 | DSH plugin: inject proxy environment variables at startup and self-check the whole proxy chain |
| 75 | [looking321-rt/dsh-tps-meter](https://github.com/looking321-rt/dsh-tps-meter) | 0 | 2026-09-10 | 2026-09-10 | 一款搭配 DSH 客户端的悬浮窗小工具，实时监测并显示会话的实时与平均 Token 输出速率（tokens/s） |
| 76 | [lovvvve/dsh-quick-actions](https://github.com/lovvvve/dsh-quick-actions) | 0 | 2026-09-07 | 2026-09-10 | Global Quick Actions for the DSH message composer |
| 77 | [lt9/dsh-simple-auth](https://github.com/lt9/dsh-simple-auth) | 0 | 2026-09-03 | 2026-09-10 | Ultra-light dsh login gate: shared key or master/guest keys, ACL-filtered session list, owner-only share/unshare FAB. |
| 78 | [mabaoguo9527/dsh-file-explorer](https://github.com/mabaoguo9527/dsh-file-explorer) | 0 | 2026-09-10 | 2026-09-10 | Workspace file explorer docked in the DeepSeek Harness sidebar — lazy file tree, Settings toggle, drag-to-resize. Also shipped as a single-session Cordis dynamic plugin. |
| 79 | [Mandarin715/dsh-autostart](https://github.com/Mandarin715/dsh-autostart) | 0 | 2026-09-10 | 2026-09-10 | Windows 专用 DSH 插件:一键开机自启 + 一键重启 DSH 服务,全程无控制台窗口 \| Windows-only DSH plugin for boot autostart and one-click restart |
| 80 | [ManoloRemiddi/DSH-Metafolder-Plugin](https://github.com/ManoloRemiddi/DSH-Metafolder-Plugin) | 0 | 2026-09-10 | 2026-09-10 | DSH Metafolder Plugin — visual meta-folders for the DeepSeek Harness sidebar workspaces: nest real folders under named, coloured groups by drag and drop, without touching paths, permissions, sessions or workspace order. |
| 81 | [masknull/dsh-model-tester](https://github.com/masknull/dsh-model-tester) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness plugin: one-click model availability testing (available / TPS / first token / elapsed) in the Models settings page |
| 82 | [masquerator-coder/dsh-im-gateway](https://github.com/masquerator-coder/dsh-im-gateway) | 0 | 2026-08-30 | 2026-09-10 | Deepseek harness im gateway |
| 83 | [masquerator-coder/dsh-memory](https://github.com/masquerator-coder/dsh-memory) | 0 | 2026-08-30 | 2026-09-10 | Deepseek Harness memory plugin |
| 84 | [masquerator-coder/dsh-preset-skills](https://github.com/masquerator-coder/dsh-preset-skills) | 0 | 2026-09-02 | 2026-09-10 | Mount each dsh agent preset's own skills/ directory, isolated per preset. Out-of-tree, zero dsh-source changes. |
| 85 | [Mempemp/DSH-runner-rlm-tools-bsl](https://github.com/Mempemp/DSH-runner-rlm-tools-bsl) | 0 | 2026-09-10 | 2026-09-10 | Плагин DeepSeek Harness: MCP-сервер rlm-tools-bsl (анализ кода 1С) запускается и останавливается вместе с DSH |
| 86 | [Meowrium/dsh-auto-continue](https://github.com/Meowrium/dsh-auto-continue) | 0 | 2026-09-10 | 2026-09-10 | dsh plugin: auto-continue after quota/rate-limit reset + peak/valley idle-task suspend/resume, with composer toggles and a status line. |
| 87 | [Meowrium/dsh-sidebar-image-zoom](https://github.com/Meowrium/dsh-sidebar-image-zoom) | 0 | 2026-09-10 | 2026-09-10 | dsh plugin: zoomable, pannable image preview for the right-sidebar document pane (wheel zoom anchored at cursor, drag pan, fit / 1:1). / dsh 右侧边栏图片预览缩放插件 |
| 88 | [Nanako660/dsh-cost-meter](https://github.com/Nanako660/dsh-cost-meter) | 0 | 2026-09-10 | 2026-09-10 | Session spend for the DSH Web client: a stats-line pill that prices the durable tokenUsage projection with user-configured per-bucket unit prices. |
| 89 | [Nicholaskin/vision-exp-tile](https://github.com/Nicholaskin/vision-exp-tile) | 0 | 2026-09-10 | 2026-09-10 | DSH（DeepSeek Harness）插件：800×800 无损切块 + 坐标标注 + 直连 DeepSeek 视觉 API 识别聚合，专治大图看不清 |
| 90 | [PerryLink/dsh-plugin-doctor](https://github.com/PerryLink/dsh-plugin-doctor) | 0 | 2026-09-07 | 2026-09-10 | Zero-dependency static + sandbox smoke detector for DeepSeek Harness plugins (R/K/D/CC layers) |
| 91 | [PerryLink/dsh-plugin-upgrade-rc1](https://github.com/PerryLink/dsh-plugin-upgrade-rc1) | 0 | 2026-09-10 | 2026-09-10 | Version-locked upgrade corridor for DSH plugins: dsh-v0.1.5-alpha.1 -> dsh-v0.1.5-rc.1 (card + skill + zero-dependency scanner) |
| 92 | [polohot/dsh-adrian-agents-group-work](https://github.com/polohot/dsh-adrian-agents-group-work) | 0 | 2026-09-10 | 2026-09-10 | Group work for the DeepSeek Harness: turn one session into a room with a chair and several member agents that message each other and share a task list. |
| 93 | [popujiang/dsh-turn-scratch](https://github.com/popujiang/dsh-turn-scratch) | 0 | 2026-09-10 | 2026-09-10 | DSH turn scratch cleanup plugin |
| 94 | [Practice019/dsh-plugins-store](https://github.com/Practice019/dsh-plugins-store) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness (DSH) plugin store - archived copies of the plugins installed in the local web profile, with manifest and profile snapshot |
| 95 | [PRTS168/dsh-wechat-suite](https://github.com/PRTS168/dsh-wechat-suite) | 0 | 2026-09-07 | 2026-09-10 | Chat with, monitor and approve your DSH agents from WeChat: two-way text/images/voice/files/video over the iLink gateway, OCR, STT/TTS, image generation, reminders, morning weather, approvals. |
| 96 | [Robin1987China/dsh-plugin-preset-default-guard](https://github.com/Robin1987China/dsh-plugin-preset-default-guard) | 0 | 2026-09-10 | 2026-09-10 | Repairs a stale agent-presets.default so New Session stops failing silently after a preset rename (DeepSeek Harness plugin). |
| 97 | [Rosmeowtis/dsh-es](https://github.com/Rosmeowtis/dsh-es) | 0 | 2026-09-10 | 2026-09-10 | DSH 使用 Everything(es.exe) 工具进行 NTFS 全盘搜索，使用  POSIX 风格路径进行交互，兼容 MSYS(git bash) 路径。 |
| 98 | [ruby1304/dsh-session-pilot](https://github.com/ruby1304/dsh-session-pilot) | 0 | 2026-09-10 | 2026-09-10 | Pilot your DeepSeek Harness conversations from inside a conversation: new_conversation, rename_session, list_sessions, read_session, archive_session model tools plus official-slot UI actions |
| 99 | [runcat-tommy/dsh-unitverse](https://github.com/runcat-tommy/dsh-unitverse) | 0 | 2026-09-09 | 2026-09-10 | Unit conversion plugin for DeepSeek Harness (DSH): one `convert` tool plus a locale-aware Web view, covering 10 categories (length, area, volume, time, angle, speed, temperature, pressure, energy/heat, power) with 80+ units. 单位换算 DSH 插件：十大类 80+ 单位，convert 工具与 Web 视图均支持中英文。 |
| 100 | [s867968286/dsh-preset-md](https://github.com/s867968286/dsh-preset-md) | 0 | 2026-09-10 | 2026-09-10 | 给 DSH 助手赋予人格、灵魂与长期记忆：用 Markdown 定义伙伴的身份、性格、准则与记忆，自动写日记、自动更新记忆。Give your DSH assistant a soul, personality, and long-term memory. |
| 101 | [Saknutella/dsh-thinking-quips](https://github.com/Saknutella/dsh-thinking-quips) | 0 | 2026-09-10 | 2026-09-10 | Playful bilingual quips for the DeepSeek Harness (DSH) running-turn indicator. |
| 102 | [scavanger2221/dsh-llm-opencode-go](https://github.com/scavanger2221/dsh-llm-opencode-go) | 0 | 2026-09-10 | 2026-09-10 | OpenCode Go models as a DeepSeek Harness provider, with session-affinity headers, a live model catalog, and a Web settings card |
| 103 | [SCP-CN-1059/dsh-zhouli](https://github.com/SCP-CN-1059/dsh-zhouli) | 0 | 2026-09-10 | 2026-09-10 | 《周礼》插件：给 DeepSeek Harness 提供带稳定坐标（篇序.职官序）的全文检索工具，含职官员额／职掌索引与 Kanripo 两本互校勘记，并附一套依六官法度行事的 agent 预设。引文可核，不凭记忆。 |
| 104 | [Shyboy0499/dsh-pr-watch](https://github.com/Shyboy0499/dsh-pr-watch) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness plugin: reports what changed in your authored pull requests since your last check — merged, closed, or gone stale. |
| 105 | [SmailPang/dsh-effort-slider](https://github.com/SmailPang/dsh-effort-slider) | 0 | 2026-09-09 | 2026-09-10 | 为 DeepSeek Harness 添加支持 Off、Low、High、Max 档位的可拖动推理强度滑块。 |
| 106 | [SodaZheng/dsh-totp](https://github.com/SodaZheng/dsh-totp) | 0 | 2026-09-09 | 2026-09-10 | 为 DeepSeek Harness 加一道由你掌控的访问验证。An access-verification step for DeepSeek Harness, under your control. |
| 107 | [sojo-negai/dsh-prompt-refine](https://github.com/sojo-negai/dsh-prompt-refine) | 0 | 2026-09-10 | 2026-09-10 | DSH 提示词优化插件 —— 发送前点一下 ✨,模型结合上下文给出「补丁式」建议,勾选回填,不抢发送权。 |
| 108 | [StevenZha0/dsh-vae-theme](https://github.com/StevenZha0/dsh-vae-theme) | 0 | 2026-09-10 | 2026-09-10 | 《庐州月 · 许嵩》— DeepSeek Harness 国风水墨主题插件 \| 夜色水墨长卷 · 金丝九宫格边框 · VAE 书法标志 · 全屏雨幕 · 国风歌词竖排轮播 |
| 109 | [suomir1995/dsh-notes](https://github.com/suomir1995/dsh-notes) | 0 | 2026-09-10 | 2026-09-10 | DSH bundle（DeepSeek Harness 插件）：笔记 —— 按目录分组的本地 Markdown 笔记，带 Web 侧栏页面，读取根/分组下的 AGENTS 等规则 md 作为写作上下文。 |
| 110 | [telagod/dsh-ssh-workspace-manager](https://github.com/telagod/dsh-ssh-workspace-manager) | 0 | 2026-09-10 | 2026-09-10 | DSH web plugin: SSH hosts, workspace bindings, remote exec/sync/compose |
| 111 | [TianJie52009/dsh-kaomoji](https://github.com/TianJie52009/dsh-kaomoji) | 0 | 2026-09-09 | 2026-09-10 | Add Japanese kaomoji to DeepSeek Harness (dsh) replies; prompt-injection plugin with a curated kaomojiya.org library. |
| 112 | [tianyagk/dsh-tradewatcher](https://github.com/tianyagk/dsh-tradewatcher) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness (DSH) web plugin: 盯盘 market-dashboard sidebar tab — three quote strips with hover intraday charts, watchlist with industry alpha, ledger-driven portfolio P&L, A-share boards & detail drawer, host-side Eastmoney relay + read-only agent tools. |
| 113 | [TodayWei/dsh-wei-sitecontrol](https://github.com/TodayWei/dsh-wei-sitecontrol) | 0 | 2026-09-10 | 2026-09-10 | Site controller for DeepSeek Harness: register websites/HTTP services and manage their lifecycle, git, and release-based SSH deploys — with server probing, stored deploy scripts, rollback and scheduled publishing. |
| 114 | [TYEclipse/dsh-boolean](https://github.com/TYEclipse/dsh-boolean) | 0 | 2026-09-09 | 2026-09-10 | Boolean algebra toolbox for DeepSeek Harness (dsh): truth tables with minterm/maxterm summaries, canonical DNF/CNF, NNF, NAND-only/NOR-only gate networks, equivalence checking |
| 115 | [uigdwunm/dsh-conversation-jump](https://github.com/uigdwunm/dsh-conversation-jump) | 0 | 2026-08-18 | 2026-09-10 | 为 DSH Web 对话区提供回到顶部 / 上一条 / 下一条 / 回到底部的圆形导航按钮，自动处理更早历史分页。 |
| 116 | [UnforgetMemory/um-dsh-azimg](https://github.com/UnforgetMemory/um-dsh-azimg) | 0 | 2026-09-08 | 2026-09-10 | Give DeepSeek Harness (DSH) agents eyes: local image analysis via vision models — um_analyze_img tool, model-capability recognition, hot-switch settings UI. |
| 117 | [vitas/dsh-model-pricing](https://github.com/vitas/dsh-model-pricing) | 0 | 2026-09-09 | 2026-09-10 | Model pricing & capability board for DeepSeek Harness: per-1M-token prices for 7,100+ models across 213 providers (models.dev + harness catalog overlay), cheapest-route comparison, capability tags, and a community promotion feed. |
| 118 | [VviLliAm-qwq/dsh-peak-balance](https://github.com/VviLliAm-qwq/dsh-peak-balance) | 0 | 2026-09-10 | 2026-09-10 | Peak/off-peak billing clock with live DeepSeek balance and per-turn cost above the dsh-tui prompt, plus an optional flashing peak-hour warning frame. |
| 119 | [Wandering233/dsh-keyless-search](https://github.com/Wandering233/dsh-keyless-search) | 0 | 2026-09-10 | 2026-09-10 | 免 API key 的多引擎搜索 provider for DeepSeek Harness (ctx.web)：真实浏览器 Google + 国际版 Bing + 中文 Bing，带代理自动探测、语言感知与浏览器空闲回收 |
| 120 | [wanghaixu-hai/dsh-effort-router](https://github.com/wanghaixu-hai/dsh-effort-router) | 0 | 2026-09-10 | 2026-09-10 | DSH 模型分流插件：按每一轮请求的难度自动选模型与思考强度——简单问题走便宜快模型，难题才叫强模型。零 token 规则判定，只在判不准的灰区问一次小模型。发送前把本轮计划同步到输入框的模型框，座位=实际；不改你的默认模型。 |
| 121 | [wbaws/dsh-scenery](https://github.com/wbaws/dsh-scenery) | 0 | 2026-09-09 | 2026-09-10 | Capy-style ambient background for the DeepSeek Harness (DSH) workspace: custom image + very large bottom black gradient + soft radial aura around the composer. Additive plugin - existing UI untouched. |
| 122 | [wcnm8888/dsh-plugin-update-audit](https://github.com/wcnm8888/dsh-plugin-update-audit) | 0 | 2026-09-10 | 2026-09-10 | Read-only update auditing for DeepSeek Harness profile plugins |
| 123 | [wesleyel/dsh-plugin-gpt-load](https://github.com/wesleyel/dsh-plugin-gpt-load) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness plugin: serve every gpt-load model from one provider group, each model on its own wire protocol (OpenAI Chat Completions or Anthropic Messages), synced from /api/models |
| 124 | [whiteS18/dsh-image-generation](https://github.com/whiteS18/dsh-image-generation) | 0 | 2026-09-09 | 2026-09-10 | DSH plugin: configure image providers in Settings and generate with image_generate |
| 125 | [wu81313-lab/dsh-image-studio](https://github.com/wu81313-lab/dsh-image-studio) | 0 | 2026-09-10 | 2026-09-10 | Inline image card for DeepSeek Harness conversations: a bottom-left edit button that annotates, erases through a generated RGBA mask, and crops or resizes, then hands the edit back to the agent. |
| 126 | [wx-yss/dsh-composer-enter](https://github.com/wx-yss/dsh-composer-enter) | 0 | 2026-09-10 | 2026-09-10 | 让 DSH 0.1.5 使用 Enter 换行、Cmd/Ctrl+Enter 提交 |
| 127 | [xytoki/dsh-cursor-agent](https://github.com/xytoki/dsh-cursor-agent) | 0 | 2026-09-09 | 2026-09-10 | 在DeepSeek Hareness中引入Cursor Hareness，获得和Cursor一致的速度与体验。非官方调用cursor api，可能引入账号风险，谨慎使用。 |
| 128 | [xzs125/dsh-codex-reset-watch](https://github.com/xzs125/dsh-codex-reset-watch) | 0 | 2026-09-09 | 2026-09-10 | DSH 插件：监控 X @thsottiaux 的 Codex reset 公告，左侧边栏底部 R 图标（常态灰 / 有重置时 #66ccff 点亮；hover 倒计时+北京时间；单击打开推文、双击立即检查并蓝色闪烁） |
| 129 | [yingjian666/dsh-zh-thinking](https://github.com/yingjian666/dsh-zh-thinking) | 0 | 2026-09-06 | 2026-09-10 | DeepSeek Harness (dsh) 插件：注入系统提示词，强制 Agent 的思维链 / 规划 / 工具推理全程使用简体中文，防止中文思考漂移为英文。零外部依赖，任意本地目录 link 即装。 |
| 130 | [zhang-guo-wen/dsh-claude-compat](https://github.com/zhang-guo-wen/dsh-claude-compat) | 0 | 2026-09-09 | 2026-09-10 | deepseek harness 插件，兼容claude的skill、rules加载规则，mcp配置 |
| 131 | [zhaoxuejie/dsh-plugin-academic-paper](https://github.com/zhaoxuejie/dsh-plugin-academic-paper) | 0 | 2026-09-08 | 2026-09-10 | DeepSeek Harness 学术文献插件：arXiv / Semantic Scholar 真实数据源检索、单篇详情、GB/T 7714 / APA / BibTeX 引用格式生成、本地文献库与批量导出，杜绝模型编造文献信息 |
| 132 | [zhaoxuejie/dsh-plugin-desktop-notice](https://github.com/zhaoxuejie/dsh-plugin-desktop-notice) | 0 | 2026-09-07 | 2026-09-10 | DSH 桌面通知插件：任务完成 / 等待输入 / 失败时，右下角弹窗 + 音效 + 手机推送（Windows / macOS / Linux） |
| 133 | [zhaoxuejie/dsh-plugin-session-export](https://github.com/zhaoxuejie/dsh-plugin-session-export) | 0 | 2026-09-07 | 2026-09-10 | DeepSeek Harness 会话黑匣子插件：全量旁路采集会话事件，一键导出美化 Markdown / HTML 复盘报告，内置 Web 统计面板 |
| 134 | [zhaoxuejie/dsh-plugin-todo-scanner](https://github.com/zhaoxuejie/dsh-plugin-todo-scanner) | 0 | 2026-09-08 | 2026-09-10 | DeepSeek Harness TODO 代码扫描插件：递归扫描本地代码标记，生成结构化清单，支持状态管理、Markdown 导出与侧边「TODO 雷达」面板。 |
| 135 | [zhaoxuejie/dsh-plugin-vault-memory](https://github.com/zhaoxuejie/dsh-plugin-vault-memory) | 0 | 2026-09-07 | 2026-09-10 | 让 DeepSeek Harness agent 把本地 Obsidian 知识库当作长期记忆与工作台：全文/语义检索、会话记忆注入、一键捕获、巡检管家（只建议不擅改） |
| 136 | [zhaoxuejie/moqian-dsh-plugin-list](https://github.com/zhaoxuejie/moqian-dsh-plugin-list) | 0 | 2026-09-10 | 2026-09-10 | DeepSeek Harness（DSH）插件清单：收录 9 个开源 dsh-plugin —— 工具安全守卫、实时日志转发、会话复盘导出、Obsidian 长期记忆、学术文献检索、TODO 扫描、桌面通知提醒、飞花令、热梗弹幕。附仓库地址、npm 包名与安装命令。 |
| 137 | [zzy6-a/dsh-upgrade-guard](https://github.com/zzy6-a/dsh-upgrade-guard) | 0 | 2026-09-10 | 2026-09-10 | DSH 升级安全网：宿主升级后自动巡检插件兼容性，支持修复/禁用；宿主启动失败时由宿主外 supervisor 自动救援或回滚到上一个宿主版本。 |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- ABccgh/dsh-desktop-dev
- balcoz/dsh-ocr-local
- benz-ai-x/dsh-session-graph
- cczzyy-cn/dsh-ui-screenshot
- Cyning12/dsh-coding-kit
- Dee3526/dsh-plugin-trtc-conai
- jedzqer/dsh-retry-plugin
- jianxx/dsh-cc-backup
- KarlOfLaw/dsh-goal-mode-enhance
- KarlOfLaw/dsh-side-chat
- pn1024/dsh-skill-hub
- PRTS168/dsh-chatnode-wechat
- songoao25/dsh-auto-compact
- songoao25/dsh-contract-drafting-agent
- songoao25/dsh-plugin-guardian
- songoao25/dsh-virtual-product-team
- Triple3h/dsh-image-read
- Triple3h/dsh-input-enhancement
- Triple3h/dsh-rxresume
- Triple3h/dsh-session-enhance
- Triple3h/dsh-stats-expand
- Triple3h/dsh-usage-stats
- uigdwunm/dsh-conversation-nav
- Wechsels/dsh-zotero-wiki
- xiongyishun666-alt/dsh-archived-sessions
- Yinxe/dsh-token-stats
