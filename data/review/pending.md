# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-19**
- 快照日期 / Snapshot date: **2026-09-19 (UTC)**
- 待审核 / Pending: **95**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **11**
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

对比上一份快照 **2026-09-18** / vs previous snapshot **2026-09-18**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **6**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [loopx-project/loopx](https://github.com/loopx-project/loopx) | 待审 / pending | 5900 | +8 | 558 | 110d | 待审高星 | 核准即 Top 2 |
| ⚠️ [slow-stack/dsh-mneme](https://github.com/slow-stack/dsh-mneme) | 待审 / pending | 112 | +0 | 15 | 36d | 待审高星 | 核准即榜 #105 |
| ⚠️ [dataelement/dsh-desktop](https://github.com/dataelement/dsh-desktop) | 待审 / pending | 7657 | — | 325 | 36d | 待审高星 | 核准即 Top 1 |
| ⚠️ [Tencent/BrowserSkill](https://github.com/Tencent/BrowserSkill) | 已核准 / approved | 5684 | +558 | 397 | 88d | 日增百星 | 日增 +558★；已不进榜单 |
| ⚠️ [Clearailhc/clearai-dsh](https://github.com/Clearailhc/clearai-dsh) | 已核准 / approved | 139 | +103 | 8 | 6d | 日增百星、新入 Top 200 | 日增 +103★；新入 Top 200 #86 |
| ⚠️ [VDERR/echocat-skill-panel-3.0](https://github.com/VDERR/echocat-skill-panel-3.0) | 已核准 / approved | 180 | +101 | 6 | 0d | 日增百星、榜单跃升 | 日增 +101★；榜单 145→66；创建 0 天 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [dataelement/dsh-desktop](https://github.com/dataelement/dsh-desktop) ⚠️ | 7657 | 2026-08-13 | 2026-09-19 | DSHDesktop：DeepSeek Harness Desktop / DeepSeek Harness 桌面版 |
| 2 | [loopx-project/loopx](https://github.com/loopx-project/loopx) ⚠️ | 5900 | 2026-05-31 | 2026-09-19 | Long-horizon agent control plane for durable, governed work across Codex, Claude Code, and other harnesses. |
| 3 | [slow-stack/dsh-mneme](https://github.com/slow-stack/dsh-mneme) ⚠️ | 112 | 2026-08-13 | 2026-09-19 | 🧠 The memory that dreams — cross-session memory for DeepSeek Harness. Offline & private, auto-consolidates in its sleep (autoDream), visualized in a memory panel. |
| 4 | [extracurricular-ai/dsh-filesnap](https://github.com/extracurricular-ai/dsh-filesnap) | 43 | 2026-08-27 | 2026-09-19 | DSH Rewind & Redo — by FileSnap. 把对话和它改过的文件一起恢复到某一轮之前（受claude code rewind启发并改进）,不需要 git 仓库,并且可以撤销恢复（redo受opencode启发并改进），由rust驱动是市面上最快最可靠的dsh rewind插件. A blazing-fast rewind and redo plugin for DeepSeek Harness, powered by a 🦀 Rust core, tracking the conversation and the files it changed, no git required, low disk consumption |
| 5 | [myc0576/SmartMoney-Cub](https://github.com/myc0576/SmartMoney-Cub) | 24 | 2026-06-25 | 2026-09-19 | Read-only trading journal and review harness: Jev typed judgments, agent integration, and a reproducible finance benchmark. No orders, no advice. |
| 6 | [Coprexist/Copree](https://github.com/Coprexist/Copree) | 8 | 2026-06-14 | 2026-09-19 | AIsChat 是一个开源 AI 群聊框架：让 AI 拥有自己的状态、记忆与生命节奏——不只是工具，是陪伴。群视界（Group World）让每个群聊绑定一个活的世界（网页 + 世界 AI + 代码 + 时间），并支持 DSH 工作区镜像双向同步。 |
| 7 | [appthin/dsh-skills-manager-plus](https://github.com/appthin/dsh-skills-manager-plus) | 2 | 2026-09-19 | 2026-09-19 | 在 DeepSeek Harness 设置界面的左侧边栏新增「技能与命令」页面， 可直接查看、启用/停用、编辑、删除与添加技能，还能把常用的提示词保存为命令， 在输入框输入 `/` 即可快速调用。Adds a *Skills & Commands* page to the left sidebar of the Settings screen, where you can view, enable/disable, edit, delete and add skills, and save frequent prompts as `/commands` that you invoke by typing `/`. |
| 8 | [buberlo/dsh-jev](https://github.com/buberlo/dsh-jev) | 2 | 2026-09-19 | 2026-09-19 | Jev-powered decision layer for DeepSeek Harness |
| 9 | [hdhgsysh/dsh-connect-qoder](https://github.com/hdhgsysh/dsh-connect-qoder) | 2 | 2026-09-19 | 2026-09-19 | Bridge local Qoder / Qoder CN models into DeepSeek Harness |
| 10 | [YichuAI/deepseek-harness-vscode](https://github.com/YichuAI/deepseek-harness-vscode) | 2 | 2026-08-15 | 2026-09-19 | Native VS Code client for DeepSeek Harness. Same workspace, same session, same agent runtime — VS Code and the browser share one Harness session. |
| 11 | [AbsoluteMikhail/dsh-locale-ru](https://github.com/AbsoluteMikhail/dsh-locale-ru) | 1 | 2026-09-19 | 2026-09-19 | Полная русская локализация веб-интерфейса DeepSeek Harness |
| 12 | [ArtlexYoung/dsh-super-code](https://github.com/ArtlexYoung/dsh-super-code) | 1 | 2026-09-12 | 2026-09-19 | 面向 DeepSeek Harness 的场景化 Agent 预设，覆盖单人交付、团队委派、方案调研和优化实验。Scenario-focused DeepSeek Harness agent presets for solo delivery, team delegation, evidence-based research, and optimization experiments. |
| 13 | [BaiZhi967/dsh-plugin-zcode-import](https://github.com/BaiZhi967/dsh-plugin-zcode-import) | 1 | 2026-09-19 | 2026-09-19 | DSH 会话导入插件：按工作区浏览本地 ZCode 的会话，勾选或整工作区导入 DeepSeek Harness · Import local ZCode conversations into DeepSeek Harness |
| 14 | [Hotsteel2901/dsh-frutiger-aero](https://github.com/Hotsteel2901/dsh-frutiger-aero) | 1 | 2026-09-19 | 2026-09-19 | 🫧 Frutiger Aero skin for DeepSeek Harness (dsh): glass over a living sky-and-water wallpaper, aqua gloss, light + dark. Rebuilds the phone layout too — drawer, dock, edge swipes, keyboard-aware composer. 玻璃质感皮肤，电脑端与手机端都适配。 |
| 15 | [Hwayn-pixel/dsh-image-skin](https://github.com/Hwayn-pixel/dsh-image-skin) | 1 | 2026-09-19 | 2026-09-19 | Universal image skin for the DSH (DeepSeek Harness) web UI - replace large UI regions and corner stickers with your own images, GIFs, or videos, from a settings submenu. |
| 16 | [Jaylor-Wang/dsh-tool-ast-grep](https://github.com/Jaylor-Wang/dsh-tool-ast-grep) | 1 | 2026-09-14 | 2026-09-19 | AST-based structural code search and syntax outline tool for DeepSeek Harness powered by ast-grep |
| 17 | [JRJRJPRO/dsh-tree](https://github.com/JRJRJPRO/dsh-tree) | 1 | 2026-09-19 | 2026-09-19 | 把 对话分支 画成 可点击的树 |
| 18 | [karottc/dsh-plugin-workspace-sorted](https://github.com/karottc/dsh-plugin-workspace-sorted) | 1 | 2026-09-19 | 2026-09-19 | 让 DeepSeek Harness 的 **工作区（Workspace）** 按「最近使用」排序的宿主（Host）插件。  侧边栏自带的「排序方式：手动排序 / 最近更新」只作用于**会话**；工作区分组的顺序永远是 Host 注册表的持久顺序。本插件让最近有活动的那个工作区排到最前面。 |
| 19 | [mustakimabdullah25-tech/dsh-screen-translator](https://github.com/mustakimabdullah25-tech/dsh-screen-translator) | 1 | 2026-09-19 | 2026-09-19 | Universal on-screen translator for DeepSeek Harness Web UI: translates UI text, attributes, Shadow DOM, and iframes across 45+ languages. |
| 20 | [shenA2024/whale-persona](https://github.com/shenA2024/whale-persona) | 1 | 2026-09-19 | 2026-09-19 | 多宿主人设引擎：一份 config.json 让 DSH 与 ZCode 共用同一套人设、工作契约、思维链语言与长期记忆；记忆由 AI 提议、人工确认后才生效（代码强制）。A persona engine for AI coding harnesses (DeepSeek Harness + ZCode). |
| 21 | [shkzhang/dsh-appearance](https://github.com/shkzhang/dsh-appearance) | 1 | 2026-09-19 | 2026-09-19 | DSH外观设置 |
| 22 | [yyh-001/DSH-X](https://github.com/yyh-001/DSH-X) | 1 | 2026-09-03 | 2026-09-19 | DeepSeek Harness 轻量 Windows 启动器。选一个版本，启动 dsh web。 |
| 23 | [1622352030/ansys-agent-bridge](https://github.com/1622352030/ansys-agent-bridge) | 0 | 2026-09-19 | 2026-09-19 | MCP server driving Ansys SpaceClaim headlessly through PyAnsys Geometry, plus a DSH plugin bundle. Guards the operations that report success without changing geometry. |
| 24 | [2404723600/dsh-router-loomy](https://github.com/2404723600/dsh-router-loomy) | 0 | 2026-09-19 | 2026-09-19 | DSH plugin: Loomy (iFlyTek) OpenAI-compatible supplier for dsh-router |
| 25 | [AEmbers/dsh-first-party](https://github.com/AEmbers/dsh-first-party) | 0 | 2026-09-19 | 2026-09-19 | 第一方 DSH 插件集合：用可控、可验证的自研实现替换高开销第三方 bundle。首个包 recall-lite 把启动期 eager 预热改为按需初始化。 |
| 26 | [Alih-b/fox-pet](https://github.com/Alih-b/fox-pet) | 0 | 2026-09-04 | 2026-09-19 | Folio the fox — an animated desktop companion with physics interactions, sleep/wake animations, and a shared sprite atlas. Runs as an Omarchy/Quickshell plugin and as a DeepSeek Harness (DSH) Cordis web plugin under dsh/. |
| 27 | [Archer76/dsh-memory-evolve-suite](https://github.com/Archer76/dsh-memory-evolve-suite) | 0 | 2026-09-19 | 2026-09-19 | DSH 长期记忆插件（dsh-memory-evolve 的再分发构建）：分层记忆・待办・技能自进化・外部 CLI 调度，另内置 3 份记忆运维技能与 14 个配套脚本 |
| 28 | [BaiZhi967/dsh-plugin-terminal-panel](https://github.com/BaiZhi967/dsh-plugin-terminal-panel) | 0 | 2026-09-18 | 2026-09-19 | DSH web plugin: real PTY terminals inside the DeepSeek Harness UI — sidebar entry, tabs, rename, theme-aware colors. DSH 网页内的终端面板插件。 |
| 29 | [BotHarness/dsh-skill](https://github.com/BotHarness/dsh-skill) | 0 | 2026-09-19 | 2026-09-19 | Full-stack DeepSeek Harness plugin development skill — generated mirror of BotHarness/BotHarness. Install: npx skills add BotHarness/dsh-skill |
| 30 | [ChaoJie0/dsh-tm-guard](https://github.com/ChaoJie0/dsh-tm-guard) | 0 | 2026-09-16 | 2026-09-19 | Zero-intervention permission gate for DSH agents on macOS: rollback-able local writes auto-allowed, network/installs/sensitive reads blocked and audited. |
| 31 | [CharlesXu-HQ/dsh-dream-rsi](https://github.com/CharlesXu-HQ/dsh-dream-rsi) | 0 | 2026-09-19 | 2026-09-19 | Experimental replay-based exploration-policy plugin for DeepSeek Harness |
| 32 | [dangxinxing090-svg/dsh-plugin-brief](https://github.com/dangxinxing090-svg/dsh-plugin-brief) | 0 | 2026-09-15 | 2026-09-19 | A DeepSeek Harness plugin that turns each agent reply into a short slide deck in plain language — for people who use the harness but do not read code. |
| 33 | [EPCN-fla/dsh-vscode-bridge](https://github.com/EPCN-fla/dsh-vscode-bridge) | 0 | 2026-09-19 | 2026-09-19 | Cordis plugin bridging the dsh-vscode extension to native DSH services (workspace grouping, session titles, archive, agent presets, permission presets) over a token-authenticated local JSON-RPC socket. |
| 34 | [ewoowe/dsh-plugin-dependency-graph-plugin](https://github.com/ewoowe/dsh-plugin-dependency-graph-plugin) | 0 | 2026-09-19 | 2026-09-19 | Plugin dependency graph for DeepSeek Harness: which plugin provides the services every other plugin injects, read from the live Cordis runtime. |
| 35 | [Furdavus/dsh-uyghurche-ui](https://github.com/Furdavus/dsh-uyghurche-ui) | 0 | 2026-09-19 | 2026-09-19 | DSH Web 界面维吾尔语（UEY）语言包：官方 locale API 注册 ئۇيغۇرچە，1,069 条界面文案（逐 key 英文回退）+ 全界面 RTL 镜像 + Intl 本地化 |
| 36 | [GooDAnDReaDY/dsh-agent-orchestrator](https://github.com/GooDAnDReaDY/dsh-agent-orchestrator) | 0 | 2026-09-18 | 2026-09-19 | Multi-agent task decomposition, DAG workflow orchestration, and prompt caching optimizer for DeepSeek Harness |
| 37 | [happyDABAI7/JiaFangTool](https://github.com/happyDABAI7/JiaFangTool) | 0 | 2026-09-19 | 2026-09-19 | OCR，语音识别，ai问答 |
| 38 | [HaydenSmith1121/dsh-wallpaper-engine](https://github.com/HaydenSmith1121/dsh-wallpaper-engine) | 0 | 2026-09-19 | 2026-09-19 | Wallpaper Engine Steam Workshop browser for DeepSeek Harness: anonymous search & browse the workshop from a sidebar panel, steam:// subscribe deep-links, Steam login detection. |
| 39 | [hfdsdfgr/dsh-balance-bar](https://github.com/hfdsdfgr/dsh-balance-bar) | 0 | 2026-09-19 | 2026-09-19 | DeepSeek Harness Web plugin: live account balance as a colour-banded vertical progress bar on the right edge of the GUI, with an animated wave above the threshold. |
| 40 | [HFUT-zhengjiahao/dsh-balance](https://github.com/HFUT-zhengjiahao/dsh-balance) | 0 | 2026-09-19 | 2026-09-19 | DeepSeek API balance, conversation token usage, and CNY cost estimation for DeepSeek Harness (DSH) |
| 41 | [HFUT-zhengjiahao/dsh-process-control](https://github.com/HFUT-zhengjiahao/dsh-process-control) | 0 | 2026-09-19 | 2026-09-19 | Local-only stop and restart controls for DeepSeek Harness (DSH) — a sidebar plugin with loopback-only process routes |
| 42 | [hj01857655/dsh-theme-studio](https://github.com/hj01857655/dsh-theme-studio) | 0 | 2026-09-19 | 2026-09-19 | dsh plugin: customize UI theme with presets, accent colors, density, radius, fonts, and custom CSS |
| 43 | [Hugo16/dsh-session-rotate-on-compact](https://github.com/Hugo16/dsh-session-rotate-on-compact) | 0 | 2026-09-13 | 2026-09-19 | 用于 DSH 的会话轮换插件。  当 DSH 完成一次自动或手动 Compact 后，插件会生成新的 Session ID，让代理 API 将下一次请求识别为新会话，从而触发账号轮询。 |
| 44 | [huxin7735-collab/dsh-maintainer-doc-guard](https://github.com/huxin7735-collab/dsh-maintainer-doc-guard) | 0 | 2026-09-18 | 2026-09-19 | Keeps a long agent turn answerable to the user's actual request: a standing maintainer-document reminder, two pre-execute gates, an objective anchor quoting your latest instruction, and a nudge stage that corrects before it blocks. |
| 45 | [iimaguest/dsh-sandbox-escalation-guard](https://github.com/iimaguest/dsh-sandbox-escalation-guard) | 0 | 2026-09-19 | 2026-09-19 | DeepSeek Harness plugin: stops the sandbox escalation fields being advertised to a model when the calling session cannot grant them, fixing the retry loop known models fall into at danger-full-access. |
| 46 | [imtokenxinluo/dsh-contract-check](https://github.com/imtokenxinluo/dsh-contract-check) | 0 | 2026-09-19 | 2026-09-19 | Zero-token contract check for DSH plugins — verifies output.render() / session-event vocabulary, warn-only. 无耗检查：DSH 插件契约体检，零 token 成本，只告警不拦截。 |
| 47 | [IQzhan/dsh-rebooter](https://github.com/IQzhan/dsh-rebooter) | 0 | 2026-09-17 | 2026-09-19 | A lightweight plugin. The default web UI opens in its own window and does not need a browser. A desktop panel starts, stops, restarts, and updates DeepSeek Harness. Closing either window does not stop the service. \| 轻量插件。默认打开的页面是独立窗口，不依赖浏览器。桌面面板用来开启、关闭、重启、更新。关掉窗口不会停掉服务。 |
| 48 | [isayrhythm/dsh-plugin-repo-snapshot](https://github.com/isayrhythm/dsh-plugin-repo-snapshot) | 0 | 2026-09-19 | 2026-09-19 | DeepSeek Harness plugin: encrypted workspace repo snapshots (including .git) backed up to your own local folder or Aliyun OSS, with a built-in settings page. |
| 49 | [IvenKooLab/loci-dsh](https://github.com/IvenKooLab/loci-dsh) | 0 | 2026-09-19 | 2026-09-19 | 🧠 loci second brain as a DeepSeek Harness (dsh) web plugin — search / ask / remember your local knowledge base from the sidebar |
| 50 | [Jiangsubei/dsh-qqbot-bridge](https://github.com/Jiangsubei/dsh-qqbot-bridge) | 0 | 2026-09-17 | 2026-09-19 | DeepSeek Harness × QQ 官方机器人插件 —— 用 **QQ 单聊**远程控制 DSH 里已有的所有工作区会话：流式输出、Markdown 渲染、文件收发、命令系统。 |
| 51 | [jianjianzhu/dsh-harness-ui](https://github.com/jianjianzhu/dsh-harness-ui) | 0 | 2026-09-19 | 2026-09-19 | Full-page Harness console for the DeepSeek Harness Web GUI: sessions, plugins, market, MCP, skills and usage in one shell. |
| 52 | [jianjianzhu/dsh-model-switcher](https://github.com/jianjianzhu/dsh-model-switcher) | 0 | 2026-09-19 | 2026-09-19 | Visual custom-provider presets and model switching for DeepSeek Harness Web. |
| 53 | [john-walks-slow/dsh-wait-subagent](https://github.com/john-walks-slow/dsh-wait-subagent) | 0 | 2026-09-19 | 2026-09-19 | wait_subagent tool for DeepSeek Harness: block until a background continuable subagent settles and return its stop reason and closing message — event-driven, zero polling. |
| 54 | [john-walks-slow/dsh-zen](https://github.com/john-walks-slow/dsh-zen) | 0 | 2026-09-06 | 2026-09-19 | Zen Mode view tab + foreground time tracker for DeepSeek Harness — a calm minimal surface while your agent works, with daily/weekly zen scores. Pure frontend, zero permissions. |
| 55 | [lengmoXXL/dsh-git](https://github.com/lengmoXXL/dsh-git) | 0 | 2026-09-13 | 2026-09-19 | A read-only git browser for the DeepSeek Harness Web GUI: a right-sidebar page with the session's working-tree changes and commit history, and the diff a click opens beside them. The host half reads the repository through ctx.fs and ctx.subprocess, so a routed (remote) execution world works unchanged. |
| 56 | [LMPrado-DZ23/awesome-agent-plugins](https://github.com/LMPrado-DZ23/awesome-agent-plugins) | 0 | 2026-09-18 | 2026-09-19 | Cross-harness catalog of MCP servers, Agent Skills and plugins for AI coding agents — exact install commands for Claude Code, Codex, Gemini CLI, Cursor, OpenCode, DeepSeek Harness and more. |
| 57 | [masknull/dsh-qoder-connect](https://github.com/masknull/dsh-qoder-connect) | 0 | 2026-09-19 | 2026-09-19 | 将 Qoder（国内版 / 国际版）的模型以个人访问令牌（PAT）接入 DeepSeek Harness —— 双变体独立配置、侧栏额度展示、上下文窗口一键切换。\|Qoder CN & international models for DeepSeek Harness via PAT. 支持 DSH 0.1.5-rc.1+。 |
| 58 | [meihaoyidian/life-workbench](https://github.com/meihaoyidian/life-workbench) | 0 | 2026-09-19 | 2026-09-19 | dsh插件：个人工作台插件 |
| 59 | [Meowrium/dsh-copy-file-path](https://github.com/Meowrium/dsh-copy-file-path) | 0 | 2026-09-19 | 2026-09-19 | dsh plugin: adds 复制相对路径 / 复制绝对路径 (copy relative / absolute path) to the delivered-file card menu of the DeepSeek Harness web UI. / dsh Web 交付文件卡片菜单增加复制相对路径与复制绝对路径。 |
| 60 | [Mhmd7-7/dsh-rtl-chat-box](https://github.com/Mhmd7-7/dsh-rtl-chat-box) | 0 | 2026-09-18 | 2026-09-19 | Adds an RTL chat box direction control to the dsh web GUI. |
| 61 | [moonbowterfly/dsh-bio-gem](https://github.com/moonbowterfly/dsh-bio-gem) | 0 | 2026-08-31 | 2026-09-19 | 基因组尺度代谢模型（GEM）构建插件：全基因组(蛋白FASTA)→自动构建+验证+补洞+报告(SBML+模型卡)；dsh-bio-genie 生态域插件 \| Genome-scale metabolic model builder for dsh (DeepSeek Harness) |
| 62 | [MoseeVision/dsh-quick-archive](https://github.com/MoseeVision/dsh-quick-archive) | 0 | 2026-09-19 | 2026-09-19 | DSH plugin: one-click archive button on every sidebar session row, beside the session menu / 侧边栏会话行的一键归档按钮 |
| 63 | [nuaaweixinye/dsh-gme-test-generator](https://github.com/nuaaweixinye/dsh-gme-test-generator) | 0 | 2026-09-14 | 2026-09-19 | GME Test Generator workflow tools for DeepSeek Harness (dsh): pick interfaces, generate and repair tests through a local Python backend, poll progress, and decide with consent. |
| 64 | [OzzyDeng-JunDeng/dsh-keyless-search](https://github.com/OzzyDeng-JunDeng/dsh-keyless-search) | 0 | 2026-09-19 | 2026-09-19 | Keyless web search for the DeepSeek Harness web_search tool — Tavily and Firecrawl no-key access, no account or configuration. |
| 65 | [PerryLink/dsh-plugin-upgrade](https://github.com/PerryLink/dsh-plugin-upgrade) | 0 | 2026-09-19 | 2026-09-19 | Plugin-author upgrade skill for DeepSeek Harness: one package, one corridor index - it detects the caller peer band, routes to the matching closed corridor card (0.1.3-alpha.1 -> 0.1.5-rc.1, 0.1.5-rc.2 -> 0.1.6-alpha.2) and runs a zero-dependency seam scanner as a bundle skill + npx CLI. |
| 66 | [PerryLink/dsh-plugin-upgrade-016](https://github.com/PerryLink/dsh-plugin-upgrade-016) | 0 | 2026-09-19 | 2026-09-19 | Corridor folded into dsh-plugin-upgrade 2.0.0 (never published under this name): its 0.1.5-rc.2 -> 0.1.6-alpha.2 card and E1-E5 scanner live in that package now. |
| 67 | [Qulierm/orbital-agents](https://github.com/Qulierm/orbital-agents) | 0 | 2026-09-18 | 2026-09-19 | Paired Endeavour and Challenger agents for DeepSeek Harness. |
| 68 | [reisen-ww/dsh-bonk-pet](https://github.com/reisen-ww/dsh-bonk-pet) | 0 | 2026-09-19 | 2026-09-19 | 敲盆宠物 · DSH 悬浮小鲸鱼插件：出错掉钢管、敲铁盆、讨白饭 |
| 69 | [rezon-aki/dsh-memory-steward](https://github.com/rezon-aki/dsh-memory-steward) | 0 | 2026-09-19 | 2026-09-19 | 记忆管家：为 dsh-memory-evolve 补上记忆入库之后的生命周期闭环——预算看门狗、整理到期提醒、待审批队列与审批 Tab、带备份执行。只读观测记忆文件，写入一律回调上游官方 HTTP API。 |
| 70 | [rinttt233/dsh-peak-brief](https://github.com/rinttt233/dsh-peak-brief) | 0 | 2026-09-19 | 2026-09-19 | DSH（DeepSeek Harness）峰谷调度插件：高峰前 N 分钟自动生成仅供 AI 恢复用的简报并停自动续跑，高峰硬挡模型请求（带一键逃生），闲时自动注入简报继续任务。 |
| 71 | [rsdgnchen/dsh-bottom-dock](https://github.com/rsdgnchen/dsh-bottom-dock) | 0 | 2026-09-19 | 2026-09-19 | DSH Web 插件：把官方右侧栏 dock（终端/文件树/文档预览）整体搬到底部，仿 iOS 上滑横杠唤出、可拖拽调高。不改官方代码，只用官方 data-* 钩子重定位；探测不到官方结构时完全惰性。 |
| 72 | [Saretheya/dsh-lantern](https://github.com/Saretheya/dsh-lantern) | 0 | 2026-09-18 | 2026-09-19 | Expose every model in your local DeepSeek Harness to the LAN over OpenAI- and Anthropic-compatible endpoints. |
| 73 | [sduwall/dsh-wall-mcp-manager](https://github.com/sduwall/dsh-wall-mcp-manager) | 0 | 2026-08-29 | 2026-09-19 | DSH 插件：集中管理 MCP 服务配置，并展示各 MCP 的工具清单、参数与返回契约 |
| 74 | [senyayume/dsh-edit-diff](https://github.com/senyayume/dsh-edit-diff) | 0 | 2026-09-19 | 2026-09-19 | DSH 插件：在文件变更工具卡片上重绘行级 diff（相同行只渲染一次 + 行内字符高亮），覆盖 run_code(PTC) 与 str_replace_editor，轮末给出改动汇总卡，并可在资源管理器中定位或复制路径。 |
| 75 | [Shadoso-w/dsh-cli-mode](https://github.com/Shadoso-w/dsh-cli-mode) | 0 | 2026-09-19 | 2026-09-19 | Command-line mode for the DeepSeek Harness web GUI: a composer line starting with ！ or ! runs as a real command in the session workspace instead of being sent to the model. |
| 76 | [solodov123123-blip/dsh-locale-ru](https://github.com/solodov123123-blip/dsh-locale-ru) | 0 | 2026-09-18 | 2026-09-19 | Russian localization for DeepSeek Harness (34 UI dictionaries, Cordis runtime, dynamic DOM translator) |
| 77 | [Stellight/dsh-chat-rail](https://github.com/Stellight/dsh-chat-rail) | 0 | 2026-09-19 | 2026-09-19 | DeepSeek Harness 中文插件：对话区右缘的网页版风格导航竖线——每条人类消息一根短横线，靠近展开可跳转的消息列表，并支持回溯更早的历史 |
| 78 | [syx2bzd/dsh-ricewhale](https://github.com/syx2bzd/dsh-ricewhale) | 0 | 2026-09-19 | 2026-09-19 | DSH Web 界面的「鲸鱼女仆」物理挂件：拖拽投掷、撞边回弹、撒币吃分连击，每吃满 500 个 token 冒一碗白饭。 |
| 79 | [TaoYe599/dsh-notify](https://github.com/TaoYe599/dsh-notify) | 0 | 2026-09-19 | 2026-09-19 | Task completion and needs-you notifications for DeepSeek Harness — web notification while the page is open, native Windows toast when the browser is closed. · DSH 任务完成/待回复通知：页面开着弹网页通知，浏览器关掉由 Host 弹原生通知。 |
| 80 | [tcgbp/dock-flash](https://github.com/tcgbp/dock-flash) | 0 | 2026-09-19 | 2026-09-19 | Extensible quick-control panel for DSH Web — switch registry, skin manager, standalone or with dock-base. |
| 81 | [thissensen/dsh-agent-studio](https://github.com/thissensen/dsh-agent-studio) | 0 | 2026-09-18 | 2026-09-19 | 可视化地精确配置 Agent 的提示词（prompt）、工具（tools）、可见技能（skills）、子代理、备用模型，轻松创建团队，根据不同任务分配不同模型。(npm 9月22日发布) |
| 82 | [ubik-dsh/deepseek-mods](https://github.com/ubik-dsh/deepseek-mods) | 0 | 2026-09-19 | 2026-09-19 | Mods and skills for DeepSeek Harness: an editable system prompt in the chat header, full Russian localization, a mod manager, and a skill-authoring toolkit with a bundled checker. Every claim verified in docs/VERIFICATION.md — including what was not covered. Bilingual docs, no build step. |
| 83 | [wild-River2016/dsh-canvas-xiaohe](https://github.com/wild-River2016/dsh-canvas-xiaohe) | 0 | 2026-09-19 | 2026-09-19 | DeepSeek Harness 插件 - 小禾画布 AI 创作助手 |
| 84 | [WoodSettler/dsh-local-proxy](https://github.com/WoodSettler/dsh-local-proxy) | 0 | 2026-09-19 | 2026-09-19 | DSH plugin: discover this machine's HTTP proxy (explicit .env value, else the Windows system proxy) and make DeepSeek Harness use it - for the agent's in-process fetches and for every child process it spawns. |
| 85 | [wupup/dsh-custom-style](https://github.com/wupup/dsh-custom-style) | 0 | 2026-09-19 | 2026-09-19 | dsh web custom style plugin |
| 86 | [wwwort/dsh-win-computer-use](https://github.com/wwwort/dsh-win-computer-use) | 0 | 2026-09-19 | 2026-09-19 | Windows-native computer use for DeepSeek Harness: one batch tool runs a whole find/click/type/wait/screenshot sequence in a single model round trip, and drives windows without taking your focus or pointer. |
| 87 | [wywincl/data-analysis-agent](https://github.com/wywincl/data-analysis-agent) | 0 | 2026-09-19 | 2026-09-19 | data analysis agent for everyone  |
| 88 | [xswt442-cmd/dsh-unsandboxed-winbash](https://github.com/xswt442-cmd/dsh-unsandboxed-winbash) | 0 | 2026-09-17 | 2026-09-19 | 让 dsh 在 Windows 上使用用户自安装的 Git Bash，并绕过其沙箱限制 \| Enable dsh to use a user-installed Git Bash on Windows by bypassing its sandbox restrictions. |
| 89 | [yaodongH/dsh-better-summary](https://github.com/yaodongH/dsh-better-summary) | 0 | 2026-09-19 | 2026-09-19 | DSH Web 插件：Codex 风格的改动汇总卡片，替换对话末尾的产出 chip 行。 |
| 90 | [Yazzyk/dsh-file-shield](https://github.com/Yazzyk/dsh-file-shield) | 0 | 2026-09-19 | 2026-09-19 | DeepSeek Harness (dsh) 插件：在 Web GUI 里点选文件或目录，屏蔽 agent 对它们的读取、搜索、写入与编辑，使机密内容与敏感词不进入对话（含敏感词导致请求 400 的场景）。Blocks an agent from reading/searching/writing/editing chosen files, keeping their contents out of the conversation. |
| 91 | [YerenChina/dsh-memory-webdav-sync](https://github.com/YerenChina/dsh-memory-webdav-sync) | 0 | 2026-09-19 | 2026-09-19 | 把 DSH 的记忆文件双向同步到任意 WebDAV 服务器（带设置界面） |
| 92 | [YouHui1/dsh-sessions-diagnosis](https://github.com/YouHui1/dsh-sessions-diagnosis) | 0 | 2026-09-19 | 2026-09-19 | Diagnose and repair DSH sessions that stopped opening after a harness upgrade — from the CLI, from an agent tool, or from a dashboard in the DSH web UI. |
| 93 | [yueyexiayu/dsh-jiyi](https://github.com/yueyexiayu/dsh-jiyi) | 0 | 2026-09-18 | 2026-09-19 | DSH desktop plugin: cross-session memory (topics, inbox, index injection) |
| 94 | [YUsaltyfish/dsh-fish-sound-notify](https://github.com/YUsaltyfish/dsh-fish-sound-notify) | 0 | 2026-09-19 | 2026-09-19 | DSH bundle: a Windows system sound when the agent asks a question /a turn ends/a permission request |
| 95 | [ZZJQ678/dsh-model-picker](https://github.com/ZZJQ678/dsh-model-picker) | 0 | 2026-09-19 | 2026-09-19 | 按渠道商（Provider）分组、可折叠的 DSH 模型选择器：替换聊天输入框右下角原生选择器。仅在 DSH 桌面版实测通过，Web 版未测试。 |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- ArtlexYoung/dsh-super-agent
- dangxinxing090-svg/dsh-plugin-plain-slides
- huangruiteng/loopx
- imMamdouhaboammar/get-fable
- modusensus/dsh-mneme
- nuaaweixinye/dsh-gme-workflow
- openrect/dsh-community-installer
- reinocheong/dsh-session-move
- shiki-dml/dsh-workspace-intelligence
- XPQHyue/dsh-web-split
- yyh-001/dsh-launcher
