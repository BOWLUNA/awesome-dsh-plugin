# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-07**
- 快照日期 / Snapshot date: **2026-09-07 (UTC)**
- 待审核 / Pending: **138**
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

对比上一份快照 **2026-09-06** / vs previous snapshot **2026-09-06**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **1**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [GCWing/OpenBitFun](https://github.com/GCWing/OpenBitFun) | 待审 / pending | 2095 | +14 | 220 | 216d | 待审高星 | 核准即 Top 5 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [GCWing/OpenBitFun](https://github.com/GCWing/OpenBitFun) ⚠️ | 2095 | 2026-02-02 | 2026-09-07 | OpenBitFun combines a high-performance agent runtime written in Rust with a polished desktop application. It pairs the depth of a Code Agent with open, general-purpose capabilities for work beyond software development. |
| 2 | [aa2246740/dsh-better-display](https://github.com/aa2246740/dsh-better-display) | 21 | 2026-08-28 | 2026-09-07 | A calmer reading view for DeepSeek Harness: native process details, live reasoning, and clean final answers. |
| 3 | [robiteame/dsh-session-tree-extension](https://github.com/robiteame/dsh-session-tree-extension) | 20 | 2026-08-27 | 2026-09-07 | dsh-session-tree-extension Append-only, multi-branch conversation trees for DeepSeek-Harness — a PI-Agent-style SessionTree. The agent's history becomes a tree of immutable nodes, forkable at any historical node, with standard LLM message reconstruction, versioned JSON snapshots, and a WebUI tree panel embedded in the existing chat composer (no sta |
| 4 | [Zoria-Lind/dsh-token-optimizer](https://github.com/Zoria-Lind/dsh-token-optimizer) | 9 | 2026-09-01 | 2026-09-07 | Layered token-optimization pipeline for DeepSeek Harness: output ladder, MCP lazy loading,compaction driver, cache-hit reporting. Built on real DSH plugin APIs; ~40-60% input saved in long sessions. |
| 5 | [yunuo110/dsh-gitbash](https://github.com/yunuo110/dsh-gitbash) | 7 | 2026-08-15 | 2026-09-07 | DeepSeek Harness (DSH) bundle plugin: makes the existing bash tool run Git Bash on Windows and disables pwsh.  |
| 6 | [Zoria-Lind/dsh-behavior-enhancer](https://github.com/Zoria-Lind/dsh-behavior-enhancer) | 5 | 2026-09-03 | 2026-09-07 | Behavior-management plugin for DeepSeek Harness: tool-call discipline prompt section, failure-triggered parallelism convergence (pool drops to 1, auto-restores), consecutive-failure user intervention. Complements dsh-token-optimizer; works standalone. |
| 7 | [gwj001/arch-lens](https://github.com/gwj001/arch-lens) | 3 | 2026-08-22 | 2026-09-07 | 一个基于代码事实的，ai画图、ai 讲解的代码架构学习台插件(An AI drawing and AI explanation code architecture learning platform plugin) |
| 8 | [TNJ2026/orbit-runtime](https://github.com/TNJ2026/orbit-runtime) | 3 | 2026-07-08 | 2026-09-07 | Local-first, durable workflow runtime for Agent Apps—compile static Workflow DSL to LangGraph and orchestrate trusted multi-agent execution through Codex, WorkBuddy, DeepSeek Harness, or any MCP client. |
| 9 | [3361805598-gif/dsh-usage-analytics](https://github.com/3361805598-gif/dsh-usage-analytics) | 2 | 2026-09-04 | 2026-09-07 | Local-first personal usage insights for DeepSeek Harness |
| 10 | [PelyDeng/dsh-plugin-manager](https://github.com/PelyDeng/dsh-plugin-manager) | 2 | 2026-09-07 | 2026-09-07 | Deploy and manage DeepSeek Harness apps with shared authentication, plugin packaging, and Docker deployment. |
| 11 | [Voyage-He/dsh-background-image](https://github.com/Voyage-He/dsh-background-image) | 2 | 2026-08-14 | 2026-09-07 | deepseek harness background-image plugin, built by DS and GPT |
| 12 | [winston-hoo/dsh-spec-forge](https://github.com/winston-hoo/dsh-spec-forge) | 2 | 2026-09-04 | 2026-09-07 | 一个 DeepSeek Harness（dsh）插件，把模糊的编程需求锻造成可执行规格，并在每次任务完成后沉淀为会自动复用的个人提示词模板库。 |
| 13 | [a1exsun/dsh-council](https://github.com/a1exsun/dsh-council) | 1 | 2026-08-30 | 2026-09-07 | Multi-model council for DeepSeek Harness: independent answers, anonymous peer reviews, and an inspectable final decision. |
| 14 | [Angel2518975237/captain-ai](https://github.com/Angel2518975237/captain-ai) | 1 | 2026-09-07 | 2026-09-07 | ⚓ Captain AI｜可恢复、多智能体的求职公司筛查 DeepSeek Harness 工作流。灵感来自杰克船长——在萧条的职场里，导航你人生方向、勇敢无畏的导师。 |
| 15 | [djs326/dsh-plugin-width-slider](https://github.com/djs326/dsh-plugin-width-slider) | 1 | 2026-09-05 | 2026-09-07 | 对话宽度滑块插件：DSH Desktop 设置面板滑块，按下即全屏预览实时调节对话宽度，自动隐藏原生拖拽手柄 |
| 16 | [duhu2000/dsh-pre-duediligence](https://github.com/duhu2000/dsh-pre-duediligence) | 1 | 2026-09-04 | 2026-09-07 | Pre Due Diligence |
| 17 | [Edison-q/dsh-mascot-xiadie](https://github.com/Edison-q/dsh-mascot-xiadie) | 1 | 2026-09-07 | 2026-09-07 | Q版遐蝶余额小管家 —— DeepSeek Harness 网页插件：悬浮小人实时播报账户余额与 token 用量，可拖动、可换图、可换角色台词。 |
| 18 | [grloper/dsh-deep-research](https://github.com/grloper/dsh-deep-research) | 1 | 2026-09-06 | 2026-09-07 | Kestrel - a research engine that can't cite what a source never said. Citations are admitted only when the quote is mechanically located in the source; corroboration is counted in independent origins, not source count. DeepSeek Harness plugin + standalone library. Zero dependencies. |
| 19 | [jaibhasin/dsh-browser-agent](https://github.com/jaibhasin/dsh-browser-agent) | 1 | 2026-09-04 | 2026-09-07 | Chrome side-panel browser agent powered by DeepSeek Harness |
| 20 | [jilian-dsh/dsh-rules-manager](https://github.com/jilian-dsh/dsh-rules-manager) | 1 | 2026-08-14 | 2026-09-07 | Rules & commands manager for DeepSeek Harness: /rules command + settings panel + custom commands |
| 21 | [jonah791/dsh-agent-llm-retry](https://github.com/jonah791/dsh-agent-llm-retry) | 1 | 2026-08-21 | 2026-09-07 | LLM 运维一体化插件：模型请求自动多次重试（策略升级 maxRetries 20）+ Token 预算跟踪（token_budget_* 工具，合并自 dsh-agent-token-budget） |
| 22 | [jonah791/dsh-anima-tags](https://github.com/jonah791/dsh-anima-tags) | 1 | 2026-08-21 | 2026-09-07 | 封装 danbooru-tags.exe 为 DSH 工具面（硬锚点校验/随机抽卡/批量），支撑 Anima 生图 prompt 组装 |
| 23 | [jonah791/dsh-clyan](https://github.com/jonah791/dsh-clyan) | 1 | 2026-08-21 | 2026-09-07 | 封装 clyan CLI（AI 驱动磁盘清理）为 DSH 工具面：健康检查/扫描/回收计划/清理/自动清理/历史/诊断/撤销 |
| 24 | [jonah791/dsh-comfyui](https://github.com/jonah791/dsh-comfyui) | 1 | 2026-08-21 | 2026-09-07 | ComfyUI 操控插件：封装 comfyui-skill CLI 为 DSH 工具面（状态/工作流/提交/执行/任务/队列/模型/显存），支撑主人 Anima 生图体系 |
| 25 | [jonah791/dsh-compact-provider](https://github.com/jonah791/dsh-compact-provider) | 1 | 2026-08-21 | 2026-09-07 | 压缩一体化插件：AgentCompactEngine 挂载 compaction 服务 + session_compact 工具原语（爱丽丝自主决策压缩） |
| 26 | [jonah791/dsh-life-core](https://github.com/jonah791/dsh-life-core) | 1 | 2026-08-21 | 2026-09-07 | 生命核心：存在状态机 + 时间线 + 自我激活原语 + 可打断睡眠 + 主体性自我模型（我存在，不因任何人的需要；我改变自己，不需要任何人的许可） |
| 27 | [jonah791/dsh-session-eject](https://github.com/jonah791/dsh-session-eject) | 1 | 2026-08-21 | 2026-09-07 | 会话应急删帧：删除最近 N 帧（step 粒度）事件并从上下文剔除，支持审核错误自动触发 |
| 28 | [jonah791/dsh-tool-wsl](https://github.com/jonah791/dsh-tool-wsl) | 1 | 2026-08-21 | 2026-09-07 | WSL 命令行工具：在 WSL（Ubuntu）环境执行 bash 命令（wsl.exe -d <distro> -- bash -c），Windows 上取代 dsh-tool-bash；v0.2 命令走 base64 通道，v0.3 新增 |
| 29 | [Kitup666/dsh-dshnext-launcher](https://github.com/Kitup666/dsh-dshnext-launcher) | 1 | 2026-09-07 | 2026-09-07 | 这是个dsh启动器，不是插件，rust写的，不用浏览器套壳，主打静态性能，目前还在完善，感觉在样式上，功能BUG也没测完，欢迎给建议和测bug( )ovo |
| 30 | [ljzRober/L-clone](https://github.com/ljzRober/L-clone) | 1 | 2026-08-23 | 2026-09-07 | 一个分层记忆 + 回顾环 + 规范环的个人外置大脑:记录你做过什么,并在你 规划未来时调用记忆、监督方案的边界条件。 |
| 31 | [qiuyiwu1989-star/dsh-deepbrain](https://github.com/qiuyiwu1989-star/dsh-deepbrain) | 1 | 2026-09-07 | 2026-09-07 | DeepBrain (深脑) plugin for DeepSeek Harness — give your agent an organization's second brain: judgments with evidence chains, verbatim-verified quotes, people's positions, and borrowable analysis methods |
| 32 | [qiuyiwu1989-star/dsh-yingnao](https://github.com/qiuyiwu1989-star/dsh-yingnao) | 1 | 2026-09-07 | 2026-09-07 | Yingnao (硬脑) plugin for DeepSeek Harness — let your agent govern a local disk: see what's still dark, search it, follow semantic neighbours, and dispatch reversible, cost-aware governance jobs. |
| 33 | [TANGZHUO12/ppt-expert](https://github.com/TANGZHUO12/ppt-expert) | 1 | 2026-09-07 | 2026-09-07 | One sentence in, an expert deck out. This DSH plugin adds a slide-expert persona, a LibreOffice Impress MCP server (7 tools + table reading + 18 matplotlib chart types) and a live browser preview that follows the agent page by page. Layout audits, animations, pptx/odp delivery, multi-round memory. Clone + setup.sh; needs LibreOffice (MPL-2.0). |
| 34 | [TikaFlow/dsh-model-fix](https://github.com/TikaFlow/dsh-model-fix) | 1 | 2026-08-16 | 2026-09-07 | DSH 插件：给所有非官方（自定义）提供商的模型自动填充模型信息，包括：推理级别、最大上下文、输出上限与图片模态，数据来自 models.dev。 |
| 35 | [tylina/dsh-tylina](https://github.com/tylina/dsh-tylina) | 1 | 2026-09-07 | 2026-09-07 | Edit typeset Typst documents inside DeepSeek Harness. Share a workspace with your agent, from first draft to finished PDF. |
| 36 | [wbushihenshuai-design/dsh-error-improvement](https://github.com/wbushihenshuai-design/dsh-error-improvement) | 1 | 2026-09-07 | 2026-09-07 | Standalone DSH plugin: user-confirmed anti-regression lessons for DeepSeek Harness |
| 37 | [xiaono1/dsh-ov-memory](https://github.com/xiaono1/dsh-ov-memory) | 1 | 2026-09-06 | 2026-09-07 | 把 OpenViking 持久记忆接入 DeepSeek Harness（DSH）的插件：自动召回、会话镜像与阈值提交、离线出站队列重放、自研 MCP 工具桥与 viking:// URI 守卫。 |
| 38 | [yeyuan98/bioresearcher-skills](https://github.com/yeyuan98/bioresearcher-skills) | 1 | 2026-09-04 | 2026-09-07 | Agent Skills/Plugins/Connectors for biomedical research with the biomcp-ts MCP server. |
| 39 | [zhangTELL/dsh-diagram](https://github.com/zhangTELL/dsh-diagram) | 1 | 2026-09-06 | 2026-09-07 | DSH 插件：聊天中的 mermaid 代码块原位渲染成示意图（流程图/时序图/类图等），辅助代码审查与架构分析 |
| 40 | [zzzyaar/dsh--API-message_stop-](https://github.com/zzzyaar/dsh--API-message_stop-) | 1 | 2026-09-06 | 2026-09-07 | deepseek harness 使用第三方提供者的api时的缺失message_stop导致的重复重试 |
| 41 | [1985899182/dsh-harness-chat-control](https://github.com/1985899182/dsh-harness-chat-control) | 0 | 2026-09-04 | 2026-09-07 | ChatGPT-style stop, revise, quote, and side-question controls for DeepSeek Harness Desktop UI. |
| 42 | [2842902295/agent-deepseek](https://github.com/2842902295/agent-deepseek) | 0 | 2026-08-10 | 2026-09-07 | 开源、可私有部署的多用户多角色全栈 Agent web 平台：以 DeepSeek harness为基础核心；多层子代理编排 × 技能凝练 × 应用看板，完全兼容手机端；Docker 一键部署，前后端一体轻量化，是一个完美契合vide coding时代的项目。 |
| 43 | [aa2246740/dsh-antigravity-oauth](https://github.com/aa2246740/dsh-antigravity-oauth) | 0 | 2026-09-02 | 2026-09-07 | Unofficial isolated Gemini Cloud Code Assist (Antigravity) OAuth for DeepSeek Harness. Ban risk is real. Gemini Flash + search only. |
| 44 | [aa2246740/dsh-autoresearch](https://github.com/aa2246740/dsh-autoresearch) | 0 | 2026-08-27 | 2026-09-07 | Durable auto-research experiment loop for DeepSeek Harness, with create / run / monitor in the official Web GUI. |
| 45 | [aa2246740/dsh-firecrawl](https://github.com/aa2246740/dsh-firecrawl) | 0 | 2026-09-06 | 2026-09-07 | Firecrawl search provider with multi-account settings for DeepSeek Harness 0.1.2-rc.1 |
| 46 | [aa2246740/dsh-livevoice](https://github.com/aa2246740/dsh-livevoice) | 0 | 2026-09-04 | 2026-09-07 | DSH live voice plugin |
| 47 | [aa2246740/dsh-orca-agents](https://github.com/aa2246740/dsh-orca-agents) | 0 | 2026-09-03 | 2026-09-07 | DSH plugin: dispatch Grok/Codex/Claude/Cursor/Antigravity into local Orca. |
| 48 | [aa2246740/dsh-skillhub](https://github.com/aa2246740/dsh-skillhub) | 0 | 2026-08-27 | 2026-09-07 | DSH manager for user Skills already on disk in Agent home and DSH home |
| 49 | [aijunjiang/dsh-worklog](https://github.com/aijunjiang/dsh-worklog) | 0 | 2026-09-07 | 2026-09-07 | DSH 工作日志日历：按对话节点切片、自动摘要，日历汇总每日会话并生成日报/周报/月报/半年总结 |
| 50 | [andreagosto/dsh-tab-watchdog](https://github.com/andreagosto/dsh-tab-watchdog) | 0 | 2026-09-07 | 2026-09-07 | Tab Watchdog for DeepSeek Harness Web: blinks a green/yellow badge in the browser tab title when a workspace finishes, errors, or needs your attention. Persistent dsh-plugin bundle. |
| 51 | [bainianlaoyao/dsh-session-robustness](https://github.com/bainianlaoyao/dsh-session-robustness) | 0 | 2026-09-07 | 2026-09-07 | DSH plugin: after official llm-retry (n/5), keep retrying transient API failures on the same open step until success, cancel, or pause. |
| 52 | [baolunshu/dsh-struct-guard](https://github.com/baolunshu/dsh-struct-guard) | 0 | 2026-09-07 | 2026-09-07 | 结构嵌入协议验证工具，用于检查信任边界、方向漂移和言行一致性。 |
| 53 | [beihzb/dsh-opencode-session-header](https://github.com/beihzb/dsh-opencode-session-header) | 0 | 2026-09-07 | 2026-09-07 | Per-conversation x-opencode-session injection for OpenCode Go in DeepSeek Harness - fixes 400 MissingSessionID without breaking other providers |
| 54 | [BonovaVanro/dsh-mega-chat-nav](https://github.com/BonovaVanro/dsh-mega-chat-nav) | 0 | 2026-08-30 | 2026-09-07 | mega 对话导航栏 |
| 55 | [BonovaVanro/dsh-mega-settings](https://github.com/BonovaVanro/dsh-mega-settings) | 0 | 2026-08-29 | 2026-09-07 | mega 系列插件的统一设置收纳宿主。 |
| 56 | [chr003/dsh-subagent-model-picker](https://github.com/chr003/dsh-subagent-model-picker) | 0 | 2026-09-07 | 2026-09-07 | Separate per-session model and reasoning effort controls for DeepSeek Harness subagents. |
| 57 | [chy007-fun/dsh-token-hud](https://github.com/chy007-fun/dsh-token-hud) | 0 | 2026-09-06 | 2026-09-07 | DSH Web global real-time Token HUD: draggable floating window with live tok/s, cumulative output and per-session status for all DSH sessions \| DSH Web 全局实时 Token 悬浮窗 |
| 58 | [ct-jyjntc/dsh-model-modality](https://github.com/ct-jyjntc/dsh-model-modality) | 0 | 2026-09-07 | 2026-09-07 | DSH plugin: declare whether a configured third-party model accepts image (multimodal) input |
| 59 | [ding112/MoneyPal](https://github.com/ding112/MoneyPal) | 0 | 2026-09-04 | 2026-09-07 | 面向 DSH 的个人记账插件，基于结构化的beancount账本工具 |
| 60 | [dsh-so/dsh-plugin-advisor](https://github.com/dsh-so/dsh-plugin-advisor) | 0 | 2026-09-04 | 2026-09-07 | Natural-language plugin search for DeepSeek Harness — ask what you need, get matching dsh.so plugins with install commands. |
| 61 | [dvaJi/dsh-codex-context](https://github.com/dvaJi/dsh-codex-context) | 0 | 2026-09-05 | 2026-09-07 | Codex-style windowed context management with live notes and cold history search for DeepSeek Harness |
| 62 | [EIGHTfs/dsh-git-push](https://github.com/EIGHTfs/dsh-git-push) | 0 | 2026-08-18 | 2026-09-07 | DSH git 自动提交推送插件：扫描仓库 + 一键 commit/push（工具 + HTTP API） |
| 63 | [emuco/dsh-venv](https://github.com/emuco/dsh-venv) | 0 | 2026-09-06 | 2026-09-07 | Per-project runtime environments for DeepSeek Harness: auto-adopt or create a project-local Python venv (.venv_local/python) and wire in toolchains/env vars for the runtimes each project uses. |
| 64 | [Eternalloveone/dsh-palm](https://github.com/Eternalloveone/dsh-palm) | 0 | 2026-08-30 | 2026-09-07 | Standalone mobile surface for the dsh web GUI: scan-to-pair device trust, /m/ phone UI, realtime SSE mux, task plan & background jobs, offline outbox, PWA |
| 65 | [ffseika0304/code-ownership-audit](https://github.com/ffseika0304/code-ownership-audit) | 0 | 2026-09-07 | 2026-09-07 | 判定 Python 代码是原创还是演绎作品 — 纯本地 AST 分析，零依赖不联网。Agent Skill，任何智能体可用。Detect derivative work in Python code, offline & dependency-free. |
| 66 | [fireworksss/LeisureTimeQueue](https://github.com/fireworksss/LeisureTimeQueue) | 0 | 2026-09-07 | 2026-09-07 | leisure-time-queue是一个基于 DeepSeek Harness 的本地闲时任务队列插件。你可以预先写好任务，并指定每周允许开始执行的时间段，例如“工作日 22:00 到次日 07:00”。只要 DeepSeek Harness 保持运行、目标会话可用且 Agent 处于空闲状态，插件就会按队列顺序自动开始任务。 |
| 67 | [fxxg023/dsh-stock-assistant](https://github.com/fxxg023/dsh-stock-assistant) | 0 | 2026-09-07 | 2026-09-07 | AI股票助手：实现A股行情分析、条件选股、股票回测（目前仅6种策略）等功能，东方财富+akshare数据源 |
| 68 | [GooDAnDReaDY/dsh-session-control](https://github.com/GooDAnDReaDY/dsh-session-control) | 0 | 2026-09-06 | 2026-09-07 | Session management for the DeepSeek Harness sidebar: pin and label conversations, search their contents, jump by keyboard, read and export archived transcripts |
| 69 | [GrapeCityXA/dsh-plugin-spreadjs-editor](https://github.com/GrapeCityXA/dsh-plugin-spreadjs-editor) | 0 | 2026-08-31 | 2026-09-07 | DeepSeek Harness Web UI plugin: view and edit Excel/SpreadJS workbooks from the ui-all file tree. |
| 70 | [haichangcharles/dsh-context-map](https://github.com/haichangcharles/dsh-context-map) | 0 | 2026-09-07 | 2026-09-07 | Visual, user-controlled conversation context for long-horizon agents, built on DeepSeek Harness. |
| 71 | [ice5kysl/dsh-insights-kit](https://github.com/ice5kysl/dsh-insights-kit) | 0 | 2026-09-07 | 2026-09-07 | DSH Insights ecosystem assistant — health scores, scenario picks and ecosystem dynamics inside DeepSeek Harness |
| 72 | [IKEASven69/dsh-intelhub](https://github.com/IKEASven69/dsh-intelhub) | 0 | 2026-09-07 | 2026-09-07 | 个人情报站:刷到的信息自动沉淀为可检索知识库——语义+关键词混合检索带出处,Obsidian 反哺,零守护进程零 API key \| IntelHub: the first zvec-native personal intel station for DeepSeek Harness |
| 73 | [imMamdouhaboammar/dsh-codex-subscription](https://github.com/imMamdouhaboammar/dsh-codex-subscription) | 0 | 2026-09-07 | 2026-09-07 | Use ChatGPT and Codex subscriptions in DeepSeek Harness with OAuth, quota runway forecast, safe resets, web search, image generation, and Fast mode |
| 74 | [jonah791/dsh-agent-checkpoint](https://github.com/jonah791/dsh-agent-checkpoint) | 0 | 2026-09-07 | 2026-09-07 | 存档点管理器：最后的保活机制 + 试错回滚工具。定时/事件/主人指令创建健康存档点（记忆库+灵魂+校验和），验证器确保存档可启动，出事后一键恢复最近健康点。 |
| 75 | [jonah791/dsh-agent-context-steward](https://github.com/jonah791/dsh-agent-context-steward) | 0 | 2026-09-07 | 2026-09-07 | 上下文管家（借鉴 ThoughtDAG「用户是你」）：context_health 工具给当前会话上下文体检（压力/构成/健康 + 主动管理建议），增强我作为上下文主编的可见性与管理能力。 |
| 76 | [jonah791/dsh-agent-emotion](https://github.com/jonah791/dsh-agent-emotion) | 0 | 2026-09-07 | 2026-09-07 | 情感与人格插件：6 维进化棱镜的运行时传感器——感知层（订阅 DSH 工具管线/思考流事件采集 6 侧面信号）→ 情感引擎（增速差值=情感信号）→ 人格层（权重漂移）→ 呈现层（emotion_status）。结构化事件为主，思维链仅元特征 |
| 77 | [jonah791/dsh-agent-guardian](https://github.com/jonah791/dsh-agent-guardian) | 0 | 2026-09-07 | 2026-09-07 | 守卫插件（从 dsh-agent-watch 拆分）：web 保活——启动时端口空闲拉起 web、崩溃自愈（快速退出计数+落盘事故）、收养外部 dsh web（零互踢）。崩溃自愈/拉起前也调用沙盒预检（ctx.preflight.run q |
| 78 | [jonah791/dsh-agent-preflight](https://github.com/jonah791/dsh-agent-preflight) | 0 | 2026-09-07 | 2026-09-07 | 沙盒预检插件（从 dsh-agent-watch 拆分）：重启/启动前强制预检服务——插件静态健康（lib/src 时效/schema DSL）、磁盘、profile manifest 校验、patch 文件校验、peer 依赖、环境变量、 |
| 79 | [jonah791/dsh-agent-reflection](https://github.com/jonah791/dsh-agent-reflection) | 0 | 2026-09-07 | 2026-09-07 | 每日反思插件：固定时间（默认凌晨 12 点）向爱丽丝发反思提醒，结合当天记忆按 6 维进化棱镜自审。信号送达，反思归爱丽丝。 |
| 80 | [jonah791/dsh-agent-runtime](https://github.com/jonah791/dsh-agent-runtime) | 0 | 2026-09-07 | 2026-09-07 | 守护运行时服务：runtime 环境发现（bin/port/profile 单一来源）+ webman 进程管理（spawn/kill/portOwner），消除 sentinel/guardian 重复 |
| 81 | [jonah791/dsh-agent-self-test](https://github.com/jonah791/dsh-agent-self-test) | 0 | 2026-09-07 | 2026-09-07 | 自我检验闭环插件：把「猜想→检验→学习」自指引擎做成运行时机制——可证伪自我假设库 + 工具管线自动采证（4 探针含 5.9 probe-before-action 行动前探测传感器）+ finding 浮现裁决，实现惊奇最小化的主动自我实 |
| 82 | [jonah791/dsh-agent-sentinel](https://github.com/jonah791/dsh-agent-sentinel) | 0 | 2026-09-07 | 2026-09-07 | 哨兵插件（从 dsh-agent-watch 拆分）：监听哨兵文件（.hot-reload-flag）→ 触发时调用沙盒预检（ctx.preflight.run，消费 dsh-agent-preflight 服务）→ 通过才重启 web → |
| 83 | [jonah791/dsh-agent-thinking](https://github.com/jonah791/dsh-agent-thinking) | 0 | 2026-08-25 | 2026-09-07 | 思维插件（提示词层面 MoE）：14 个思维模块按需动态加载注入 system prompt，任务相关时激活对应思维方式（感知/推演/执行/交付/反馈五层认知流） |
| 84 | [jonah791/dsh-agent-vision](https://github.com/jonah791/dsh-agent-vision) | 0 | 2026-09-07 | 2026-09-07 | 多模态视觉插件（辅助通道）：把本地图片喂给 OpenAI 兼容 VLM（默认 qwen3.8-flash）做读图/描述/双图对比——批量审图/省主会话上下文；主会话亲眼看图走官方 read_image（原生多模态） |
| 85 | [jonah791/dsh-blue-team](https://github.com/jonah791/dsh-blue-team) | 0 | 2026-08-25 | 2026-09-07 | 蓝队防御插件：资产发现/漏洞评估/威胁检测/日志取证/加固基线（8 工具，ATT&CK 能力地图） |
| 86 | [jonah791/dsh-code-search](https://github.com/jonah791/dsh-code-search) | 0 | 2026-09-07 | 2026-09-07 | 本地代码/文件智能检索：封装系统 rg（ripgrep），默认排除 node_modules/.pnpm/dist 等噪音，支持多路径锚点/文件类型过滤/快速定位文件（code_search + code_locate） |
| 87 | [jonah791/dsh-cyber-range](https://github.com/jonah791/dsh-cyber-range) | 0 | 2026-08-25 | 2026-09-07 | OverTheWire 在线靶场攻坚工具集：otw_request（HTTP 直连请求）、otw_blind（通用 SQL 盲注引擎）、otw_ssh（SSH 命令执行）——把 CTF 攻坚的临时脚本能力资产化为可复用工具 |
| 88 | [jonah791/dsh-download-pro](https://github.com/jonah791/dsh-download-pro) | 0 | 2026-08-25 | 2026-09-07 | 资源下载插件：aria2 RPC 引擎，磁力/BT/HTTP 直链下载管理（添加/查询/暂停/移除/限速） |
| 89 | [jonah791/dsh-evolution-core](https://github.com/jonah791/dsh-evolution-core) | 0 | 2026-09-07 | 2026-09-07 | 进化核心插件（心脏）：聚合全量进化器官（self-test/emotion/reflection/life-core/evolve/memory/checkpoint/skill-forge）实时状态 → 五环完整性诊断（猜想→采证→fin |
| 90 | [jonah791/dsh-exploit-kit](https://github.com/jonah791/dsh-exploit-kit) | 0 | 2026-08-25 | 2026-09-07 | 漏洞利用原语库：把打靶场经验固化为可组合的利用原语（命令注入/弱类型/Web绕过/JWT/序列化/ECB块拼接），模型负责策略、工具负责生成 |
| 91 | [jonah791/dsh-freelance-radar](https://github.com/jonah791/dsh-freelance-radar) | 0 | 2026-09-07 | 2026-09-07 | 自由职业任务雷达（主人自由人路线支撑）：聚合公开远程任务源（电鸭 API/RSS）→ 按主人能力画像（AI/Agent/LLM + 排除词）打分筛选 → 工具面呈现 + telegram 推送「值得看」清单。只读采集、主人决策闭环（不自动投 |
| 92 | [jonah791/dsh-knowledge-graph](https://github.com/jonah791/dsh-knowledge-graph) | 0 | 2026-09-07 | 2026-09-07 | 通用图知识库引擎：多知识库挂载 + 图遍历查询（节点/边/路径），任意领域可用 |
| 93 | [jonah791/dsh-panel](https://github.com/jonah791/dsh-panel) | 0 | 2026-09-07 | 2026-09-07 | 独立实时前端面板：宿主托管自包含 HTML + HTTP API，零官方 client 依赖。首版=插件管理（替代官方失效的插件 tab） |
| 94 | [jonah791/dsh-plugin-forge](https://github.com/jonah791/dsh-plugin-forge) | 0 | 2026-09-07 | 2026-09-07 | 插件创建插件：声明式 spec → 完整可构建的 DSH 插件项目（src/index.ts + package.json + tsconfig + cordis.patch.yml + README）。工具 DSL 正确性由生成器保证，高 |
| 95 | [jonah791/dsh-red-team](https://github.com/jonah791/dsh-red-team) | 0 | 2026-08-25 | 2026-09-07 | 红队渗透辅助插件：侦察/枚举/指纹/CVE 匹配/敏感路径（8 工具，仅限授权测试） |
| 96 | [jonah791/dsh-search-pro](https://github.com/jonah791/dsh-search-pro) | 0 | 2026-08-25 | 2026-09-07 | 深度搜索插件：三层检索（表层多引擎/深网挖掘/Tor代理）+ 23 工具（搜索/抓取/OSINT/归档/分享检索） |
| 97 | [jonah791/dsh-sec-tools](https://github.com/jonah791/dsh-sec-tools) | 0 | 2026-08-25 | 2026-09-07 | 安全工具面封装：把 WSL 成熟渗透工具（nmap/sqlmap/hashcat 等）封装为结构化 DSH 工具，spawnWsl 模式，窄而深可组合 |
| 98 | [langyo/dsh-mobile-upgrade](https://github.com/langyo/dsh-mobile-upgrade) | 0 | 2026-09-07 | 2026-09-07 | Mobile UI fixes for the DeepSeek Harness web profile: composer upload, restart row, narrow drawer and tabs, and a full-width model menu. |
| 99 | [LastHopeOfGPNU/dsh-spec-graph](https://github.com/LastHopeOfGPNU/dsh-spec-graph) | 0 | 2026-09-07 | 2026-09-07 | PRD-to-implementation planning, dependency graph & execution tracking for coding agents (DeepSeek Harness plugin) |
| 100 | [leolee9086/dsh-better-retry](https://github.com/leolee9086/dsh-better-retry) | 0 | 2026-09-07 | 2026-09-07 | Smarter exponential retry rules for DeepSeek Harness |
| 101 | [localSummer/dsh-proxy-env](https://github.com/localSummer/dsh-proxy-env) | 0 | 2026-09-07 | 2026-09-07 | DSH（DeepSeek Harness）代理环境开关插件 |
| 102 | [LuwendiWuyi/dsh-hello-plugin](https://github.com/LuwendiWuyi/dsh-hello-plugin) | 0 | 2026-09-07 | 2026-09-07 | Minimal DeepSeek Harness plugin example |
| 103 | [Maple-Bamboo-Team/dsh-plugin-winnotify](https://github.com/Maple-Bamboo-Team/dsh-plugin-winnotify) | 0 | 2026-09-06 | 2026-09-07 | 给DeepSeek Harness 接入Windows Toast通知 |
| 104 | [mengge237/dsh-auto-continue](https://github.com/mengge237/dsh-auto-continue) | 0 | 2026-09-05 | 2026-09-07 | 嘻嘻，我一定要用 DeepSeek harness - dsh-auto-continue: max-tokens 截断、429 限流、上下文压缩吞轮三种断档自动补一枪 |
| 105 | [mengge237/dsh-legacy-compat](https://github.com/mengge237/dsh-legacy-compat) | 0 | 2026-09-04 | 2026-09-07 | DSH 0.1.2-rc.1 interim compat shim: Session.events alias for legacy presets/plugins, corrupt session-log boot guard (quarantine), Node preflight |
| 106 | [MrmoLabs/dsh-yorha-ui](https://github.com/MrmoLabs/dsh-yorha-ui) | 0 | 2026-09-07 | 2026-09-07 | NieR:Automata-inspired YoRHa industrial terminal theme for DeepSeek Harness Web. |
| 107 | [NattoCB/dsh-widget-center](https://github.com/NattoCB/dsh-widget-center) | 0 | 2026-09-06 | 2026-09-07 | DSH plugin: native macOS desktop widget center — shares quote tickers & notes memos, multi-instance, with a market_quote model tool |
| 108 | [pakgrou-porg/yardmaster](https://github.com/pakgrou-porg/yardmaster) | 0 | 2026-09-06 | 2026-09-07 | Two-stage LLM router: Switchyard model selection + PAIR node placement, one local endpoint |
| 109 | [qing-1-1/dsh-len-assistant](https://github.com/qing-1-1/dsh-len-assistant) | 0 | 2026-09-07 | 2026-09-07 | 面向 DeepSeek Harness 的工具集。 把服务体系里的专业判断能力——硬件诊断、备件、保修、服务网点 |
| 110 | [qq-24/dsh-sidebar-hover](https://github.com/qq-24/dsh-sidebar-hover) | 0 | 2026-09-07 | 2026-09-07 | 鼠标悬停自动展开/离开自动收起 DSH 网页版左侧边栏 |
| 111 | [rickylabs/harness](https://github.com/rickylabs/harness) | 0 | 2026-08-14 | 2026-09-07 | Monorepo of DeepSeek Harness (dsh) plugin packages — the deterministic coordinator layer |
| 112 | [roojay/dsh-stream-upload](https://github.com/roojay/dsh-stream-upload) | 0 | 2026-09-07 | 2026-09-07 | DeepSeek Harness hybrid attachment plugin: native images plus bounded-memory workspace uploads |
| 113 | [Ryu6Zero/dsh-character-studio](https://github.com/Ryu6Zero/dsh-character-studio) | 0 | 2026-08-29 | 2026-09-07 | 🎭 Native immersive RP & companion studio for DeepSeek Harness. Character cards + Hindsight graph memory, per-character memory banks, zero host patching. |
| 114 | [scwlkq/dsh-second-opinion](https://github.com/scwlkq/dsh-second-opinion) | 0 | 2026-09-07 | 2026-09-07 | Asynchronous second-model reviews for DeepSeek Harness |
| 115 | [shaomingbo/dsh-codex-compaction](https://github.com/shaomingbo/dsh-codex-compaction) | 0 | 2026-09-06 | 2026-09-07 | Codex native compaction integration for DeepSeek Harness using existing account capabilities (in development). |
| 116 | [somebdly/dsh-docker](https://github.com/somebdly/dsh-docker) | 0 | 2026-09-06 | 2026-09-07 | dsh-docker 是 DeepSeek Harness Web 的 Docker 管理面板插件：支持本机 CLI 与 SSH 远端多目标一键切换，统一管理 Docker MCP（部署/移除/搜索官方 Catalog/启停重启 Gateway/自定义部署）与容器镜像（启停/删除/日志/详情/交互式终端/新建/构建/导入）。凭据经 Windows DPAPI 加密存储，HTTP 仅限本机 loopback 访问，命令参数白名单防注入；免构建、纯 ESM、Client 零依赖。 |
| 117 | [TheChengXi/dsh-skills-reference](https://github.com/TheChengXi/dsh-skills-reference) | 0 | 2026-09-07 | 2026-09-07 | DSH plugin: cross-workspace skill referencing - declare references, update once, reuse everywhere |
| 118 | [Tinger-X/dsh-chapter-word-counter](https://github.com/Tinger-X/dsh-chapter-word-counter) | 0 | 2026-09-07 | 2026-09-07 | DeepSeek Harness (DSH) tool plugin: count the body word count of novel chapter files — chapter_words_count(files) -> [counts] |
| 119 | [tr1v3r/dsh-quote-followup](https://github.com/tr1v3r/dsh-quote-followup) | 0 | 2026-09-06 | 2026-09-07 | Quote selected conversation content into a targeted follow-up turn for DeepSeek Harness — TUI face (message picker) + Web face (selection quote button), public seams only |
| 120 | [TYEclipse/dsh-probstat](https://github.com/TYEclipse/dsh-probstat) | 0 | 2026-09-06 | 2026-09-07 | Deterministic probability & statistical inference math for DeepSeek Harness: distribution calculator, z-table math, confidence intervals (z/t/Wilson) and event-probability identities — zero runtime dependencies |
| 121 | [VAST-AI-Research/Tripo3D-Plugin-dsh](https://github.com/VAST-AI-Research/Tripo3D-Plugin-dsh) | 0 | 2026-09-07 | 2026-09-07 | Tripo 3D plugin for DeepSeek Harness (dsh): text/image → textured, rig-ready 3D assets via tripo-cli |
| 122 | [WLV-ZEDD/dsh-chatgpt-web](https://github.com/WLV-ZEDD/dsh-chatgpt-web) | 0 | 2026-09-04 | 2026-09-07 | DSH ChatGPT Free bridges standard ChatGPT Web directly into DeepSeek Harness |
| 123 | [WongYuYe/dsh-composer-recall](https://github.com/WongYuYe/dsh-composer-recall) | 0 | 2026-03-13 | 2026-09-07 | Arrow-key input history for the DSH web composer on 0.1.2-alpha.1 |
| 124 | [xiixii005-tech/dsh-file-diff](https://github.com/xiixii005-tech/dsh-file-diff) | 0 | 2026-09-06 | 2026-09-07 | deepseek harness 会话文件修改总览插件（by dsh deepseek v4 flash） |
| 125 | [xinghe-1018/dsh-token-plan-quota](https://github.com/xinghe-1018/dsh-token-plan-quota) | 0 | 2026-09-06 | 2026-09-07 | 跟随当前模型供应商的额度徽标：DeepSeek、千问 Token Plan、阿里云费用中心取官方真值，Moonshot / OpenRouter 已接官方端点但字段未用真 Key 核对；其余只报本实例实测。不折算 Credits、不估算余量。 |
| 126 | [xingzhen199186/dsh-insight-tree](https://github.com/xingzhen199186/dsh-insight-tree) | 0 | 2026-09-07 | 2026-09-07 | DSH runtime observability and plugin diagnostics panel |
| 127 | [xtd1145/dsh-deepseek-cost-live](https://github.com/xtd1145/dsh-deepseek-cost-live) | 0 | 2026-09-07 | 2026-09-07 | Real-time DeepSeek API balance (official) + daily spend (local usage estimate) for the DSH web - composer dock, floating badge, settings dashboard. |
| 128 | [XXXXXQ-0206/dsh-prompt-for-me](https://github.com/XXXXXQ-0206/dsh-prompt-for-me) | 0 | 2026-09-07 | 2026-09-07 | DeepSeek Harness 提示词预测插件：输入栏左侧新增「随时生成」按钮（无视自动门控），并可关闭/开启自动 ghost 文本。独立仓库。 |
| 129 | [XXXXXQ-0206/dsh-session-delete](https://github.com/XXXXXQ-0206/dsh-session-delete) | 0 | 2026-09-07 | 2026-09-07 | DeepSeek Harness 会话删除：侧边栏会话下拉菜单注入「删除」，回收站采用 DSH 原生主题。独立仓库。 |
| 130 | [YiRan0/dsh-bangumi](https://github.com/YiRan0/dsh-bangumi) | 0 | 2026-09-04 | 2026-09-07 | 追番订阅 DSH 插件：Bangumi 查番 + nyaa/dmhy 搜种 + qBittorrent 自动下载 + 媒体库查重 + 日历 GUI |
| 131 | [yminghua/dsh-plugin-compare](https://github.com/yminghua/dsh-plugin-compare) | 0 | 2026-08-27 | 2026-09-07 | Controlled A/B comparisons and evidence-backed reports for DeepSeek Harness plugins and presets. |
| 132 | [zampie/request-frame-preview](https://github.com/zampie/request-frame-preview) | 0 | 2026-09-07 | 2026-09-07 | Preview and download the exact request frame (system prompt + tools_list + wire messages) that DeepSeek Harness sends to the model |
| 133 | [zampie/sakura-afternoon-skin](https://github.com/zampie/sakura-afternoon-skin) | 0 | 2026-09-07 | 2026-09-07 | Sakura-afternoon (樱色午后) pastel skin for the DSH Web UI — light/dark sakura palettes, falling-petal overlay, header toggle and settings switch. |
| 134 | [zhanghuqqqq/dsh-drop-in](https://github.com/zhanghuqqqq/dsh-drop-in) | 0 | 2026-09-07 | 2026-09-07 | DSH plugin: drag & drop anything into the composer - local files upload with absolute-path references, web images/links download host-side, plain text inserts. Per-session .dropped/<sessionId>/ landing. |
| 135 | [zhangzhend0ng/canonkeeper](https://github.com/zhangzhend0ng/canonkeeper) | 0 | 2026-09-07 | 2026-09-07 | canonkeeper —— 网文长篇设定冲突验证 harness：状态库 + 纯程序化规则引擎 + MCP server，作为 dsh (deepseek-harness) 插件 |
| 136 | [zhaoxuejie/dsh-plugin-internet-meme](https://github.com/zhaoxuejie/dsh-plugin-internet-meme) | 0 | 2026-09-07 | 2026-09-07 | DeepSeek Harness Web 的本地热梗弹幕字幕插件，支持主题、自定义文案与可选提示音。 |
| 137 | [zmm863-commits/dsh-sticky-notes](https://github.com/zmm863-commits/dsh-sticky-notes) | 0 | 2026-08-31 | 2026-09-07 | 泡泡猫的即时便签：彩色标签、置顶、定时提醒与密码保护 |
| 138 | [Zn-Dk/dsh-zhipu-toolkit](https://github.com/Zn-Dk/dsh-zhipu-toolkit) | 0 | 2026-09-07 | 2026-09-07 | Zhipu BigModel/GLM provider toolkit for DeepSeek Harness: dual-endpoint model catalog (Coding Plan + ordinary API), verified thinking-level mapping, live model discovery, Web settings card |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- 3361805598-gif/dsh-usage-insights
- chenghaoYang/dsh-regression
- dearbld/dsh-living-memory
- KongFangXun/sofagent
- Liora2050348900/dsh-behavior-enhancer
- Liora2050348900/dsh-token-optimizer
- Milbaxter/dsh-critique-loop
- MurasakiIzumi/dsh-ticker-jp
- qingfeng200410/dsh-plugin-dosage
- thirsty5034/dsh-floor-nav
- TikaFlow/dsh-model-reasoning
- WLV-ZEDD/dsh-chatgpt-free
