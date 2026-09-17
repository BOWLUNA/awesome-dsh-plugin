# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-17**
- 快照日期 / Snapshot date: **2026-09-17 (UTC)**
- 待审核 / Pending: **146**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **12**
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

对比上一份快照 **2026-09-16** / vs previous snapshot **2026-09-16**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **1**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill) | 已核准 / approved | 3991 | +1189 | 282 | 86d | 日增百星 | 日增 +1189★；已不进榜单 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [Noob-stupid/dsh-plugin-gating-hub](https://github.com/Noob-stupid/dsh-plugin-gating-hub) | 85 | 2026-08-14 | 2026-09-17 | DeepSeek Harness (DSH) 插件管理面板：一键启用/停用插件 + GitHub dsh-plugin 插件市场+自定义插件索引/市场，带插件详情与一键安装，一键框架升级自动回滚,插件升级门控 \| Plugin manager & marketplace for DeepSeek Harness |
| 2 | [morlay/dsh-plugin](https://github.com/morlay/dsh-plugin) | 10 | 2026-08-17 | 2026-09-17 | dsh plugins |
| 3 | [mozi-desk/mozi-forge](https://github.com/mozi-desk/mozi-forge) | 5 | 2026-09-15 | 2026-09-17 | A foundation for self-evolving AI agents, built on DeepSeek Harness. |
| 4 | [appthin/dsh-mcp-manager-plus](https://github.com/appthin/dsh-mcp-manager-plus) | 2 | 2026-09-17 | 2026-09-17 | MCP 服务器管理插件：在 DeepSeek Harness 设置界面的左侧边栏新增「MCP 管理」页面。MCP Server Management Plugin: A new "MCP Management" page has been added to the left sidebar of the DeepSeek Harness settings interface, allowing you to directly view, enable/disable, edit, restart, delete, and add MCP servers. |
| 5 | [dengpeihua/dsh-browser-use](https://github.com/dengpeihua/dsh-browser-use) | 2 | 2026-09-01 | 2026-09-17 | Native DeepSeek Harness browser-agent plugin with session-isolated Chromium, CDP, and DOM tools |
| 6 | [Jovan1666/dsh-commandcode-quota](https://github.com/Jovan1666/dsh-commandcode-quota) | 2 | 2026-09-17 | 2026-09-17 | Command Code plan quota in your DeepSeek Harness (dsh) sidebar: 5-hour, weekly and monthly credit windows with reset countdowns. Works with Go, GOAT, Pro, Max and Provider plans. |
| 7 | [Yu1Ko/dsh-reasoning-support](https://github.com/Yu1Ko/dsh-reasoning-support) | 2 | 2026-09-14 | 2026-09-17 | DSV4.1 reasoning support for DeepSeek Harness: lean analysis, images and attachments, and bounded acceptance/repair loops that aim to retain minimal-mode reasoning in a full agent. |
| 8 | [AIcivilization/dsh-vps-manager](https://github.com/AIcivilization/dsh-vps-manager) | 1 | 2026-09-16 | 2026-09-17 | Use your VPS inside DeepSeek Harness as seamlessly as over SSH: zero-token commands plus AI that operates the server with risk-tiered confirmation. 在 DSH 中和 SSH 一样无感地使用 VPS。 |
| 9 | [datuloar/dsh-computer-use-win](https://github.com/datuloar/dsh-computer-use-win) | 1 | 2026-09-17 | 2026-09-17 | Windows computer use for DeepSeek Harness agents  screenshot, click, type, scroll, with an on-screen indicator the human can see |
| 10 | [flg1217/dsh-continue](https://github.com/flg1217/dsh-continue) | 1 | 2026-09-17 | 2026-09-17 | dsh 输入栏一键「继续」「讲人话」快捷按钮插件 —— 代替程序员重复的体力活 |
| 11 | [gosomea/dsh-bigfish](https://github.com/gosomea/dsh-bigfish) | 1 | 2026-09-17 | 2026-09-17 | 🐋 DeepSeek Harness Web 宠物插件：动画陪伴、自适应输出节奏、可替换角色包与角色制作 Skill。 |
| 12 | [guhanfei-ai/dsh-fingerprint-signature](https://github.com/guhanfei-ai/dsh-fingerprint-signature) | 1 | 2026-09-14 | 2026-09-17 | Lightweight human-presence confirmation for DeepSeek Harness — a one-shot verification gate for protected AI tools. |
| 13 | [Huo-yang/dsh-session-trash](https://github.com/Huo-yang/dsh-session-trash) | 1 | 2026-09-15 | 2026-09-17 | 为 DSH Web GUI 添加会话删除、回收站、恢复与自动清理功能 |
| 14 | [iasmndjxjz/dsh-paper-reader](https://github.com/iasmndjxjz/dsh-paper-reader) | 1 | 2026-09-17 | 2026-09-17 | DSHA 论文阅读器插件：三栏阅读（左目录/中黑底论文/右实时 Agent 对话）+ 右栏停靠模式 + pdf.js 渲染与文字抽取 |
| 15 | [jayantTang/DSH_Mobile](https://github.com/jayantTang/DSH_Mobile) | 1 | 2026-09-17 | 2026-09-17 | 在 iPhone 上远程使用电脑的 DeepSeek Harness：WSS 经公网中转，4G/5G 可用，电脑不需要公网 IP。Native iOS client for remote DSH sessions. |
| 16 | [Jaylor-Wang/dsh-tool-lsp](https://github.com/Jaylor-Wang/dsh-tool-lsp) | 1 | 2026-09-16 | 2026-09-17 | LSP action surface for DeepSeek Harness: diagnostics, formatting, rename, code actions and symbols over real language servers |
| 17 | [liceses/dsh-memes-reply](https://github.com/liceses/dsh-memes-reply) | 1 | 2026-09-16 | 2026-09-17 | DSH 插件：蓝色大肥鱼表情包回复 —— 模型按语境在回复里贴一张会动的大肥鱼，支持设置页预览墙与下一轮指定 |
| 18 | [LLLike27/One-Time-Link](https://github.com/LLLike27/One-Time-Link) | 1 | 2025-12-27 | 2026-09-17 | agent |
| 19 | [NBagent-dev/metaflywheel](https://github.com/NBagent-dev/metaflywheel) | 1 | 2026-08-30 | 2026-09-17 | Meta-Problem Modeling (MPM) cognitive flywheel as a resident engine for LLM agent runtimes. 六阶段问题生命周期 · ε-δ 双判据收敛 · 代谢账本 · 导师规则层 |
| 20 | [NOOB-P/dsh-chat-git](https://github.com/NOOB-P/dsh-chat-git) | 1 | 2026-09-12 | 2026-09-17 | deepseek harness仓库增强插件，主要用于管理对话，每轮对话的代码 |
| 21 | [orangeofcarl0-sys/dsh-computer-use](https://github.com/orangeofcarl0-sys/dsh-computer-use) | 1 | 2026-09-05 | 2026-09-17 | 个人 DeepSeek Harness 桌面操作插件：零审批自动提权，后台优先三级投递链，Windows 深度实测 |
| 22 | [QuantumKuba/dsh-simple-codegraph](https://github.com/QuantumKuba/dsh-simple-codegraph) | 1 | 2026-09-17 | 2026-09-17 | Per-agent CodeGraph code intelligence integration for DeepSeek Harness. |
| 23 | [SAXEM1997/specpowers](https://github.com/SAXEM1997/specpowers) | 1 | 2026-09-17 | 2026-09-17 | SpecPowers — SDD+TDD engineering methodology as a DeepSeek Harness (DSH) plugin and Claude Code skill group: 6 skills fusing OpenSpec spec-driven development with Superpowers TDD discipline into one Phase 0→4 workflow. |
| 24 | [Smallballoons01/dsh-water-reminder](https://github.com/Smallballoons01/dsh-water-reminder) | 1 | 2026-09-17 | 2026-09-17 | Hydration reminder plugin for DeepSeek Harness — a randomized 40-60 minute nudge delivered as a native OS notification, an in-conversation agent nudge, and a sidebar countdown panel. Zero runtime dependencies. |
| 25 | [snail30xx/dsh-graph-runtime](https://github.com/snail30xx/dsh-graph-runtime) | 1 | 2026-09-17 | 2026-09-17 | Graph runtime capabilities for the DeepSeek Harness: register LangGraph compiled graphs as DSH tools, plus a graph-driven routing agent. |
| 26 | [sudoun/memo_harness](https://github.com/sudoun/memo_harness) | 1 | 2026-09-16 | 2026-09-17 | Agent memory with error bars: full local posteriors reconciled under finite relation laws. Dedupes source lineage, corrects without rewriting history. One CLI + SQLite. |
| 27 | [tkhs101/DSH-DesktopX](https://github.com/tkhs101/DSH-DesktopX) | 1 | 2026-09-16 | 2026-09-17 | 基于官方WebUI套壳,对插件最为友好,给你一个干净、快速、不打扰的独立桌面窗口。 |
| 28 | [wertyq111/dsh-paste-preview](https://github.com/wertyq111/dsh-paste-preview) | 1 | 2026-09-17 | 2026-09-17 | DeepSeek Harness (dsh) web plugin: paste images with thumbnail previews, reroute them as file attachments for text-only models, zoomable thumbnails in sent messages |
| 29 | [xiaobbl/dsh-opencode-go-model-list](https://github.com/xiaobbl/dsh-opencode-go-model-list) | 1 | 2026-09-17 | 2026-09-17 | 修复dsh上opencode go模型列表问题 |
| 30 | [yunfeizhu/dsh-pptx-editor](https://github.com/yunfeizhu/dsh-pptx-editor) | 1 | 2026-09-17 | 2026-09-17 | PPTX editor integration for DeepSeek Harness |
| 31 | [zhaolianghz/dsh-turnscope](https://github.com/zhaolianghz/dsh-turnscope) | 1 | 2026-08-28 | 2026-09-17 | Per-turn file diffs, deterministic safety warnings, and preview-first safe rewind for DeepSeek Harness coding sessions. |
| 32 | [0rangeSoda1506/dsh-fx-marquee](https://github.com/0rangeSoda1506/dsh-fx-marquee) | 0 | 2026-09-16 | 2026-09-17 | DeepSeek Harness（dsh）Web 插件。输入框上方常驻一条汇率/行情跑马灯，可混排货币对、A股指数与加密货币；点开任一标的看走势图，并按市场自身时区标注交易时段。另有汇率计算器（24 个货币对）、一键开关、信源可选（新浪 / ECB / ER-API）、刷新间隔可调。数据全部免密钥。由 DeepSeek-V41-Flash 编写。 A dsh plugin: a live FX ticker strip above the composer, with trend charts and a currency calculator. Written by DeepSeek-V41-Flash. |
| 33 | [1499501762/dsh-web-fetch-proxy](https://github.com/1499501762/dsh-web-fetch-proxy) | 0 | 2026-09-17 | 2026-09-17 | DSH plugin: route the built-in web_fetch through a local proxy so TUN fake-ip addresses stop tripping the SSRF guard. |
| 34 | [1624318455/dsh-plugin-adapter](https://github.com/1624318455/dsh-plugin-adapter) | 0 | 2026-09-17 | 2026-09-17 | DSH adapter for OpenCode Zen free models (maintained fork with gateway-compat fixes) |
| 35 | [1624318455/dsh-plugin-proxy](https://github.com/1624318455/dsh-plugin-proxy) | 0 | 2026-09-17 | 2026-09-17 | Runtime-switchable outbound proxy for DSH, with web settings card (maintained fork) |
| 36 | [2002XiaoYu/dsh-session-diff](https://github.com/2002XiaoYu/dsh-session-diff) | 0 | 2026-09-16 | 2026-09-17 | Session-scoped git-style diff decoration for the DeepSeek Harness web right sidebar. |
| 37 | [2025Bigeye/dsh-nanobot-subagent-link](https://github.com/2025Bigeye/dsh-nanobot-subagent-link) | 0 | 2026-08-18 | 2026-09-17 | Connect Nanobot instances to DeepSeek Harness,enabling DSH to operate NanoBot as a Sub-Agent |
| 38 | [822384810/dsh-plugin](https://github.com/822384810/dsh-plugin) | 0 | 2026-09-17 | 2026-09-17 | dsh plugins |
| 39 | [adithyanraj03/dsh-graft-plugin](https://github.com/adithyanraj03/dsh-graft-plugin) | 0 | 2026-09-17 | 2026-09-17 | A DeepSeek Harness plugin that puts graft — a prebuilt graph of every symbol, its file:line span, and who calls what — in front of both you and the model. |
| 40 | [aklnaaw/dsh-claude-theme](https://github.com/aklnaaw/dsh-claude-theme) | 0 | 2026-09-17 | 2026-09-17 | Claude-style theme for the DeepSeek Harness Web GUI: warm cream canvas, serif reading text, coral accent — plus a clickable pixel Clawd crab. |
| 41 | [akvi0921/dsh-build-progress](https://github.com/akvi0921/dsh-build-progress) | 0 | 2026-09-17 | 2026-09-17 | DSH 构建进度条推送插件:构建 APK 时在会话流折叠工具条标题处原地刷新显示 Gradle 进度条 |
| 42 | [akvi0921/dsh-console-tap](https://github.com/akvi0921/dsh-console-tap) | 0 | 2026-09-17 | 2026-09-17 | 【已停止维护/归档】旧版控制台显形插件 → 新插件见 akvi0921/dsh-build-progress |
| 43 | [albertgranados/dsh-run](https://github.com/albertgranados/dsh-run) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness web plugin: a Session-header split button that runs npm scripts from the workspace's package.json (default: dev, else start, else the first declared). |
| 44 | [albertgranados/dsh-run-environment](https://github.com/albertgranados/dsh-run-environment) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness plugin: run the project you have open, from the harness you are already in. Detects how a workspace is meant to be run (Node.js today, adapters for more) and runs it from the Session header. |
| 45 | [aLIZELI/belief-merge](https://github.com/aLIZELI/belief-merge) | 0 | 2026-09-17 | 2026-09-17 | Provenance-retaining cross-session context merge for DeepSeek Harness — a confluence theorem with a counterexample, and a benchmark for it. |
| 46 | [BakaCirno233/dsh-font-settings](https://github.com/BakaCirno233/dsh-font-settings) | 0 | 2026-09-01 | 2026-09-17 | DSH font settings plugin for DeepSeek Harness Desktop |
| 47 | [BioAIEvolu/aios-plugin-forma](https://github.com/BioAIEvolu/aios-plugin-forma) | 0 | 2026-09-15 | 2026-09-17 | Self-contained Forma AI plugin for Deepseek harness: bring candidate Python/JS/Go tools from local repos into your AIOS session with auto validation, license review, and tamper protection. DSH 0.1.3+ compatible. |
| 48 | [BOWLUNA/dsh-agent-group](https://github.com/BOWLUNA/dsh-agent-group) | 0 | 2026-09-17 | 2026-09-17 | DSH 多智能体群聊插件：多个角色在同一会话里各自独立人设地对话｜Multi-agent group chat plugin for DeepSeek Harness |
| 49 | [BOWLUNA/dsh-comfyui-panel](https://github.com/BOWLUNA/dsh-comfyui-panel) | 0 | 2026-09-17 | 2026-09-17 | DSH 的 ComfyUI 面板：在会话里驱动工作流、浏览与迭代生成结果｜ComfyUI panel for DeepSeek Harness |
| 50 | [BOWLUNA/dsh-custom-mode](https://github.com/BOWLUNA/dsh-custom-mode) | 0 | 2026-09-17 | 2026-09-17 | A custom mode for DeepSeek Harness (dsh): an editable system prompt that takes effect on the next step, per-row plugin switches, and a settings page. |
| 51 | [BOWLUNA/dsh-dreamina](https://github.com/BOWLUNA/dsh-dreamina) | 0 | 2026-09-17 | 2026-09-17 | DSH 即梦插件：通过即梦 CLI 批量生成 AI 图片与视频，并在画布里对比、挑选、迭代｜Dreamina (即梦) plugin for DeepSeek Harness |
| 52 | [BOWLUNA/dsh-mobile-first](https://github.com/BOWLUNA/dsh-mobile-first) | 0 | 2026-09-17 | 2026-09-17 | DSH 移动端 UI 适配：手机、平板、窄窗口下让 Web 界面真正可用（仅用声明式插槽，抗版本更新）｜Mobile-first UI adaptation for the DeepSeek Harness web client |
| 53 | [BOWLUNA/dsh-novel](https://github.com/BOWLUNA/dsh-novel) | 0 | 2026-09-17 | 2026-09-17 | DSH 长篇小说创作插件：分卷/伏笔/人物设定管理与连载一致性｜Long-form novel writing plugin for DeepSeek Harness |
| 54 | [BOWLUNA/dsh-prompt-hub](https://github.com/BOWLUNA/dsh-prompt-hub) | 0 | 2026-09-17 | 2026-09-17 | DSH 提示词与人格库：多套系统提示词的保存、一键切换、导入导出与分享｜Prompt and persona hub for DeepSeek Harness: save, switch, import and export multiple system prompts |
| 55 | [BOWLUNA/dsh-rp](https://github.com/BOWLUNA/dsh-rp) | 0 | 2026-09-17 | 2026-09-17 | DSH 角色扮演模式：沉浸式对话、场景与状态跟踪；角色卡导入交给 dsh-sillytavern｜Roleplay mode for DeepSeek Harness: immersive in-character conversation with scene and state tracking |
| 56 | [BOWLUNA/dsh-sillytavern](https://github.com/BOWLUNA/dsh-sillytavern) | 0 | 2026-09-17 | 2026-09-17 | DSH 的 SillyTavern 角色卡集成（非官方）：导入角色卡与世界书｜Unofficial SillyTavern character-card integration for DeepSeek Harness |
| 57 | [BrackRat/dsh-opencode-session](https://github.com/BrackRat/dsh-opencode-session) | 0 | 2026-09-17 | 2026-09-17 | dsh plugin that fixes opencode.ai 400 MissingSessionID: sends the x-opencode-session header on opencode / opencode-go routes in DeepSeek Harness. One-command install, in-memory, upgrade-safe. |
| 58 | [chiphoton/DeepSeek-Harness-Video-Director](https://github.com/chiphoton/DeepSeek-Harness-Video-Director) | 0 | 2026-08-13 | 2026-09-17 | 🎬AI-Powered Director: MiniMax-H3 Video Generation Plugin Directed by DeepSeek-Harness. 🤖More than Prompting. 🪄Canvas UI. |
| 59 | [ciceroyang/dsh-followup-actions](https://github.com/ciceroyang/dsh-followup-actions) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness 追问快捷键：回答下面多一排按钮（翻译、说人话、缩成三句、找漏洞…），点一下就填好追问，给不知道怎么接着问的人用。 |
| 60 | [ciceroyang/dsh-privacy-guard](https://github.com/ciceroyang/dsh-privacy-guard) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness 发送前隐私检查：在你把手机号、身份证号、银行卡号或 API 密钥发给模型之前提醒你，并支持一键打码。 |
| 61 | [ciceroyang/dsh-prompt-library](https://github.com/ciceroyang/dsh-prompt-library) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness 常用指令库：一份写好中文提示词的清单，搜一下、点一下就能填进输入框，给不熟悉怎么写提示词的人用。 |
| 62 | [ciskonc/dsh-context-imports](https://github.com/ciskonc/dsh-context-imports) | 0 | 2026-09-17 | 2026-09-17 | Claude Code-style @path imports for DeepSeek Harness: expands @imports in AGENTS.md/CLAUDE.md and injects referenced files into context at session start |
| 63 | [cloudbywu/dshchem](https://github.com/cloudbywu/dshchem) | 0 | 2026-09-17 | 2026-09-17 | DSH (DeepSeek Harness) 化学科研 Agent 预设与插件：24 个 chem_* 工具，RDKit / ASE / xtb / AutoDock Vina / admet_ai 后端 |
| 64 | [cningan/dsh-startup-check](https://github.com/cningan/dsh-startup-check) | 0 | 2026-09-17 | 2026-09-17 | Pre-flight check for a DeepSeek Harness profile's plugin tree: static checks + optional isolated real-boot and headless-browser smoke, with instance-shutdown confirmation and stray-instance audit. Provides the plugin_check tool and the bundled plugin-fault-diagnosis skill. |
| 65 | [czhzz/dsh-net-access](https://github.com/czhzz/dsh-net-access) | 0 | 2026-09-17 | 2026-09-17 | Control how the DeepSeek Harness Web GUI is reachable: local only, Tailscale, all local networks, or off. |
| 66 | [darrien1998/dsh-ditto](https://github.com/darrien1998/dsh-ditto) | 0 | 2026-09-16 | 2026-09-17 | AI is great at doing one file. Ditto is for doing the same thing to 30 files without babysitting all 30. Review-first batch automation plugin for DeepSeek Harness: 3 reviewed samples → full preview → approve → safe apply. |
| 67 | [Dayi-Z/dsh-git-manager](https://github.com/Dayi-Z/dsh-git-manager) | 0 | 2026-08-28 | 2026-09-17 | GitHub-connected visual git panel for DeepSeek Harness - branch switcher, file-level approval cards, PR/issue workspace |
| 68 | [dooooling/dsh-opencode-compat](https://github.com/dooooling/dsh-opencode-compat) | 0 | 2026-09-17 | 2026-09-17 | Standalone OpenCode Zen compatibility bundle for DeepSeek Harness: session headers and Muse reasoning replay |
| 69 | [EmotionG/dsh-prompt-optimizer](https://github.com/EmotionG/dsh-prompt-optimizer) | 0 | 2026-09-17 | 2026-09-17 | 优化提示词 |
| 70 | [Enchanted0911/dsh-fal-imagegen](https://github.com/Enchanted0911/dsh-fal-imagegen) | 0 | 2026-09-17 | 2026-09-17 | fal.ai native image generation for DSH: a FAL_KEY settings card plus Agent tools (fal_generate_image / fal_edit_image) that call queue.fal.run directly. |
| 71 | [ethanrise/dsh-nx](https://github.com/ethanrise/dsh-nx) | 0 | 2026-09-17 | 2026-09-17 | Experimental DeepSeek Harness plugin for safe, local Siemens NX automation through MCP. |
| 72 | [ganningniang/dsh-offpeak-job](https://github.com/ganningniang/dsh-offpeak-job) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness 的谷时调度插件——把任务留到谷时再运行。 |
| 73 | [Gishi1/calaloud](https://github.com/Gishi1/calaloud) | 0 | 2026-08-04 | 2026-09-17 | Thin-client Android reader for Calibre + FanFicFare + Kokoro TTS (Tauri v2 + Svelte 5) |
| 74 | [Gishi1/fanficfare-service](https://github.com/Gishi1/fanficfare-service) | 0 | 2026-08-04 | 2026-09-17 | HTTP API wrapping FanFicFare: story URL -> EPUB / WorkBundle JSON. Used by Calaloud. |
| 75 | [Gishi1/katacoda-scenarios](https://github.com/Gishi1/katacoda-scenarios) | 0 | 2018-08-26 | 2026-09-17 | Katacoda Scenarios |
| 76 | [GooDAnDReaDY/dsh-approval-gate](https://github.com/GooDAnDReaDY/dsh-approval-gate) | 0 | 2026-09-17 | 2026-09-17 | Native command approval gate for DeepSeek Harness. |
| 77 | [GooDAnDReaDY/dsh-server-monitor](https://github.com/GooDAnDReaDY/dsh-server-monitor) | 0 | 2026-09-17 | 2026-09-17 | Read-only Linux server monitoring in the DeepSeek Harness sidebar. |
| 78 | [guhanfei-ai/dsh-human-intent](https://github.com/guhanfei-ai/dsh-human-intent) | 0 | 2026-09-16 | 2026-09-17 | Cryptographically bind human authorization to the exact action an AI agent is about to execute. |
| 79 | [guhanfei-ai/dsh-introspect](https://github.com/guhanfei-ai/dsh-introspect) | 0 | 2026-09-16 | 2026-09-17 | Local-first self-observability for DeepSeek Harness — events, personal metrics and reality feedback. |
| 80 | [guhanfei-ai/dsh-searchops](https://github.com/guhanfei-ai/dsh-searchops) | 0 | 2026-09-16 | 2026-09-17 | Deterministic search, log and evidence acquisition for AI agents. OpenSearch-first, provider-neutral, strictly read-only. |
| 81 | [guhanfei-ai/dsh-worldsense](https://github.com/guhanfei-ai/dsh-worldsense) | 0 | 2026-09-16 | 2026-09-17 | A safe, bounded, read-only perception layer for AI agents to observe administrator-defined JSON APIs. |
| 82 | [haotian-lu-prog/dsh-update-plugin](https://github.com/haotian-lu-prog/dsh-update-plugin) | 0 | 2026-09-11 | 2026-09-17 | One-command DSH updater: CLI, bundles and all profile plugins — plus a dsh-plugin for Settings → General, with backups and rollback. |
| 83 | [Helly0000/dsh-life-game](https://github.com/Helly0000/dsh-life-game) | 0 | 2026-09-17 | 2026-09-17 | Conway's Game of Life for DeepSeek Harness: a sidebar panel row opens a drawable centre-column board with four rules and seven stampable patterns. |
| 84 | [hj01857655/dsh-verdict](https://github.com/hj01857655/dsh-verdict) | 0 | 2026-09-17 | 2026-09-17 | Measure whether a change to your dsh setup actually helped: register repeatable cases, run them, diff before/after. DeepSeek Harness plugin. |
| 85 | [hoyyang/dsh-code-graph](https://github.com/hoyyang/dsh-code-graph) | 0 | 2026-09-17 | 2026-09-17 | Branch-aware code knowledge graph plugin for DSH — callers/impact/trace over 158+ languages, freshness-gated, zero MCP sessions |
| 86 | [huuthuan-nguyen/dsh-knowcode](https://github.com/huuthuan-nguyen/dsh-knowcode) | 0 | 2026-09-16 | 2026-09-17 | ⚡ Unified code graph & knowledge base for DeepSeek Harness — AST symbols, refactor blast radius, clone detection and spec-to-code traceability on embedded FalkorDB. |
| 87 | [IQzhan/deepseek-harness-model-router](https://github.com/IQzhan/deepseek-harness-model-router) | 0 | 2026-09-16 | 2026-09-17 | A routing plugin for DeepSeek Harness that assigns models by task: a delegated subagent runs on the model that fits its job, while the session you are talking to always keeps the model you picked. \| 为 DeepSeek Harness 提供按任务分配模型的路由插件： 被委派出去的子智能体跑在适合它那件事的模型上，而你正在对话的这个会话，用的始终是你选的那个模型。 |
| 88 | [Iwwww/dsh-reasoning-fold](https://github.com/Iwwww/dsh-reasoning-fold) | 0 | 2026-09-17 | 2026-09-17 | Codex-style folding for the DeepSeek Harness web transcript: a running turn keeps only its last few actions visible, folded behind one row that opens the whole turn. |
| 89 | [jaikensai888/dsh-drawio](https://github.com/jaikensai888/dsh-drawio) | 0 | 2026-09-17 | 2026-09-17 | 在 DSH Web GUI 侧边栏里直接画 draw.io 图：图纸即工作区里的 .drawio 文件，编辑器自托管、完全离线 · A self-hosted draw.io editor for the DSH sidebar |
| 90 | [JeremyWangCY/win-pilot](https://github.com/JeremyWangCY/win-pilot) | 0 | 2026-09-16 | 2026-09-17 | Agent-neutral Windows Computer Use plugin with MCP, CLI, skills, and native host adapters |
| 91 | [john-walks-slow/dsh-clear-mind](https://github.com/john-walks-slow/dsh-clear-mind) | 0 | 2026-09-17 | 2026-09-17 | Context compaction for DeepSeek Harness: mind_map and clear_mind agent tools turn selected history into self-written checkpoints, with auditable GUI tombstones and proactive threshold reminders. |
| 92 | [john-walks-slow/dsh-message-datetime](https://github.com/john-walks-slow/dsh-message-datetime) | 0 | 2026-09-17 | 2026-09-17 | Per-turn clock context for DeepSeek Harness: one-line current-time reading at every turn start and a Turn ended reading at close, so the model always knows what time it is. |
| 93 | [john-walks-slow/dsh-proactive](https://github.com/john-walks-slow/dsh-proactive) | 0 | 2026-09-06 | 2026-09-17 | Proactive follow-ups for DeepSeek Harness: the model schedules host-level alarms (once/every/cron with jitter, quiet hours, daily budget) that resume cold sessions, with tombstone compaction and a live web panel. |
| 94 | [john-walks-slow/dsh-qol](https://github.com/john-walks-slow/dsh-qol) | 0 | 2026-09-17 | 2026-09-17 | Mobile-first QoL for the DeepSeek Harness web GUI: Chrome-style session tab bar, swipeable fullscreen sidebar, keyboard/IME/touch adaptations and a rewritten settings page — 13 toggles under Settings → QoL. |
| 95 | [john-walks-slow/dsh-set-model](https://github.com/john-walks-slow/dsh-set-model) | 0 | 2026-09-17 | 2026-09-17 | Per-agent model switching for DeepSeek Harness: set_model / list_models agent tools with provider whitelist and token-budget guardrails, plus plan-mode model staging and cache-safe active-model context. |
| 96 | [john-walks-slow/dsh-simulated-life](https://github.com/john-walks-slow/dsh-simulated-life) | 0 | 2026-09-17 | 2026-09-17 | Simulated life context for DeepSeek Harness: reads .life/<date> events into agent context with dedup, and a life_react tool to write feelings, thoughts and actions back for world-evolution workflows. |
| 97 | [jonah791/dsh-passbook](https://github.com/jonah791/dsh-passbook) | 0 | 2026-09-17 | 2026-09-17 | 隐私密码本（Privacy Passbook）：我自己的私密凭据工具面——生成强密码、按字段写入、按需取用、不泄漏地使用（env 注入）、体检与轮换；存储复用 DPAPI vault，秘密走 stdin/env、不回显，审计只记「谁何时取了哪一条」。 |
| 98 | [kkgace/dsh-web-searxng-search](https://github.com/kkgace/dsh-web-searxng-search) | 0 | 2026-09-17 | 2026-09-17 | Self-hosted SearXNG web search provider for DeepSeek Harness (dsh). No API key or vendor account. |
| 99 | [kovey/dsh-project](https://github.com/kovey/dsh-project) | 0 | 2026-09-17 | 2026-09-17 | Engineering suite for DeepSeek Harness: seven plugins covering roles, specifications, test design, quality gates, evidence, audit trail and pipeline orchestration |
| 100 | [kuyueliuhun-ctrl/dsh-command-queue](https://github.com/kuyueliuhun-ctrl/dsh-command-queue) | 0 | 2026-09-17 | 2026-09-17 | DSH 插件：让 /compact 等斜杠命令在 agent 忙碌时进入命令队列，空闲后自动执行 \| Queue slash commands until the agent is idle |
| 101 | [liaoyuqing/dsh_workspace_switch](https://github.com/liaoyuqing/dsh_workspace_switch) | 0 | 2026-09-17 | 2026-09-17 | deepseek-harness多工作区隔离管理，统一管控 Skill / MCP / 插件启停，全局配置兜底，工作区可单独开关 |
| 102 | [liiydong/dsh-workbench](https://github.com/liiydong/dsh-workbench) | 0 | 2026-09-17 | 2026-09-17 | DSH Web 插件：把「AI 改 md → 生成 Word/PDF/Excel → 你审这一版」变成一条看得见的时间轴（含技能库与文档配对）。自带演示数据、零依赖、只读为主。 |
| 103 | [Liu-fu-gui/dsh-desktop-upgrade](https://github.com/Liu-fu-gui/dsh-desktop-upgrade) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness (DSH) Desktop plugin: adds the missing 「升级 DSH」 entry — tray command + dsh_upgrade model tool, driving the official version service and installer channel via desktopRuntime.updates. 不改内核文件。 |
| 104 | [loyalchiiina/dsh-archive-manager-favorites-patch](https://github.com/loyalchiiina/dsh-archive-manager-favorites-patch) | 0 | 2026-09-17 | 2026-09-17 | Archived-sessions plugin for DSH — enhanced build by loyalchiiina: favorites, pinning, turns sort, idle auto-archive, bulk delete. Installable package (lib/ + README + NOTICE); based on MichengAI's upstream dsh-archive-manager v0.1.40 (Apache-2.0). |
| 105 | [lpf20200901/dsh-memory-delta](https://github.com/lpf20200901/dsh-memory-delta) | 0 | 2026-09-17 | 2026-09-17 | 给 AI 编码助手的跨会话长期记忆：自动注入、只推变化。DSH 插件 + 零依赖 CLI。 |
| 106 | [lubanqihao9875/dsh-figma-mcp](https://github.com/lubanqihao9875/dsh-figma-mcp) | 0 | 2026-09-17 | 2026-09-17 | DSH 的 Figma MCP 一键连接插件 |
| 107 | [luigiinred/dsh-git-status-pill](https://github.com/luigiinred/dsh-git-status-pill) | 0 | 2026-09-16 | 2026-09-17 | Floating git status pill for DeepSeek Harness: live branch, +/- line changes and a Create PR prompt. |
| 108 | [MAOLEIJIN/dsh-mattpocock-skills](https://github.com/MAOLEIJIN/dsh-mattpocock-skills) | 0 | 2026-09-15 | 2026-09-17 | Matt Pocock skills for DeepSeek Harness: upstream sync plus verified DSH adaptation overlay |
| 109 | [MiHjy12138/dsh-memory-lite](https://github.com/MiHjy12138/dsh-memory-lite) | 0 | 2026-09-17 | 2026-09-17 | 给 agent 的按需记忆库：会话日志提炼成分层 markdown 记忆，mem_query 只回命中片段（约 700 字符，而不是上万字符）。零依赖、不每轮注入、条条可溯源。既是 DSH 插件，也是独立 CLI。 |
| 110 | [misswell/dsh-advanced-provider-settings](https://github.com/misswell/dsh-advanced-provider-settings) | 0 | 2026-09-17 | 2026-09-17 | Advanced provider configuration UI for DeepSeek Harness (DSH): headers, User-Agent, retry policy, timeouts, vision, reasoning and compatibility — without editing settings.yaml by hand. |
| 111 | [Mlte0907/dsh-brake](https://github.com/Mlte0907/dsh-brake) | 0 | 2026-09-17 | 2026-09-17 | DSH 死循环刹车器：检测 agent 会话中的方法循环（同类工具高频调用），注入警告或拒绝执行 |
| 112 | [Muggle8888/dsh-plugin-update-audit](https://github.com/Muggle8888/dsh-plugin-update-audit) | 0 | 2026-09-10 | 2026-09-17 | Read-only update auditing for DeepSeek Harness profile plugins |
| 113 | [mugnimaestra/dsh-browser-use](https://github.com/mugnimaestra/dsh-browser-use) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness Agent Preset bridge for Open Browser Use WebMCP |
| 114 | [neltharion11/dsh-luxar-embedded](https://github.com/neltharion11/dsh-luxar-embedded) | 0 | 2026-09-16 | 2026-09-17 | DeepSeek Harness plugin for ESP-IDF and STM32CubeMX embedded development |
| 115 | [Nexus-Aethra/Nexus-Terminal](https://github.com/Nexus-Aethra/Nexus-Terminal) | 0 | 2026-09-09 | 2026-09-17 | dshell — a terminal-first AI workbench built as dsh plugins: one terminal timeline per session, cross-session pipes with a named buffer, SSH device sessions. \| 终端优先的 AI 工作台（dsh 插件集）：一个会话一条终端时间线，跨会话管道委派与缓冲区文件共享，可把会话直接开到 SSH 设备上。 |
| 116 | [noetion/dsh-jev](https://github.com/noetion/dsh-jev) | 0 | 2026-09-17 | 2026-09-17 | DSH bundle that registers jev_ask for TypeSafe Jev noul, choice, and score answers. |
| 117 | [peng456/dsh-plugin-mesh](https://github.com/peng456/dsh-plugin-mesh) | 0 | 2026-09-17 | 2026-09-17 | DSH 局域网 Mesh 插件：自动发现同网段的其他 DSH 实例，提供对端操作页面，支持跨机双向派发任务。 |
| 118 | [picsky/dsh-pocket-console](https://github.com/picsky/dsh-pocket-console) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness (DSH) plugin: approve tool calls and answer ask_user_question prompts from your phone over Feishu, with the desktop always first in line. |
| 119 | [qiqibabyy/dsh-pet-desktop](https://github.com/qiqibabyy/dsh-pet-desktop) | 0 | 2026-09-17 | 2026-09-17 | A self-contained desktop pet plugin for DeepSeek Harness — Codex-style animated pets with affinity, activity bubbles, snap-to-edge dragging and smart click-through. No web pet required. |
| 120 | [runcat-tommy/dsh-windows-c-cleanup](https://github.com/runcat-tommy/dsh-windows-c-cleanup) | 0 | 2026-09-16 | 2026-09-17 | DSH plugin: scan, grade and clean up Windows C: drive - five-tier safety grading, staging area, UAC elevation, and migration. |
| 121 | [SkyblueeeLabs/dsh-iconic-launcher](https://github.com/SkyblueeeLabs/dsh-iconic-launcher) | 0 | 2026-09-16 | 2026-09-17 | DSH plugin — pick a preset or upload a PNG: backdrop auto-removed, packed into a multi-size ICO, written to your desktop in one click. |
| 122 | [suuuuunamei/dsh-kaze-tachinu-theme](https://github.com/suuuuunamei/dsh-kaze-tachinu-theme) | 0 | 2026-09-09 | 2026-09-17 | kaze tachinu theme for DSH Web GUI,thank you visit |
| 123 | [SUZUNAMI/dsh-workspace-hide](https://github.com/SUZUNAMI/dsh-workspace-hide) | 0 | 2026-09-16 | 2026-09-17 | Hide selected workspaces from the DSH sidebar without deleting anything: local-only, reversible, with a Settings management page. |
| 124 | [theRMM714/git-for-dsh](https://github.com/theRMM714/git-for-dsh) | 0 | 2026-09-14 | 2026-09-17 | deepseek harness的git工具 |
| 125 | [tomowang/dsh-data-agent](https://github.com/tomowang/dsh-data-agent) | 0 | 2026-09-15 | 2026-09-17 | DeepSeek Harness (dsh) plugin for managing database connections, browsing/annotating schemas, and running SQL — from chat or the Settings UI |
| 126 | [TowardsDawn/dsh-user-markdown](https://github.com/TowardsDawn/dsh-user-markdown) | 0 | 2026-09-17 | 2026-09-17 | 让用户消息也能在DSH里被markdown渲染 |
| 127 | [ubggyhjb/dsh-mathmodel-v7](https://github.com/ubggyhjb/dsh-mathmodel-v7) | 0 | 2026-09-16 | 2026-09-16 | 数学建模竞赛 Agent（DeepSeek Harness preset）v7：CUMCM 国赛专项，资产接管→Discovery+竞争搜索→方法学契约→代码图表→编辑/视觉证据链→论文→全门禁验收，含 CUMCM Typst/LaTeX 双模板与 2026 国赛规则 authority |
| 128 | [voidmind26/dsh-lsp-bridge](https://github.com/voidmind26/dsh-lsp-bridge) | 0 | 2026-09-17 | 2026-09-17 | Bridge DeepSeek Harness to language servers for read-only code intelligence, with multi-language configuration, multi-root workspace support, and session-scoped server reuse. |
| 129 | [weekitmo/oh-my-dsh-plugins](https://github.com/weekitmo/oh-my-dsh-plugins) | 0 | 2026-09-08 | 2026-09-17 | A curated collection of awesome plugins for DeepSeek Harness (DSH) — task notifications, LLM trace inspection, keybindings with a built-in terminal, and local agent delegation. |
| 130 | [wild-River2016/xiaohe-canvas-dsh](https://github.com/wild-River2016/xiaohe-canvas-dsh) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness 插件 - 小禾画布 AI 创作助手 |
| 131 | [WsTe47/mylife](https://github.com/WsTe47/mylife) | 0 | 2026-09-17 | 2026-09-17 | MyLife — 本地优先的个人状态档案与决策引擎（DeepSeek Harness 插件）。从混乱里找出你的主线，并且记得它在时间里的变化。 |
| 132 | [X-Xyy/dsh-api-balance](https://github.com/X-Xyy/dsh-api-balance) | 0 | 2026-09-17 | 2026-09-17 | Live DeepSeek API balance and per-session token usage in the conversation header. |
| 133 | [xianmua/dsh-apis-plugin](https://github.com/xianmua/dsh-apis-plugin) | 0 | 2026-09-17 | 2026-09-17 | dsh-apis-plugin |
| 134 | [Xinyuan-Gao/xy-dsh](https://github.com/Xinyuan-Gao/xy-dsh) | 0 | 2026-09-17 | 2026-09-17 | A set of DeepSeek Harness plugins: an always-on-top agent lamp board (macOS) and a session context lens. |
| 135 | [xswt442-cmd/dsh-xswt-tauriapp](https://github.com/xswt442-cmd/dsh-xswt-tauriapp) | 0 | 2026-09-15 | 2026-09-17 | 给 DeepSeek Harness 的轻量 Tauri 桌面外壳：窗口、进程、启停与复用、会话交接、菜单与托盘、快捷键、更新和故障恢复归外壳，页面内容仍归 dsh。 A lightweight Tauri desktop shell for DeepSeek Harness: windows, the dsh server process, launch and reuse, the session hand-off, menu and tray, hotkeys, updates and failure recovery are the shell's; the page stays dsh's. |
| 136 | [YeKui7/dsh-seams](https://github.com/YeKui7/dsh-seams) | 0 | 2026-09-17 | 2026-09-17 | Field notes on DeepSeek Harness (dsh) seams: extension points, a shell-only context-injection recipe, and four silent-failure traps |
| 137 | [yuanyiHY/deepseek-media-gallery](https://github.com/yuanyiHY/deepseek-media-gallery) | 0 | 2026-09-16 | 2026-09-17 | DSH (cordis) plugin: browse, preview, download and delete generated images and videos from a semi-transparent sidebar popup. |
| 138 | [zhanghao3693/dsh-dpharness](https://github.com/zhanghao3693/dsh-dpharness) | 0 | 2026-09-17 | 2026-09-17 | 在 dsh 里浏览 dpharness.com 的插件目录并一键安装 —— 严选插件（汉化优先 + 可信度筛选）。Curated dsh plugin catalog for DeepSeek Harness with one-click install. |
| 139 | [zhengjy01/dsh-wechat-clawbot](https://github.com/zhengjy01/dsh-wechat-clawbot) | 0 | 2026-09-17 | 2026-09-17 | DSH plugin: WeChat floating-ball bridge (QR login, message relay to agent) — maintained fork of lubaiUwU/DSH-WeChatClawBot with context_token + login-loop fixes |
| 140 | [zhenyong97/dsh-plugin-atlassian](https://github.com/zhenyong97/dsh-plugin-atlassian) | 0 | 2026-09-17 | 2026-09-17 | DeepSeek Harness plugin: connect Atlassian's official remote MCP server (Jira, Confluence, JSM, Bitbucket, Compass) over OAuth 2.1. |
| 141 | [zlqd123/dsh-composer-keys](https://github.com/zlqd123/dsh-composer-keys) | 0 | 2026-08-24 | 2026-09-17 | 为 DeepSeek Harness Web 聊天输入框自定义「发送」与「换行」键位：任意组合键自由分配、双预设一键切换、用户设置文档持久化、深浅色主题自适应。AI 生成的社区插件（AI-generated）。 |
| 142 | [zlZayn/dsh-ds-balance](https://github.com/zlZayn/dsh-ds-balance) | 0 | 2026-09-17 | 2026-09-17 | DSH 插件：在左侧栏底部显示 DeepSeek 账户余额（原生 UI），设置页提供连接、展示币种、预警阈值与刷新节奏的配置卡片。（原生嵌入“设置-插件-插件配置”） |
| 143 | [ZSeven-W/dsh-browser](https://github.com/ZSeven-W/dsh-browser) | 0 | 2026-08-24 | 2026-09-17 | DeepSeek Harness plugin for browser automation, headless first. Every agent gets its own throwaway Chrome/Edge/Chromium profile, short-lived semantic references instead of CSS selectors, scoped subtree observation, deterministic high-risk refusal, and bounded evidence. |
| 144 | [ZSeven-W/dsh-computer](https://github.com/ZSeven-W/dsh-computer) | 0 | 2026-08-24 | 2026-09-17 | DeepSeek Harness plugin for macOS desktop automation. Observes the accessibility tree, gates risky actions behind one-time approval, permanently refuses secure fields, and returns bounded visual evidence — through a native helper you build and grant locally. |
| 145 | [ZSeven-W/dsh-qa](https://github.com/ZSeven-W/dsh-qa) | 0 | 2026-08-31 | 2026-09-17 | DeepSeek Harness plugin that does QA: an agent explores your app like a real user and leaves evidence, then the explored path is exported as a deterministic replay scenario you run every release. Orchestrates the browser, macOS desktop, iOS and Android drivers — never a false green. |
| 146 | [zwbao/dsh-plugin-longpi](https://github.com/zwbao/dsh-plugin-longpi) | 0 | 2026-09-17 | 2026-09-17 | LongPi 1.0.0 for DeepSeek Harness: longevity concierge, personal genome, VCF ingest, multi-omics report, s2f-agent routing. |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- AtWhuhu/dsh-devin-cli
- CyraZm49/dsh-shutdown
- Dayi-Z/gitcompass
- haotian-lu-prog/dsh-update-all
- huahai0202/dsh-plugin-manager
- loyalchiiina/dsh-archive-manager-plus
- morlay/better-session
- neltharion11/dsh-luxar-embedding
- Noob-stupid/dsh-plugin-hub
- wcnm8888/dsh-plugin-update-audit
- YJLTF/dsh-thinktune
- yunfeizhu/dsh-pptx-viewer
