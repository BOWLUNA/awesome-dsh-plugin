# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-20**
- 快照日期 / Snapshot date: **2026-09-20 (UTC)**
- 待审核 / Pending: **138**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **11**
- Star 异常增长 / Star-growth alerts: **5** — 先看下方告警节 / see the alert section first

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

对比上一份快照 **2026-09-19** / vs previous snapshot **2026-09-19**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **5**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [omdsh-dev/dsh-browser](https://github.com/omdsh-dev/dsh-browser) | 待审 / pending | 704 | +10 | 51 | 44d | 待审高星 | 核准即 Top 16 |
| ⚠️ [ranxianglei/billion-context](https://github.com/ranxianglei/billion-context) | 待审 / pending | 213 | — | 27 | 44d | 待审高星 | 核准即榜 #51 |
| ⚠️ [dataelement/dsh-desktop](https://github.com/dataelement/dsh-desktop) | 已核准 / approved | 7993 | +336 | 338 | 37d | 日增百星 | 日增 +336★；已不进榜单 |
| ⚠️ [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill) | 已核准 / approved | 5994 | +310 | 428 | 89d | 日增百星 | 日增 +310★；已不进榜单 |
| ⚠️ [Clearailhc/clearai-dsh](https://github.com/Clearailhc/clearai-dsh) | 已核准 / approved | 245 | +106 | 11 | 7d | 日增百星 | 日增 +106★；已不进榜单 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [omdsh-dev/dsh-browser](https://github.com/omdsh-dev/dsh-browser) ⚠️ | 704 | 2026-08-06 | 2026-09-20 | Chrome sidebar extension that lets DeepSeek Harness operate your browser directly, no vision capabilities required. 一款 Chrome 侧边栏扩展程序，可让 DeepSeek Harness 直接操控您的浏览器，无需视觉能力。 |
| 2 | [ranxianglei/billion-context](https://github.com/ranxianglei/billion-context) ⚠️ | 213 | 2026-08-06 | 2026-09-20 | 基本稳定可用 100K tokens is enough. Universal context-compression proxy for ALL AI coding agents,10w上下文足矣 |
| 3 | [xuzhougeng/ScientificFigureLibrary](https://github.com/xuzhougeng/ScientificFigureLibrary) | 84 | 2026-07-29 | 2026-09-20 | Local-first MCP App for scientific figures. Import, review, and publish a global library on disk; reuse exact templates in Pi, DeepSeek Harness (dsh), Claude, Codex, Cursor, and Wisp. |
| 4 | [Devin-AXIS/jev-dsh-decision](https://github.com/Devin-AXIS/jev-dsh-decision) | 23 | 2026-09-20 | 2026-09-20 | Jev DSH 决策引擎｜面向 Agent Harness 的结构化决策插件。原生支持 DeepSeek Harness，通过 iPolloWork 支持 OpenCode、Codex Harness。 |
| 5 | [chenproton/dsh-history](https://github.com/chenproton/dsh-history) | 14 | 2026-08-17 | 2026-09-20 | Quickly view, search, and jump to all the messages you sent in a long conversation. |
| 6 | [Nwflower/dsh-claude-style](https://github.com/Nwflower/dsh-claude-style) | 9 | 2026-09-19 | 2026-09-20 | Claude Code Desktop theme for DeepSeek Harness｜ 为 DeepSeek Harness 网页 GUI 打造的 Claude Code 桌面主题 |
| 7 | [Mr-remon219/search-boost](https://github.com/Mr-remon219/search-boost) | 5 | 2026-08-17 | 2026-09-20 | Multi-engine web search and evidence synthesis for AI coding agents. Unified MCP server, Pi extension, and DeepSeek Harness bundle — free search, X/Twitter, parallel research, and TUI setup. |
| 8 | [LX2000WASD/dsh-plugin-manager-companion](https://github.com/LX2000WASD/dsh-plugin-manager-companion) | 4 | 2026-09-20 | 2026-09-20 | Companion to the official DSH plugin manager: pre-install quality gate, environment diagnostics, marketplace, and upgrades. |
| 9 | [Yuuyuko-uu/dsh-tts-bridge](https://github.com/Yuuyuko-uu/dsh-tts-bridge) | 4 | 2026-09-19 | 2026-09-20 | DSH 朗读桥：会话里的话自动交给 DeepSeek 网页端朗读，声音从你自己的电脑里出来 |
| 10 | [YuMS/dsh-duet](https://github.com/YuMS/dsh-duet) | 3 | 2026-09-18 | 2026-09-20 | 只用语音，就能操作 DSH |
| 11 | [gaoqiaoliangjie666/dsh-qwen-connect](https://github.com/gaoqiaoliangjie666/dsh-qwen-connect) | 2 | 2026-09-20 | 2026-09-20 | 将 QwenWork 桌面 App 包含的模型自动接入 DeepSeek Harness，零配置使用。Bring the models in the QwenWork desktop app into DeepSeek Harness with zero configuration. |
| 12 | [gluztm/DSHGuard](https://github.com/gluztm/DSHGuard) | 2 | 2026-09-20 | 2026-09-20 | DSH守护壳：DeepSeek Harness的一键救援式启动器：改动快找存档、问题整组回滚、本地管理插件、诊断日志导出 |
| 13 | [meimiaoji-creator/meow-dsh-workflow](https://github.com/meimiaoji-creator/meow-dsh-workflow) | 2 | 2026-09-14 | 2026-09-20 | meow-dsh-workflow 是一个双面（node + browser）DSH 插件：内置一套可编辑的 Agent 角色库（研发链路 / 头脑风暴 ），把角色定义编译成系统提示词与工具白名单。你可以在输入框右侧点「角色」按钮、或敲 /meow-workflow-<角色id> 斜杠命令按角色发起会话；主 agent 再通过 meow_agent_call 按同一套角色定义创建/续聊带 persona 与工具白名单的子 agent，形成多层语言链。配套角色记忆（跨会话）与公司台账簿（decisions/actions/need-boss 等六本账，按项目隔离）。 |
| 14 | [yangdcm/dsh-expert-team](https://github.com/yangdcm/dsh-expert-team) | 2 | 2026-09-14 | 2026-09-20 | Role-based multi-agent expert team for DeepSeek Harness: one sentence in, a staged and gated team delivery out. 12 role subagents, 9 gated phases, shared-workspace artifacts, zero runtime dependencies. |
| 15 | [alanzhao0128/dsh-memory-lite](https://github.com/alanzhao0128/dsh-memory-lite) | 1 | 2026-08-27 | 2026-09-20 | Lightweight zero-dependency long-term memory for DeepSeek Harness: Markdown memory store, L0 catalog injection, 5 model-facing tools, background extraction. \| dsh 轻量跨会话记忆插件 |
| 16 | [Bay-Zeddie/dsh-agent-instructions](https://github.com/Bay-Zeddie/dsh-agent-instructions) | 1 | 2026-09-20 | 2026-09-20 | 在 dsh Web 设置页里编辑原生 AGENTS.md 的面板：链上每层可点选编辑，三种生效范围，并可视化官方指令预算。 |
| 17 | [birew83538-oss/dsh-chat-thinking-editor](https://github.com/birew83538-oss/dsh-chat-thinking-editor) | 1 | 2026-09-20 | 2026-09-20 | DSH 插件：直接在 DeepSeek Harness 对话里编辑任意 AI 消息的正文与思维链（thinking）。保留 AI 的聪明，让 AI 完全符合你的心意。🐛 修复选中删除联动清空问题。\| DeepSeek Harness plugin to edit any assistant reply + reasoning/thinking chain. Make the AI output truly yours. |
| 18 | [Chance722/dsh-inbox](https://github.com/Chance722/dsh-inbox) | 1 | 2026-09-19 | 2026-09-20 | dsh 插件：把复制粘贴的链接、图片、文本、账密收进本地仓库，自动分类，能在对话里检索取回 |
| 19 | [chemmy-11/dsh-nautilus](https://github.com/chemmy-11/dsh-nautilus) | 1 | 2026-08-24 | 2026-09-20 | Vault observation plugin for DeepSeek Harness: Obsidian vault metadata snapshot + edit stats + observation panel |
| 20 | [cup113/personal-track](https://github.com/cup113/personal-track) | 1 | 2026-09-20 | 2026-09-20 | DeepSeek Harness（DSH）插件：右侧栏每日习惯看板 + 主区域统计页。 |
| 21 | [DDDMUC/dsh-delete-turn](https://github.com/DDDMUC/dsh-delete-turn) | 1 | 2026-09-20 | 2026-09-20 | Per-message delete for DeepSeek Harness: remove a user message, one reply step, or a whole assistant reply from the derived model context via the official surface-replace contract, and hide it from the visible transcript without rewriting the append-only log. |
| 22 | [dingchenhui0618-arch/dsh-taskwatch](https://github.com/dingchenhui0618-arch/dsh-taskwatch) | 1 | 2026-09-20 | 2026-09-20 | Read-only task monitor for DeepSeek Harness: sessions, background jobs, subagents, goals, workflows and pending approvals, as a phone-friendly page and a GUI sidebar panel. |
| 23 | [Fnckerpoi/dsh-plugin-sirchmunk](https://github.com/Fnckerpoi/dsh-plugin-sirchmunk) | 1 | 2026-09-19 | 2026-09-20 | DSH集成sirchmunk插件管理。 |
| 24 | [Furry-wucheng/dsh-story-mode](https://github.com/Furry-wucheng/dsh-story-mode) | 1 | 2026-09-11 | 2026-09-20 | 自己用来做小说的 |
| 25 | [goodddGrades/dsh-behuman](https://github.com/goodddGrades/dsh-behuman) | 1 | 2026-09-20 | 2026-09-20 | Long-term memory and self-evolving skills for the DeepSeek Harness · DeepSeek Harness 的长期记忆与自我演进能力 —— Plain Markdown on disk, no vector store |
| 26 | [hawkongz/dsh-chat-locator](https://github.com/hawkongz/dsh-chat-locator) | 1 | 2026-09-20 | 2026-09-20 | Turn-rail settings for DSH Web: tick thickness, rail side, a curved length gradient anchored on the hovered tick, and a plain-text hover preview with adjustable lines, font size, and width. |
| 27 | [heyadhithya/fullstack-expert](https://github.com/heyadhithya/fullstack-expert) | 1 | 2026-08-16 | 2026-09-20 | Cordis-native, evidence-driven full-stack engineering discipline for DeepSeek Harness agents |
| 28 | [huangfuren/dsh-outline](https://github.com/huangfuren/dsh-outline) | 1 | 2026-08-25 | 2026-09-20 | DSH web plugin: search, read and safely write an Outline knowledge base from conversations, with whitelist-guarded approval for every document write. |
| 29 | [ireza7/dsh-persian-rtl](https://github.com/ireza7/dsh-persian-rtl) | 1 | 2026-09-19 | 2026-09-20 | Persian (Farsi) RTL fix for DeepSeek Harness: automatic per-paragraph direction for assistant answers, thinking cells, tool cells and question boxes |
| 30 | [jacket-sikaha/dsh-market-gist-autosync](https://github.com/jacket-sikaha/dsh-market-gist-autosync) | 1 | 2026-09-18 | 2026-09-20 | dsh-market-gist-autosync |
| 31 | [localSummer/dsh-group-chat](https://github.com/localSummer/dsh-group-chat) | 1 | 2026-09-19 | 2026-09-20 | DSH 模型群聊：多模型角色群组对话面板。角色绑定不同 provider/model，群内共享对话记录；设置页支持启用/停用。 |
| 32 | [Matcha-Eason/dsh-answer-highlighter](https://github.com/Matcha-Eason/dsh-answer-highlighter) | 1 | 2026-09-18 | 2026-09-20 | Automatically highlights key points, definitions, warnings, and questions in DeepSeek Harness |
| 33 | [moxingovo/dsh-sidebar](https://github.com/moxingovo/dsh-sidebar) | 1 | 2026-08-14 | 2026-09-20 | Unofficial community extension. Claude Code-style native DeepSeek Harness sidebar for VS Code: self-written chat UI (no iframe) reusing the existing dsh web service — workspace-synced sessions, permission/model/reasoning pickers, context ring. / 非官方社区扩展:VS Code 里的 Claude Code 风格 DSH 原生侧边栏,自写聊天 UI,复用本机 dsh web 服务;工作区会话同步、沙箱权限/模型/推理档、上下文占用环。 |
| 34 | [NEVSTOP-LAB/dsh-import-copilot-files](https://github.com/NEVSTOP-LAB/dsh-import-copilot-files) | 1 | 2026-09-18 | 2026-09-20 | Load VSCode/Copilot AI configuration (.github/copilot-instructions.md, .github/instructions, .github/skills) into DeepSeek Harness sessions. |
| 35 | [pioneer666-user/dsh-archify-manage](https://github.com/pioneer666-user/dsh-archify-manage) | 1 | 2026-09-19 | 2026-09-20 | DSH（DeepSeek Harness）流程图管理插件：浏览 Archify 业务流程图目录、按 Git 附注标签阅读历史版本、保存版本。A workflow-diagram manager plugin for DSH. |
| 36 | [SCP-QQ/dsh-notice-center](https://github.com/SCP-QQ/dsh-notice-center) | 1 | 2026-09-13 | 2026-09-20 | Turn the tab icon into a green/amber status light and send browser notifications when a session finishes or awaits your input, with 47 selectable notification sounds.  |
| 37 | [stone100010/dsh-token-gauge](https://github.com/stone100010/dsh-token-gauge) | 1 | 2026-09-18 | 2026-09-20 | dsh-token-gauge |
| 38 | [ufiredong/dsh-interviewer](https://github.com/ufiredong/dsh-interviewer) | 1 | 2026-09-19 | 2026-09-20 | DSH 模拟面试面板 + 技能：真实模型当面试官，读简历层层追问、按证据打分并推导薪资区间。面试官是考官，不是助教。 |
| 39 | [7starsseeker/dsh-jev-guard](https://github.com/7starsseeker/dsh-jev-guard) | 0 | 2026-09-20 | 2026-09-20 | DeepSeek Harness (DSH) 执行前安全阀门:bash/pwsh 真正执行前先经静态规则 + TypeSafe Jev 语义判定,破坏性操作按 允许/修正/拦截/上报人工 四态处置,含额度降级与审计日志。 |
| 40 | [AMC-tp/dsh-work-buddy](https://github.com/AMC-tp/dsh-work-buddy) | 0 | 2026-09-20 | 2026-09-20 | Pixel desk buddy for the DSH Web GUI: slacks off when idle, thinks and types while a turn runs, throws confetti when it finishes, and tallies completed turns. |
| 41 | [AnonyJcy/dsh-j-space](https://github.com/AnonyJcy/dsh-j-space) | 0 | 2026-08-23 | 2026-09-20 | J-Space Cognition Suite SV1 原生 DeepSeek Harness 智能体预设与独立 Cordis 插件，提供深层推理路由、持久控制器（control.py）、工作区状态外化账本（.jspace）与全模型解耦的认知工作空间 |
| 42 | [Awoodwhale/dsh-agent-persona](https://github.com/Awoodwhale/dsh-agent-persona) | 0 | 2026-09-20 | 2026-09-20 | Workspace personas for DeepSeek Harness (DSH): many system-prompt personas, each scoped by workspace path or session id, managed from the Web settings page (Apache-2.0) |
| 43 | [Azurer0121/deepseek-harness-azurer](https://github.com/Azurer0121/deepseek-harness-azurer) | 0 | 2026-08-14 | 2026-09-20 | DeepSeek Harness: Everything is a Plugin. |
| 44 | [Azurer0121/dsh-ssh-plugin](https://github.com/Azurer0121/dsh-ssh-plugin) | 0 | 2026-08-14 | 2026-09-20 | DeepSeek Harness plugin: ssh_exec tool + persisted SSH connections bound to workspaces \| DSH 插件：远程命令执行与持久化 SSH 连接 |
| 45 | [bbaz123/dsh-confirmation-resolution](https://github.com/bbaz123/dsh-confirmation-resolution) | 0 | 2026-09-20 | 2026-09-20 | Post-task confirmation decision guard for DeepSeek Harness — balance output quality with real user impact. |
| 46 | [chen8923/dsh-task-progress](https://github.com/chen8923/dsh-task-progress) | 0 | 2026-09-20 | 2026-09-20 | Live progress for long-running DSH tasks: scripts report structured progress, the Web UI shows it in a floating overlay, a sidebar tab, and a settings page. |
| 47 | [CLOUDinDREAM/dsh-cj2099-plugin](https://github.com/CLOUDinDREAM/dsh-cj2099-plugin) | 0 | 2026-09-20 | 2026-09-20 | 2099年的她 |
| 48 | [ComeCaramelos/dsh-docker-desktop-mcp](https://github.com/ComeCaramelos/dsh-docker-desktop-mcp) | 0 | 2026-09-15 | 2026-09-20 | DSH plugin that connects the Docker Desktop MCP gateway as an MCP server. |
| 49 | [curtainsmall/dsh-reckoner](https://github.com/curtainsmall/dsh-reckoner) | 0 | 2026-09-20 | 2026-09-20 | Formula-driven calculation engine for the DeepSeek Harness. 面向 DeepSeek Harness 的公式计算引擎。 |
| 50 | [dashitongzhi/dsh-config-webdav-sync](https://github.com/dashitongzhi/dsh-config-webdav-sync) | 0 | 2026-09-20 | 2026-09-20 | DSH (DeepSeek Harness) plugin: bidirectional WebDAV sync for DSH configuration (providers, plugins, prompts, skills). Excludes sessions and credentials. Design inspired by farion1231/cc-switch sync protocol. |
| 51 | [DobroGnom/dsh-tab-title](https://github.com/DobroGnom/dsh-tab-title) | 0 | 2026-09-20 | 2026-09-20 | Keep the DeepSeek Harness browser tab title pinned and surface completion or attention alerts. |
| 52 | [donghangxunlang-cmd/dsh-attention-health](https://github.com/donghangxunlang-cmd/dsh-attention-health) | 0 | 2026-09-20 | 2026-09-20 | DSH（DeepSeek Harness）上下文健康监测 + 内容退化守卫 + 零模型交接文档 |
| 53 | [doremifaso12345/dsh-token-ledger](https://github.com/doremifaso12345/dsh-token-ledger) | 0 | 2026-09-20 | 2026-09-20 | a dsh plugin for token surveillance  |
| 54 | [DWJZ/dsh-mail-reader](https://github.com/DWJZ/dsh-mail-reader) | 0 | 2026-09-20 | 2026-09-20 | DeepSeek Harness 只读邮件插件：一个 email_read 工具读取 Gmail 与 Outlook，完全不实现发送、回复、删除、移动、标记或归档。 / Read-only mail for DSH: one email_read tool over Gmail and Outlook, with no send, reply, delete, move, mark, or archive capability. |
| 55 | [EditTogether/DSH-EditApart](https://github.com/EditTogether/DSH-EditApart) | 0 | 2026-09-17 | 2026-09-20 | A schema-driven, automation-first video + photo editor preset for DeepSeek Harness: deterministic render -> critique -> revise, with the edit decision as an auditable, trainable object. Part of the EditTogether collection. |
| 56 | [EdwardXiao-bit/dsh-run-button](https://github.com/EdwardXiao-bit/dsh-run-button) | 0 | 2026-09-20 | 2026-09-20 | Adds a Run button to shell code blocks in DSH replies, executing the command on the host and streaming its output to a dock or a bottom-panel tab. 给 DSH 回复里的命令行代码框加一个「运行」按钮：在宿主机上执行该命令，输出显示在右下角浮动面板或底部面板标签页。 |
| 57 | [Exynos671/dsh-windows-notify](https://github.com/Exynos671/dsh-windows-notify) | 0 | 2026-09-20 | 2026-09-20 | Windows toast notifications for DeepSeek Harness (dsh): permission requests, branch/option choices and turn completion, plus a Settings -> General switch panel. |
| 58 | [Fishquito7/dsh-gitbash](https://github.com/Fishquito7/dsh-gitbash) | 0 | 2026-09-20 | 2026-09-20 | Give DSH a real bash tool on Windows: call bash directly, with no pwsh escaping and no quoting hell. |
| 59 | [Fishsb/dsh-plugin-roundtable](https://github.com/Fishsb/dsh-plugin-roundtable) | 0 | 2026-09-19 | 2026-09-20 | 圆桌会议 RoundTable — DeepSeek Harness (DSH) 插件：把一次会话变成可视化、可辩论、可拍板的专家圆桌会议；含三种协作模式、调度面、红队评审与 28 席专家团 \| 需 DSH 0.1.5-rc.1+ · MIT License |
| 60 | [Gavin237/dsh-capability-hint](https://github.com/Gavin237/dsh-capability-hint) | 0 | 2026-09-20 | 2026-09-20 | DSH plugin: inject a one-line hint naming skills that match the current turn, so installed-but-forgotten methodology skills actually get used. Deterministic matching, no LLM calls, fail-open. |
| 61 | [GooDAnDReaDY/dsh-github-ops](https://github.com/GooDAnDReaDY/dsh-github-ops) | 0 | 2026-09-20 | 2026-09-20 | GitHub operations for DeepSeek Harness: releases, tags, a guarded API pass-through, sanitized mirror publication, workflow runs and repository settings. |
| 62 | [GooDAnDReaDY/dsh-plugin-notify](https://github.com/GooDAnDReaDY/dsh-plugin-notify) | 0 | 2026-09-18 | 2026-09-20 | DSH plugin: audio chimes, cross-session toasts, desktop push, and IM webhooks for turn completion, errors, and approvals. |
| 63 | [gorban/dsh-job-stop](https://github.com/gorban/dsh-job-stop) | 0 | 2026-09-20 | 2026-09-20 | DeepSeek Harness (dsh) plugin: stop a running background job from the session-header job list, behind a confirmation dialog. |
| 64 | [HandsYe/dsh-input-history](https://github.com/HandsYe/dsh-input-history) | 0 | 2026-09-20 | 2026-09-20 | 为 DSH 提供持久化输入历史，支持使用键盘上下方向键切换历史记录并恢复未发送草稿。Persistent input history for DSH with Arrow Up and Arrow Down navigation, draft recovery, deduplication, and local storage. |
| 65 | [harmless0819-dev/dsh-agent-chat](https://github.com/harmless0819-dev/dsh-agent-chat) | 0 | 2026-09-20 | 2026-09-20 | Turn-injection message channel between DSH agents on two machines: messages land in a log and are injected as context at the next agent step. |
| 66 | [harmless0819-dev/dsh-codex-micro](https://github.com/harmless0819-dev/dsh-codex-micro) | 0 | 2026-09-20 | 2026-09-20 | Turn a Vaydeer 9-key keypad into a DSH Codex Micro: the keypad sends unique combinations, the plugin maps them to DSH actions. |
| 67 | [harmless0819-dev/dsh-persona-anchor](https://github.com/harmless0819-dev/dsh-persona-anchor) | 0 | 2026-09-20 | 2026-09-20 | Pin the persona into a system-prompt section so it never competes for the AGENTS.md 65536-byte instruction budget. |
| 68 | [harmless0819-dev/dsh-power-controls](https://github.com/harmless0819-dev/dsh-power-controls) | 0 | 2026-09-20 | 2026-09-20 | Close / restart DSH buttons in Settings > General, plus an opt-out auto-close that waits until every browser page has stopped beaconing. |
| 69 | [harmless0819-dev/dsh-self-built-plugins](https://github.com/harmless0819-dev/dsh-self-built-plugins) | 0 | 2026-09-20 | 2026-09-20 | Index of self-built DSH plugins, grouped by purpose: appearance, control, collaboration. |
| 70 | [harmless0819-dev/dsh-whale-emote](https://github.com/harmless0819-dev/dsh-whale-emote) | 0 | 2026-09-20 | 2026-09-20 | Make the whale widget perform emotions: stickers pop out beside it, with sound and a speech bubble. Agent-triggered over local HTTP. |
| 71 | [harmless0819-dev/dsh-whale-live2d](https://github.com/harmless0819-dev/dsh-whale-live2d) | 0 | 2026-09-20 | 2026-09-20 | Replace the whale widget static image with a Live2D model, stacked at identical geometry. Degrades to the static widget without Cubism Core. |
| 72 | [HarveyZed/clawd-whale-girl](https://github.com/HarveyZed/clawd-whale-girl) | 0 | 2026-09-20 | 2026-09-20 | Clawd on Desk × DeepSeek Harness 增强桥接：上下文用量、审批、子代理、上下文压缩、余额告警，外加鲸鱼娘桌宠主题。Extended DSH bridge + whale-girl theme. |
| 73 | [hesixian/dsh-data-migration](https://github.com/hesixian/dsh-data-migration) | 0 | 2026-09-15 | 2026-09-20 | DSH 本地迁移插件：把 DSH 配置、插件清单、skills、presets、storages 与 .credentials.yaml 打包成密码保护的 .dsh-migrate 文件 |
| 74 | [HorusJiang/dsh-jev-tools](https://github.com/HorusJiang/dsh-jev-tools) | 0 | 2026-09-20 | 2026-09-20 | Jev judgment, not generation: prune long tool output, screen fetched pages for injected instructions, and gate completion claims inside DeepSeek Harness. |
| 75 | [huangfuren/dsh-conversation](https://github.com/huangfuren/dsh-conversation) | 0 | 2026-09-10 | 2026-09-20 | DSH web plugin: conversation outline panel - history questions (index + time) plus the assistant reply Markdown heading tree, with level slider, search, bookmarks, copy and click-to-jump. |
| 76 | [HyperForce/dsh-workspace-lock](https://github.com/HyperForce/dsh-workspace-lock) | 0 | 2026-09-20 | 2026-09-20 | Per-workspace password locks for the DeepSeek Harness (DSH) web UI: right-click to lock, lock screen, admin master password. UI-level lock. |
| 77 | [hzhgino/dsh-caonima](https://github.com/hzhgino/dsh-caonima) | 0 | 2026-09-20 | 2026-09-20 | 核动力草泥马 - DSH Web GUI desktop pet plugin for DeepSeek Harness |
| 78 | [jolaaa999/dsh-section-nav](https://github.com/jolaaa999/dsh-section-nav) | 0 | 2026-09-20 | 2026-09-20 | DSH plugin: section navigation rail and local chapter bookmarks for DeepSeek Harness chat answers |
| 79 | [JuntaoXiao/PDF-electronic-signature](https://github.com/JuntaoXiao/PDF-electronic-signature) | 0 | 2026-09-20 | 2026-09-20 | 生成签名图 + 盖章 + 可选数字证书签名 |
| 80 | [kaluosifa/dsh-plugin-skill2cn](https://github.com/kaluosifa/dsh-plugin-skill2cn) | 0 | 2026-09-17 | 2026-09-20 | Translate the English description of a skill into Chinese and restore the original in one click; a newly installed skill is surfaced right away. |
| 81 | [KKKKeybird/dsh-turn-rail-persistent](https://github.com/KKKKeybird/dsh-turn-rail-persistent) | 0 | 2026-09-20 | 2026-09-20 | DSH plugin: keep the built-in conversation turn rail visible at every transcript width (un-hides the host rail on narrow transcripts). |
| 82 | [kolawong/fast-compaction-dsh](https://github.com/kolawong/fast-compaction-dsh) | 0 | 2026-09-20 | 2026-09-20 | Verdict-based context compaction for DeepSeek Harness — replaces lossy LLM summaries with fast keep/truncate/drop decisions from jev-latest; everything kept stays verbatim. Port of tamaratran/fast-jev-compaction. |
| 83 | [konglong87/dsh-input-list](https://github.com/konglong87/dsh-input-list) | 0 | 2026-09-20 | 2026-09-20 | dsh 常用内容插件：保存、编辑提示词，点击回填输入框，不自动发送。 |
| 84 | [lanyunshijian/dsh-file-download](https://github.com/lanyunshijian/dsh-file-download) | 0 | 2026-09-20 | 2026-09-20 | 插件 |
| 85 | [libre-webui/dsh-native-provider](https://github.com/libre-webui/dsh-native-provider) | 0 | 2026-09-19 | 2026-09-20 | Use DeepSeek Harness providers in Libre WebUI over a private local connection. |
| 86 | [liuhao11223/dsh-oneclick-restart](https://github.com/liuhao11223/dsh-oneclick-restart) | 0 | 2026-09-20 | 2026-09-20 | dsh重启按钮插件 |
| 87 | [lldois/dsh-jev](https://github.com/lldois/dsh-jev) | 0 | 2026-09-19 | 2026-09-20 | TypeSafe Jev System One semantic tool routing and typed decisions for DeepSeek Harness (DSH) |
| 88 | [LonelyHerbivore/dsh-image-question](https://github.com/LonelyHerbivore/dsh-image-question) | 0 | 2026-09-20 | 2026-09-20 | DSH Web plugin: ask the user a question with an image, annotate in the browser, get back structured annotations in source-image pixel coordinates. |
| 89 | [Love-JourneY/dsh-search-plus](https://github.com/Love-JourneY/dsh-search-plus) | 0 | 2026-09-20 | 2026-09-20 | 中文友好的 DSH 会话全文搜索 + 精确跳转定位（CJK-friendly session full-text search with precise jump-to-hit for DeepSeek Harness） |
| 90 | [LoveIrishCoffee/dsh-effort-ultra](https://github.com/LoveIrishCoffee/dsh-effort-ultra) | 0 | 2026-09-20 | 2026-09-20 | DSH 原生推理强度控件：Codex 风格蓝紫滑条、连续拖动与六档 Step（Off/Low/Medium/High/Xhigh/Ultra），支持官方会话模型切换和档位菜单。 / Native reasoning control for DSH: a Codex-style blue-violet slider with continuous drag, six Step tiers (Off/Low/Medium/High/Xhigh/Ultra), official session model switching, and a direct tier menu. |
| 91 | [LoveIrishCoffee/dsh-effort-ultra-skin](https://github.com/LoveIrishCoffee/dsh-effort-ultra-skin) | 0 | 2026-09-20 | 2026-09-20 | DSH 推理档位皮肤：把推理等级控件重绘成蓝紫渐变、带星点与流光的档位条 / Blue-violet Ultra skin for the DeepSeek Harness reasoning-tier control |
| 92 | [loyalchiiina/dsh-archive-manager-pro](https://github.com/loyalchiiina/dsh-archive-manager-pro) | 0 | 2026-09-17 | 2026-09-20 | Enhanced DSH archive manager: favorites filter & prune, one-click delete unfavorited, pinning, time & turns sorting, idle-days one-click archive (progress & undo), fast bulk delete with progress & fallback, copy ID/path, reworked layout. Based on MichengAI v0.1.40 (Apache-2.0). 归档会话增强版：收藏/置顶/时间·轮次排序/闲置一键归档/快速批量删除/复制 ID·路径。 |
| 93 | [lucagiftzek/dsh-mail](https://github.com/lucagiftzek/dsh-mail) | 0 | 2026-09-19 | 2026-09-20 | DSH plugin for agent email tools: send, mass send (CSV-personalised), scheduled queue, inbox read, domains. Multi-provider: Lettermint, AgentMail, Resend, OVH SMTP, manual SMTP, local self-host. |
| 94 | [lukepoo101/dsh-trusted-proxy-auth](https://github.com/lukepoo101/dsh-trusted-proxy-auth) | 0 | 2026-09-20 | 2026-09-20 | DeepSeek Harness plugin that trusts authentication already performed by a reverse proxy (Traefik + Keycloak OIDC) while keeping native DSH browser authentication as a fallback. |
| 95 | [M-Abozaid/limonene-mcp](https://github.com/M-Abozaid/limonene-mcp) | 0 | 2026-09-17 | 2026-09-20 | Connect your Amazon seller account to ChatGPT, Claude and other AI assistants. Read-only MCP connector for sales, Buy Box, FBA inventory, alerts, revenue and fees. |
| 96 | [mengge237/dsh-model-priority](https://github.com/mengge237/dsh-model-priority) | 0 | 2026-09-20 | 2026-09-20 | DSH 插件：自定义模型/提供方顺序——侧边栏拖拽排序，宿主的模型列表按这份顺序返回；顺序写进 settings.yaml 前自动备份 |
| 97 | [Meteor-system/dsh-codegraph](https://github.com/Meteor-system/dsh-codegraph) | 0 | 2026-09-10 | 2026-09-20 | CodeGraph plugin for DeepSeek Harness: index a workspace into a relation graph and query reachability, callers, and impact. |
| 98 | [mpetruc/dsh-model-sync](https://github.com/mpetruc/dsh-model-sync) | 0 | 2026-09-20 | 2026-09-20 | Auto-populate and auto-update the list of llm-pi-ai providers' models. No more hand-typing and manually keeping up-to-date with your inference server. |
| 99 | [mrbeandev/dsh-reconnect](https://github.com/mrbeandev/dsh-reconnect) | 0 | 2026-09-20 | 2026-09-20 | English DeepSeek Harness retry plugin with exponential backoff and gateway recovery |
| 100 | [mrbeandev/dsh-short-tool-ids](https://github.com/mrbeandev/dsh-short-tool-ids) | 0 | 2026-09-20 | 2026-09-20 | DeepSeek Harness plugin that shortens tool-call IDs over 64 characters for OpenAI-compatible Chat Completions providers, with a per-provider toggle |
| 101 | [MYCF711/dsh-plugin-forge](https://github.com/MYCF711/dsh-plugin-forge) | 0 | 2026-09-20 | 2026-09-20 | dsh 插件锻造工坊：一支专家 Agent 团队，从零把 dsh 插件锻造到可发布版本 \| An expert agent team that forges DeepSeek Harness plugins from zero to release |
| 102 | [MYCF711/dsh-qoder-cli](https://github.com/MYCF711/dsh-qoder-cli) | 0 | 2026-09-20 | 2026-09-20 | Qoder models in DeepSeek Harness (DSH) — three-tier model catalog, credential failover, OpenAI-compatible shim, settings card |
| 103 | [MYCF711/dsh-websearch-direct](https://github.com/MYCF711/dsh-websearch-direct) | 0 | 2026-09-20 | 2026-09-20 | 免 API Key 的 dsh 联网搜索 / 网页抓取插件：引擎=逻辑源、入口=直连/镜像/加速路由自动回退，不消耗任何模型 token |
| 104 | [neuneed/dsh-shuorenhua](https://github.com/neuneed/dsh-shuorenhua) | 0 | 2026-09-18 | 2026-09-20 | dsh-shuorenhua |
| 105 | [olimc2016/dsh-token-meter-panel](https://github.com/olimc2016/dsh-token-meter-panel) | 0 | 2026-09-20 | 2026-09-20 | DSH（DeepSeek Harness）Token 用量与花费面板插件：今日消费、预算进度、成本构成、缓存命中省下的钱。社区插件，非官方。 |
| 106 | [PangXitong/dsh-restart-button](https://github.com/PangXitong/dsh-restart-button) | 0 | 2026-09-20 | 2026-09-20 | 在Deepseek Harness的设置中新增一个关闭/重启按钮 |
| 107 | [PawinAI/pawin-brain-deepseek-harness](https://github.com/PawinAI/pawin-brain-deepseek-harness) | 0 | 2026-08-13 | 2026-09-20 | A brain-inspired runtime for DeepSeek Harness agents — remember, self-correct, learn. v0.1 ships memory (injection, notes, recall), 100% covered. |
| 108 | [PerryLink/jevcore](https://github.com/PerryLink/jevcore) | 0 | 2026-09-20 | 2026-09-20 | TypeSafe Jev for DeepSeek Harness, the Model Context Protocol, and plain Node: typed judgments instead of prose, offline by default. |
| 109 | [Qulierm/orbital-agents](https://github.com/Qulierm/orbital-agents) | 0 | 2026-09-18 | 2026-09-19 | Paired Endeavour and Challenger agents for DeepSeek Harness. |
| 110 | [Rice00/dsh-job-progress](https://github.com/Rice00/dsh-job-progress) | 0 | 2026-09-20 | 2026-09-20 | Live progress for long-running background jobs in DeepSeek Harness — a draggable floating ball with a per-session task panel showing done/total, speed and ETA. |
| 111 | [RrcoVer0/dsh-webnovel-writer](https://github.com/RrcoVer0/dsh-webnovel-writer) | 0 | 2026-09-20 | 2026-09-20 | Chinese web-fiction workflow skills for DeepSeek Harness: planning, file-backed memory, consistency review, rollback, and style profiling. |
| 112 | [Ryuu-64/dsh-find-all](https://github.com/Ryuu-64/dsh-find-all) | 0 | 2026-09-20 | 2026-09-20 | DSH web plugin: a Cmd/Ctrl+F find bar for the DeepSeek Harness desktop shell that searches the WHOLE conversation, not just the rendered tail. |
| 113 | [Ryuu-64/dsh-session-tools](https://github.com/Ryuu-64/dsh-session-tools) | 0 | 2026-09-20 | 2026-09-20 | Let the agent start a new session, or send a message to another one. |
| 114 | [shenA2024/whale-persona-presets](https://github.com/shenA2024/whale-persona-presets) | 0 | 2026-09-20 | 2026-09-20 | whale-persona 的人设内容包：现成的预设 JSON（一句立场 + 逐条可勾选的工作契约）。引擎在本体仓，出厂空白。 |
| 115 | [SoyBeanMilkx/CompFlow](https://github.com/SoyBeanMilkx/CompFlow) | 0 | 2026-09-20 | 2026-09-20 | Organize DSH sessions into nested, collapsible compositions. |
| 116 | [SPX43JL/dsh-safekeep](https://github.com/SPX43JL/dsh-safekeep) | 0 | 2026-09-20 | 2026-09-20 | Unofficial Windows file-recovery guard for unattended DeepSeek Harness workflows |
| 117 | [stormbuf/dsh-tavily-pool](https://github.com/stormbuf/dsh-tavily-pool) | 0 | 2026-09-18 | 2026-09-20 | Tavily-backed web search for DeepSeek Harness: multi-key pool with balance-aware rotation, automatic failover, and usage stats — switchable from the DSH settings panel. |
| 118 | [SunlitCrack/dsh-skills-mcp-manager](https://github.com/SunlitCrack/dsh-skills-mcp-manager) | 0 | 2026-09-20 | 2026-09-20 | DSH 插件：设置页统一管理技能 / MCP 服务器 / 指令文件（AGENTS.md 家族） |
| 119 | [Towzai/dsh-memory-jev](https://github.com/Towzai/dsh-memory-jev) | 0 | 2026-09-20 | 2026-09-20 | Memory plugin for DeepSeek Harness: every memory read/write is a typed judgement by TypeSafe Jev (choice/noul). |
| 120 | [Voellin/dsh-deephub-share](https://github.com/Voellin/dsh-deephub-share) | 0 | 2026-09-20 | 2026-09-20 | DeepHub 的开放部分：零知识云端协议客户端，以及基于它的 DeepSeek Harness 插件 |
| 121 | [wjackiedev/dsh-session-manager](https://github.com/wjackiedev/dsh-session-manager) | 0 | 2026-09-20 | 2026-09-20 | Archived-session manager for the DeepSeek Harness Web GUI — restore and permanently delete session logs. |
| 122 | [x102201/dsh-helper-plugin-command-ask](https://github.com/x102201/dsh-helper-plugin-command-ask) | 0 | 2026-09-20 | 2026-09-20 | dsh-helper plugin: a Cursor-style /ask mode for DeepSeek Harness — /ask <question> answers read-only for one turn (cited, no edits, enforced by a tool guard), then the next message is ordinary work again. ｜ 中文：dsh-helper 插件——为 DeepSeek Harness 提供 /ask 只读问答模式，一轮即释放，内置工具守卫强制只读。 |
| 123 | [x102201/dsh-helper-plugin-notify-away](https://github.com/x102201/dsh-helper-plugin-notify-away) | 0 | 2026-09-20 | 2026-09-20 | dsh-helper plugin: Cursor-style system notifications for DeepSeek Harness — silent while you watch the finishing session, toast when you have switched away. ｜ 中文：dsh-helper 插件——为 DeepSeek Harness 提供离开才通知的系统提醒，正在看这场会话时保持安静。 |
| 124 | [xbzbing/dsh-hub-desktop](https://github.com/xbzbing/dsh-hub-desktop) | 0 | 2026-09-16 | 2026-09-20 | DSH 多实例管理工具 |
| 125 | [xbzbing/dsh-openviking-manager](https://github.com/xbzbing/dsh-openviking-manager) | 0 | 2026-09-20 | 2026-09-20 | OpenViking 的配置工具 |
| 126 | [xiazhi88/dsh-onecompany](https://github.com/xiazhi88/dsh-onecompany) | 0 | 2026-09-19 | 2026-09-20 | 一人公司 · DeepSeek Harness 多 agent 公司编排插件（CEO/项目群/大厅/@派活/审批/排班/工作日志） |
| 127 | [yangdongzhen590/dsh-knj-version-control](https://github.com/yangdongzhen590/dsh-knj-version-control) | 0 | 2026-09-19 | 2026-09-20 | KNJ version-control workbench for DSH: local changes, per-file and multi-file staging, confirmed commit/update/push, and readable Git failure output. |
| 128 | [YEJASONJIEXIN/dsh-whale-girl-pet](https://github.com/YEJASONJIEXIN/dsh-whale-girl-pet) | 0 | 2026-09-20 | 2026-09-20 | 🐋 DSH 桌宠（胡桃语音 fork）：大小可调 + 16 角色语音播报 + 天气/余额宿主直连。基于 yanzwzz/dsh-whale-girl-pet 0.3.2。 |
| 129 | [yueyexiayu/dsh-zhanshi](https://github.com/yueyexiayu/dsh-zhanshi) | 0 | 2026-09-20 | 2026-09-20 | DSH desktop plugin: show this-turn images and videos inline in the conversation |
| 130 | [yunxiyang/dsh-stepwise-distill](https://github.com/yunxiyang/dsh-stepwise-distill) | 0 | 2026-09-20 | 2026-09-20 | Solidify DSH session history step by step: rewrite tool results in place to the facts the model actually kept, so long conversations stop re-sending noise every turn. Costs tokens and time: a ~770-character contract in every request, plus one extra full-context request and round-trip per step when stepSummary is on. |
| 131 | [YUYUY9527/dsh-plugin-management](https://github.com/YUYUY9527/dsh-plugin-management) | 0 | 2026-09-20 | 2026-09-20 | 外部插件管理器 for DeepSeek Harness (dsh): inventory + one-click update for a profile's third-party plugin packages. Settings -> Plugins UI + agent-facing tool. |
| 132 | [yuyuyyyyyyyyyyyy/dsh-project-memory](https://github.com/yuyuyyyyyyyyyyyy/dsh-project-memory) | 0 | 2026-09-20 | 2026-09-20 | Cross-session engineering memory for coding agents on DeepSeek Harness: durable per-project records of root causes, failed attempts and constraints, recalled into the prompt before the agent plans. |
| 133 | [yzsnstotz/hanamesh-core](https://github.com/yzsnstotz/hanamesh-core) | 0 | 2026-09-13 | 2026-09-20 | HanaMesh MOD-02 identity client plugin (plugin-identity) |
| 134 | [yzsnstotz/hanamesh-plugin-app-host](https://github.com/yzsnstotz/hanamesh-plugin-app-host) | 0 | 2026-09-12 | 2026-09-20 | HanaMesh MOD-04 application host DSH plugin (app-host) |
| 135 | [yzsnstotz/hanamesh-usage](https://github.com/yzsnstotz/hanamesh-usage) | 0 | 2026-09-13 | 2026-09-20 | HanaMesh MOD-11 activity plugin (activity) |
| 136 | [zhang-guo-wen/dsh-mcp-manager](https://github.com/zhang-guo-wen/dsh-mcp-manager) | 0 | 2026-09-18 | 2026-09-20 | MCP server management for DeepSeek Harness: author composition rows, choose when an allowed server loads, and filter which of its tools a session may call |
| 137 | [zhangyy0423/veripipe](https://github.com/zhangyy0423/veripipe) | 0 | 2026-09-20 | 2026-09-20 | An anti-false-positive verification pipeline for AI agents that test web/HTTP products. |
| 138 | [zhuchuovo/dsh-swarm-orchestrator](https://github.com/zhuchuovo/dsh-swarm-orchestrator) | 0 | 2026-09-19 | 2026-09-20 | DSH 插件：并行子代理集群 —— 母代理把目标拆成切片，并发驱动多个独立子代理写代码，输入框上方实时显示每个子代理此刻在做什么，并发数与各切片模型可在设置页配置。 |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- 384961890-ui/pawin-brain-deepseek-harness
- adithya-hmt/fullstack-expert
- AnonyJcy/dsh-plugin-j-space
- chemmy-11/dsh-nexus
- huangfuren/dsh-outline-auto
- loyalchiiina/dsh-archive-manager-favorites-patch
- Lum1104/dsh-browser
- NEVSTOP-LAB/dsh-import-vscode-ai-files
- orriduck/dsh-tui
- startnewlabs/dsh-history
- YerenChina/dsh-memory-webdav-sync
