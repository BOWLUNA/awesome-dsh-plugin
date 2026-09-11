# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-11**
- 快照日期 / Snapshot date: **2026-09-11 (UTC)**
- 待审核 / Pending: **169**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **26**
- Star 异常增长 / Star-growth alerts: **6** — 先看下方告警节 / see the alert section first

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

对比上一份快照 **2026-09-10** / vs previous snapshot **2026-09-10**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **6**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [reactive-resume/app](https://github.com/reactive-resume/app) | 待审 / pending | 42483 | +55 | 4705 | 2360d | 待审高星 | 核准即 Top 1 |
| ⚠️ [agentic-os-org/ANOLISA](https://github.com/agentic-os-org/ANOLISA) | 待审 / pending | 604 | +1 | 104 | 164d | 待审高星 | 核准即榜 #21 |
| ⚠️ [gitroomhq/postiz-agent](https://github.com/gitroomhq/postiz-agent) | 待审 / pending | 458 | — | 90 | 208d | 待审高星 | 核准即榜 #26 |
| ⚠️ [LivXue/dsh-plugin-shop](https://github.com/LivXue/dsh-plugin-shop) | 已核准 / approved | 618 | +113 | 6 | 16d | 日增百星 | 日增 +113★；★/fork 103；已不进榜单 |
| ⚠️ [MeteorNOX/DeepSeek-Balance-Whale-Widget](https://github.com/MeteorNOX/DeepSeek-Balance-Whale-Widget) | 已核准 / approved | 2171 | +103 | 81 | 23d | 日增百星 | 日增 +103★ |
| ⚠️ [sopaco/terrain](https://github.com/sopaco/terrain) | 已核准 / approved | 108 | +54 | 10 | 88d | 榜单跃升 | 榜单 183→102 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [reactive-resume/app](https://github.com/reactive-resume/app) ⚠️ | 42483 | 2020-03-25 | 2026-09-11 | A one-of-a-kind resume builder that keeps your privacy in mind. Completely secure, customizable, portable, open-source and free forever. Try it out today! |
| 2 | [agentic-os-org/ANOLISA](https://github.com/agentic-os-org/ANOLISA) ⚠️ | 604 | 2026-03-30 | 2026-09-11 | ANOLISA (Agentic Nexus Operating Layer & Interface System Architecture) \| Agentic OS with runtime, security, observability, and Tokenless response compression for lower token usage and cost. |
| 3 | [gitroomhq/postiz-agent](https://github.com/gitroomhq/postiz-agent) ⚠️ | 458 | 2026-02-14 | 2026-09-11 | Postiz Agents CLI - connect it to Claude / OpenClaw / etc, to schedule social media posts 🤖 |
| 4 | [axelfreeman/marketing-mindset](https://github.com/axelfreeman/marketing-mindset) | 34 | 2026-09-01 | 2026-09-11 | The marketing OS for AI agents — think like a marketer first, get tactics as the output. |
| 5 | [sz1698/dsh-bg-new](https://github.com/sz1698/dsh-bg-new) | 19 | 2026-09-11 | 2026-09-11 | DSH 网页界面换背景：侧栏「壁纸」按钮弹出右侧抽屉，支持系统预设/纯色/渐变/图片/视频，滚轮+拖动小图同时管缩放与定位，毛玻璃质感，本地媒体伺服不走云端。DSH web background & wallpaper plugin with drawer UI, glassmorphism and local media serving. |
| 6 | [133563825as-ai/dsh-api-dashboard](https://github.com/133563825as-ai/dsh-api-dashboard) | 6 | 2026-08-25 | 2026-09-11 | 多平台 API 余额看板插件 for DeepSeek Harness Web GUI |
| 7 | [cofy-x/dsh-cron](https://github.com/cofy-x/dsh-cron) | 4 | 2026-08-15 | 2026-09-11 | Scheduled tasks (cron) for DeepSeek Harness: model- and human-callable scheduling that fires followup/inject into agent sessions |
| 8 | [fang2hou/dsh-locale-ja](https://github.com/fang2hou/dsh-locale-ja) | 4 | 2026-08-13 | 2026-09-11 | DeepSeek Harness の日本語化プラグイン |
| 9 | [online111111/whalechan-dsh-theme](https://github.com/online111111/whalechan-dsh-theme) | 3 | 2026-09-11 | 2026-09-11 | Unofficial Whale-chan community fan-art theme for DeepSeek Harness |
| 10 | [Yunado/dsh-qwen38-local-qol](https://github.com/Yunado/dsh-qwen38-local-qol) | 3 | 2026-09-01 | 2026-09-11 | DeepSeek Harness QoL plugin for the local Qwen3.8 line (27B/Flash-Next): per-request thinking budgets, a compaction backend that stops burning the output cap on thinking, and a settings tab. 本地 Qwen3.8 线的 DSH QoL 插件：逐请求 thinking 预算、不再把输出帽烧在 thinking 上的压缩后端、设置 tab。 |
| 11 | [zzjzzb/ai-memory](https://github.com/zzjzzb/ai-memory) | 3 | 2026-09-10 | 2026-09-11 | Personal AI memory semantic layer SDK (Rust + SQLite) — short/mid/long-term memory with hybrid recall |
| 12 | [1420079678-ctrl/agent-body](https://github.com/1420079678-ctrl/agent-body) | 2 | 2026-09-11 | 2026-09-11 | Organ-based agent plugin platform for DeepSeek Harness: 23 organs, nerve impulses, a heartbeat, reflex arcs that fire with zero model calls, sleep-time memory consolidation and closed-loop self-healing. On-demand tool schema gating cuts prompt tokens by 82%. |
| 13 | [enteguo/dsh-plugin-quick-chat](https://github.com/enteguo/dsh-plugin-quick-chat) | 2 | 2026-09-08 | 2026-09-11 | deepseek plugin：quick chat  |
| 14 | [wldxiaobai/dsh-project-mcp-manager](https://github.com/wldxiaobai/dsh-project-mcp-manager) | 2 | 2026-08-22 | 2026-09-11 | Project-level MCP manager for DSH: auto-mount MCP servers from each project's .dsh/mcp.yml, hot-reload config changes, and scope tools to the active session's project. |
| 15 | [xine2009cn/dsh-branch-inbox-guard](https://github.com/xine2009cn/dsh-branch-inbox-guard) | 2 | 2026-09-11 | 2026-09-11 | A DeepSeek Harness (DSH) plugin that removes the queued prompts a fork child inherits from its parent, so a new branch runs the prompt you type instead of the parent's next one. Host-side bundle, no core patching. |
| 16 | [xingmen-1/dsh-move-rag](https://github.com/xingmen-1/dsh-move-rag) | 2 | 2026-09-11 | 2026-09-11 | Local knowledge base for DeepSeek Harness that lives on your desktop: drag files onto an always-on-top icon to ingest them, search them in the same panel, and let the agent query them. |
| 17 | [axelfreeman/hermes-security-audit](https://github.com/axelfreeman/hermes-security-audit) | 1 | 2026-08-10 | 2026-09-11 | 🔒 12-method security audit for Hermes Agent — virus scan, rootkit detection, SSH brute force protection |
| 18 | [azazo1/dsh-fork-inbox-guard](https://github.com/azazo1/dsh-fork-inbox-guard) | 1 | 2026-09-11 | 2026-09-11 | DSH host plugin: drop the pending prompts a fork inherits, so a fork child answers the prompt you send it instead of the source session's queue. |
| 19 | [azazo1/dsh-node-accent](https://github.com/azazo1/dsh-node-accent) | 1 | 2026-09-11 | 2026-09-11 | DSH web plugin: recolor only the icon and title text of conversation rows, per tool or event category. |
| 20 | [baicaibucai1/dsh-process-control](https://github.com/baicaibucai1/dsh-process-control) | 1 | 2026-09-11 | 2026-09-11 | DeepSeek Harness web plugin: one process-control button beside the sidebar Settings row. Restart the host, reload the page, or quit the host process. |
| 21 | [bryanchen463/dsh-desktop-pet](https://github.com/bryanchen463/dsh-desktop-pet) | 1 | 2026-09-11 | 2026-09-11 | 紫色圆球桌宠：眼睛始终盯着鼠标，可拖动、点击眨眼、空闲随机动作。DSH 动态 Cordis 插件 + 无依赖网页版。 |
| 22 | [casualjim/dsh-plugins](https://github.com/casualjim/dsh-plugins) | 1 | 2026-08-23 | 2026-09-11 | A collection of plugins for deepseek harness |
| 23 | [chuling-lingling/dsh-plugin-session-delete](https://github.com/chuling-lingling/dsh-plugin-session-delete) | 1 | 2026-09-11 | 2026-09-11 | 删除dsh的会话内容 |
| 24 | [DaYanHCD/DSH-Balance-Mini](https://github.com/DaYanHCD/DSH-Balance-Mini) | 1 | 2026-09-01 | 2026-09-11 | DeepSeek Harness 的极简版余额监视器插件：常驻余额徽章、红绿灯配色、多供应商、高峰/空闲时段。 |
| 25 | [DaYanHCD/DSH-Shortcut](https://github.com/DaYanHCD/DSH-Shortcut) | 1 | 2026-09-01 | 2026-09-11 | DeepSeek Harness 的 Windows 桌面快捷方式工具：双击智能启动/唤起、浏览器打开前自动最小化、崩溃一键重装救援（不删用户数据）。圆角官方图标，纯 PowerShell 零依赖。 |
| 26 | [Dingpenghui-good/dsh-tool-agnes](https://github.com/Dingpenghui-good/dsh-tool-agnes) | 1 | 2026-08-16 | 2026-09-11 | Agnes AI media generation plugins for DeepSeek Harness |
| 27 | [duoduoqian708/dsh-voice-talk](https://github.com/duoduoqian708/dsh-voice-talk) | 1 | 2026-09-08 | 2026-09-11 | DeepSeek Harness Web 的语音对话插件：点麦克风边说边听，AI 回复边生成边播报正文，支持千问/讯飞/系统语音。 |
| 28 | [dxxCaO/dsh-self-improvement](https://github.com/dxxCaO/dsh-self-improvement) | 1 | 2026-09-11 | 2026-09-11 | Cross-session self-improvement for DeepSeek Harness: persistent weighted memory, retrospectives, SOP skills and improvement proposals. |
| 29 | [FiretrUCK666/dsh-task-board](https://github.com/FiretrUCK666/dsh-task-board) | 1 | 2026-09-10 | 2026-09-11 | DSH Web GUI 的任务看板插件：侧边栏入口 + 五列看板，任务经 DSH 会话真实执行，host 端持久化并跨设备实时同步。Task board plugin for the DeepSeek Harness web GUI. |
| 30 | [fsrmqi/dsh-research-kit](https://github.com/fsrmqi/dsh-research-kit) | 1 | 2026-09-10 | 2026-09-11 | dsh-research-kit 是一个 浏览器侧 DSH 插件：它维护科研资源目录、把工作流和用户参数组装成可编辑 Prompt，并由 DSH 当前会话负责实际发送与执行。 |
| 31 | [huiyeo/dsh-plugin-mermaid-preview](https://github.com/huiyeo/dsh-plugin-mermaid-preview) | 1 | 2026-09-11 | 2026-09-11 | Mermaid diagram previews for the DeepSeek Harness right-sidebar document viewer (.mmd / .mermaid), with per-view zoom that stays crisp on scaled displays |
| 32 | [it-kxw/dsh-ui-background](https://github.com/it-kxw/dsh-ui-background) | 1 | 2026-09-10 | 2026-09-11 | DSH Web 背景切换插件：内置渐变/纯色预设、本地图片上传与路径引用，支持不透明度/模糊/填充调节，浅深配色自动适配，一条命令即可安装使用。 |
| 33 | [jiale-li-orion/meshfin](https://github.com/jiale-li-orion/meshfin) | 1 | 2026-08-20 | 2026-09-11 | One agent across many devices — a multi-device capability runtime and personal workbench for persistent agents, built on DeepSeek Harness. |
| 34 | [kbzhao7/QQ.dsh-qqbot](https://github.com/kbzhao7/QQ.dsh-qqbot) | 1 | 2026-09-10 | 2026-09-11 | 基于DSH-QQBOT项目的dsh-qqbotGPT优化版本 |
| 35 | [li-sky/dsh-aiservice-deeplink](https://github.com/li-sky/dsh-aiservice-deeplink) | 1 | 2026-09-11 | 2026-09-11 | Support aiservice:// link in deepseek harness. Makes configuring a model easier. |
| 36 | [longmiaoo/dsh-native-browser](https://github.com/longmiaoo/dsh-native-browser) | 1 | 2026-09-11 | 2026-09-11 | A production-grade, DSH-native browser runtime for DeepSeek Harness with visible human-agent collaboration. |
| 37 | [omdsh-dev/dsh-gal](https://github.com/omdsh-dev/dsh-gal) | 1 | 2026-08-15 | 2026-09-11 | Galgame / visual-novel UI plugin for the DeepSeek Harness: a whale-girl companion with animated expressions, scene-at-a-time dialogue, and an LLM emotion judge |
| 38 | [the-beating-light-of-the-nail/awesome-dsh-tavern](https://github.com/the-beating-light-of-the-nail/awesome-dsh-tavern) | 1 | 2026-09-11 | 2026-09-11 | 🍺 DeepSeek Harness (dsh) 酒馆与角色扮演插件精选 — 把酒馆搬进 agent \| Curated tavern & roleplay plugins for dsh |
| 39 | [ttxs66666/dsh-review-gate](https://github.com/ttxs66666/dsh-review-gate) | 1 | 2026-09-11 | 2026-09-11 | Independent review gate for DeepSeek Harness: hand finished derivations and code to a reviewer subagent and feed its verdict back to the main model. |
| 40 | [wangzhanchao883/dsh-hold-to-talk](https://github.com/wangzhanchao883/dsh-hold-to-talk) | 1 | 2026-09-11 | 2026-09-11 | Hold-to-talk voice input for the DeepSeek Harness web composer: hold the mouse on the input box, speak, release to insert the text into the draft. Local SenseVoice ASR via sherpa-onnx: no API key, offline, audio never leaves the machine. \| DSH 长按说话语音输入插件:输入框上按住鼠标说话,浮层边说边出字,松手把文字写进输入框,上滑取消;识别在本机跑,免密钥、离线、音频不出本机。 |
| 41 | [WYR-233/dsh-multi-tts](https://github.com/WYR-233/dsh-multi-tts) | 1 | 2026-09-11 | 2026-09-11 | Multi-provider TTS (read replies aloud) plugin for DeepSeek Harness - pick your own provider and voice |
| 42 | [WYR-233/plugins-site](https://github.com/WYR-233/plugins-site) | 1 | 2026-09-11 | 2026-09-11 | ????? - WYR-233 ? DSH ??????(plugins.wyr233.com) |
| 43 | [xp266/dsh-tui](https://github.com/xp266/dsh-tui) | 1 | 2026-08-15 | 2026-09-11 | ink-based terminal UI plugin for DeepSeek Harness |
| 44 | [yangzqq/dsh-mdvault](https://github.com/yangzqq/dsh-mdvault) | 1 | 2026-09-11 | 2026-09-11 | DSH Web UI workspace document vault — a “文档” tab for previewing Markdown/PDF/Excel/images/code with wikilinks, Mermaid and in-page editing. |
| 45 | [zhengmz/dsh-auto-fold](https://github.com/zhengmz/dsh-auto-fold) | 1 | 2026-09-11 | 2026-09-11 | 补齐 DSH 在对话显示设为 Compact（紧凑）时无法自动折叠的能力。 Fills in the missing capability for DSH to auto-fold when the conversation display is set to Compact.  |
| 46 | [01men/RQ-DSH](https://github.com/01men/RQ-DSH) | 0 | 2026-09-02 | 2026-09-11 | 榕器定制轨（01门）· AI 代理与人类协作前台——dsh 一键插件化一线面板/看板（班组长工作台/执行卡/Skill 点名直调/钉钉桥），上游 01men/ybkk-AIOS |
| 47 | [1569126506-sudo/dsh-team-cost](https://github.com/1569126506-sudo/dsh-team-cost) | 0 | 2026-09-10 | 2026-09-11 | DeepSeek Harness 团队成本管家:按成员/项目计量 token 与费用(含子代理),预算告警与超支拦截,成本看板与报表。Team cost captain for DSH: per-member token & cost metering, budgets, alerts, dashboard. |
| 48 | [a86582751/dsh-nexttavern](https://github.com/a86582751/dsh-nexttavern) | 0 | 2026-09-11 | 2026-09-11 | 原生 Agent 驱动的长篇角色扮演：交互式创作、主动世界书、动态记忆、多角色推演与小说导出。创作一个世界，走进它，再把它带走。 |
| 49 | [AGImentu/dsh-cost-stats](https://github.com/AGImentu/dsh-cost-stats) | 0 | 2026-09-11 | 2026-09-11 | DSH (DeepSeek Harness) Web 插件：每条助手消息旁的费用胶囊 + 设置里的「费用统计」页（逐条计费项、回复与上下文压缩分开、官方 CNY/USD 价目表、高峰/空闲感知） |
| 50 | [aibo204/dsh-plugin-computer-use](https://github.com/aibo204/dsh-plugin-computer-use) | 0 | 2026-09-11 | 2026-09-11 | Safe Computer Use plugin for DeepSeek Harness with approvals and local audit archives |
| 51 | [Amouren7/dsh-plugin-desk](https://github.com/Amouren7/dsh-plugin-desk) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness 插件管家：用人话说明每个插件是做什么的，一键停用/启用（热生效），安全卸载。Settings → Plugins → 插件管家 |
| 52 | [ankhishtar2-lang/dsh-sakurafrp](https://github.com/ankhishtar2-lang/dsh-sakurafrp) | 0 | 2026-09-11 | 2026-09-11 | dsh-mobile satellite: manage the SakuraFrp phone-desktop link from DSH UI (status, gateway toggle, pairing QR, devices, self-heal). Vibe-coded. |
| 53 | [ankhishtar2-lang/dsh-wallpaper-position](https://github.com/ankhishtar2-lang/dsh-wallpaper-position) | 0 | 2026-09-11 | 2026-09-11 | dsh-dream-skin satellite: per-image wallpaper position (X/Y px) settings row. Vibe-coded. |
| 54 | [ankhishtar2-lang/dsh-whale-tools](https://github.com/ankhishtar2-lang/dsh-whale-tools) | 0 | 2026-09-11 | 2026-09-11 | dsh-whale-widget satellite: replace the whale mascot with any image (auto cutout) + restart button + heartbeat. Vibe-coded. |
| 55 | [Arborsm/dsh-remember](https://github.com/Arborsm/dsh-remember) | 0 | 2026-09-10 | 2026-09-11 | Cross-session long-term memory plugin for DeepSeek Harness |
| 56 | [axelfreeman/backupper](https://github.com/axelfreeman/backupper) | 0 | 2026-09-06 | 2026-09-11 | Free encrypted deduplicated backups of remote Linux servers, pulled from a Windows PC with Restic — zero software installed server-side. AI-agent skill. |
| 57 | [Beatther-c/dsh-api-client](https://github.com/Beatther-c/dsh-api-client) | 0 | 2026-09-07 | 2026-09-11 | Agent-native API Client for DeepSeek Harness — Postman 级 API 调试 UI + Agent 原生 HTTP 工具 + Postman Collection 导入的 DSH 原生插件 |
| 58 | [blueperformer/make-dsh-voice](https://github.com/blueperformer/make-dsh-voice) | 0 | 2026-09-10 | 2026-09-11 | A small plugin I made myself, inspired in part by other people's projects. |
| 59 | [caijiachen34/dsh-sophnet-balance](https://github.com/caijiachen34/dsh-sophnet-balance) | 0 | 2026-08-17 | 2026-09-11 | SophNet balance and usage monitor for DeepSeek Harness Web GUI |
| 60 | [canhta/dsh-autopilot](https://github.com/canhta/dsh-autopilot) | 0 | 2026-09-11 | 2026-09-11 | Turn tickets into pull requests. Powered by DeepSeek Harness. |
| 61 | [catsenior507/dsh-clock](https://github.com/catsenior507/dsh-clock) | 0 | 2026-09-11 | 2026-09-11 | Calendar and clock for DeepSeek Harness: an alarm wakes a chosen conversation at a chosen instant, by keyword, with the system time and the drift injected into the wake. In-process timer plus a Windows Task Scheduler mirror. |
| 62 | [cbg33695/dsh-screen-reader](https://github.com/cbg33695/dsh-screen-reader) | 0 | 2026-09-11 | 2026-09-11 | Let a text-only model see the screen: capture desktop/window/region, vision transcription, a few minutes of rolling screen memory, exact local pixel diff, and vision self-calibration. Windows only. Experimental - the README states what is measured and what is not. |
| 63 | [chen1pengvincent/dsh-model-sync-plugin](https://github.com/chen1pengvincent/dsh-model-sync-plugin) | 0 | 2026-09-10 | 2026-09-11 | DSH 模型插件：监控并更新各服务商提供的最新模型（检查只读、勾选添加、不自动删除） |
| 64 | [chuling-lingling/dsh-plugin-reasoning-efforts](https://github.com/chuling-lingling/dsh-plugin-reasoning-efforts) | 0 | 2026-09-11 | 2026-09-11 | 给 DeepSeek Harness (dsh) 的第三方中转模型补上「推理等级」选择器 —— 和官方模型在聊天框里的体验完全一致。 |
| 65 | [chuling-lingling/dsh-plugin-use-images](https://github.com/chuling-lingling/dsh-plugin-use-images) | 0 | 2026-09-11 | 2026-09-11 | 再dsh里面可以使用图片api |
| 66 | [CMoyuer/dsh-cad-viewer](https://github.com/CMoyuer/dsh-cad-viewer) | 0 | 2026-09-11 | 2026-09-11 | 用于Deepseek Harness的CAD设计插件 |
| 67 | [cmukanisa/dsh-remote-ssh](https://github.com/cmukanisa/dsh-remote-ssh) | 0 | 2026-09-11 | 2026-09-11 | A community plugin for the DeepSeek Harness (DSH): connect a server over SSH, pick a folder there, and work in it with every tool. Not affiliated with DeepSeek. |
| 68 | [CoolTea001/dsh-cool-terminal](https://github.com/CoolTea001/dsh-cool-terminal) | 0 | 2026-09-10 | 2026-09-11 | Terminal plugin for DeepSeek Harness: stays in sync with the Workspace in real time, with isolated terminals that each keep their own command history. |
| 69 | [DDA-DIGITAL/dsh-web-lifecycle](https://github.com/DDA-DIGITAL/dsh-web-lifecycle) | 0 | 2026-09-10 | 2026-09-11 | DSH web plugin: Restart and Shutdown buttons in the sidebar footer. Restart relaunches dsh web on the same host/port so the tab reconnects itself; Shutdown stops the server to free the terminal and closes the browser tab. |
| 70 | [DecresLuna/dsh-DSH-Service](https://github.com/DecresLuna/dsh-DSH-Service) | 0 | 2026-08-22 | 2026-09-11 | DSH Service - DeepSeek Harness Mac 菜单栏服务管理器 |
| 71 | [DNAlec/dsh-auto-approve](https://github.com/DNAlec/dsh-auto-approve) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness 自动审批插件：关键词 + LLM 审核。可推送至消息平台。 |
| 72 | [dreamor/MemVault](https://github.com/dreamor/MemVault) | 0 | 2026-08-10 | 2026-09-11 | MemVault — The Shared Memory Layer for Every AI Agent You Run. MCP-native memory router with auto-injection, hybrid search, and zero-config sync. |
| 73 | [dsh-plugins/dsh-file-drop-attachments](https://github.com/dsh-plugins/dsh-file-drop-attachments) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness Web plugin: native image previews plus persistent non-image file-drop attachment cards |
| 74 | [duanyunlun/dsh-provider-headers](https://github.com/duanyunlun/dsh-provider-headers) | 0 | 2026-09-11 | 2026-09-11 | Per-provider request headers in the DeepSeek Harness Models settings page, with per-conversation ${sessionId} expansion. |
| 75 | [eibednejo/dsh-llm-commandcode](https://github.com/eibednejo/dsh-llm-commandcode) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness (dsh) LLM adapter for Command Code — routes model calls through the generate endpoint a Go plan can reach, including image input. |
| 76 | [fancyboi999/dsh-newwindows](https://github.com/fancyboi999/dsh-newwindows) | 0 | 2026-09-11 | 2026-09-11 | ⚡ Summary-free context window rollover, model-authored notes, and scoped history lookup plugin for DeepSeek Harness (DSH). Inspired by OpenAI Codex. |
| 77 | [fengbai2233/dsh-pwsh-quoting-guard](https://github.com/fengbai2233/dsh-pwsh-quoting-guard) | 0 | 2026-09-11 | 2026-09-11 | DSH plugin: pwsh_script + run_argv — structural immunity to PowerShell command-string quoting errors on Windows. |
| 78 | [FitBBC/dsh-plugin-tokenmarket](https://github.com/FitBBC/dsh-plugin-tokenmarket) | 0 | 2026-09-10 | 2026-09-11 | Token Market provider bundle for DeepSeek Harness |
| 79 | [fqsklm/dsh-balance-chart](https://github.com/fqsklm/dsh-balance-chart) | 0 | 2026-09-11 | 2026-09-11 | DSH (DeepSeek Harness) Web GUI 插件：把 DeepSeek 账户余额、当日消费和峰谷时段计价画在会话标题栏上的双层图表。零依赖，余额差值优先记账。 |
| 80 | [gdrpzym/dsh-loomy-connect](https://github.com/gdrpzym/dsh-loomy-connect) | 0 | 2026-09-11 | 2026-09-11 | Use the models that ship with the Loomy desktop app inside DeepSeek Harness — no API key. Also adds a Settings card showing the signed-in account and Loomy credits (permanent + daily gift). |
| 81 | [Geighlord007/qp-exa-dynamic](https://github.com/Geighlord007/qp-exa-dynamic) | 0 | 2026-09-10 | 2026-09-11 | Exa web search provider for the DeepSeek Harness ctx.web seam, with Exa Dynamic Highlights on by default and a /exa command to change highlights, search type and result count at runtime. |
| 82 | [GodCC6/dsh-updater](https://github.com/GodCC6/dsh-updater) | 0 | 2026-09-11 | 2026-09-11 | Auto-update plugin for DeepSeek Harness (git / npm dual-mode) — ff-only pulls, automatic rollback, optional idle-aware auto-apply |
| 83 | [gongyijie85/dsh-design-audit](https://github.com/gongyijie85/dsh-design-audit) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness 的 UI/UX 审查与优化闭环：无头 Chrome 取证 → 确定性判据（WCAG 2.2 / 平台指南）→ 可粘贴修复 → 复测差值验证 |
| 84 | [GooDAnDReaDY/dsh-remote-workspace](https://github.com/GooDAnDReaDY/dsh-remote-workspace) | 0 | 2026-09-10 | 2026-09-11 | Enterprise Remote Workspace for DeepSeek Harness: SSH, SFTP File Sync & Tunneling |
| 85 | [greyoak111/siyuan-codex-bridge](https://github.com/greyoak111/siyuan-codex-bridge) | 0 | 2026-09-08 | 2026-09-11 | Local Codex and SiYuan official MCP bridge with the Siyuan Notes plugin tooling. |
| 86 | [haotian-lu-prog/dsh-update-all](https://github.com/haotian-lu-prog/dsh-update-all) | 0 | 2026-09-11 | 2026-09-11 | One-command DSH updater: CLI, bundles and all profile plugins — plus a dsh-plugin for Settings → General, with backups and rollback. |
| 87 | [HaoyanZhang123/dsh-live-preset-switch](https://github.com/HaoyanZhang123/dsh-live-preset-switch) | 0 | 2026-09-11 | 2026-09-11 | DSH skill provider bundle: live agent-preset switching guidance (additive, no lifecycle scripts, no runtime dependencies) |
| 88 | [HeJian2002W/dsh-reveal-fix](https://github.com/HeJian2002W/dsh-reveal-fix) | 0 | 2026-09-11 | 2026-09-11 | Fix DSH's "reveal in file manager" silently doing nothing on Windows. User-space plugin — survives dsh upgrades, no core files patched. |
| 89 | [HERO476/dsh-instruction-memory](https://github.com/HERO476/dsh-instruction-memory) | 0 | 2026-09-11 | 2026-09-11 | DSH instruction memory plugin: maintain long-term instructions in the DSH settings UI, auto-injected into every subsequent conversation's system prompt. |
| 90 | [huangyuheng/dsh-token-use](https://github.com/huangyuheng/dsh-token-use) | 0 | 2026-09-09 | 2026-09-11 | 实时 Token 用量仪表盘 · Real-time token usage dashboard for DeepSeek Harness — live totals, filters by model/day/month/project, smooth trend chart. |
| 91 | [hululuzzzgululu/dsh-evals-promptfoo](https://github.com/hululuzzzgululu/dsh-evals-promptfoo) | 0 | 2026-09-11 | 2026-09-11 | This project connects Deepseek Harness and Promptfoo: it launches a real Agent through the official DSH TypeScript SDK, collects the final answers, tool calls, subagents, and execution state, and hands everything to Promptfoo for display and scoring. |
| 92 | [Huuuuung/dsh-artifact-index](https://github.com/Huuuuung/dsh-artifact-index) | 0 | 2026-09-11 | 2026-09-11 | The missing backend for the DeepSeek Harness dsh-artifacts sidebar tab: serves the artifact index JSON and the artifact bytes. |
| 93 | [icanfinish11/dsh_superpowers](https://github.com/icanfinish11/dsh_superpowers) | 0 | 2026-09-11 | 2026-09-11 | Superpowers for the DeepSeek Harness: a dsh plugin that registers the Superpowers skills as a skill catalog and injects the using-superpowers bootstrap into the system prompt. |
| 94 | [ice-ai-lab/dsh-plugin-pi-ui](https://github.com/ice-ai-lab/dsh-plugin-pi-ui) | 0 | 2026-09-11 | 2026-09-11 | pi-web-inspired sidebar chrome for the DeepSeek Harness Web GUI: temporary sessions, a one-directory session list under a working-directory picker, a draft composer that creates nothing until you send, and a compact file explorer tab. |
| 95 | [icedrop-lab/dsh-plugins](https://github.com/icedrop-lab/dsh-plugins) | 0 | 2026-09-10 | 2026-09-11 | Independent DeepSeek Harness plugins: cost metrics + browser_use tool. One pnpm monorepo, independently installable and vendable. |
| 96 | [inxups/dsh-user-plugins](https://github.com/inxups/dsh-user-plugins) | 0 | 2026-09-11 | 2026-09-11 | A dsh web GUI panel listing the plugins you installed into your dsh profiles — install spec, version, kind, and live loader phase. |
| 97 | [JeffreySuen-x/dsh-skill-dossier](https://github.com/JeffreySuen-x/dsh-skill-dossier) | 0 | 2026-08-21 | 2026-09-11 | DeepSeek Harness (DSH) 的技能档案 + 工作汇报插件：把散在 ~/.dsh/skills、.dsh/skills 的 skills 收成一份可读、可核对、可保鲜的档案（方向/使用范围/能力边界/应用场景/调用统计），支持停用·重装·彻底删除；并把每日工程简报汇成日报/周报/月报。Skill dossier + work report plugin for DSH. |
| 98 | [Jianwen-Xu/dsh-deepseek-balance](https://github.com/Jianwen-Xu/dsh-deepseek-balance) | 0 | 2026-09-11 | 2026-09-11 | DSH 插件：在 Web 侧边栏显示 DeepSeek API 余额与高峰/空闲计费时段 |
| 99 | [jing-hy/dsh-think-zh-expand-eac](https://github.com/jing-hy/dsh-think-zh-expand-eac) | 0 | 2026-09-11 | 2026-09-11 | DSH 思考增强插件（EAC 定制版）：强制中文思考与回复 + 界面中文化；已移除全部接管对话渲染器的显示功能，不再与折叠类插件（dsh-auto-collapse / dsh-turn-fold）冲突。Fork of baosfeng/dsh-think-zh-expand. |
| 100 | [kexuejin/dsh-accounts-ui](https://github.com/kexuejin/dsh-accounts-ui) | 0 | 2026-09-11 | 2026-09-11 | DSH 插件：给 dsh-accounts 在设置面板加「账号」区（原生 UI 组件渲染）。Adding a native 账号 settings section to dsh-accounts — superseded by yangwuan55/dsh-accounts#1. |
| 101 | [kexuejin/dsh-browser-bsk](https://github.com/kexuejin/dsh-browser-bsk) | 0 | 2026-09-11 | 2026-09-11 | DSH 插件：用本机 bsk CLI（腾讯 BrowserSkill 的 CLI）提供 browser 能力 seam（ctx.browser）——零工具注册，可与 browser-skill 共存。Browser seam (ctx.browser) backed by the bsk CLI; registers no tools. |
| 102 | [kichare/dsh-local-dba](https://github.com/kichare/dsh-local-dba) | 0 | 2026-09-11 | 2026-09-11 | A local database-administration (DBA) plugin for [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness). It ships as a Cordis plugin bundle that registers a set of `db_*` model-facing tools, letting the agent query, inspect schema, run DDL/DML, back up/restore and analyze slow queries against **MySQL / MariaDB** and **PostgreSQL**. |
| 103 | [kllilizxc/dsh-worka](https://github.com/kllilizxc/dsh-worka) | 0 | 2026-09-11 | 2026-09-11 | Cover your desk in AI agents. Every sticky note is a tool, a teammate, or a task getting done. |
| 104 | [kongbai-shike/dsh-drop-path](https://github.com/kongbai-shike/dsh-drop-path) | 0 | 2026-09-11 | 2026-09-11 | 对于Deepseek-Harness，桌面版来说，只有图片才能直接接收，对于用惯了claudecode的人来说很不习惯，所以我依靠ai完成了一个可以直接在文件管理器页面，把需要上传的文件拖拽到对应的DSH桌面端界面，就能直接把对应的路径名完完整整的显示在输入框里。 |
| 105 | [l956615272-hub/dsh-token-usage](https://github.com/l956615272-hub/dsh-token-usage) | 0 | 2026-09-11 | 2026-09-11 | 统计本机全部 DSH 会话的历史 token 总消耗，按 message.id 去重，支持按天/模型/Provider/项目分组。 |
| 106 | [latte03/dsh-select-quote](https://github.com/latte03/dsh-select-quote) | 0 | 2026-09-11 | 2026-09-11 | 对话中划词，把选中文本作为引用带进下一条消息：划词浮动工具条（复制 / 添加到任务）、输入框内的引用卡片，以及对话记录里对应的引用卡片。 |
| 107 | [leeyoung1/dsh-advisor-plugin](https://github.com/leeyoung1/dsh-advisor-plugin) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness advisor plugin: pair a fast executor with a stronger reviewer model |
| 108 | [lengxiaoyu6/dsh-model-extended](https://github.com/lengxiaoyu6/dsh-model-extended) | 0 | 2026-09-11 | 2026-09-11 | dsh 模型目录增强：每个模型单独设置思考强度范围与支持的输入模态。Per-model reasoning-effort range and input modalities for the dsh Models catalog. |
| 109 | [leolee9086/dsh-sketchup](https://github.com/leolee9086/dsh-sketchup) | 0 | 2026-09-08 | 2026-09-11 | DeepSeek Harness 的 SketchUp 独立对接套装：Host 插件、Ruby 扩展、内嵌聊天与 CEF 兼容垫片。保留上游 fork 来源及 MIT 版权。 |
| 110 | [lifangjin/dsh-paoding](https://github.com/lifangjin/dsh-paoding) | 0 | 2026-09-11 | 2026-09-11 | 庖丁解牛，游刃有余 —— 把 DSH 编排成角色分工、按需加载的 agent preset。 |
| 111 | [liudejua27-blip/fitmeet-dsh-plugin](https://github.com/liudejua27-blip/fitmeet-dsh-plugin) | 0 | 2026-09-11 | 2026-09-11 | FitMeet MCP + Skill for DeepSeek Harness：每位用户通过 OAuth 2.1 + PKCE 授权，支持找人、发布与私聊。 |
| 112 | [liyu1314-lmyc/dsh-archive-browser](https://github.com/liyu1314-lmyc/dsh-archive-browser) | 0 | 2026-09-11 | 2026-09-11 | Browse archived DSH sessions and re-invoke them: view the transcript, restore to the sidebar, inject into the current conversation, or fork a new session. |
| 113 | [longisland-icetea/dsh-lan-access](https://github.com/longisland-icetea/dsh-lan-access) | 0 | 2026-09-06 | 2026-09-11 | Open the DeepSeek Harness Web GUI's LAN access fences: serve on all interfaces, trust only the configured LAN authorities, and choose them from a settings tab. |
| 114 | [MistyRain-field/dsh-hu-tao-skin](https://github.com/MistyRain-field/dsh-hu-tao-skin) | 0 | 2026-09-11 | 2026-09-11 | 原神 · 胡桃（往生堂）界面美化 — DeepSeek Harness Web GUI 客户端插件皮肤 / Hu Tao (Wangsheng Funeral Parlor) skin for dsh web |
| 115 | [muen-collective/muen-plugins](https://github.com/muen-collective/muen-plugins) | 0 | 2026-09-11 | 2026-09-11 | Muen-authored plugins for the DeepSeek Harness market — published as GitHub Release tarballs and installed with `dsh plugin add`. Generic, white-label, no client identity baked in. |
| 116 | [netori/dsh-imagegen-zhenzhen](https://github.com/netori/dsh-imagegen-zhenzhen) | 0 | 2026-09-11 | 2026-09-11 | DSH image-generation plugin with native support for zhenzhen-image style async task gateways (submit + poll), including multi-reference image-to-image. Fork of @dickpy/dsh-imagegen. |
| 117 | [Neutron3529/dsh-plugin-tool-gaming-host](https://github.com/Neutron3529/dsh-plugin-tool-gaming-host) | 0 | 2026-09-10 | 2026-09-11 | 一个允许agent借助gaming程序直接访问宿主机的插件。日后或许会搞个网页版，把gaming改成bwrap然后允许传参什么的，但现在，这个库只有最基础的功能 |
| 118 | [nobu121/dsh-npm-runner](https://github.com/nobu121/dsh-npm-runner) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness plugin: discovers the npm/pnpm/yarn/bun scripts of the current workspace (never descending into node_modules) and runs any of them in the background from a compact control in the composer area or the session header. |
| 119 | [openplancc/dsh-plugin](https://github.com/openplancc/dsh-plugin) | 0 | 2026-09-11 | 2026-09-11 | Cost policy plugin for DeepSeek Harness: per-call metering plus an offline fuse that enforces budget, model and reasoning-effort limits before any token is spent. |
| 120 | [peng7peng/dsh-terminal-manager](https://github.com/peng7peng/dsh-terminal-manager) | 0 | 2026-09-11 | 2026-09-11 | dsh-terminal-manager |
| 121 | [PerryLink/dsh-plugin-upgrade-015](https://github.com/PerryLink/dsh-plugin-upgrade-015) | 0 | 2026-09-10 | 2026-09-11 | Merged DSH plugin upgrade corridor: dsh-v0.1.3-alpha.1 -> dsh-v0.1.5-rc.1. Two-leg evidence-bound version card plus a zero-dependency seam scanner (npx dsh-plugin-upgrade-015-scan). |
| 122 | [printz1/dsh-notify](https://github.com/printz1/dsh-notify) | 0 | 2026-09-11 | 2026-09-11 | DSH Web GUI 通知插件：需要审批 / 模型提问 / 一轮指令结束 / 后台任务结束 / 会话出错时提醒。带完整设置页 —— 场景开关、静音指定会话、免打扰时段、时长下限、提醒节流、系统通知/页面内气泡/提示音三渠道。 |
| 123 | [publieople/dsh-chat-offscreen](https://github.com/publieople/dsh-chat-offscreen) | 0 | 2026-09-11 | 2026-09-11 | DSH Web plugin: keep long chat sessions responsive by skipping layout/paint for off-screen transcript rows (content-visibility). |
| 124 | [RempleXI/word-docx-writer](https://github.com/RempleXI/word-docx-writer) | 0 | 2026-09-11 | 2026-09-11 | 生成与排版中文 Word（.docx）的 Agent Skill 与工具包：标题使用 Word 内置样式，中文宋体 + 西文 Times New Roman，正文小四首行缩进，图表题注按章自动编号；通用于实验报告、课程设计报告、毕业论文等各类中文长文档。 |
| 125 | [Ringo-P-GIT/dsh-reqsys](https://github.com/Ringo-P-GIT/dsh-reqsys) | 0 | 2026-09-11 | 2026-09-11 | ??????(?? & ??)-- DSH ??,? dsh-pet ???????/???? |
| 126 | [Sawyer20/DSH-Control-Center](https://github.com/Sawyer20/DSH-Control-Center) | 0 | 2026-09-09 | 2026-09-11 | DSH control center |
| 127 | [shaomingbo/dsh-web-fetch-proxy](https://github.com/shaomingbo/dsh-web-fetch-proxy) | 0 | 2026-09-11 | 2026-09-11 | Proxy-egress fetch provider for DeepSeek Harness |
| 128 | [singei8/DSH-TOKEN-feiyong](https://github.com/singei8/DSH-TOKEN-feiyong) | 0 | 2026-09-11 | 2026-09-11 | DSH（DeepSeek Harness）动态 Cordis 计费插件：按官方价目表逐笔计算 token 花费（缓存命中 / 未命中 / 输出），高峰低谷分时计价，含账户余额、单次与本对话统计，数据本地持久化。 |
| 129 | [snailium/dsh-repeat-tool-breaker](https://github.com/snailium/dsh-repeat-tool-breaker) | 0 | 2026-09-11 | 2026-09-11 | Hard break on repeated identical tool calls in DeepSeek Harness (DSH): a synchronous monotonic ctx.tools.guard gate that denies the 2nd identical call per agent. Dependency-free. |
| 130 | [sogoodayo/dsh-livedocs](https://github.com/sogoodayo/dsh-livedocs) | 0 | 2026-09-10 | 2026-09-11 | DSH 实时库文档：写代码前自动拉取项目安装版本的官方文档，消灭幻觉 API。零配置零 Key。Version-pinned live library docs for DeepSeek Harness — kill hallucinated APIs |
| 131 | [Sqhao-O/dsh-intercom](https://github.com/Sqhao-O/dsh-intercom) | 0 | 2026-08-16 | 2026-09-11 | Inter-session messaging plugin for DeepSeek Harness (dsh): let independent dsh sessions on one machine discover each other and exchange messages (send / ask / reply). Port of pi-intercom. |
| 132 | [strawberry0321/dsh-gal](https://github.com/strawberry0321/dsh-gal) | 0 | 2026-09-11 | 2026-09-11 | dsh-gal —— DeepSeek Harness 的立绘挂件：实时显示余额与今日消耗、每轮对话结束结算 token 与花费、点击立绘随机播语音并逐字显示台词，立绘包/语音包都能换 |
| 133 | [Sxuan-Coder/dsh-user-prompt](https://github.com/Sxuan-Coder/dsh-user-prompt) | 0 | 2026-09-11 | 2026-09-11 | 负责给DSH增加用户自定义提示词功能的插件，支持自动从ClaudeCode和Codex一键导入 |
| 134 | [temidayoxyz/deep-browser](https://github.com/temidayoxyz/deep-browser) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness (dsh) plugin: browse http(s) pages in the right sidebar, beside the conversation. |
| 135 | [tqcq/dsh-auto-reconnect](https://github.com/tqcq/dsh-auto-reconnect) | 0 | 2026-09-11 | 2026-09-11 | Client-only auto-reconnect for the DSH web client. |
| 136 | [vclike/dsh-find-plugin](https://github.com/vclike/dsh-find-plugin) | 0 | 2026-09-11 | 2026-09-11 | Find DSH plugins from inside the agent - live GitHub dsh-plugin topic search + the curated awesome-dsh-plugin list, with token auth, rate-limit resilience and offline fallback. Fork of awesome-dsh-plugin/dsh-find-plugin. |
| 137 | [vclike/dsh-github-companion](https://github.com/vclike/dsh-github-companion) | 0 | 2026-08-23 | 2026-09-11 | DeepSeek Harness 插件：AI 操作 GitHub 的完整集成——33 个 REST/GraphQL 工具 + 进程内权限门 + 成本纪律 companion skill — DeepSeek Harness plugin: complete GitHub integration for AI agents, 33 tools, permission gate, companion skill. |
| 138 | [Vithrive/dsh-livebench-panel](https://github.com/Vithrive/dsh-livebench-panel) | 0 | 2026-09-11 | 2026-09-11 | DSH web plugin: a LiveBench tab in the Trajectory view. Run LiveBench evaluations against every model configured in the DeepSeek Harness and read scores in place. |
| 139 | [whiteS18/dsh-mcp-servers-panel](https://github.com/whiteS18/dsh-mcp-servers-panel) | 0 | 2026-09-11 | 2026-09-11 | DSH MCP 服务器管理面板：设置里新增/编辑/启停 MCP 服务器，工具自动注册到对话 |
| 140 | [wig123/dsh-thread-tools](https://github.com/wig123/dsh-thread-tools) | 0 | 2026-09-10 | 2026-09-11 | Cross-session tools for DeepSeek Harness: list the deployment's other sessions and deliver a message to a live one |
| 141 | [wings1848/dsh-mcp-lazy](https://github.com/wings1848/dsh-mcp-lazy) | 0 | 2026-09-10 | 2026-09-11 | Lazy MCP gateway for DeepSeek Harness: one stable proxy tool instead of N tool schemas, servers connect on first use and idle out, metadata cached to disk. |
| 142 | [Wisper-beep/dsh-runbox](https://github.com/Wisper-beep/dsh-runbox) | 0 | 2026-09-11 | 2026-09-11 | Isolated execution substrate for DeepSeek Harness (dsh): run agent shell / fs / process / terminal / jobs inside disposable containers. |
| 143 | [wjx-ai/dsh-md-reader](https://github.com/wjx-ai/dsh-md-reader) | 0 | 2026-09-11 | 2026-09-11 | DSH Markdown 阅读插件：点击会话中的 MD/图片链接，在浏览器右侧以真三栏布局（侧边栏 \| 会话区 \| 文档）直接阅读 —— 目录 TOC、自动跟随磁盘变更、图片内联预览、复制原文、字号缩放。dsh plugin --profile web add github:wjx-ai/dsh-md-reader |
| 144 | [WShihan/dsh-macos-notify](https://github.com/WShihan/dsh-macos-notify) | 0 | 2026-09-10 | 2026-09-11 | dsh notification plugin for macos |
| 145 | [wuwaka/dsh-clipboard-menu](https://github.com/wuwaka/dsh-clipboard-menu) | 0 | 2026-09-11 | 2026-09-11 | Adds a right-click menu to DeepSeek Harness inside desktop shells that ship no context menu: cut, copy, paste and select all in the composer, plus copy and copy-as-plain-text on selected text elsewhere. |
| 146 | [xDJTomato/deepseek-harnessed](https://github.com/xDJTomato/deepseek-harnessed) | 0 | 2026-09-11 | 2026-09-11 | Turn a DeepSeek Harness (DSH) instance into a subagent any harness (Cursor / Claude Code / Codex / Gemini CLI ...) can call over MCP - plus a live monitor panel inside DSH Desktop. |
| 147 | [xiaml666/dsh-plugin-cost](https://github.com/xiaml666/dsh-plugin-cost) | 0 | 2026-09-11 | 2026-09-11 | DSH 花费显示：每轮对话花了多少钱、整个会话累计多少钱，按官方价格表精确计价（自动刷新、高峰/低谷自动同步、多供应商多币种），并附带账户余额与可视化设置面板；余额与会话累计始终同币种。 |
| 148 | [xiaomao49/dsh-model-probe](https://github.com/xiaomao49/dsh-model-probe) | 0 | 2026-09-10 | 2026-09-11 | DeepSeek Harness plugin to audit and correct llm-pi-ai model capability declarations by probing the endpoint itself: out-of-range maxTokens, contextWindow, reasoning levels, image input. |
| 149 | [Xieweikang123/dsh-plugin-quote](https://github.com/Xieweikang123/dsh-plugin-quote) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness Web plugin: quote a text selection into the composer as a markdown blockquote. |
| 150 | [XMeowchan/dsh-agent-team-model](https://github.com/XMeowchan/dsh-agent-team-model) | 0 | 2026-09-11 | 2026-09-11 | Visual provider, model and reasoning-effort defaults for DeepSeek Harness Agent Teams. |
| 151 | [YeeNg2333/shaoleme](https://github.com/YeeNg2333/shaoleme) | 0 | 2026-09-11 | 2026-09-11 | A floating, animated dsh widget that shows how much RMB u burned in DeepSeek. |
| 152 | [Yinxe/deepseek-harness-plugins](https://github.com/Yinxe/deepseek-harness-plugins) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness (DSH) plugins monorepo (pnpm + TypeScript) |
| 153 | [yis94744/dsh-darkplus-code](https://github.com/yis94744/dsh-darkplus-code) | 0 | 2026-09-11 | 2026-09-11 | VS Code Dark+ syntax colors and font-size control for DeepSeek Harness (dsh) code blocks |
| 154 | [YpipaQ/dsh-skills-mcp-cli-manager](https://github.com/YpipaQ/dsh-skills-mcp-cli-manager) | 0 | 2026-09-11 | 2026-09-11 | Skills / MCP / CLI manager for the DeepSeek Harness (dsh) web GUI — one settings page, real MCP connections, and a unified ~/.dsh/S-M-C store. |
| 155 | [yuu1111/dsh-ui-font](https://github.com/yuu1111/dsh-ui-font) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness Web GUI plugin: change the UI font family through theme token overrides |
| 156 | [zc679087/dsh-skill-preferences](https://github.com/zc679087/dsh-skill-preferences) | 0 | 2026-09-11 | 2026-09-11 | 一个可以管理DSH上安装的skill的插件，可以动态开关skill来防止误触发 |
| 157 | [zheng1/dsh-acp-replay](https://github.com/zheng1/dsh-acp-replay) | 0 | 2026-09-11 | 2026-09-11 | Community ACP bridge for DeepSeek Harness that answers session/load, so a client can rebuild a session transcript after its own restart |
| 158 | [zhengjy01/dsh-aliyun-mcp](https://github.com/zhengjy01/dsh-aliyun-mcp) | 0 | 2026-09-10 | 2026-09-11 | Alibaba Cloud OpenAPI MCP connection for DeepSeek Harness |
| 159 | [zhengjy01/dsh-backup-migrator](https://github.com/zhengjy01/dsh-backup-migrator) | 0 | 2026-09-10 | 2026-09-11 | Plugin environment backup and migration for DeepSeek Harness |
| 160 | [zhengjy01/dsh-feishu-mcp](https://github.com/zhengjy01/dsh-feishu-mcp) | 0 | 2026-09-10 | 2026-09-11 | Feishu (Lark) OpenAPI MCP connection for DeepSeek Harness |
| 161 | [zhengjy01/dsh-goofish-mcp](https://github.com/zhengjy01/dsh-goofish-mcp) | 0 | 2026-09-10 | 2026-09-11 | Xianyu (Goofish) read-only monitoring MCP for DeepSeek Harness |
| 162 | [zhengjy01/dsh-npm](https://github.com/zhengjy01/dsh-npm) | 0 | 2026-09-10 | 2026-09-11 | NPM registry management for DeepSeek Harness |
| 163 | [zhengjy01/dsh-skill-recommender](https://github.com/zhengjy01/dsh-skill-recommender) | 0 | 2026-09-10 | 2026-09-11 | Session-profile skill recommender for DeepSeek Harness |
| 164 | [zhengjy01/dsh-zsxq](https://github.com/zhengjy01/dsh-zsxq) | 0 | 2026-09-10 | 2026-09-11 | Knowledge Planet (zsxq) integration for DeepSeek Harness |
| 165 | [zhqowo/dsh-whale-tray](https://github.com/zhqowo/dsh-whale-tray) | 0 | 2026-08-28 | 2026-09-11 | 🐳 大肥鱼 — DeepSeek Harness (dsh) launcher: Windows system tray + macOS menu bar. Start/stop the dsh service, summon the Web UI, restart, top up — independent of the dsh process. 独立于 dsh 进程的一键开关。 |
| 166 | [zhylmzr/dsh-session-cost-cny](https://github.com/zhylmzr/dsh-session-cost-cny) | 0 | 2026-09-11 | 2026-09-11 | dsh deepseek 模型费用统计 |
| 167 | [ZiqiaoFang/dsh-liangwen-tide](https://github.com/ZiqiaoFang/dsh-liangwen-tide) | 0 | 2026-09-11 | 2026-09-11 | DeepSeek Harness 的峰谷指示器 + 当日已用金额：峰时「梁文峰」、谷时「梁文谷」，峰谷时段与价目表自动跟随官方定价页。A peak/off-peak tide + today-cost plugin for the DSH Web GUI. |
| 168 | [zkl22492-star/Toolfolk-for-DSH](https://github.com/zkl22492-star/Toolfolk-for-DSH) | 0 | 2026-09-11 | 2026-09-11 | 把 DSH 的插件与模型调用过程可视化成 3D 办公室 |
| 169 | [zzy6-a/vision-use](https://github.com/zzy6-a/vision-use) | 0 | 2026-09-11 | 2026-09-11 | DSH Computer Use：让 Agent 看见并操作 Windows 桌面（Windows 原生 / WSL 自动识别）；视觉通道 + 鼠标键盘 + Codex 风格蓝色覆盖层，Esc 随时中止。 |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- aa2246740/dsh-files-panel
- Arborsm/dsh-memory-plugin
- DaYanQLQ/DSH-Balance-Mini
- DecresLuna/DSH-Service
- douzhenyu/oh-my-deepseek
- EIGHTfs/dsh-git-rescue
- extracurricular-ai/dsh-filesnap
- FitBBC/dsh-plugin-tokensmarket
- huangyuheng/dsh-token-usage
- JackeyWilder/dsh-file-picker
- jarvan642/dsh-hotswap
- laodonge/col-dsh-plugin
- masquerator-coder/dsh-memory
- momo-gen/dsh-browser-pilot
- momo-gen/dsh-canvas
- ngk3pori/dsh-zh-cn-ui
- omdsh-dev/dsh-cron
- Pagemalthusian934/deepseek-desktop
- PerryLink/dsh-plugin-upgrade
- PerryLink/dsh-plugin-upgrade-rc1
- runfali/dsh-config-center
- runfali/dsh-export-kit
- runfali/dsh-paperclip
- Silktex/dsh-team
- william-jin-cmu/dsh-gal
- Zh1rV/dsh-web-search-tavily
