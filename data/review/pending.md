# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-09**
- 快照日期 / Snapshot date: **2026-09-09 (UTC)**
- 待审核 / Pending: **115**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **16**
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

对比上一份快照 **2026-09-08** / vs previous snapshot **2026-09-08**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **4**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [Minglink/dsh-infinite-gen-4](https://github.com/Minglink/dsh-infinite-gen-4) | 待审 / pending | 1181 | +35 | 77 | 24d | 待审高星 | 核准即 Top 12 |
| ⚠️ [LiPu-jpg/Openwrite](https://github.com/LiPu-jpg/Openwrite) | 待审 / pending | 699 | — | 114 | 189d | 待审高星 | 核准即 Top 17 |
| ⚠️ [jigjoy-ai/baro](https://github.com/jigjoy-ai/baro) | 待审 / pending | 120 | — | 10 | 170d | 待审高星 | 核准即榜 #89 |
| ⚠️ [antibrow/dsh-antibrow](https://github.com/antibrow/dsh-antibrow) | 已核准 / approved | 86 | +41 | 0 | 22d | 榜单跃升 | 榜单 200→120 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [Minglink/dsh-infinite-gen-4](https://github.com/Minglink/dsh-infinite-gen-4) ⚠️ | 1181 | 2026-08-15 | 2026-09-09 | DeepSeek v4.1 flash 网络安全红队工具（无限四代） — jailbreak prompts and test suite for DeepSeek    求 Star 收藏 ⭐ |
| 2 | [LiPu-jpg/Openwrite](https://github.com/LiPu-jpg/Openwrite) ⚠️ | 699 | 2026-03-03 | 2026-09-09 | dsh-Openwrite：OpenWrite 的 DeepSeek Harness 小说创作插件，含统一创作 Agent、90 个小说工具、原生工作台与标准审稿 DAG |
| 3 | [jigjoy-ai/baro](https://github.com/jigjoy-ai/baro) ⚠️ | 120 | 2026-03-22 | 2026-09-09 | A CLI that turns a goal into a pull request - and a sandbox for testing concurrent AI coding agents on the Mozaik runtime. |
| 4 | [NoneadChina/dsh-nonead-universal-robots](https://github.com/NoneadChina/dsh-nonead-universal-robots) | 4 | 2026-09-07 | 2026-09-09 | A plugin enabling DSH to directly control Universal Robots (UR) arms using natural language, developed by Nonead Technology based on the self-developed nUR MCP Server's source logic. (Suzhou Nonead Robot Technology Co., Ltd.)  |
| 5 | [Andy8647/dsh-auto-approval](https://github.com/Andy8647/dsh-auto-approval) | 3 | 2026-08-08 | 2026-09-09 | Automode for DeepSeek Harness: a fourth permission preset — full access with an LLM classifier as the only gate before every tool call. |
| 6 | [lansi-ai/dsh-forge](https://github.com/lansi-ai/dsh-forge) | 3 | 2026-08-25 | 2026-09-09 | 把 DeepSeek Harness 做成一个真正的桌面应用：Electron 主进程内嵌 Cordis Host（与官方 Web 版同内核、零移植）， 渲染进程加载官方 Web UI 发行物（file:///自定义协议 + IPC 桥接，不开放 HTTP 端口）， 所有桌面原生能力（托盘、全局热键、系统通知、剪贴板、开机自启、协议唤起、多窗口）以 host 插件 形态注入运行时， 与官方「一切皆插件」的架构同构——不是给网页套壳，而是把桌面能力变成可装配、可卸载、可审查的插件树。  AI 驱动开发声明 |
| 7 | [TNJ2026/promptaflow](https://github.com/TNJ2026/promptaflow) | 3 | 2026-07-08 | 2026-09-09 | Local-first, durable workflow runtime for Agent Apps—compile static Workflow DSL to LangGraph and orchestrate trusted multi-agent execution through Codex, WorkBuddy, DeepSeek Harness, or any MCP client. |
| 8 | [agent-mobile/dsh-mobile](https://github.com/agent-mobile/dsh-mobile) | 2 | 2026-09-08 | 2026-09-09 | Flutter mobile app + Dart wire-protocol SDK for the DeepSeek Harness (dsh) |
| 9 | [AngelosZou/dsh-github-router](https://github.com/AngelosZou/dsh-github-router) | 2 | 2026-08-19 | 2026-09-09 | Read-only GitHub access for agents, wrapping several tools. Inside the tool it automatically probes and selects whichever GitHub access method works locally, and tries network proxies on its own. That cuts down the network and parsing problems an agent may hit when accessing GitHub, and the overhead of it repeatedly trying different approaches. |
| 10 | [MIHassan3/DSH-Launcher](https://github.com/MIHassan3/DSH-Launcher) | 2 | 2026-09-09 | 2026-09-09 | this is a launcher for the official DeepSeek Harness. no modifications it just launches what DeepSeek develops. |
| 11 | [yangwuan55/dsh-accounts](https://github.com/yangwuan55/dsh-accounts) | 2 | 2026-09-09 | 2026-09-09 | DSH 凭据桥接插件：AI 代填登录表单/注入 env 运行 CLI，值不进模型上下文；附网页管理界面 |
| 12 | [173787247/dsh-wsl-fetch](https://github.com/173787247/dsh-wsl-fetch) | 1 | 2026-09-09 | 2026-09-09 | Proxy-aware web_fetch for WSL: official web_fetch through Windows HTTP_PROXY instead of a DNS-pinned public IP. |
| 13 | [acryldev/dsh-cordis](https://github.com/acryldev/dsh-cordis) | 1 | 2026-09-08 | 2026-09-09 | dsh-cordis |
| 14 | [DamonBao/dsh-models-input-modalities](https://github.com/DamonBao/dsh-models-input-modalities) | 1 | 2026-09-09 | 2026-09-09 | DeepSeek Harness Web plugin: per-model input-modality selector (text/image) on the Models settings page for third-party (pi-ai) providers. |
| 15 | [dangpangch/dsh-acp](https://github.com/dangpangch/dsh-acp) | 1 | 2026-09-03 | 2026-09-09 | dsh plugin to run DeepSeek Harness (dsh) agents in Zed’s Agent Panel. |
| 16 | [fiven577/dsh-whale-widget-sankou](https://github.com/fiven577/dsh-whale-widget-sankou) | 1 | 2026-09-08 | 2026-09-09 | DSH 小鲸鱼余额挂件·三口皮肤版 —— 基于 MeteorNOX/DeepSeek-Balance-Whale-Widget（MIT）的修改版：自定义桌宠“三口”形象/语音/不同状态动画，含余额提醒与菜单修复 |
| 17 | [Illuminated2020/dsh-lark-claw](https://github.com/Illuminated2020/dsh-lark-claw) | 1 | 2026-09-04 | 2026-09-09 | Turn DeepSeek Harness into your personal AI claw.将你的DeepSeek Harness变成飞书上的个人龙虾助手。 |
| 18 | [kirbylynx/deepshell-agent](https://github.com/kirbylynx/deepshell-agent) | 1 | 2026-09-09 | 2026-09-09 | A desktop agent powered by DeepSeek Harness. |
| 19 | [kvmem/dsh-super-advisor](https://github.com/kvmem/dsh-super-advisor) | 1 | 2026-09-09 | 2026-09-09 | DSH SuperAdvisor: on-demand second opinions from a stronger model, with editable requests and per-call human approval. |
| 20 | [little-traincar/dsh-imagegen](https://github.com/little-traincar/dsh-imagegen) | 1 | 2026-09-09 | 2026-09-09 | Image generation plugin for DeepSeek Harness — Doubao Seedream 5.0 Pro / qwen-image-3.0-pro, watermark-free, verbatim in-image text, inline chat display. |
| 21 | [lucagiftzek/dsh-artifacts](https://github.com/lucagiftzek/dsh-artifacts) | 1 | 2026-09-09 | 2026-09-09 | An Artifacts tab for the DSH (DeepSeek Harness) web GUI sidebar: lists the files an agent produced and previews them in place, with live reload. |
| 22 | [ManTou-kaya/dsh-voice-input](https://github.com/ManTou-kaya/dsh-voice-input) | 1 | 2026-09-09 | 2026-09-09 | Voice input for the DSH Web composer: browser Web Speech with a Windows offline (System.Speech) fallback. |
| 23 | [NokorinNishikino/Kidai-Hub](https://github.com/NokorinNishikino/Kidai-Hub) | 1 | 2026-09-02 | 2026-09-09 | Kidai Hub (纪代中枢) — 统一承载 Kidai 系列插件界面的容器：侧边栏入口 + 全屏 Hub 页,各插件面板注册进 kidai-hub.tabs。有 Hub 进 Hub,没有 Hub 独立出现。 |
| 24 | [qigelunbiya/DSH-Patrol](https://github.com/qigelunbiya/DSH-Patrol) | 1 | 2026-08-26 | 2026-09-09 | Browser patrol & website inspection plugin for DeepSeek Harness (DSH). Teach once, replay deterministic runbooks with managed Chromium, screenshots, credentials, checkpoints and selector recovery. |
| 25 | [ToLiveAndLove/dsh-tool-adb](https://github.com/ToLiveAndLove/dsh-tool-adb) | 1 | 2026-08-20 | 2026-09-09 | DeepSeek Harness (DSH) plugin exposing Android Debug Bridge (adb) operations as model-facing tools: devices, shell, install, uninstall, screenshot, push/pull, logcat |
| 26 | [weilantianhai/dsh-command-skill-list](https://github.com/weilantianhai/dsh-command-skill-list) | 1 | 2026-09-09 | 2026-09-09 | /skills command for DSH — list skills with auto-translated descriptions (zh↔en) |
| 27 | [winditer/dsh-temp-chat](https://github.com/winditer/dsh-temp-chat) | 1 | 2026-08-18 | 2026-09-09 | A temporary dialogue elf designed specifically for DSH |
| 28 | [winsonpong98-cloud/dsh-distillation-director](https://github.com/winsonpong98-cloud/dsh-distillation-director) | 1 | 2026-09-09 | 2026-09-09 | 蒸馏主管：把一本书蒸馏成可执行 Agent 技能（V4.1 三闸门禁制） |
| 29 | [xiongyishun666-alt/dsh-archived-sessions](https://github.com/xiongyishun666-alt/dsh-archived-sessions) | 1 | 2026-09-09 | 2026-09-09 | DSH 设置面板新增「已归档会话」页：列出全部已归档会话并一键恢复。Settings page listing archived sessions with one-click restore. |
| 30 | [483218131/dsh-composer-collapse](https://github.com/483218131/dsh-composer-collapse) | 0 | 2026-09-09 | 2026-09-09 | Three-mode height manager for the DSH Web composer: auto / pinned open / pinned collapsed. DSH Web 输入框高度三态管理插件。 |
| 31 | [Aafff623/dsh-keyboard-manager](https://github.com/Aafff623/dsh-keyboard-manager) | 0 | 2026-09-06 | 2026-09-09 | Keyboard shortcuts for the DeepSeek Harness Web UI |
| 32 | [acryldev/pi-cordis](https://github.com/acryldev/pi-cordis) | 0 | 2026-09-09 | 2026-09-09 | pi-cordis |
| 33 | [AncientMoon114/dsh-minitui](https://github.com/AncientMoon114/dsh-minitui) | 0 | 2026-09-08 | 2026-09-09 | A  light TUI plugin for Deepseek Harness. |
| 34 | [andregoncalves/dsh-balance](https://github.com/andregoncalves/dsh-balance) | 0 | 2026-08-16 | 2026-09-09 | Provider-aware balance chip for the DeepSeek Harness web sidebar: DeepSeek, OpenRouter, Moonshot/Kimi, Zhipu/GLM, MiniMax. Lightweight, zero runtime deps, no core patches. |
| 35 | [Andy8647/dsh-automode](https://github.com/Andy8647/dsh-automode) | 0 | 2026-09-09 | 2026-09-09 | Automode for DeepSeek Harness: a fourth permission preset — full access with an LLM classifier as the only gate before every tool call. |
| 36 | [artemiroshnichenko/dsh-plugins](https://github.com/artemiroshnichenko/dsh-plugins) | 0 | 2026-09-09 | 2026-09-09 | Production-ready plugins for DeepSeek Harness (DSH): remote SSH agent execution, integrated terminal & file tree, security guardrails, skills & MCP server console. |
| 37 | [asymptotee/dsh-terminal](https://github.com/asymptotee/dsh-terminal) | 0 | 2026-09-07 | 2026-09-09 | Claude Code-style terminal UI plugin for DeepSeek Harness |
| 38 | [azazo1/dsh-copy-session-ref](https://github.com/azazo1/dsh-copy-session-ref) | 0 | 2026-09-09 | 2026-09-09 | 在会话行菜单复制规范 @session mention, 粘贴到输入框即可召回该会话上下文 |
| 39 | [baddying/dsh-geolibre](https://github.com/baddying/dsh-geolibre) | 0 | 2026-09-09 | 2026-09-09 | DeepSeek Harness plugin: render GeoJSON/vector data into an interactive GeoLibre map and let agents operate the live map (layers, styles, view, GeoLibre algorithms and Whitebox WASM tools) through agent tools. |
| 40 | [blauerberg/dsh-subagent-concurrency-limit](https://github.com/blauerberg/dsh-subagent-concurrency-limit) | 0 | 2026-09-05 | 2026-09-09 | Limit concurrent DeepSeek Harness subagent turns and delegation runs |
| 41 | [cjm-m/dsh-paste-code-block](https://github.com/cjm-m/dsh-paste-code-block) | 0 | 2026-09-08 | 2026-09-09 | Cherry Studio-style paste: text/code blocks pasted into the DSH Web composer collapse into a bordered, collapsible, language-tagged card; restored as fenced code blocks on send. |
| 42 | [ClickPM/dsh-acp-interactive](https://github.com/ClickPM/dsh-acp-interactive) | 0 | 2026-09-02 | 2026-09-09 | Editor-facing ACP server for Zed and other ACP clients, composed from published DeepSeek Harness plugins. Community-maintained; not affiliated with DeepSeek. |
| 43 | [CooperZhuang/dsh-context-window](https://github.com/CooperZhuang/dsh-context-window) | 0 | 2026-09-09 | 2026-09-09 | DSH 插件：复刻 Codex 最新上下文窗口管理 — token 预算提示 / 模型可调用的 new_context / 交接式换窗替代摘要压缩 \| DSH plugin reimplementing Codex's context window management: token-budget notice, model-facing new_context, handoff window reset instead of summary compaction |
| 44 | [dblate/dsh-read-image-view](https://github.com/dblate/dsh-read-image-view) | 0 | 2026-09-09 | 2026-09-09 | Show local images read by read_image directly in the DeepSeek Harness web chat — inline thumbnail + lightbox, pure client plugin |
| 45 | [dp419936514/dsh-plugin-updater](https://github.com/dp419936514/dsh-plugin-updater) | 0 | 2026-09-09 | 2026-09-09 | Safe one-click plugin updater for DeepSeek Harness (dsh): backup, verified update with real boot smoke test, auto-rollback, and a launch-aware restart button. 深度求索 Harness 插件安全一键更新器 |
| 46 | [dsh-publish/dsh-pair-quick](https://github.com/dsh-publish/dsh-pair-quick) | 0 | 2026-09-09 | 2026-09-09 | dsh ???????????:?????????????????? |
| 47 | [edgeseeker7/dsh-subagent-progress](https://github.com/edgeseeker7/dsh-subagent-progress) | 0 | 2026-09-09 | 2026-09-09 | Live subagent progress dock for DeepSeek Harness — npm: dsh-subagent-progress |
| 48 | [ffseika0304/code-ownership-audit-java](https://github.com/ffseika0304/code-ownership-audit-java) | 0 | 2026-09-09 | 2026-09-09 | Java 版代码所有权体检：判定 Java 代码是原创还是演绎作品。纯本地 JavaParser AST 分析，依赖烤进 audit.jar，零装包、不联网、不调模型。 |
| 49 | [fhidalgodev/dsh-odoo-sdd](https://github.com/fhidalgodev/dsh-odoo-sdd) | 0 | 2026-09-08 | 2026-09-09 | Odoo SDD - Plugin DeepSeek Harness (DSH) |
| 50 | [Fishsb/dsh-shoucang-memory](https://github.com/Fishsb/dsh-shoucang-memory) | 0 | 2026-09-07 | 2026-09-09 | Long-term memory plugin for DeepSeek Harness (DSH): layered memory library + session distillation + deep-sleep consolidation + settings panel. 守藏记忆插件。 |
| 51 | [Harzva/dsh-superterminal](https://github.com/Harzva/dsh-superterminal) | 0 | 2026-09-09 | 2026-09-09 | DSH SuperTerminal: native multipane terminals, a local agent library, and DSH-powered command advice. |
| 52 | [himeope/dsh-queue-first-enter](https://github.com/himeope/dsh-queue-first-enter) | 0 | 2026-09-09 | 2026-09-09 | DeepSeek Harness (dsh) Web plugin: with an empty composer, Enter steers the first queued message into the running turn. |
| 53 | [I-am-shy/dsh-my-plugins](https://github.com/I-am-shy/dsh-my-plugins) | 0 | 2026-09-07 | 2026-09-09 | "My Plugins" Management Panel: Only manages plugins you have installed yourself (view / enable / disable / uninstall) 「我的插件」管理面板：只管理你自己安装的插件（查看 / 启用 / 关闭 / 卸载） |
| 54 | [icanfinish11/dsh-context-mode](https://github.com/icanfinish11/dsh-context-mode) | 0 | 2026-09-09 | 2026-09-09 | Context window optimization for DeepSeek Harness agents. Sandboxes tool output in-process (only what you print enters the conversation), persists session memory in an FTS5 knowledge base, and enforces routing via a system-prompt routing section. |
| 55 | [jarvislee90s-dot/dsh-foxbell-pet](https://github.com/jarvislee90s-dot/dsh-foxbell-pet) | 0 | 2026-08-16 | 2026-09-09 | Foxbell 桌宠：DSH Web 右下角可拖拽小狐狸，多项目状态监控 + 完成语音提醒 + 显隐开关 |
| 56 | [jh1016248/dsh-save-session](https://github.com/jh1016248/dsh-save-session) | 0 | 2026-09-09 | 2026-09-09 | DSH plugin: export the current session as filtered Markdown or rendered HTML (with TOC) via one-click buttons in the session header |
| 57 | [jockiller/dsh-translator](https://github.com/jockiller/dsh-translator) | 0 | 2026-09-08 | 2026-09-09 | 基于 DeepSeek Harness (DSH) 插件规范打造的输入框悬浮快捷翻译与历史找回挂件。支持直接复用当前会话已选大模型，内置智谱 AI 免费模型预设，并支持添加多个自定义 OpenAI 兼容接口。 |
| 58 | [Jumqyc/dsh-wsl-gpufix](https://github.com/Jumqyc/dsh-wsl-gpufix) | 0 | 2026-09-09 | 2026-09-09 | A deepseek harness plugin that allows the model access to GPU on WSL2. |
| 59 | [Kazusa1085/dsh-awesome-model-setting](https://github.com/Kazusa1085/dsh-awesome-model-setting) | 0 | 2026-09-09 | 2026-09-09 | DSH插件：提供“模型能力”设置页面，用于声明模型输入模态、上下文窗口、输出上限及图像配额，无需手动编辑 `settings.yaml` 文件。 |
| 60 | [kezan31/dsh-copy-tool](https://github.com/kezan31/dsh-copy-tool) | 0 | 2026-08-26 | 2026-09-09 | Enhanced line-selection copy tool for DeepSeek Harness |
| 61 | [kiwings/dsh-security](https://github.com/kiwings/dsh-security) | 0 | 2026-09-09 | 2026-09-09 | Plugins for performing security audits using dsh |
| 62 | [lalalaleo/dsh-draft](https://github.com/lalalaleo/dsh-draft) | 0 | 2026-09-08 | 2026-09-09 | A Markdown-based draft-board plugin for dsh: live-preview editing and local persistence. |
| 63 | [laodonge/col-dsh-plugin](https://github.com/laodonge/col-dsh-plugin) | 0 | 2026-09-09 | 2026-09-09 | COL (Context Organization Layer) as a DeepSeek Harness / Cordis plugin: ctx.col provides persistent organizational Contexts with replaceable executors - verified write-back, audited history, model-callable tools. Peer dep @deepseek-ai/cordis only. |
| 64 | [LAYZR114/dsh-project-memory](https://github.com/LAYZR114/dsh-project-memory) | 0 | 2026-09-09 | 2026-09-09 | 北极星记忆：DSH 项目记忆插件。Project Memory plugin: tiered injection, semantic recall, hard-guard for critical memories, per-project isolation. |
| 65 | [LiKanGame/dsh-custom-context-injector](https://github.com/LiKanGame/dsh-custom-context-injector) | 0 | 2026-09-09 | 2026-09-09 | dsh-custom-context-injector 提供「自定义上下文」设置页并注入到模型上下文，支持落盘持久化。 |
| 66 | [lingchunya/dsh-workspace-enhance](https://github.com/lingchunya/dsh-workspace-enhance) | 0 | 2026-09-09 | 2026-09-09 | 为 DeepSeek Harness 提供 Codex 风格工作区会话绑定、会话顶部快捷归档及已归档会话管理中心 |
| 67 | [lodfather/dsh-workspace-alias](https://github.com/lodfather/dsh-workspace-alias) | 0 | 2026-09-09 | 2026-09-09 | DeepSeek Harness plugin: group sessions synced from other machines into the local workspace of the same project via cross-device path aliasing (e.g. macOS /Volumes/Data/notes vs Windows F:\notes), with an in-app settings editor for the alias table. |
| 68 | [markelayan/agents-in-the-loop](https://github.com/markelayan/agents-in-the-loop) | 0 | 2026-08-31 | 2026-09-09 | Cross-session call center for DeepSeek Harness (DSH) agents: session_message delivery between sessions + a named contacts directory with name-only self-registration. File-based config, local-only, no telemetry. |
| 69 | [Meteor-system/mattpocock-skills-for-dsh](https://github.com/Meteor-system/mattpocock-skills-for-dsh) | 0 | 2026-09-08 | 2026-09-09 | Matt Pocock Skills for DSH: grilling, spec/ticket flows, TDD, and review as a portable DeepSeek Harness preset |
| 70 | [Miyamiz39/dsh-koein](https://github.com/Miyamiz39/dsh-koein) | 0 | 2026-09-09 | 2026-09-09 | Wake-word voice input for DeepSeek Harness: an always-on local keyword spotter (KWS) wakes the agent, then local offline ASR turns what you say next into a submitted message. No API key, no cloud, no typing. 语音唤醒 + 本地语音识别插件。 |
| 71 | [Mlte0907/dsh-teams-x](https://github.com/Mlte0907/dsh-teams-x) | 0 | 2026-09-06 | 2026-09-09 | TeamsX for DeepSeek Harness - durable multi-agent teams (captain, members, dependency-aware tasks, mailboxes) with an all-SVG activity panel |
| 72 | [mobfish-ai/cortex-harness-open](https://github.com/mobfish-ai/cortex-harness-open) | 0 | 2026-08-21 | 2026-09-09 | Cortex Harness — open protocol, schema, and reference tooling |
| 73 | [MrtHmk/dsh-windows-launcher](https://github.com/MrtHmk/dsh-windows-launcher) | 0 | 2026-09-08 | 2026-09-09 | 为 DeepSeek Harness 打造的 Windows 一键启动器:双击图标,立即打开界面; 服务未启动时自动在后台拉起,全程无黑窗、无任务栏命令行图标,一次点击只开一个页面。 |
| 74 | [MX1syk/dsh-x-opencode-session](https://github.com/MX1syk/dsh-x-opencode-session) | 0 | 2026-09-09 | 2026-09-09 | 一个 DeepSeek Harness（DSH）插件，为 LLM provider 请求注入动态/随机的 HTTP 请求头。DSH 的 pi-ai provider 只支持静态 headers 字符串，无法表达动态值；本插件通过包装 globalThis.fetch，按 urlPatterns 匹配请求并注入 ${uuid} 等模板值（每个 DSH 进程铸造唯一且在进程内稳定的会话 id），解决 opencode-go 网关对 x-opencode-session 头的要求（缺失会返回 400 Model is unavailable）。零默认、卸载安全、日志自动脱敏凭据。 |
| 75 | [nateyu/dsh-session-vault](https://github.com/nateyu/dsh-session-vault) | 0 | 2026-09-04 | 2026-09-09 | A DeepSeek Harness settings plugin. It lists and deletes sessions the sidebar hides: archived sessions, or blank sessions whose log has no turn/start. A session whose log cannot be read is listed too, marked “Unreadable” — this page is the only surface left that can remove it. Subagent sessions are excluded. |
| 76 | [Nath-Vikky/dsh-fisher](https://github.com/Nath-Vikky/dsh-fisher) | 0 | 2026-09-08 | 2026-09-09 | 摸鱼海岸：面向 DeepSeek Harness 的轻操作钓鱼与收藏娱乐插件。 |
| 77 | [Nesarf/mega-index-map](https://github.com/Nesarf/mega-index-map) | 0 | 2026-09-09 | 2026-09-09 | Cross-workspace interop Library: record, index and search files, tools, environments, knowledge and work records across workspaces for reuse. |
| 78 | [new-256/dsh-session-cleaner](https://github.com/new-256/dsh-session-cleaner) | 0 | 2026-08-28 | 2026-09-09 | DSH 会话清理宿主插件：侧边栏原生「移入回收站」+ 回收站管理页 + HTTP API（两级可恢复删除、同名防删错、活跃会话保护） |
| 79 | [Noah-wang/dsh-agent-pet](https://github.com/Noah-wang/dsh-agent-pet) | 0 | 2026-09-08 | 2026-09-09 | A pet in the DeepSeek Harness Web UI that changes pose with your agent, with an eight-pose sprite sheet you can generate from one sentence. |
| 80 | [NokorinNishikino/Kidai-Clipboard](https://github.com/NokorinNishikino/Kidai-Clipboard) | 0 | 2026-09-09 | 2026-09-09 | Kidai-ClipBoard (纪代剪贴板, KCB) — 跨会话剪贴板 + 会话预设：复制内容随时回填当前会话，把会话存为预设供下一步分支，支持右侧停靠侧栏、文件夹树与标签体系。 |
| 81 | [omdsh-dev/dsh-better-workbench](https://github.com/omdsh-dev/dsh-better-workbench) | 0 | 2026-09-09 | 2026-09-09 | DSH 工作台插件，把常用的页面或者应用，Pin 在工作台 |
| 82 | [PerryLink/dsh-autotier](https://github.com/PerryLink/dsh-autotier) | 0 | 2026-09-09 | 2026-09-09 | Automatic strong/cheap model-tier routing for DeepSeek Harness: intent-gated tier landing on the agent/request waterfall, plan-mode handoff (strong plans, cheap implements), deterministic high-risk guards on tools/pre-execute, failure escalation with TTL fallback, a /tier command, and tier status tools |
| 83 | [PerryLink/dsh-plugin-upgrade](https://github.com/PerryLink/dsh-plugin-upgrade) | 0 | 2026-09-09 | 2026-09-09 | Version-locked DeepSeek Harness plugin upgrade skill (0.1.3-alpha.1 -> 0.1.5-alpha.1) plus a zero-dependency seam scanner, packaged as a bundle skill and an npx CLI. |
| 84 | [PRTS168/dsh-chatnode-wechat](https://github.com/PRTS168/dsh-chatnode-wechat) | 0 | 2026-09-07 | 2026-09-09 | Chat with, monitor, and approve your DSH agents from WeChat. DeepSeek Harness bundle over the unofficial iLink gateway: two-way text/images/voice/files/video, OCR, STT/TTS, image generation, reminders, morning weather, approvals. |
| 85 | [readfish/dsh-client-theme-cyber](https://github.com/readfish/dsh-client-theme-cyber) | 0 | 2026-09-09 | 2026-09-09 | DeepSeek Harness 主题 |
| 86 | [ruisenbai/dsh-turn-fold](https://github.com/ruisenbai/dsh-turn-fold) | 0 | 2026-09-09 | 2026-09-09 | Two-level folding for DeepSeek Harness reasoning and tool calls (targets DSH 0.1.5-alpha.1) |
| 87 | [ShenXuAkaEkstasis/dsh-ai-saas-deal-finder](https://github.com/ShenXuAkaEkstasis/dsh-ai-saas-deal-finder) | 0 | 2026-09-09 | 2026-09-09 | DSH plugin that finds the cheapest legitimate AI/SaaS purchase option based on region, eligibility, payment methods, taxes, and service policies. |
| 88 | [siweimofang/zhishe-a2a-legacy](https://github.com/siweimofang/zhishe-a2a-legacy) | 0 | 2026-08-22 | 2026-09-09 | 知设AI装修顾问 - 主仓库(知识库+DSH插件+GEO) |
| 89 | [sojo-negai/dsh-mcp-plus](https://github.com/sojo-negai/dsh-mcp-plus) | 0 | 2026-09-09 | 2026-09-09 | 图形化管理 DSH 的 MCP 服务器 —— 配置、状态、工具注册一站式完成。 |
| 90 | [songer522/dsh-launcher](https://github.com/songer522/dsh-launcher) | 0 | 2026-09-08 | 2026-09-09 | macOS menu bar app for the DeepSeek Harness web server, with a Host plugin that publishes the running server's port, PID and tokenized URL |
| 91 | [songofhawk/dsh-alpha](https://github.com/songofhawk/dsh-alpha) | 0 | 2026-08-20 | 2026-09-09 | Multi-machine, multi-agent orchestration and control platform for DSH: route tasks across devices, workspaces, and Agent runtimes with streaming, approvals, and recovery. |
| 92 | [StellatoL/retro](https://github.com/StellatoL/retro) | 0 | 2026-08-16 | 2026-09-09 | The experience retrospective plugin which organizes goals, feedback, and tool failures from conversations into retrospective drafts, which are then manually reviewed and distilled into an Obsidian knowledge base, with support for weekly reports, rule proposals, and blog integration. |
| 93 | [sueqet/dsh-todo-board](https://github.com/sueqet/dsh-todo-board) | 0 | 2026-09-09 | 2026-09-09 | Cross-session TODO board for DeepSeek Harness (dsh): a draggable floating panel groups tasks by working directory, each task carries a run mode (remind / auto-continue in the current session / auto-open a new session) and two checkboxes (AI done, user verified). |
| 94 | [TYEclipse/dsh-complex](https://github.com/TYEclipse/dsh-complex) | 0 | 2026-09-08 | 2026-09-09 | Complex-number math toolbox for DeepSeek Harness: parse, arithmetic, polar conversion, principal branch functions, n-th roots |
| 95 | [TyrantG/dsh-titlecraft](https://github.com/TyrantG/dsh-titlecraft) | 0 | 2026-09-09 | 2026-09-09 | DSH 会话标题插件：支持自定义模板、语义图标及可选 AI 生成与精修。A DeepSeek Harness session-title plugin with custom templates, semantic icons, and optional AI generation and refinement. |
| 96 | [UnforgetMemory/um-dsh-plugin-skills](https://github.com/UnforgetMemory/um-dsh-plugin-skills) | 0 | 2026-09-08 | 2026-09-09 | Agent skill pack for DSH plugin development · 18-page distilled official dev guide (bilingual) · umdshdev |
| 97 | [Uronika/dsh-gpp](https://github.com/Uronika/dsh-gpp) | 0 | 2026-09-09 | 2026-09-09 | DeepSeek Harness game-programming assistant: a local hybrid-search tool (BM25 + bge-m3 semantic) over Robert Nystrom's Game Programming Patterns, with bilingual metadata for all 19 patterns and Unity C# idiom mappings. Ships tooling and self-authored metadata only — no book text. |
| 98 | [vecnode/dsh-vn-plugins](https://github.com/vecnode/dsh-vn-plugins) | 0 | 2026-09-08 | 2026-09-09 | 🤖 DeepSeek Harness Plugins |
| 99 | [Wedomizing/Dsh_genshin_nicole_skin](https://github.com/Wedomizing/Dsh_genshin_nicole_skin) | 0 | 2026-09-06 | 2026-09-09 | 来自世界之外的智慧所诞生的进步，每天都比过去一百年的积累更多 |
| 100 | [weibaohui/dsh-webdav-server](https://github.com/weibaohui/dsh-webdav-server) | 0 | 2026-09-08 | 2026-09-09 | dsh 插件 · WebDAV 服务器：把一个目录变成 Windows/macOS/Linux 都能挂载成本地磁盘的服务（令牌认证/只读模式/热更新配置） |
| 101 | [WiseXin/dsh-antigravity](https://github.com/WiseXin/dsh-antigravity) | 0 | 2026-09-09 | 2026-09-09 | Analysis and local fix for dsh-antigravity plugin CallId export error in DSH Desktop Beta |
| 102 | [Witherwithwinter/Codinput](https://github.com/Witherwithwinter/Codinput) | 0 | 2026-09-05 | 2026-09-09 | 代码编辑器风格的DSH创作器——带行号、分栏Markdown预览、六种可停靠布局，输出纯文本Markdown \| Code-editor-style composer for DSH — line numbers, split Markdown preview, six dockable layouts, sends plain-text Markdown |
| 103 | [wsjwu58-cmd/dsh-session-doctor](https://github.com/wsjwu58-cmd/dsh-session-doctor) | 0 | 2026-09-09 | 2026-09-09 | Community Session Doctor integration for DeepSeek Harness |
| 104 | [xby-skill/xby-detect-aigc](https://github.com/xby-skill/xby-detect-aigc) | 0 | 2026-09-09 | 2026-09-09 | 识别输入图片是否由人工智能（AIGC）直接生成，例如使用文生图/图生图类工具产出的合成图片。适用于需要甄别图片是否属于 AI 合成产物的场景，例如平台内容治理中的AI 内容标识、广告与新闻图片的真实来源核验、版权与合规筛查等。返回整体 AI 生成概率 score（0~1，越接近 1 越可能为 AI 生成，score>0.5 判定为 AI 生成）及是否为AI 生成标识 isFake。本能力不检测人为编辑、篡改或拼接的图片（这类图请使用通用鉴伪或证件鉴伪能力）。 |
| 105 | [xby-skill/xby-detect-fake](https://github.com/xby-skill/xby-detect-fake) | 0 | 2026-09-09 | 2026-09-09 | 对图片进行真伪鉴别的综合检测能力：识别图片是否为人工智能生成，或是否被人为编辑、篡改。适用于需要核验图片真实性的场景，例如网络图片溯源核验、媒体内容审核、可疑图片初筛等。返回整体伪造概率 score（0~1，越接近 1 越可能为伪造，score>0.5 判定为伪造）及是否伪造标识 isFake。 |
| 106 | [xby-skill/xby-detect-fake-certificate](https://github.com/xby-skill/xby-detect-fake-certificate) | 0 | 2026-09-09 | 2026-09-09 | 针对证件的图片鉴伪能力：识别证件图片是否为人工智能生成，或其证件内容区域是否被人工编辑、篡改（如改字、抠贴拼接等）。适用于各类身份、证照类图片的真实性核验场景，例如证件照审核、证照上传审查、身份核验与风控等。返回整体伪造概率 score（0~1，越接近 1 越可能为伪造，score>0.5 判定为伪造）及是否伪造标识 isFake。 |
| 107 | [xby-skill/xby-detect-fake-face](https://github.com/xby-skill/xby-detect-fake-face) | 0 | 2026-09-09 | 2026-09-09 | 针对人脸图片的真伪鉴伪能力：识别图片是否为人工智能生成，或人脸区域是否被深度伪造 / AI 换脸篡改。适用于需要核验人像真实性的场景，例如证照人脸审核、视频通话与直播的人像核验、肖像与版权人脸核验等。本能力专注人脸真伪鉴定，不检测图像中非人脸区域的复制—移动、拼接等局部篡改（这类图片请使用通用图片鉴伪能力）。返回整体伪造概率 score（0~1，越接近 1 越可能为伪造，score>0.5 判定为伪造）及是否伪造标识 isFake。 |
| 108 | [xby-skill/xby-fake](https://github.com/xby-skill/xby-fake) | 0 | 2026-09-09 | 2026-09-09 | 对图片进行真伪鉴别的工具集，检测图片是否为人工智能生成，或是否被人为篡改。包括：通用图片鉴伪检测、AI生成图片检测、证件图片鉴伪检测、人脸图片鉴伪检测。 |
| 109 | [yangcanbin31-coder/dsh-nazuna-wallpaper-engine](https://github.com/yangcanbin31-coder/dsh-nazuna-wallpaper-engine) | 0 | 2026-09-09 | 2026-09-09 | NAZUNA (彻夜之歌) themed wallpaper-engine for DeepSeek Harness: 七草荠 mascot, moonlight-violet liquid glass. Derivative of elysia395/dsh-wallpaper-engine v0.7.1 (MIT). |
| 110 | [YJLTF/dsh-thinktune](https://github.com/YJLTF/dsh-thinktune) | 0 | 2026-09-09 | 2026-09-09 | DeepSeek Harness（dsh）的 Ollama 适配器插件：让 qwen3.8 等思考模型的思考强度成为一个可配置、可选择的一等参数，同时原生支持多模态图片输入，并可在四种常见的思考控制协议之间一键切换。 |
| 111 | [ytmaps/dsh-flowtext](https://github.com/ytmaps/dsh-flowtext) | 0 | 2026-09-01 | 2026-09-09 | 鱼先生模块化OB |
| 112 | [zhang8019/dsh-permission-matrix](https://github.com/zhang8019/dsh-permission-matrix) | 0 | 2026-09-09 | 2026-09-09 | Permission matrix for DeepSeek Harness: 3 sandbox modes x 4 approval strategies = 9 presets, with global and LLM-robot defaults, three-tier risk policies, audit log and git checkpoint. |
| 113 | [zhaoxuejie/dsh-plugin-log-forwarder](https://github.com/zhaoxuejie/dsh-plugin-log-forwarder) | 0 | 2026-09-09 | 2026-09-09 | DeepSeek Harness 实时日志转发插件：将 Agent 运行事件实时转发到 WebSocket / Loki / 本地文件 |
| 114 | [zpis666/dsh-context-budget](https://github.com/zpis666/dsh-context-budget) | 0 | 2026-09-09 | 2026-09-09 | 在 DSH 模型设置页为每个 pi-ai 路由配置上下文窗口、压缩阈值与保留预算，并在输入框右下角按厂商提供思考强度选择器。 · Per-route context window, compaction threshold, and vendor-aware thinking-effort controls for DSH models. |
| 115 | [zzzmmmnn/dsh-openkapsel](https://github.com/zzzmmmnn/dsh-openkapsel) | 0 | 2026-09-08 | 2026-09-09 | Remote-only OpenKapsel workspace bridge for the DeepSeek Harness: replaces host filesystem and shell tools with a fail-closed remote tool set. Self-hosted alternative to cloud agent sandboxes. |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- 1x1-lab/dsh-auto-execute
- buildbeforewepitch/agentscars
- dougen/dsh-deepseek-usage
- easyv-ai/dsh-jumpserver
- easyv-ai/dsh-pve
- edisontaisite/codex-harness-control
- Fakek0f3sT/dsh-mcp-diff
- lansi-ai/dsh-desktop
- lecutu/dsh-slide-reflex
- lijiajia96/dsh-tool-adb
- markelayan/dsh-taskboard-flow
- Minglink/dsh-infinite-gen-3
- mozhuanzuojing/dsh-agent-pill
- QuanQQQ/dsh-plugin-dev-manager
- winditer/dsh-elf
- ytmaps/dsh-subagent-flowtext
