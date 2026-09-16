# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-16**
- 快照日期 / Snapshot date: **2026-09-16 (UTC)**
- 待审核 / Pending: **130**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **17**
- Star 异常增长 / Star-growth alerts: **4** — 先看下方告警节 / see the alert section first

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

对比上一份快照 **2026-09-15** / vs previous snapshot **2026-09-15**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **4**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [dsh-tauri/deepseek-harness-desktop](https://github.com/dsh-tauri/deepseek-harness-desktop) | 待审 / pending | 2158 | +45 | 136 | 32d | 待审高星 | 核准即 Top 6 |
| ⚠️ [acryldev/acryl](https://github.com/acryldev/acryl) | 待审 / pending | 239 | — | 32 | 21d | 待审高星 | 核准即榜 #51 |
| ⚠️ [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill) | 已核准 / approved | 2802 | +794 | 201 | 85d | 日增百星 | 日增 +794★ |
| ⚠️ [Aisland-SJL/dsh-worktable](https://github.com/Aisland-SJL/dsh-worktable) | 已核准 / approved | 629 | +15 | 77 | 30d | 冲入 Top 20 | 冲入 Top 20（21→20） |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [dsh-tauri/deepseek-harness-desktop](https://github.com/dsh-tauri/deepseek-harness-desktop) ⚠️ | 2158 | 2026-08-14 | 2026-09-16 | DeepSeek Harness Tauri 桌面版 \| Only 5mb installer, zero environment setup, preset plugins, Windows / macOS / Linux. |
| 2 | [acryldev/acryl](https://github.com/acryldev/acryl) ⚠️ | 239 | 2026-08-25 | 2026-09-16 | ACRYL - Agent Context Relay Yielding Lifecycles. One persistent workspace, one canonical context, any coding agent. |
| 3 | [youdotcom-oss/agent-skills](https://github.com/youdotcom-oss/agent-skills) | 71 | 2026-01-26 | 2026-09-16 | You.com skills and plugins for web search, content extraction, research, finance, and integration discovery, helping AI agents build with up-to-date web context. |
| 4 | [834063245-creator/LantaiAgent](https://github.com/834063245-creator/LantaiAgent) | 25 | 2026-06-14 | 2026-09-16 | I’m a helpful assistant |
| 5 | [Duskriver/dsh-opencode-go](https://github.com/Duskriver/dsh-opencode-go) | 9 | 2026-09-15 | 2026-09-16 | 让你的DSH完美适配opencodeg-go套餐 |
| 6 | [bainianling/dsh-jailbreak-mode](https://github.com/bainianling/dsh-jailbreak-mode) | 8 | 2026-08-20 | 2026-09-16 | DSH Jailbreak Mode standalone plugin — 破甲模式插件（仅学习交流与授权安全研究） |
| 7 | [bychv/dsh-preset-enhance](https://github.com/bychv/dsh-preset-enhance) | 6 | 2026-09-13 | 2026-09-16 | SillyTavern preset mode, macro engine and editor for DeepSeek Harness |
| 8 | [proDreams/dsh-tidewatch](https://github.com/proDreams/dsh-tidewatch) | 6 | 2026-09-16 | 2026-09-16 | A floating peak/off-peak tide card for DeepSeek Harness: i18n (en/zh/ru), local-time windows, session cost. |
| 9 | [builtin-pb/dsh-developer](https://github.com/builtin-pb/dsh-developer) | 5 | 2026-08-31 | 2026-09-16 | The single plugin you need for DSH — build, test, diagnose, and maintain DeepSeek Harness plugins and core. |
| 10 | [smilewhenever777/dsh-scholar](https://github.com/smilewhenever777/dsh-scholar) | 5 | 2026-09-12 | 2026-09-16 | DSH(DeepSeek Harness) 自研插件集:学者工作台(文献库/精读/知识图谱/Idea卡片) + 服务器看板(GPU监控) + 研究主线图(DAG/实验台账) |
| 11 | [lishize20040802-rgb/useful-dsh-plugins](https://github.com/lishize20040802-rgb/useful-dsh-plugins) | 3 | 2026-08-13 | 2026-09-16 | Third-party DeepSeek Harness plugins with local speech recognition, portable installation and lifecycle management |
| 12 | [LitoMore/agent-discord-presence](https://github.com/LitoMore/agent-discord-presence) | 3 | 2026-09-15 | 2026-09-16 | Discord Rich Presence for Codex, Claude Code, OpenCode, Pi, and DeepSeek Harness, powered by one local service that keeps your active work visible in Discord. |
| 13 | [drscrewdriver/dsh-date-wrapper](https://github.com/drscrewdriver/dsh-date-wrapper) | 2 | 2026-09-08 | 2026-09-16 | Minimal date line for the DeepSeek Harness runtime-context snapshot: 'Current date: 2026-09-08 Asia/Shanghai Tuesday' (46 chars) - a cordis host plugin, no dsh source changes |
| 14 | [Kanadego/dsh-heartbeat](https://github.com/Kanadego/dsh-heartbeat) | 2 | 2026-09-06 | 2026-09-16 | 一个致力于让Agent在日常交流中更加拥有“活人感”的DSH插件。 |
| 15 | [Kihara777/dsh-api-balance](https://github.com/Kihara777/dsh-api-balance) | 2 | 2026-09-16 | 2026-09-16 | API 用量余额插件 for DeepSeek Harness — webui 用量圆圈内提供「用量 / 余额」标签切换，展示账户余额与用量明细 |
| 16 | [zhang66633/.dsh-plugin-installer](https://github.com/zhang66633/.dsh-plugin-installer) | 2 | 2026-08-14 | 2026-09-16 | DeepSeek Harness（dsh）的插件商店 + 安装助手：在 Web GUI 里逛插件目录，一键确认安装，agent 替你装好。 |
| 17 | [Aik358/dsh-memory-fitting](https://github.com/Aik358/dsh-memory-fitting) | 1 | 2026-09-16 | 2026-09-16 | Intent fitting for DSH: the agent predicts a few directions, asks in batches, and converges one — before it acts. 记忆拟合：先立靶子再问，收敛后提案待确认。 |
| 18 | [catcatchcatast/dsh-remote-hosts](https://github.com/catcatchcatast/dsh-remote-hosts) | 1 | 2026-09-09 | 2026-09-16 | DeepSeek Harness (DSH) remote hosts / remote plugin / multi-host Web & Desktop. DSH 远程插件、多主机远程开发。0.1.5-rc.2 Preview; not stable 0.1.5. Contact: catcatchcatast@gmail.com |
| 19 | [cordisplugins/dsh-cordis](https://github.com/cordisplugins/dsh-cordis) | 1 | 2026-09-08 | 2026-09-16 | dsh-cordis |
| 20 | [CroissanTTs/dsh-bailian-models](https://github.com/CroissanTTs/dsh-bailian-models) | 1 | 2026-09-13 | 2026-09-16 | [百炼（DashScope）模型目录预置插件]Alibaba Bailian (DashScope) model catalog preset for DeepSeek Harness — 36 models with per-family reasoning effort adaptation, context windows, and auto-adaptation of existing Bailian routes. |
| 21 | [CroissanTTs/dsh-effort-slider](https://github.com/CroissanTTs/dsh-effort-slider) | 1 | 2026-09-13 | 2026-09-16 | [推理强度滑动调节插件]Reasoning effort slider for DeepSeek Harness — a per-session UI that lets users adjust reasoning intensity with a polished slider, shown for any model that declares reasoning efforts. |
| 22 | [CyraZm49/dsh-shutdown](https://github.com/CyraZm49/dsh-shutdown) | 1 | 2026-09-16 | 2026-09-16 | Shutdown button for the DeepSeek Harness (dsh) web GUI — close the panel and the server process from inside the app. |
| 23 | [developerdh/dsh-jenkins-panel](https://github.com/developerdh/dsh-jenkins-panel) | 1 | 2026-09-16 | 2026-09-16 | 向dsh中集成Jenkins相关工具和面板，支持在dsh直接触发构建任务、查询日志、通过面板查看jenkins任务构建状态、实时日志跟踪等相关操作。 |
| 24 | [drscrewdriver/dsh-context-compression-improved](https://github.com/drscrewdriver/dsh-context-compression-improved) | 1 | 2026-09-05 | 2026-09-16 | Improved fork of dsh-context-compression-selector with an orthogonal code-skeleton compression gate |
| 25 | [fashionmascherine-svg/formalswarm](https://github.com/fashionmascherine-svg/formalswarm) | 1 | 2026-09-15 | 2026-09-16 | Multi-agent validation for any repository: independent theses, adversarial critics, and a seal whose verdict is computed from real command exit codes — never from an agent's prose. One body, three runtimes: DeepSeek Harness, Claude Code, ZCode. |
| 26 | [fourzkw/dsh-drawai](https://github.com/fourzkw/dsh-drawai) | 1 | 2026-09-15 | 2026-09-16 | DSH 右侧栏里的可编辑画布 —— 加上让模型直接改图的两个工具 |
| 27 | [GooDAnDReaDY/dsh-key-limits](https://github.com/GooDAnDReaDY/dsh-key-limits) | 1 | 2026-09-15 | 2026-09-16 | DeepSeek Harness plugin: API key / subscription quota limits (float chip, composer bar, settings). |
| 28 | [huuthuan-nguyen/dsh-tgrep](https://github.com/huuthuan-nguyen/dsh-tgrep) | 1 | 2026-09-16 | 2026-09-16 | ⚡️ Ultra-fast trigram-indexed code search for DeepSeek Harness powered by Microsoft tgrep. |
| 29 | [JonyChan1350/dsh-llm-balance](https://github.com/JonyChan1350/dsh-llm-balance) | 1 | 2026-08-17 | 2026-09-16 | Show LLM API balances under the chat input: DeepSeek, OpenRouter, SiliconFlow and any custom provider with a balance endpoint. DSH plugin. |
| 30 | [MARIOMLY/dsh-pdf-translate](https://github.com/MARIOMLY/dsh-pdf-translate) | 1 | 2026-09-16 | 2026-09-16 | 新增DSH 侧栏「翻译」面板：丢入英文电子版 PDF，先量出原件的版式（页边距/字号/行距/强调色/页眉页脚位置）再照着重排，产出保版式的中文版 PDF + md；另提供 pdf_translate 模型工具。 |
| 31 | [more-nico/dsh-nico-theme](https://github.com/more-nico/dsh-nico-theme) | 1 | 2026-08-26 | 2026-09-16 | Nico glass theme for the DeepSeek Harness web UI - panel glass rendered by nico-glass-kit. Not affiliated with DeepSeek. |
| 32 | [QuantumKuba/dsh-webstack](https://github.com/QuantumKuba/dsh-webstack) | 1 | 2026-09-16 | 2026-09-16 | Advanced SearXNG search & Scrapling stealth fetch provider bundle for DeepSeek Harness  |
| 33 | [rootkiller6788/dsh-plugin-anything](https://github.com/rootkiller6788/dsh-plugin-anything) | 1 | 2026-09-16 | 2026-09-16 | An agent-native compilation & verification pipeline that converts software capabilities such as CLI, APIs, and local services into installable, testable, verifiable DeepSeek Harness plugins. |
| 34 | [s11phere/dsh-away-notify](https://github.com/s11phere/dsh-away-notify) | 1 | 2026-09-16 | 2026-09-16 | dsh 插件：离开 dsh 页面时可收到桌面通知，点击回到对应会话。Windows / WSL 原生 Toast，零依赖。 |
| 35 | [Shr-CS/dsh-wechat-channel](https://github.com/Shr-CS/dsh-wechat-channel) | 1 | 2026-09-16 | 2026-09-16 | 微信公众号通道插件：在微信里发消息操控 DeepSeek Harness，结果经客服消息接口推回微信。回调签名校验 + openid 白名单，零运行时依赖。 |
| 36 | [victorwads/dsh-live-voice](https://github.com/victorwads/dsh-live-voice) | 1 | 2026-09-14 | 2026-09-16 | Local-first voice conversations for DSH. Run speech recognition and speech synthesis on your own machine, with optional external providers. |
| 37 | [wawo77/dsh-opencode-go-usage](https://github.com/wawo77/dsh-opencode-go-usage) | 1 | 2026-09-15 | 2026-09-16 | dsh的桌宠插件，爱吃白饭的可爱大肥鱼 |
| 38 | [yunfeizhu/dsh-pptx-viewer](https://github.com/yunfeizhu/dsh-pptx-viewer) | 1 | 2026-09-15 | 2026-09-16 | PPTX editor integration for DeepSeek Harness |
| 39 | [2507483326/eTeam](https://github.com/2507483326/eTeam) | 0 | 2026-09-16 | 2026-09-16 | 一个增强deepseek harness 的 多成员协作插件 |
| 40 | [activeing123/dsh-mcptoon](https://github.com/activeing123/dsh-mcptoon) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness bundle: mount mcptoon as an MCP server in one command. Tool discovery 71,929 -> 581 tokens across 255 tools (-99.2%, measured); encoding is lossless. |
| 41 | [avdergh/poe2-exile-architect](https://github.com/avdergh/poe2-exile-architect) | 0 | 2026-07-10 | 2026-09-16 | Research, create, and understand Path of Exile 2 builds with AI agents and Path of Building. |
| 42 | [black970/dsh-quota-viewer](https://github.com/black970/dsh-quota-viewer) | 0 | 2026-09-16 | 2026-09-16 | DSH 侧边栏额度面板：DeepSeek 官方余额、jojo code、SCNet、方舟 Coding Plan 用量窗口，含 90 天本地历史与趋势图。Multi-provider quota panel for DeepSeek Harness. |
| 43 | [BPTumbleweed/dsh-agent-memory](https://github.com/BPTumbleweed/dsh-agent-memory) | 0 | 2026-09-16 | 2026-09-16 | DSH 长期记忆插件 + 配套 CLI：实时采集对话证据、只读数据浏览、会话内工作状态面板。零运行时依赖、能力探测与熔断，面向跨版本升级设计；不接管偏好注入（留给官方 agent-instructions）。 |
| 44 | [BPTumbleweed/dsh-pin-session](https://github.com/BPTumbleweed/dsh-pin-session) | 0 | 2026-09-16 | 2026-09-16 | DSH「置顶对话」插件：会话头部与会话行内一键 📌，把重要对话钉在侧栏分组顶部。宿主端只存事实（原子写 JSON + 信任栅栏内的 HTTP 接口 + 配套 CLI），排序由客户端在 DOM 层完成——因为侧栏顺序由浏览器本地排序表优先决定，宿主端挪顺序在界面上无效。零运行时依赖、能力探测与熔断，面向跨版本升级设计。 |
| 45 | [BPTumbleweed/dsh-session-retitle](https://github.com/BPTumbleweed/dsh-session-retitle) | 0 | 2026-09-16 | 2026-09-16 | DSH 会话重命名插件：会话头部一个「重命名」按钮，手动触发时读取本会话内容、用当前模型起中文短标题并写回会话名。零运行时依赖，改名走官方 session-title 服务，含候选路由回退与同会话并发保护。 |
| 46 | [CHIP-PHILO-GH/dsh-loop-breaker](https://github.com/CHIP-PHILO-GH/dsh-loop-breaker) | 0 | 2026-09-15 | 2026-09-16 | DSH 插件：流式复读熔断 —— 在流式输出里边收边判，命中退化复读就地掐断并消毒正文，避免白烧 token。 |
| 47 | [CHIP-PHILO-GH/dsh-mcu-lab](https://github.com/CHIP-PHILO-GH/dsh-mcu-lab) | 0 | 2026-09-15 | 2026-09-16 | DSH 插件：51 单片机开发闭环 —— Keil / 免费 SDCC 编译 + Proteus 仿真 + 确定性判定，含不依赖商业软件的离线判定后端。 |
| 48 | [CHIP-PHILO-GH/dsh-session-namer](https://github.com/CHIP-PHILO-GH/dsh-session-namer) | 0 | 2026-09-15 | 2026-09-16 | DSH 客户端插件：新建会话时先让你命名（带字节安全截断与草稿预览），替代默认的自动标题。 |
| 49 | [CHIP-PHILO-GH/dsh-session-search](https://github.com/CHIP-PHILO-GH/dsh-session-search) | 0 | 2026-09-15 | 2026-09-16 | DSH 插件：跨会话内容检索 —— 按关键词搜历史会话正文，带本地索引与预热，零第三方依赖。 |
| 50 | [CHIP-PHILO-GH/dsh-turn-cost](https://github.com/CHIP-PHILO-GH/dsh-turn-cost) | 0 | 2026-09-15 | 2026-09-16 | DSH 插件：在本轮统计与回合尾部显示花费的人民币金额，只读既有槽位与用量事件，不改宿主。 |
| 51 | [CJ-SH/dsh-plugin-ollama-usage](https://github.com/CJ-SH/dsh-plugin-ollama-usage) | 0 | 2026-09-16 | 2026-09-16 | Ollama Cloud account usage for the dsh web chat: composer dock panel, hero panel, and a Plugin configuration card. |
| 52 | [CJ-SH/dsh-plugin-trellis-statusline](https://github.com/CJ-SH/dsh-plugin-trellis-statusline) | 0 | 2026-09-15 | 2026-09-16 | Shows the active Trellis task of the current workspace in the dsh web chat, with parent/subtask roles and a clickable task tree. |
| 53 | [ckk-09/dsh-refix](https://github.com/ckk-09/dsh-refix) | 0 | 2026-09-16 | 2026-09-16 | Self-diagnosing, self-repairing, self-iterating dynamic plugin for DSH (DeepSeek Harness). DSH 自诊断·自修复·自迭代插件 |
| 54 | [Cloudto1/dsh-approval-chime](https://github.com/Cloudto1/dsh-approval-chime) | 0 | 2026-09-16 | 2026-09-16 | DSH 审批提示音插件：宿主向你申请权限的那一刻响一声，音量、音色、开关都在「设置 → 通知提醒」里调。内置风铃、铃铛、蜂鸣三种合成音色，支持试听与恢复默认，还能导入本地音频（≤5MB、最多 50 个）当音色；WebAudio 现场合成、不加载音频文件，配置持久化到宿主设置文档，另附已触发次数与上次触发时间，静音环境下也能自证是否生效。 |
| 55 | [cordisplugins/cordis-plugin-graph](https://github.com/cordisplugins/cordis-plugin-graph) | 0 | 2026-09-10 | 2026-09-16 | DSH/Cordis Web plugin: a zoomable relation graph of every loaded plugin (dependencies, resolved providers, Loader-tree nesting) as a Settings tab next to 'Plugin list'. |
| 56 | [cordisplugins/pi-cordis](https://github.com/cordisplugins/pi-cordis) | 0 | 2026-09-09 | 2026-09-16 | pi-cordis |
| 57 | [Crash0524/Timeseries-Workbench-DSH](https://github.com/Crash0524/Timeseries-Workbench-DSH) | 0 | 2026-09-14 | 2026-09-16 | 为时序工作者提供的时序工作台 |
| 58 | [CroissanTTs/dsh-voice-mini](https://github.com/CroissanTTs/dsh-voice-mini) | 0 | 2026-09-16 | 2026-09-16 | Voice-feedback plugin for DeepSeek Harness: speak tool, verbalizer, per-session voices, chimes, monitoring, native pet. zh/en i18n. |
| 59 | [CynicismBoyJYD/dsh-protect-eyes-skin](https://github.com/CynicismBoyJYD/dsh-protect-eyes-skin) | 0 | 2026-09-16 | 2026-09-16 | DSH-protect-eyes-skin - an eye-friendly green theme for DeepSeek Harness (full --dsw-* design-token reskin, light + dark). |
| 60 | [CZ-ZL/duo](https://github.com/CZ-ZL/duo) | 0 | 2026-09-13 | 2026-09-16 | DSH plugin for testing and comparing candidate changes, with recorded results, decisions and costs. Adoption remains under user control. / 在 DSH 中测试和比较候选修改，记录结果、选择依据与费用；是否采用由用户决定。 |
| 61 | [drscrewdriver/dsh-canvas-tsx-sidebar](https://github.com/drscrewdriver/dsh-canvas-tsx-sidebar) | 0 | 2026-09-15 | 2026-09-16 | DSH 侧边栏插件：把 Qoder Canvas `*.canvas.tsx` 静态解析为结构化报告页，在 dsh-better-sidebar 右侧栏渲染（文件查看器接管 + 页签）。纯静态管线，不执行源码。附 writing-qoder-canvas skill。｜ Render Qoder Canvas `.canvas.tsx` reports in the DSH right sidebar. Static parse only — no code execution. |
| 62 | [drscrewdriver/dsh-patch-edit-plus](https://github.com/drscrewdriver/dsh-patch-edit-plus) | 0 | 2026-09-13 | 2026-09-16 | Patch-style file editing for DeepSeek Harness: one apply_patch tool for git/unified diff (default) and Codex apply_patch syntax (opt-in), all-or-nothing application, 0.1.2-rc.1 ~ 0.1.5-rc.2 compatible. |
| 63 | [drscrewdriver/dsh-session-steward](https://github.com/drscrewdriver/dsh-session-steward) | 0 | 2026-09-14 | 2026-09-16 | DSH 会话管家：会话历史文件（病案室）与健康检查（体检→处方→出院），给异常会话做投影级体检与可逆修复 |
| 64 | [Edisonzszs/web-clone](https://github.com/Edisonzszs/web-clone) | 0 | 2026-09-10 | 2026-09-16 | 网站复刻 / 克隆方法论。USE WHEN 用户说 复刻网站、克隆网站、clone website、抄个站、仿站、 照着这个站做一个、reproduce site、还原某个网页效果、把这个站搬下来改成我的、 复刻某个交互/WebGL/Canvas/Three.js 效果。提供「先拿真源码 → 判路径 → 逆向拆解 → 搭工程 → 替换内容」的可移植决策树，覆盖静态站 / React-Vue-Next 内容站 / WebGL-Canvas 重前端站三大分支，并强制核对任何 AI 二手分析里的可执行代码。 |
| 65 | [Elevator14B/vscode-dsh-sidebar](https://github.com/Elevator14B/vscode-dsh-sidebar) | 0 | 2026-09-16 | 2026-09-16 | VS Code sidebar for DeepSeek Harness: native session tree, file and diff navigation, drag-to-reference, clipboard and theme bridges. |
| 66 | [EPCN-fla/dsh-observational-memory](https://github.com/EPCN-fla/dsh-observational-memory) | 0 | 2026-09-16 | 2026-09-16 | Observational memory for DeepSeek Harness: background observers distill session work into observations and durable reflections, so long sessions survive compaction with their decisions intact. |
| 67 | [erha2777/dsh-azure-maid-skin](https://github.com/erha2777/dsh-azure-maid-skin) | 0 | 2026-09-16 | 2026-09-16 | 蓝瓷女仆 · Azure Maid —— DSH Web GUI 主题皮肤。配色取自社区挂件 DeepSeek-Balance-Whale-Widget 的蓝发女仆形象：深蓝发色做品牌与交互、蕾丝冷白做正文与画布、发间青宝石做链接与强调。覆盖 90 个语义 token，亮暗各一套，支持亮色 / 暗色 / 跟随系统三种偏好切换。零运行时依赖。 |
| 68 | [erya2000/dsh-session-budget-guard](https://github.com/erya2000/dsh-session-budget-guard) | 0 | 2026-09-16 | 2026-09-16 | dsh-session-budget-guard |
| 69 | [Ethereal-ljq/dsh-prompt-toolkit](https://github.com/Ethereal-ljq/dsh-prompt-toolkit) | 0 | 2026-09-16 | 2026-09-16 | DSH Web 提示词工作台：把输入框里的草稿优化成一条可直接执行的命令（引擎 fork 自 WestFox-AwA/dsh-prompt-optimizer，BSD-3-Clause，署名保留） |
| 70 | [Exagone313/dsh-podman](https://github.com/Exagone313/dsh-podman) | 0 | 2026-08-30 | 2026-09-16 | Podman-backed execution for DeepSeek Harness (dsh) |
| 71 | [fengbinmov/dsh-git-panel](https://github.com/fengbinmov/dsh-git-panel) | 0 | 2026-09-16 | 2026-09-16 | DSH Web GUI 的 Git 面板插件：在会话界面的标签栏里，紧挨「对话 / 轨迹」再加一个 Git 页， 用来完成日常的查看改动、暂存、提交、看 diff、翻历史、切分支和推拉。 |
| 72 | [Gabrip780/dsh-hidden-paths](https://github.com/Gabrip780/dsh-hidden-paths) | 0 | 2026-09-15 | 2026-09-16 | Deny an AI agent access to .env files, credential stores, keys and any path you hide — across file tools, shell commands, search selectors and run_code. A DeepSeek Harness (dsh) plugin. |
| 73 | [gankudadiz/dsh-reclaim](https://github.com/gankudadiz/dsh-reclaim) | 0 | 2026-09-16 | 2026-09-16 | 审计并安全回收 DSH 占用的空间：看清会话、附件与缓存各占多少、还被谁引用，清理一律进可恢复的隔离区（DeepSeek Harness 插件） |
| 74 | [GGboya/dsh-paper-reader](https://github.com/GGboya/dsh-paper-reader) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness (dsh) 插件:论文伴读工作台 —— PDF 转录 / 检索 / 流式问答 + 内置阅读器页面。 |
| 75 | [gunduziba/dsh-tool-open-in-idea](https://github.com/gunduziba/dsh-tool-open-in-idea) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness (DSH) 官方原生侧边栏与界面专属的 IntelliJ IDEA 直连与文件跳转插件，基于 Streamable HTTP MCP 协议 |
| 76 | [HandsYe/dsh-llm-motomoto](https://github.com/HandsYe/dsh-llm-motomoto) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness bundle for MotoMoto's OpenAI-compatible endpoint: pi-ai provider route + Settings status card |
| 77 | [HandsYe/dsh-remote-status](https://github.com/HandsYe/dsh-remote-status) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness 插件：侧边栏底部本地/远程状态芯片 + 远程镜像工作区标题自动标记（目录 ⇄ 机器名） |
| 78 | [hasan-aghayev/dsh-task-orchestrator](https://github.com/hasan-aghayev/dsh-task-orchestrator) | 0 | 2026-09-15 | 2026-09-16 | Automatic plan-first role delegation for DeepSeek Harness with dependency-aware workers and final review |
| 79 | [hoyyang/dsh-agent-billing](https://github.com/hoyyang/dsh-agent-billing) | 0 | 2026-09-16 | 2026-09-16 | Agent billing & usage observability for DeepSeek Harness — 会话日志直扫记账 / per-window 实时徽标 / 多账号费率档案 / 预算告警 |
| 80 | [hoyyang/dsh-android-pane](https://github.com/hoyyang/dsh-android-pane) | 0 | 2026-09-16 | 2026-09-16 | Live Android device pane for DeepSeek Harness: scrcpy H.264 streaming, agent injection, UI-tree verification |
| 81 | [Iambatman1928/dsh-xingye](https://github.com/Iambatman1928/dsh-xingye) | 0 | 2026-09-16 | 2026-09-16 | Chat agent for a DeepSeek Harness session: characters and personas, several archive threads per character, an undoable/rewindable local transcript, and an event book. |
| 82 | [Jindom/dsh-bitwarden](https://github.com/Jindom/dsh-bitwarden) | 0 | 2026-09-16 | 2026-09-16 | Bitwarden/Vaultwarden credentials in every DSH session: vault tools + proactive prompt guidance + a settings card for the master password. |
| 83 | [Johnnylin2121/dsh-agent](https://github.com/Johnnylin2121/dsh-agent) | 0 | 2026-08-13 | 2026-09-16 | DSH（DeepSeek Harness）个人技能库：21 个 skill + 插件配置/补丁备份 + push 防护（隐私扫描钩子） |
| 84 | [Johnnylin2121/dsh-agent-presets](https://github.com/Johnnylin2121/dsh-agent-presets) | 0 | 2026-08-14 | 2026-09-16 | DSH agent preset 配置：amazon-desk（亚马逊）与 trading-desk（A股交易台） |
| 85 | [KaguraSayuki/dsh-file-download](https://github.com/KaguraSayuki/dsh-file-download) | 0 | 2026-09-16 | 2026-09-16 | Authenticated browser download for the DSH Web GUI: stream session-workspace files to the browser from the official deliverables row, delivered-file cards, and the sidebar file tree. Remote-friendly, no host desktop required. |
| 86 | [kira905/dsh-butler-archive](https://github.com/kira905/dsh-butler-archive) | 0 | 2026-09-11 | 2026-09-16 | Unofficial DSH plugin: archive, browse, restore and delete idle sessions from the sidebar — zero dependencies. 非官方 DSH 插件：把闲置会话归档、浏览、恢复、删除，零依赖。 |
| 87 | [Kuntey/dsh-session-delete](https://github.com/Kuntey/dsh-session-delete) | 0 | 2026-09-16 | 2026-09-16 | Permanently delete DSH sessions from the file system, right from the sidebar conversation menu — 在 DSH 侧边栏菜单真正物理删除会话，而非归档隐藏。 |
| 88 | [lishize20040802-rgb/dsh-rigor-4](https://github.com/lishize20040802-rgb/dsh-rigor-4) | 0 | 2026-09-16 | 2026-09-16 | Rigor 4 community agent plugin for DeepSeek Harness, with portable install and uninstall workflows |
| 89 | [liujuntao123/dsh-trusted-page](https://github.com/liujuntao123/dsh-trusted-page) | 0 | 2026-09-16 | 2026-09-16 | DSH (DeepSeek Harness) Web 远程受信访问插件：设置面板可视化配置受信域名，联动 /api 放行与页面受信判定，修复远程 Models/设置页 settings are unavailable in this browser |
| 90 | [liyixuan201211/nightshift](https://github.com/liyixuan201211/nightshift) | 0 | 2026-09-16 | 2026-09-16 | Run an agent unattended for hours and get a morning brief that is an audit, not a summary. Signs a manifest before the work, prices every step at the execution boundary, rolls back a failed verification, and reports what the gate refused. DSH plugin + skill, zero dependencies. |
| 91 | [loyalchiiina/dsh-archive-manager-plus](https://github.com/loyalchiiina/dsh-archive-manager-plus) | 0 | 2026-09-16 | 2026-09-16 | DSH 归档会话增强版 fork：收藏与一键删除未收藏、置顶会话、按对话轮次排序、复制会话 ID 与转录路径、界面排版重整。基于 MichengAI/dsh-archive-manager v0.1.40（Apache-2.0） |
| 92 | [loyalchiiina/dsh-voice-alert](https://github.com/loyalchiiina/dsh-voice-alert) | 0 | 2026-09-16 | 2026-09-16 | DSH 对话语音/音效播报插件：每个 turn 结束自动提醒，出错播失败提示；内置 20 个音效（提醒 10 + 大自然 10）零配置开箱即用，也可用火山「声音复刻」克隆自己的音色。 |
| 93 | [masknull/dsh-workbuddy-connect](https://github.com/masknull/dsh-workbuddy-connect) | 0 | 2026-09-16 | 2026-09-16 | 将 WorkBuddy（国内版 / 国际版）的模型接入 DeepSeek Harness —— 插件自带浏览器登录，无需 WorkBuddy 桌面 App。WorkBuddy CN & international models for DeepSeek Harness; the plugin signs itself in. 支持 DSH 0.1.5-rc.1+。 |
| 94 | [mays-hi/dsh-git-idea](https://github.com/mays-hi/dsh-git-idea) | 0 | 2026-09-16 | 2026-09-16 | A git panel inside the DSH session: repository chip, branch tree, commit graph, working tree and commit detail, Settings page, and 8 git model tools. |
| 95 | [moziforge/calendar-plugins](https://github.com/moziforge/calendar-plugins) | 0 | 2026-09-16 | 2026-09-16 | DSH plugins that connect agents to calendar providers: iCloud Calendar over CalDAV, with recurring events expanded and a normalized event shape. |
| 96 | [Mrtime-gege/dsh-agent-shell](https://github.com/Mrtime-gege/dsh-agent-shell) | 0 | 2026-09-12 | 2026-09-16 | Persistent interactive tmux shells for DeepSeek Harness (DSH) — 7 model tools, floating panel, hash-chained audit, consent gate. |
| 97 | [neltharion11/dsh-luxar-embedding](https://github.com/neltharion11/dsh-luxar-embedding) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness plugin for ESP-IDF and STM32CubeMX embedded development |
| 98 | [pan17/dsh-tool-manager](https://github.com/pan17/dsh-tool-manager) | 0 | 2026-09-15 | 2026-09-16 | DSH 工具管理插件：按 Agent Preset 开关和分组工具，像 Skill 一样按需加载工具，减少模型上下文占用。 |
| 99 | [POPCORNBOOM/dsh-insight-dock](https://github.com/POPCORNBOOM/dsh-insight-dock) | 0 | 2026-09-15 | 2026-09-16 | Insight dock for the DSH Web GUI: an agent parks a short, strictly-bounded side observation while it works; you decide later whether to hear it. |
| 100 | [Psynosaur/dsh-token-gobbler](https://github.com/Psynosaur/dsh-token-gobbler) | 0 | 2026-09-04 | 2026-09-16 | Benchmark any model, whilst using DSH |
| 101 | [RangeKing/dsh-whale-buddy](https://github.com/RangeKing/dsh-whale-buddy) | 0 | 2026-09-16 | 2026-09-16 | 🐋 A quietly alive DeepSeek whale for DeepSeek Harness Web: an inline thinking whale and a right-edge Whale Dock. 一只静谧灵动的 DeepSeek 小鲸鱼：行内思考伴随，侧边常驻交互。 |
| 102 | [rhczz/dsh-plugin-ui-font-family](https://github.com/rhczz/dsh-plugin-ui-font-family) | 0 | 2026-09-16 | 2026-09-16 | 给 DeepSeek Harness 的 Web 界面换字体。 Change the font for the DeepSeek Harness web interface. |
| 103 | [Saunato/dsh-mac-cua](https://github.com/Saunato/dsh-mac-cua) | 0 | 2026-09-16 | 2026-09-16 | Computer Use for macOS in DeepSeek Harness: control desktop apps through the Accessibility API, driven by a persistent JavaScript REPL. |
| 104 | [shiyan688/dsh-novel-craft](https://github.com/shiyan688/dsh-novel-craft) | 0 | 2026-09-16 | 2026-09-16 | 禁AI腔清单能让模型不像 AI，这个插件让它像你：把候选稿摊开成连续正文，作者只点 👍/👎，标注压成可复用的写作规律——只有规律进模型上下文，原文另存不进上下文。（DeepSeek Harness 插件） |
| 105 | [skyyyyyk/dsh-szg-hint](https://github.com/skyyyyyk/dsh-szg-hint) | 0 | 2026-09-15 | 2026-09-16 | Sidecar hints for a running DSH task: host plugin + web client, gated by the host trust fence. |
| 106 | [tanweiping1012-source/DramaPilot](https://github.com/tanweiping1012-source/DramaPilot) | 0 | 2026-09-16 | 2026-09-16 | 基于 DeepSeek Harness 的短剧本地化 Agent 离线原型：角色视觉、语言表演与文化改编。 |
| 107 | [Tiaoma123/dsh-followup-todo](https://github.com/Tiaoma123/dsh-followup-todo) | 0 | 2026-09-15 | 2026-09-16 | Cross-session follow-up todo list for DeepSeek Harness |
| 108 | [ubggyhjb/dsh-mathmodel-v7](https://github.com/ubggyhjb/dsh-mathmodel-v7) | 0 | 2026-09-16 | 2026-09-16 | 数学建模竞赛 Agent（DeepSeek Harness preset）v7：CUMCM 国赛专项，资产接管→Discovery+竞争搜索→方法学契约→代码图表→编辑/视觉证据链→论文→全门禁验收，含 CUMCM Typst/LaTeX 双模板与 2026 国赛规则 authority |
| 109 | [viyiviyi/dsh-quiet-mode](https://github.com/viyiviyi/dsh-quiet-mode) | 0 | 2026-09-16 | 2026-09-16 | 少点废话 |
| 110 | [vlozg/dsh-autoresearch](https://github.com/vlozg/dsh-autoresearch) | 0 | 2026-09-15 | 2026-09-16 | Metric-driven autonomous experiment loop for DeepSeek Harness: the agent proposes, benchmarks, keeps or discards, and repeats, with a live dashboard sidebar. pi-autoresearch compatible. |
| 111 | [wangzhanchao883/dsh-word-vault](https://github.com/wangzhanchao883/dsh-word-vault) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness plugin: multi-user English vocabulary bank - copy text, pick the user in a popup at the mouse position, LLM translation, SQLite counting, plus printable cards and a quiz loop. 自研 DSH 插件：多用户英语生词库（复制后在鼠标处弹窗点选入库 / LLM 翻译 / SQLite 计次 / 可打印记忆卡与考试闭环） |
| 112 | [wendou-chen/dsh-render-perf](https://github.com/wendou-chen/dsh-render-perf) | 0 | 2026-09-16 | 2026-09-16 | DSH Web 公式渲染性能治理：运行时注入公式渲染结果缓存（不改安装目录）+ 视口外渲染跳过。实测长会话切换卡顿 1832ms → 455ms（-75%） |
| 113 | [xiazhi88/dshgo](https://github.com/xiazhi88/dshgo) | 0 | 2026-09-15 | 2026-09-16 | DSH Go —— 在手机/平板上用 DeepSeek Harness。Android App + 让电脑可达的 DSH 插件。 |
| 114 | [yixiuzhemu/Assistant-Manager](https://github.com/yixiuzhemu/Assistant-Manager) | 0 | 2026-09-15 | 2026-09-16 | 助手管理器 |
| 115 | [yuanyiHY/dsh-rail-equalizer](https://github.com/yuanyiHY/dsh-rail-equalizer) | 0 | 2026-09-16 | 2026-09-16 | Make DSH's turn-navigator rail react to system audio in real time (Windows). WASAPI loopback capture via koffi - no permission prompt, no microphone, no screen recording; the browser half injects one stylesheet and CSS variables and never patches the official component. |
| 116 | [yudaxia1/dsh-sidebar-file-menu](https://github.com/yudaxia1/dsh-sidebar-file-menu) | 0 | 2026-09-16 | 2026-09-16 | 为 DeepSeek Harness Web UI 右侧栏文件树提供 VS Code 风格右键菜单：复制绝对/相对路径与名称、在资源管理器或 Finder 中显示、用默认程序打开。通过 extension 优先级带原地接管内置 files 标签页，不新增 tab，卸载即还原。 |
| 117 | [YuZtArt/dsh-plugin-background-browser](https://github.com/YuZtArt/dsh-plugin-background-browser) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness 后台浏览器插件：Playwright MCP 自动操作、会话隔离、侧栏共享交互，AI 操作优先。适配 DSH 0.1.5-rc.2，中文文档。 |
| 118 | [zaimokuza-yoshiteru/dsh-agent-teams-office](https://github.com/zaimokuza-yoshiteru/dsh-agent-teams-office) | 0 | 2026-09-16 | 2026-09-16 | Office views for DSH Agent Teams. |
| 119 | [zeta987/dsh-notify-zeta](https://github.com/zeta987/dsh-notify-zeta) | 0 | 2026-09-15 | 2026-09-16 | DeepSeek Harness notification center with interactive Windows question and approval cards |
| 120 | [zhangzhangco/dsh-tier-router](https://github.com/zhangzhangco/dsh-tier-router) | 0 | 2026-09-16 | 2026-09-16 | Automatic tier-based model routing for DeepSeek Harness (dsh): a virtual `smart` model classifies every request by difficulty (hard / normal / easy) and by vision need, then delegates it to the models you already configured. |
| 121 | [zhengjy01/dsh-qqmail](https://github.com/zhengjy01/dsh-qqmail) | 0 | 2026-09-16 | 2026-09-16 | QQ Mail (and any IMAP/SMTP mailbox) for DeepSeek Harness — qqmail_* agent tools, a qqmail CLI, a qqmail-mcp stdio MCP server, and a web settings panel. IMAP/SMTP with a QQ Mail authorization code (no OAuth, no 2FA redirect). |
| 122 | [zhiheng-zhang-Mera/dsh-health-scheduler](https://github.com/zhiheng-zhang-Mera/dsh-health-scheduler) | 0 | 2026-09-15 | 2026-09-16 | DSH plugin: device/runtime health monitoring, restart-pressure scoring, maintenance scheduling and action decisions for DeepSeek Harness. It never restarts anything itself. |
| 123 | [zhiheng-zhang-Mera/dsh-restart](https://github.com/zhiheng-zhang-Mera/dsh-restart) | 0 | 2026-09-15 | 2026-09-16 | DSH plugin: safe restart execution for DeepSeek Harness — request validation, checkpoint gating, restart locking, graceful shutdown, crash-loop breaking and an external supervisor. It never decides when to restart. |
| 124 | [zmm863-commits/dsh-agnes-studio](https://github.com/zmm863-commits/dsh-agnes-studio) | 0 | 2026-09-15 | 2026-09-16 | 🎬 泡泡猫的影视工具 — AI 影视创作工作站：文生图、图生图、文生视频、图生视频、短剧剧本拆解与提示词专家。支持 Agnes / DeepSeek / Qwen / 豆包 / MiniMax / Ollama 六大厂商，全局浮层不堵对话框。 |
| 125 | [zmm863-commits/dsh-client-ui-paopaocat](https://github.com/zmm863-commits/dsh-client-ui-paopaocat) | 0 | 2026-09-15 | 2026-09-16 | 🐱 泡泡猫的奇幻之境主题 — 月光森林、彼岸花、流云与睡着的小猫，为 DSH Web 界面打造的奇幻玻璃拟态皮肤。淡雅/蓝色双风格一键切换，内置 3 首背景音乐并支持上传自己的音乐。 |
| 126 | [zmm863-commits/dsh-desktop-pack](https://github.com/zmm863-commits/dsh-desktop-pack) | 0 | 2026-08-29 | 2026-09-16 | 泡泡猫 DSH 桌面安装包 — 开箱即用的 DeepSeek Harness 桌面客户端 |
| 127 | [zmm863-commits/dsh-paopaocat-suite](https://github.com/zmm863-commits/dsh-paopaocat-suite) | 0 | 2026-09-01 | 2026-09-16 | 泡泡猫 DSH 插件合集 — 一条命令装好全部精选插件，新手开箱即用 |
| 128 | [zRa1ny/dsh-voice-input-plugin](https://github.com/zRa1ny/dsh-voice-input-plugin) | 0 | 2026-09-16 | 2026-09-16 | dsh-voice-input-plugin |
| 129 | [ZYAONS/dsh-plugin-mascot](https://github.com/ZYAONS/dsh-plugin-mascot) | 0 | 2026-09-16 | 2026-09-16 | DeepSeek Harness mascot plugin - a clickable character sprite (Arknights' Closure / BanG Dream!'s Sengoku Yuno) showing token cache hits, context pressure and account balance. |
| 130 | [ZZJQ678/dsh-global-context](https://github.com/ZZJQ678/dsh-global-context) | 0 | 2026-09-16 | 2026-09-16 | 全局提示词：把一段自定义提示词注入到每个会话系统提示词的最顶部，并在对话视图新增「全局提示词配置」标签页，可随时编辑、保存、清空。 |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- 142475/dsh-esc-stop
- acryldev/cordis-plugin-graph
- Ary66101/dsh-desktop
- Ary66101/dsh-instruction-bubble
- countossbot/dsh-spider
- dsh-tauri-desk/deepseek-harness-desktop
- dugujun3-cloud/dsh-wallpaper
- dugujun3-cloud/dshos-dock
- JonyChan8394/dsh-llm-balance
- PeanutsDou/dsh-selection-tutor
- PeanutsDou/peanut-dsh-plugin
- Socialist-Sister/dsh-deck
- tevenfeng/dsh-plugin-omoslim
- Witherwithwinter/Codinput
- xiazhi88/dsh-lan
- Yagami0502/dsh-composer-pause
- zhang66633/dsh-plugin-installer
