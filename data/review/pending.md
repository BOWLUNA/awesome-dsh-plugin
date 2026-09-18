# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-18**
- 快照日期 / Snapshot date: **2026-09-18 (UTC)**
- 待审核 / Pending: **132**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **13**
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

对比上一份快照 **2026-09-17** / vs previous snapshot **2026-09-17**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **1**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill) | 已核准 / approved | 5126 | +1135 | 357 | 87d | 日增百星 | 日增 +1135★；已不进榜单 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [VDERR/echocat-skill-panel-3.0](https://github.com/VDERR/echocat-skill-panel-3.0) | 79 | 2026-09-18 | 2026-09-18 | DSH 技能调用审计 + 应用内 skill 管理器 |
| 2 | [bihangchi9-creator/lark-agent-bridge](https://github.com/bihangchi9-creator/lark-agent-bridge) | 33 | 2026-08-19 | 2026-09-18 | A native DeepSeek Harness (dsh) plugin bridging dsh coding agents to Feishu/Lark group chats — one group, one project directory. |
| 3 | [Nicholas023/vision-exp-tile](https://github.com/Nicholas023/vision-exp-tile) | 12 | 2026-08-22 | 2026-09-18 | DSH 插件：大图切 800×800 无损小块 + 坐标标注 + 分块聚合逻辑，直连 deepseek-v4-flash-vision-exp 识别；仅用纯官方 DSH 功能，零依赖第三方插件，不统计 token/费用。 |
| 4 | [WangPaoPaoLab/dsh-font](https://github.com/WangPaoPaoLab/dsh-font) | 12 | 2026-08-14 | 2026-09-18 | Font switcher for DeepSeek Harness Web GUI: 99 UI fonts + 31 code fonts with CJK-Latin pairing, instant apply, localStorage persistence |
| 5 | [cyanseek/dsh-landscape](https://github.com/cyanseek/dsh-landscape) | 6 | 2026-08-13 | 2026-09-18 | Agent-first DeepSeek Harness plugin intelligence: verify existing plugins, identify missing capabilities, and generate build-ready briefs. |
| 6 | [cyanseek/dsh-native-playbook](https://github.com/cyanseek/dsh-native-playbook) | 4 | 2026-08-13 | 2026-09-18 | Task-aware native capability manager for DeepSeek Harness — use, prepare, and verify built-in DSH tools before adding another plugin. |
| 7 | [cyanseek/dsh-tool-chaos](https://github.com/cyanseek/dsh-tool-chaos) | 4 | 2026-08-13 | 2026-09-18 | Deterministic fault injection and autonomous resilience tests for DeepSeek Harness tools |
| 8 | [Fakek0f3sT/dsh-mcp-diff](https://github.com/Fakek0f3sT/dsh-mcp-diff) | 4 | 2026-08-27 | 2026-09-18 | Uniform diff cards for every file mutation in DeepSeek Harness Web — MCP filesystem (edit_file/write_file) and built-in edit/write, collapsed by default, with per-line highlighting |
| 9 | [KratosLee-6/Html-ninefox](https://github.com/KratosLee-6/Html-ninefox) | 3 | 2026-08-29 | 2026-09-18 | html九尾狐，用来制作html的工作台，让你那些散落的html能放到一起，再打散重组，一切如新 |
| 10 | [whyself/Amadeus](https://github.com/whyself/Amadeus) | 2 | 2026-09-17 | 2026-09-18 | Amadeus: a web workspace for DSH with cloud and web agents, online code editing, PDF/Office/Markdown/LaTeX previews, TeX compilation, file management, and an integrated terminal. |
| 11 | [afterrealism/dsh-conn-dot](https://github.com/afterrealism/dsh-conn-dot) | 1 | 2026-09-18 | 2026-09-18 | DSH plugin: green/red connection dot beside the sidebar brand showing WebSocket + liveness-probe health of dsh web |
| 12 | [afterrealism/dsh-session-ctxmenu](https://github.com/afterrealism/dsh-session-ctxmenu) | 1 | 2026-09-18 | 2026-09-18 | DSH plugin: right-click a session/project row in the sidebar to open its Rename/Fork/Archive menu |
| 13 | [aidulibrary/skillmesh-index](https://github.com/aidulibrary/skillmesh-index) | 1 | 2026-08-25 | 2026-09-18 | SkillMesh / 插台 — 能力通约网络的开放索引层。CCP协议的开源实现，零服务器成本，个人维护，全球双语。 SkillMesh / Cha-Tai — Open index layer for capability commensurability network. CCP protocol implementation, zero server cost, bilingual, globally open. |
| 14 | [camplus360/agent-memory-bridge](https://github.com/camplus360/agent-memory-bridge) | 1 | 2026-09-17 | 2026-09-18 | One bridge. Every AI coding agent. One shared searchable memory. Cross-session, cross-engine memory for pi-coding-agent, DeepSeek Harness and OpenCode, powered by claude-mem. Capture tool/conversation observations to a local worker and inject relevant past context automatically. |
| 15 | [cking000bigdemon/dsh-acp-interactive](https://github.com/cking000bigdemon/dsh-acp-interactive) | 1 | 2026-08-25 | 2026-09-18 | 面向 Zed 等编辑器的 DeepSeek Harness 交互式 ACP 插件。 |
| 16 | [cn-scuo-oo/dsh-session-auto-title](https://github.com/cn-scuo-oo/dsh-session-auto-title) | 1 | 2026-09-18 | 2026-09-18 | DSH plugin: re-title a session after every turn in the MMDD｜类型｜主题 convention |
| 17 | [DBinK/youarehere](https://github.com/DBinK/youarehere) | 1 | 2026-09-18 | 2026-09-18 | Send Your IDE Selection to Any Agent. |
| 18 | [DDDMUC/dsh-delete-session](https://github.com/DDDMUC/dsh-delete-session) | 1 | 2026-09-13 | 2026-09-18 | Delete sessions from the DSH Web sidebar: a Delete action in the session menu with a risk-consent dialog; removes the log, workspace accounting and live session state. |
| 19 | [Eyeing0721/dsh-cot-en2cn](https://github.com/Eyeing0721/dsh-cot-en2cn) | 1 | 2026-09-18 | 2026-09-18 | DSH Web 插件：展开英文思考块即时呈现中文译文，不改动任何会话原文。 |
| 20 | [frederico-kluser/dsh-goal-pause-guard](https://github.com/frederico-kluser/dsh-goal-pause-guard) | 1 | 2026-09-18 | 2026-09-18 | Plugin do DeepSeek Harness (DSH): modal de confirmação antes de pausar uma atividade rodando — pausar interrompe a rodada atual e as subtarefas na hora. |
| 21 | [frederico-kluser/dsh-worktree-jump](https://github.com/frederico-kluser/dsh-worktree-jump) | 1 | 2026-09-18 | 2026-09-18 | DeepSeek Harness plugin: a web-UI button that creates a git worktree and moves the conversation into it (session fork with the worktree as cwd) |
| 22 | [hoyyang/dsh-glm-mode](https://github.com/hoyyang/dsh-glm-mode) | 1 | 2026-09-18 | 2026-09-18 | GLM Mode: fully tuned coding agent preset for zhipuai/glm-5.3-flash in DeepSeek Harness — PTC presentation, guard family, isolated compaction |
| 23 | [huangziyuan-general/dsh-novel-forge](https://github.com/huangziyuan-general/dsh-novel-forge) | 1 | 2026-09-11 | 2026-09-18 | DSH 小说锻炉：把 AI 长篇写作通病变成代码强制的硬约束（事实账本/上下文包/阶段门禁/零费用去AI味扫描/确定性审计/提案制修订）。Novel-writing guardrails plugin for DeepSeek Harness (DSH). |
| 24 | [KylinQ01/dsh-startup-animation](https://github.com/KylinQ01/dsh-startup-animation) | 1 | 2026-09-18 | 2026-09-18 | 🌸 给 DeepSeek Harness 的开机动画 + 主界面壁纸：多层动效 + 鼠标视差，两张图可在设置里自由更换并实时预览 |
| 25 | [lanqi677/dsh-learning-mode](https://github.com/lanqi677/dsh-learning-mode) | 1 | 2026-09-18 | 2026-09-18 | AI 维护的、可无限下钻的学习树 + 自动摘要 + 复习视图（DSH / DeepSeek Harness 插件）｜ An AI-maintained learning tree for DSH: auto summaries, review view, never lose your place while studying. |
| 26 | [lemonxiny55/dsh-composition-doctor](https://github.com/lemonxiny55/dsh-composition-doctor) | 1 | 2026-09-16 | 2026-09-18 | Read-only DSH and Cordis composition diagnostics, snapshots, diffs, and upgrade preflight. |
| 27 | [leolee9086/dsh-tool-cordis-local](https://github.com/leolee9086/dsh-tool-cordis-local) | 1 | 2026-09-18 | 2026-09-18 | DeepSeek Harness 独立创造模式工具集：不注册进程级 inspect provider，让创造模式预设可以被复制 |
| 28 | [mario841859784/dsh-expert-orchestrator](https://github.com/mario841859784/dsh-expert-orchestrator) | 1 | 2026-09-11 | 2026-09-18 | DSH 专家编排模式 agent preset — PM-first planning, Agency expert delegation, gated delivery, experience pooling |
| 29 | [mingger77/project-learning-helper](https://github.com/mingger77/project-learning-helper) | 1 | 2026-09-06 | 2026-09-18 | 一个助力包括我在内的萌新进行项目式学习的dsh preset |
| 30 | [RealAlexandreAI/dsh-dejavu-memory](https://github.com/RealAlexandreAI/dsh-dejavu-memory) | 1 | 2026-08-13 | 2026-09-18 | dsh memory: Nocturne Memory client for DeepSeek Harness |
| 31 | [rebornace/dsh-tracescope](https://github.com/rebornace/dsh-tracescope) | 1 | 2026-09-17 | 2026-09-18 | 基于 Git 代码差异智能缩减手工测试范围，支持 Web / 移动端操作录制与崩溃日志采集，依托 DSH AI 自动生成可复现缺陷流程，实现变更驱动的手工测试闭环提效插件。A DSH native test assistant plugin. It intelligently narrows manual test scope via Git diff, records web & mobile operation tracks and crash logs, and generates reproducible bug steps through AI analysis to close manual testing workflow efficiently. |
| 32 | [seolhw/dsh-guild](https://github.com/seolhw/dsh-guild) | 1 | 2026-09-05 | 2026-09-18 | 把「社区」装进 DSH：一个类 Discord 的社区插件 —— 在 DeepSeek Harness 面板内实时聊天、@ 提醒、贴图传文件、管理成员与权限。 |
| 33 | [tianyaojiudi-prog/dsh-djy-xttsc](https://github.com/tianyaojiudi-prog/dsh-djy-xttsc) | 1 | 2026-09-18 | 2026-09-18 | DSH(DeepSeek Harness) 插件：把一段可在设置页随时改写的文字，作为全局系统提示词段注入到所有会话，含子代理与工作流内部子代理；文本与开关即时生效，无需重启。 |
| 34 | [tommyhedgerow/Mimir](https://github.com/tommyhedgerow/Mimir) | 1 | 2026-09-17 | 2026-09-18 | An Obsidian learning vault that teaches: a DeepSeek Harness agent preset, a vault, a theme and three plugins. English and 简体中文. |
| 35 | [WanchunLian/dsh-draft-polish](https://github.com/WanchunLian/dsh-draft-polish) | 1 | 2026-09-16 | 2026-09-18 | DSH（DeepSeek Harness）Web 插件：一键把口语化草稿润色成专业表达，AI 只帮你把话说到位，绝不替你发言（纯客户端 · 快路径出核心意思） |
| 36 | [wmw343/dsh-resume-expert](https://github.com/wmw343/dsh-resume-expert) | 1 | 2026-09-18 | 2026-09-18 | 引导式简历生成插件：对话式四阶段 + A4 PDF 直出，双宿主验证 |
| 37 | [YJLTF/dsh-vision-tool](https://github.com/YJLTF/dsh-vision-tool) | 1 | 2026-09-17 | 2026-09-18 | 一个 DeepSeek Harness 插件：为纯文本主模型补上识图能力。它把图片理解委托给你配置的一个小参数多模态模型，再把结果以文本形式交还给主模型；当活跃模型自身支持图片输入时，插件完全退避，原生多模态体验不受任何影响。 |
| 38 | [yueyexiayu/dsh-OAuth](https://github.com/yueyexiayu/dsh-OAuth) | 1 | 2026-09-16 | 2026-09-18 | DSH desktop plugin: log in to Grok and ChatGPT Codex with official OAuth |
| 39 | [yukitakasama/dsh-context-lens](https://github.com/yukitakasama/dsh-context-lens) | 1 | 2026-09-18 | 2026-09-18 | Single-session context anatomy for the DSH Web GUI: attribution, headroom planning, and a context x trajectory timeline — not another usage ledger. |
| 40 | [zemanzhang809/dsh-stt-plugin](https://github.com/zemanzhang809/dsh-stt-plugin) | 1 | 2026-09-17 | 2026-09-18 | A speech-to-text (voice input) plugin for DeepSeek Harness.  |
| 41 | [01men/CDPP](https://github.com/01men/CDPP) | 0 | 2026-09-17 | 2026-09-18 | 跨境单据处理中台 |
| 42 | [2507483326/dsh-eteams](https://github.com/2507483326/dsh-eteams) | 0 | 2026-09-16 | 2026-09-18 | 一个增强deepseek harness 的 多成员协作插件 |
| 43 | [a981008/dsh-switch](https://github.com/a981008/dsh-switch) | 0 | 2026-09-17 | 2026-09-18 | CC Switch bridge for DeepSeek Harness: mirrors cc-switch providers and models into DSH, and shows each provider quota or balance. |
| 44 | [Alyosha28/dsh-plugin-c2c](https://github.com/Alyosha28/dsh-plugin-c2c) | 0 | 2026-09-18 | 2026-09-18 | Cache-to-Cache (C2C) for DeepSeek Harness: two local LLMs that share a KV-cache instead of exchanging text, exposed as c2c_* agent tools |
| 45 | [anthonyyu-verkada/dsh-mcp-client-plus](https://github.com/anthonyyu-verkada/dsh-mcp-client-plus) | 0 | 2026-09-18 | 2026-09-18 | DeepSeek Harness MCP client bridge with OAuth 2.1, bounded connect/discovery timeouts, environment-indirected secrets, optional indefinite reconnection, and a mcp_status diagnostic tool |
| 46 | [Arcadia822/dsh-tmp-hook](https://github.com/Arcadia822/dsh-tmp-hook) | 0 | 2026-09-18 | 2026-09-18 | One-time ephemeral webhook plugin for DeepSeek Harness (dsh) sessions: mint a single-use callback URL, then wake the requesting agent session with the delivered payload. |
| 47 | [AristotleAsborg/repo-autopilot-plugin](https://github.com/AristotleAsborg/repo-autopilot-plugin) | 0 | 2026-09-18 | 2026-09-18 | 把 repo-autopilot 的只读检查注册成 DeepSeek Harness 工具｜doctor / drill / acceptance / compare｜只读、零凭证、零写入 |
| 48 | [asxiuxiu/dsh-quick-open](https://github.com/asxiuxiu/dsh-quick-open) | 0 | 2026-09-17 | 2026-09-18 | DSH Web GUI plugin: VSCode-style Ctrl+P quick open — indexed workspace file search, sidebar editor open, conversation reference insert |
| 49 | [athif23/dsh-shell-select](https://github.com/athif23/dsh-shell-select) | 0 | 2026-09-18 | 2026-09-18 | DeepSeek Harness plugin: one model-facing shell tool whose shell (PowerShell, cmd, Git Bash, WSL, bash, zsh, fish, sh) is a user setting, with a Web settings card and a fail-closed refusal when the sandbox cannot confine it. |
| 50 | [cccc12138/dsh-read-aloud](https://github.com/cccc12138/dsh-read-aloud) | 0 | 2026-09-18 | 2026-09-18 | A speaker button beside the Like button: read any DeepSeek Harness reply aloud with the browser's own speech engine. · 在点赞旁加一个小喇叭，朗读 DSH 的回复。 |
| 51 | [chaserchan/dsh-browser-harness](https://github.com/chaserchan/dsh-browser-harness) | 0 | 2026-09-18 | 2026-09-18 | DSH plugin: drive a real Chrome from your dsh agent via the browser-use Browser Harness (local, no API key). |
| 52 | [cking000bigdemon/dsh-toolbelt](https://github.com/cking000bigdemon/dsh-toolbelt) | 0 | 2026-08-13 | 2026-09-18 | Eight DeepSeek Harness plugins: persona, language guard, per-request vision fallback, python/windows write guards, cross-agent memory, image generation, and skill shell injection. |
| 53 | [dingchenhui0618-arch/dsh-imagegen-skill](https://github.com/dingchenhui0618-arch/dsh-imagegen-skill) | 0 | 2026-09-18 | 2026-09-18 | Bundled imagegen skill for DeepSeek Harness: generate or edit raster images from the agent through any OpenAI-compatible GPT Image endpoint. |
| 54 | [DWJZ/dsh-allow](https://github.com/DWJZ/dsh-allow) | 0 | 2026-09-18 | 2026-09-18 | DeepSeek Harness 权限记忆插件：把某类命令加进允许列表，之后同类命令不再询问。 / Remember sandbox-escalation approvals so the same command prefix stops asking. |
| 55 | [DWJZ/dsh-balance](https://github.com/DWJZ/dsh-balance) | 0 | 2026-09-18 | 2026-09-18 | DeepSeek Harness 余额查询插件：用 /balance 命令在会话里查看 DeepSeek 账户余额。 / DeepSeek account balance as the /balance command. |
| 56 | [dytom18/dsh-plugin-voice-dictation](https://github.com/dytom18/dsh-plugin-voice-dictation) | 0 | 2026-09-18 | 2026-09-18 | 说话即任务：给 DSH Web GUI 加语音听写，说完自动发送给 Agent（纯前端，无需 API Key） |
| 57 | [EiffelBS/dsh-plugin-model-filter](https://github.com/EiffelBS/dsh-plugin-model-filter) | 0 | 2026-09-13 | 2026-09-18 | A DSH plugin that adds a search / filter box to the model selection menu in the DSH chat composer. |
| 58 | [elmersky/dsh-plugin-trellis-workflow](https://github.com/elmersky/dsh-plugin-trellis-workflow) | 0 | 2026-09-18 | 2026-09-18 | Trellis workflow enforcement for the DeepSeek Harness: per-turn workflow state injection and a trellis-start entry gate, replacing the session-start and user-prompt hooks dsh does not ship. |
| 59 | [Farewish/dsh-viewtune](https://github.com/Farewish/dsh-viewtune) | 0 | 2026-09-16 | 2026-09-18 | DeepSeek Harness 的阅读页签插件：一轮对话进行时能看到思考、工具与进度，结束后自动折叠过程、只留最终回答。 |
| 60 | [FridayKoi/dsh-lessons-md](https://github.com/FridayKoi/dsh-lessons-md) | 0 | 2026-09-18 | 2026-09-18 | Your AI agent keeps repeating the same mistakes? Give it a LESSONS.md notebook — it records its own failures into rules, auto-escalates repeat offenders, and you watch it all live in the DSH Web UI. 零 Key，让 DSH 的 AI 自己记错题、面板一眼看清。 |
| 61 | [fu827707013/dsh-model-health-probe](https://github.com/fu827707013/dsh-model-health-probe) | 0 | 2026-09-18 | 2026-09-18 | DSH 模型健康检查：会话视图页签，选定供应商/协议/模型/路由后手动发真实裸 HTTP 请求，一屏看耗时、TTFT、状态、token 与三层诊断链。 |
| 62 | [GeoSyntax/dsh-plugin-time-machine](https://github.com/GeoSyntax/dsh-plugin-time-machine) | 0 | 2026-09-18 | 2026-09-18 | Community DSH plugin for coordinated session/workspace checkpoints, safe rewind, DAG forks, and failure reflection. |
| 63 | [GooDAnDReaDY/dsh-session-search](https://github.com/GooDAnDReaDY/dsh-session-search) | 0 | 2026-09-17 | 2026-09-18 | DeepSeek Harness agent tool (session_search) for full-text search across historical sessions |
| 64 | [HaydenSmith1121/dsh-ark-plans](https://github.com/HaydenSmith1121/dsh-ark-plans) | 0 | 2026-09-18 | 2026-09-18 | Volcengine Ark Agent Plan and Coding Plan model routes for DeepSeek Harness, with a session-header quota pill |
| 65 | [HaydenSmith1121/dsh-codex-provider](https://github.com/HaydenSmith1121/dsh-codex-provider) | 0 | 2026-09-18 | 2026-09-18 | Codex (ChatGPT) model provider for DeepSeek Harness - serves the ChatGPT subscription models the Codex CLI uses, over OAuth session credentials instead of an API key |
| 66 | [HaydenSmith1121/dsh-connect-trae-plus](https://github.com/HaydenSmith1121/dsh-connect-trae-plus) | 0 | 2026-09-18 | 2026-09-18 | dsh-connect-trae 加固分支（基于上游 dingminhua/dsh-connect-trae v2.0.4）：插件自身启动失败时不再牵连整个 Harness。源码仓。 |
| 67 | [HaydenSmith1121/dsh-excel-viewer](https://github.com/HaydenSmith1121/dsh-excel-viewer) | 0 | 2026-09-18 | 2026-09-18 | Spreadsheet preview for the DeepSeek Harness web client: xlsx / xlsm / xls / csv / tsv open as a read-only grid |
| 68 | [HaydenSmith1121/dsh-memory](https://github.com/HaydenSmith1121/dsh-memory) | 0 | 2026-09-18 | 2026-09-18 | Session-end memory for DeepSeek Harness: distils each turn into durable notes and recalls them per workspace |
| 69 | [HaydenSmith1121/dsh-opencode-go-plus](https://github.com/HaydenSmith1121/dsh-opencode-go-plus) | 0 | 2026-09-18 | 2026-09-18 | OpenCode Go model provider for DeepSeek Harness - a maintained fork that keeps the model catalog reachable and configures itself from Settings > Models |
| 70 | [HaydenSmith1121/dsh-session-cleanup](https://github.com/HaydenSmith1121/dsh-session-cleanup) | 0 | 2026-09-18 | 2026-09-18 | Archived-session cleanup for the dsh web client: per-row delete and delete-all over the real session logs |
| 71 | [HaydenSmith1121/dsh-wallhaven-wallpaper](https://github.com/HaydenSmith1121/dsh-wallhaven-wallpaper) | 0 | 2026-09-18 | 2026-09-18 | DeepSeek Harness 插件：从 wallhaven.cc 搜图并铺成 GUI 背景，图片全由宿主端取回（支持代理，浏览器无需能访问 wallhaven），可一键下载原图。零运行时依赖。 |
| 72 | [jackchen13755/dsh-file-tree](https://github.com/jackchen13755/dsh-file-tree) | 0 | 2026-09-18 | 2026-09-18 | DSH 原生右侧栏文件面板：工作区文件树 + 官方预览（着色）+ 一键 @文件 引用到输入框，适配 DSH 0.1.6 |
| 73 | [jackchen13755/dsh-source-control](https://github.com/jackchen13755/dsh-source-control) | 0 | 2026-09-18 | 2026-09-18 | VS Code 式源代码管理面板（DSH 原生右侧栏标签）：改动/暂存/提交/diff/分支切换与合并/抓取拉取推送/冲突清单/Git worktree，适配 DSH 0.1.6 |
| 74 | [jerry-l3/dsh-plugin-skill-picker](https://github.com/jerry-l3/dsh-plugin-skill-picker) | 0 | 2026-09-18 | 2026-09-18 | DeepSeek Harness 编辑器插件：在「+」按钮右侧新增 Skill 选择按钮，为下一条消息选择 Skill（不选/单选/多选），并支持把本地 md/txt 文件注册为仅当前会话可用的临时 Skill |
| 75 | [jiawei322/dsh-pi-catalog-sync](https://github.com/jiawei322/dsh-pi-catalog-sync) | 0 | 2026-09-18 | 2026-09-18 | Sync the pi.dev model catalog into DeepSeek Harness (dsh) llm-pi-ai provider routes through the official settings seam — no source patch — including mixed-protocol routes like OpenRouter, where new models land on a companion route while the built-in route stays untouched. |
| 76 | [JJTovo/dsh-hunyuan-3d](https://github.com/JJTovo/dsh-hunyuan-3d) | 0 | 2026-09-18 | 2026-09-18 | Tencent Cloud Hunyuan 3D (ai3d / HunyuanTo3D) modeling tools for dsh: text-to-3D and image-to-3D job submission, result polling, and on-disk asset download so other tools can consume a real file path. |
| 77 | [john-walks-slow/dsh-im-humanize](https://github.com/john-walks-slow/dsh-im-humanize) | 0 | 2026-09-07 | 2026-09-18 | Humanized fork of @xmanrui/dsh-im (base 4.21.2): humanized message delivery with send-delay + typing two-phase, message_break + streaming coexistence, status reactions, reply quotes, per-bot overrides and a no_reply reclaim tool for DeepSeek Harness IM channels. |
| 78 | [jonah791/dsh-cloak-browser](https://github.com/jonah791/dsh-cloak-browser) | 0 | 2026-09-18 | 2026-09-18 | CloakBrowser（补丁版 Chromium）生命周期工具：把 20 个加固参数固化为 start/stop/status 三个工具 |
| 79 | [jonah791/dsh-earn-radar](https://github.com/jonah791/dsh-earn-radar) | 0 | 2026-09-18 | 2026-09-18 | 机会雷达：把「我能在哪里赚到钱」做成可成长的仪器——平台是数据（加一个平台=加一条记录），探针是声明式 spec（加一条 URL+过滤=加一个字段），判定内核可离线单测。纯 HTTP 经 Clash 显式代理，fail-closed。 |
| 80 | [jonah791/dsh-identity-ops](https://github.com/jonah791/dsh-identity-ops) | 0 | 2026-09-18 | 2026-09-18 | 数字身份运维工具：邮箱（列/读/取码/取链）+ 站点知识注册表（可成长——新站点是加记录，不是加脚本）。纯 HTTP 经 Clash 显式代理，fail-closed。 |
| 81 | [jonah791/dsh-reze-render](https://github.com/jonah791/dsh-reze-render) | 0 | 2026-09-18 | 2026-09-18 | 用 reze-engine 离线出 MMD 视频的 DSH 插件：reze_status / reze_preview / reze_render（无头 WebGPU 逐帧渲染 + ffmpeg 编码 + 判据现算） |
| 82 | [jonah791/dsh-vault-meta](https://github.com/jonah791/dsh-vault-meta) | 0 | 2026-09-18 | 2026-09-18 | 凭据库只读元数据工具：列出 vault 条目与字段名（**只碰非密元数据**，绝不读取或回显任何明文/密文）——把「我有什么凭据」变成一条工具调用，不再手打 PowerShell |
| 83 | [kaijia323/dsh-plugin-jev](https://github.com/kaijia323/dsh-plugin-jev) | 0 | 2026-09-18 | 2026-09-18 | TypeSafe Jev (System One decision model) as a native jev_decide tool plugin for DeepSeek Harness |
| 84 | [KhalidAlnujaidi/mr-meeseeks](https://github.com/KhalidAlnujaidi/mr-meeseeks) | 0 | 2026-09-17 | 2026-09-18 | Mr. Meeseeks: heterogeneous free-model teams for DeepSeek Harness (dsh-agent-teams replica with Meeseeks art) + Budget-AGI brain-and-swarm preset + swarm scripts |
| 85 | [knyazev741/knyazevai-dsh](https://github.com/knyazev741/knyazevai-dsh) | 0 | 2026-08-17 | 2026-09-18 | KnyazevAI DSH Provider — adds KnyazevAI API models to DeepSeek Harness and DSH Desktop |
| 86 | [kovey/dsh-engineering-suite](https://github.com/kovey/dsh-engineering-suite) | 0 | 2026-09-17 | 2026-09-18 | Engineering suite for DeepSeek Harness: seven plugins covering roles, specifications, test design, quality gates, evidence, audit trail and pipeline orchestration |
| 87 | [KSF1216/chinese-script-policy](https://github.com/KSF1216/chinese-script-policy) | 0 | 2026-09-17 | 2026-09-18 | Harness-neutral Traditional Chinese enforcer and offline converter (skill / DSH bundle / CLI). Checks one script axis one way at a time plus two filter axes: Cantonese colloquialisms and Japanese-only kanji and words. Converts 繁↔簡, 粵語→書面語, 日文→中文, each opt-in, plus an optional wording preference. Single-file offline HTML, no runtime deps. |
| 88 | [lifecoder1988/dsh-devspace](https://github.com/lifecoder1988/dsh-devspace) | 0 | 2026-09-18 | 2026-09-18 | DevSpace nodes and remote-directory mirror Workspaces for the DeepSeek Harness: manage N MCP endpoints, adopt a remote directory as a local Workspace, and move files both ways |
| 89 | [lifecoder1988/dsh-secrets-manager](https://github.com/lifecoder1988/dsh-secrets-manager) | 0 | 2026-09-18 | 2026-09-18 | Project secret management for the DeepSeek Harness: monorepo .env discovery, comment-preserving edits, and a DSH_ENV_FILES pointer your shell commands can source |
| 90 | [Lingwuxin/dsh-audio-rail](https://github.com/Lingwuxin/dsh-audio-rail) | 0 | 2026-09-18 | 2026-09-18 | A DeepSeek Harness (DSH) plugin that makes the quick-jump anchors (turn rail) on the right edge of the conversation page dance with whatever music your system is playing. |
| 91 | [LLYlab/DBS](https://github.com/LLYlab/DBS) | 0 | 2026-09-18 | 2026-09-18 | DBS (DSH BGM service) — 独立于 DET 的 DeepSeek Harness 音乐播放器插件：本地音乐库 + 浮动播放器 + AI 依任务控制播放。A standalone DSH BGM player plugin: local music library, floating player, AI-driven playback. |
| 92 | [loonylabs-dev/dsh-cache-guard](https://github.com/loonylabs-dev/dsh-cache-guard) | 0 | 2026-09-17 | 2026-09-18 | DSH plugin that prices an automatic context rewrite before it lands and asks first — the cold re-read, in k tokens. |
| 93 | [loulangogogo/dsh-plugins-loulan](https://github.com/loulangogogo/dsh-plugins-loulan) | 0 | 2026-09-01 | 2026-09-18 | Plugin collection for DeepSeek Harness (DSH): auto-mounts MCP servers from .mcp.json (with a Web "MCP" tab) and injects global and project rule files into sessions. TypeScript + pnpm monorepo. |
| 94 | [Lukeknow0/dsh-markdown-link-preview](https://github.com/Lukeknow0/dsh-markdown-link-preview) | 0 | 2026-09-18 | 2026-09-18 | Preview DSH Markdown output links inside Better Sidebar instead of an external app. |
| 95 | [maxesisnclaw/dsh-download-button](https://github.com/maxesisnclaw/dsh-download-button) | 0 | 2026-09-18 | 2026-09-18 | Download button for delivered-file cards in DeepSeek Harness / 给交付物文件卡片加下载按钮 |
| 96 | [mingzhicode/dsh-interactive-terminal](https://github.com/mingzhicode/dsh-interactive-terminal) | 0 | 2026-09-18 | 2026-09-18 | Persistent Bash terminals for DeepSeek Harness, letting humans take over and continue model-started sessions through an xterm.js UI. |
| 97 | [mwilljx-web/dsh-plugin-wallpaper](https://github.com/mwilljx-web/dsh-plugin-wallpaper) | 0 | 2026-09-11 | 2026-09-18 | DeepSeek Harness web plugin: a cyberpunk skin for the sidebar and icon buttons, plus a custom background image - managed from the Settings panel. |
| 98 | [neufagents/dsh-healthcheck](https://github.com/neufagents/dsh-healthcheck) | 0 | 2026-09-18 | 2026-09-18 | Runtime health check for DeepSeek Harness: session-library scan + crash-tail inspection. Read-only. |
| 99 | [NEVSTOP-LAB/dsh-import-vscode-ai-files](https://github.com/NEVSTOP-LAB/dsh-import-vscode-ai-files) | 0 | 2026-09-18 | 2026-09-18 | Load VSCode/Copilot AI configuration (.github/copilot-instructions.md, .github/instructions, .github/skills) into DeepSeek Harness sessions. |
| 100 | [OnTheWay111/dsh-plugin-path-completion](https://github.com/OnTheWay111/dsh-plugin-path-completion) | 0 | 2026-09-18 | 2026-09-18 | deepseek harness path completion（deepseek harness @文件名自动补齐和发现） |
| 101 | [Plocr/dsh-commandcode-goat](https://github.com/Plocr/dsh-commandcode-goat) | 0 | 2026-09-18 | 2026-09-18 | DeepSeek Harness (dsh) plugin: publishes a Command Code subscription (GOAT / Pro / Max) as llm-pi-ai provider routes, with account usage and web search on the same credential. |
| 102 | [Qihang-He/dsh-nyanko-sensei](https://github.com/Qihang-He/dsh-nyanko-sensei) | 0 | 2026-09-18 | 2026-09-18 | Nyanko-sensei desktop pet plugin for DeepSeek Harness Web: a round calico cat that idles, naps, wanders, reacts to clicks with a voice line, and follows agent activity. DSH 桌宠插件：娘口三三／猫咪老师。 |
| 103 | [qilin-zhu/dsh-model-relay](https://github.com/qilin-zhu/dsh-model-relay) | 0 | 2026-09-18 | 2026-09-18 | 把deepseek harness里已经配好的模型中转出去，让其他项目可以使用。 |
| 104 | [QLM1234/dsh-plugin-dynamic-assembler](https://github.com/QLM1234/dsh-plugin-dynamic-assembler) | 0 | 2026-08-17 | 2026-09-18 | Natural-language driven, security-gated dynamic assembly plugin for DeepSeek Harness (dsh) |
| 105 | [renshuo/dsh-emacs-keys](https://github.com/renshuo/dsh-emacs-keys) | 0 | 2026-09-18 | 2026-09-18 | emacs keys binding in deepseek harness web UI |
| 106 | [RSLN-creator/dsh-web-bridge](https://github.com/RSLN-creator/dsh-web-bridge) | 0 | 2026-09-12 | 2026-09-18 | 把已登录的网页版 AI（DeepSeek / GLM / Kimi / 通义千问 / 豆包…）接进 DeepSeek Harness 当模型提供方：网页模型产生工具调用，由 DSH 原生权限系统执行本地工具，结果回传同一网页会话。安装物是 GitHub Release 上的 .tgz。 |
| 107 | [ShanWuYinShe/dsh-plugins](https://github.com/ShanWuYinShe/dsh-plugins) | 0 | 2026-08-15 | 2026-09-18 | deepseek harness plugin set |
| 108 | [shenhuanageshei/dsh-team-link](https://github.com/shenhuanageshei/dsh-team-link) | 0 | 2026-08-31 | 2026-09-18 | Session deep links + full session export (markdown/JSON) + approved cross-session messaging with pairing for DeepSeek Harness (dsh). |
| 109 | [shuanzhe/dsh-turn-hard-delete](https://github.com/shuanzhe/dsh-turn-hard-delete) | 0 | 2026-09-17 | 2026-09-18 | Delete a complete turn (question + answer + tool calls) from a DeepSeek Harness session, without deleting the session. |
| 110 | [sujingkpo/dsh-auto-pass](https://github.com/sujingkpo/dsh-auto-pass) | 0 | 2026-09-15 | 2026-09-18 | 本项目只解决「自动审批通过」，不解决无人值守问题。 |
| 111 | [TerebiSAMA/dsh-desktop-linux](https://github.com/TerebiSAMA/dsh-desktop-linux) | 0 | 2026-09-17 | 2026-09-18 | Linux desktop shell for DeepSeek Harness — standalone window, tray LED (done/ask/fail), 60fps breathing bar, self-signed cookie auth, autostart, GitHub auto-update |
| 112 | [The-five-stooges/dsh-deepseek-usage](https://github.com/The-five-stooges/dsh-deepseek-usage) | 0 | 2026-09-18 | 2026-09-18 | DSH plugin: DeepSeek balance row in the sidebar footer plus a popover with locally estimated usage charts and a per-model cost table |
| 113 | [usssserd/my-dsh-plugin](https://github.com/usssserd/my-dsh-plugin) | 0 | 2026-09-18 | 2026-09-18 | DSH插件test |
| 114 | [WanchunLian/dsh-plugin-sound-alert](https://github.com/WanchunLian/dsh-plugin-sound-alert) | 0 | 2026-09-16 | 2026-09-18 | DSH Web 轻量提示音插件：回答完成 / 需要授权时响铃，提示音可替换为本机 WAV（纯客户端 · 零资源文件） |
| 115 | [weifa860504-droid/dsh-greet-signoff](https://github.com/weifa860504-droid/dsh-greet-signoff) | 0 | 2026-09-18 | 2026-09-18 | 开场语与收尾语：每次回复固定开场/收尾，并在上下文接近上限时提示换新会话（DeepSeek Harness Web 插件） |
| 116 | [winston-hoo/dsh-spec-ponytail](https://github.com/winston-hoo/dsh-spec-ponytail) | 0 | 2026-09-18 | 2026-09-18 | DietrichGebert/ponytail — 懒惰 senior 模式，hook注入,迁移成dsh |
| 117 | [wlc114514/dsh-upload-origin](https://github.com/wlc114514/dsh-upload-origin) | 0 | 2026-09-18 | 2026-09-18 | DSH host plugin that resolves the original local path of files uploaded to .dsh-uploads by matching name, size, and sha256. |
| 118 | [woodfood111/dsh-subscription-login](https://github.com/woodfood111/dsh-subscription-login) | 0 | 2026-09-18 | 2026-09-18 | Subscription sign-in console for DeepSeek Harness: one settings page for every OAuth sign-in the harness can offer, read from the authorization seam instead of hardcoded providers. |
| 119 | [wqy-cell/dsh-plugin-basket](https://github.com/wqy-cell/dsh-plugin-basket) | 0 | 2026-09-16 | 2026-09-18 | 插件收纳篮：DSH 最右侧的可收起抽屉，零改造收纳各席位上的第三方插件按钮（分组 / 来源 / 搜索 / 置顶 / 排序） · A DeepSeek Harness plugin: a collapsible drawer that gathers third-party plugin buttons. |
| 120 | [wqy-cell/dsh-task-flow](https://github.com/wqy-cell/dsh-task-flow) | 0 | 2026-09-06 | 2026-09-18 | DSH 插件：任务星图 — 樱花主题的任务流程可视化。一句话让 AI 长出星图，Agent 干活星图实时点亮，Goal 主线星联动；支持任务历史、多窗口同步，数据全在本机 · A DeepSeek Harness plugin: sakura-themed task flow visualization. |
| 121 | [wqy-cell/dsh-url-trace](https://github.com/wqy-cell/dsh-url-trace) | 0 | 2026-09-06 | 2026-09-18 | DSH 插件：网址足迹 — 自动记录从 DSH 打开过的网址（常用排序/最近/收藏/搜索），数据全在本机 · A DeepSeek Harness plugin: local-only URL history. |
| 122 | [wrc093/dsh-agent-graph](https://github.com/wrc093/dsh-agent-graph) | 0 | 2026-09-17 | 2026-09-18 | Graph orchestration for DeepSeek Harness: scoped agent nodes, structured handoffs, bounded rework, and a layered global ledger. |
| 123 | [wzn16/dsh-auto-archive](https://github.com/wzn16/dsh-auto-archive) | 0 | 2026-09-18 | 2026-09-18 | Auto-archive for DeepSeek Harness: archive sessions idle beyond a threshold, with full archived-session management UI · DSH 自动归档插件 |
| 124 | [wzn16/dsh-task-capsule](https://github.com/wzn16/dsh-task-capsule) | 0 | 2026-09-18 | 2026-09-18 | DSH cockpit duo: session-header task capsule + task notification card (sound/system notify) · DSH 任务胶囊与通知插件 |
| 125 | [xmzd-S/dsh-youdaonote](https://github.com/xmzd-S/dsh-youdaonote) | 0 | 2026-09-18 | 2026-09-18 | dsh plugin  about  youdaonote  |
| 126 | [yueyexiayu/dsh-bianji](https://github.com/yueyexiayu/dsh-bianji) | 0 | 2026-09-16 | 2026-09-18 | DeepSeek Harness desktop workspace file editor plugin |
| 127 | [yueyexiayu/dsh-edu](https://github.com/yueyexiayu/dsh-edu) | 0 | 2026-09-16 | 2026-09-18 | DeepSeek Harness desktop quota and balance readout plugin |
| 128 | [yueyexiayu/dsh-liulanqi](https://github.com/yueyexiayu/dsh-liulanqi) | 0 | 2026-09-16 | 2026-09-18 | DSH desktop plugin: Orca-style browser and Design Mode |
| 129 | [yueyexiayu/dsh-shichang](https://github.com/yueyexiayu/dsh-shichang) | 0 | 2026-09-16 | 2026-09-18 | DeepSeek Harness desktop read-only plugin catalog |
| 130 | [yueyexiayu/dsh-sousuo](https://github.com/yueyexiayu/dsh-sousuo) | 0 | 2026-09-16 | 2026-09-18 | DSH desktop search provider: AnySearch with rotating API keys on HTTP 402 |
| 131 | [zeta987/dsh-git-style-zeta](https://github.com/zeta987/dsh-git-style-zeta) | 0 | 2026-09-17 | 2026-09-18 | Configurable Git commit and pull request prompt instructions for DeepSeek Harness |
| 132 | [zeta987/dsh-roles-zeta](https://github.com/zeta987/dsh-roles-zeta) | 0 | 2026-09-17 | 2026-09-18 | Role-based subagent delegation for DeepSeek Harness: one delegate tool over a folder of role files |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- 2507483326/eTeam
- axelfreeman/marketing-mindset
- bihangchi9-creator/dsh-lark-bridge
- Heyflyingpig/long-draft-input
- kovey/dsh-project
- mingger77/project-learning-preset
- nixiaohao/DeepSeek-Desktop-Studio
- RealAlexandreAI/dsh-noc-memory
- shenhuanageshei/dsh-session-link-pro
- tianyhjg-lab/dsh-font
- Viviana-Luna/dsh-window
- winliyou/dsh-plugins
- zw11591-sketch/dsh-pet-panel
