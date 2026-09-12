# 待审核仓库 / Pending review

> 新增到 `dsh-plugin` Topic 下、带有简介、尚未经维护者核实的仓库。本文件由 `scripts/update.mjs` 每日刷新，仅供审核使用，不是用户可见页面。
>
> Repositories newly added to the `dsh-plugin` topic that the maintainer has not verified yet. Refreshed daily by `scripts/update.mjs`; review-only, not a user-facing page.

- 生成时间 / Generated: **2026-09-12**
- 快照日期 / Snapshot date: **2026-09-12 (UTC)**
- 待审核 / Pending: **181**
- 从快照消失的已核准仓库 / Approved repositories missing from the snapshot: **17**
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

对比上一份快照 **2026-09-11** / vs previous snapshot **2026-09-11**。规则：日增 ≥100★；已核准仓新入 Top 200（且 Δ≥50）/ 名次跃升 ≥50 / 冲入 Top 20；待审仓 ≥100★ 且核准后将进入 Top 200。

- 看 Star 是否与 fork、提交活跃度、仓库年龄匹配（高星零 fork、创建当天几百星，多为刷星）
- 是否把已有高星的通用项目贴上 `dsh-plugin` Topic 蹭榜——插件本身可进目录，但应加入 `leaderboard_exclusions`，理由写清 stars accrued as …
- 待审仓若核准会直接冲进 Top 20 / Top 200，先确认热度来自 **DSH 插件本身**
- 已核准仓的异常跃升：确认后同样可记入 `leaderboard_exclusions`，不必下架目录

Check stars against forks, commit activity and age (hundreds of stars on day one, or high stars with zero forks, usually look bought). A generic high-star project that only just tagged `dsh-plugin` can stay in the catalog but should go to `leaderboard_exclusions` (reason: stars accrued as …). If approving a pending repo would drop it into Top 20 / Top 200, confirm the audience is the DSH plugin itself.

- 告警数 / Alerts: **1**

| Project | Queue | Stars | Δ | Forks | Age | Signals | 审核提示 / Hint |
| --- | --- | ---: | ---: | ---: | ---: | --- | --- |
| ⚠️ [reactive-resume/reactive-resume](https://github.com/reactive-resume/reactive-resume) | 待审 / pending | 42526 | +43 | 4708 | 2361d | 待审高星 | 核准即 Top 1 |


| # | Project | Stars | Created | First seen | Description |
| ---: | --- | ---: | ---: | ---: | --- |
| 1 | [reactive-resume/reactive-resume](https://github.com/reactive-resume/reactive-resume) ⚠️ | 42526 | 2020-03-25 | 2026-09-12 | A one-of-a-kind resume builder that keeps your privacy in mind. Completely secure, customizable, portable, open-source and free forever. Try it out today! |
| 2 | [yinnho/aginxbrowser](https://github.com/yinnho/aginxbrowser) | 19 | 2026-06-19 | 2026-09-12 | The browser built for AI agents — fetch live pages as markdown, render JS/SPAs with built-in V8, take screenshots without Chromium, meta-search 5 engines, and drive interactive login sessions. One Rust binary, stealth TLS fingerprints, MCP native for Claude Code & Cursor. Headless browser alternative to Puppeteer/Playwright. |
| 3 | [lanbaolu/dsh-fail-soft](https://github.com/lanbaolu/dsh-fail-soft) | 8 | 2026-08-18 | 2026-09-12 | ⛔ 已停止更新（2026-09-12）：坏插件隔离等保底能力已内置于 DSH Desktop → 请直接使用 https://github.com/dataelement/dsh-desktop |
| 4 | [Stellum-Waq/dsh-pet-ronaldo](https://github.com/Stellum-Waq/dsh-pet-ronaldo) | 5 | 2026-08-15 | 2026-09-12 | C罗桌宠 · DeepSeek Harness 桌面宠物插件：葡萄牙 7 号 chibi 吉祥物，随 Agent 状态切换动画，对话完成 SIU 庆祝 + 提示音，支持导入自定义 spritesheet 统一管理 |
| 5 | [KhalilYamber/dsh-tidewatch](https://github.com/KhalilYamber/dsh-tidewatch) | 3 | 2026-08-19 | 2026-09-12 | DeepSeek 峰谷时刻悬浮徽章 · dsh plugin：实时峰谷档位、下一阶段倒计时、本次会话 API 花费（含三段历史价格档）\| A floating tide badge for DeepSeek Harness: live peak/off-peak phase, countdown and session cost. |
| 6 | [Menghuan1918/dsh-apollo](https://github.com/Menghuan1918/dsh-apollo) | 3 | 2026-09-09 | 2026-09-12 | 把单一会话不可能的巨任务拆成无数可验证子系统，大规模并行有纪律执行 |
| 7 | [minhdevtry/dsh-markdown-ide](https://github.com/minhdevtry/dsh-markdown-ide) | 3 | 2026-08-14 | 2026-09-12 | DSH Plugin for Markdown like Notion experience |
| 8 | [yan-mc/dsh-normify](https://github.com/yan-mc/dsh-normify) | 3 | 2026-09-06 | 2026-09-12 | Normify · DSH 插件：把项目架构写成归一化的分形模块树，三层校验（写时 / 校验 / 冻结回执）、30 个 normify_* 工具 + normify-gen 技能，一键渲染单文件交互式架构图；支持伴随式开发（change_open → brief → check → 实施 → refresh → change_close）。 |
| 9 | [StyleJeke/dsh-tunnel-plugin](https://github.com/StyleJeke/dsh-tunnel-plugin) | 2 | 2026-09-12 | 2026-09-12 | 把本机的 DeepSeek Harness Web GUI 安全地发布到公网， 让你在外面用浏览器就能用家里那台机器。 |
| 10 | [wwwangzilin/dsh-luna-preset](https://github.com/wwwangzilin/dsh-luna-preset) | 2 | 2026-09-12 | 2026-09-12 | DeepSeek Harness 的「露娜模式」agent preset：魔界小恶魔人设 + 六层情感引擎（emotion_sense），能力等同内置 standard preset |
| 11 | [xiaomujiang/dsh-user-question-nav](https://github.com/xiaomujiang/dsh-user-question-nav) | 2 | 2026-08-24 | 2026-09-12 | 在 DeepSeek Harness 对话界面中快速定位上一个/下一个用户问题。点击浮动按钮自动滚动到对应位置，告别手动滑动查找 |
| 12 | [173787247/dsh-wsl-obscura](https://github.com/173787247/dsh-wsl-obscura) | 1 | 2026-09-05 | 2026-09-12 | DeepSeek Harness tools: drive Obscura headless browser from WSL. |
| 13 | [alk233/dsh-wechat-status](https://github.com/alk233/dsh-wechat-status) | 1 | 2026-09-12 | 2026-09-12 | WeChat login watchdog for DSH: surfaces dsh-wechat session loss as a Web UI banner instead of silently dropping queued messages. AI-generated, educational use only. |
| 14 | [apex-mochen/dsh-clock-context](https://github.com/apex-mochen/dsh-clock-context) | 1 | 2026-09-12 | 2026-09-12 | Give your DSH agent a clock: injects the current date and time into the runtime context on every turn, so the agent can read the time instead of inferring it. |
| 15 | [canelaslorenzoenego-ai/Orderzx](https://github.com/canelaslorenzoenego-ai/Orderzx) | 1 | 2026-09-12 | 2026-09-12 | A live, stealth-capable, autonomous Chrome inside your DeepSeek Harness conversation — set-of-marks vision, Chrome-for-Android desktop-view parity, human takeover, 4-tier CAPTCHA handoff, standalone panel for any device (dsh-browser plugin). |
| 16 | [chengxianglibra/dsh-data-analysis](https://github.com/chengxianglibra/dsh-data-analysis) | 1 | 2026-08-26 | 2026-09-12 | data analysis plugin for deepseek harness. |
| 17 | [Clearailhc/clearai-dsh](https://github.com/Clearailhc/clearai-dsh) | 1 | 2026-09-12 | 2026-09-12 | ClearAI is a native DSH plugin that brings the Epistemic Loop to DeepSeek Harness. |
| 18 | [Dayi-Z/dsh-learn-wiki](https://github.com/Dayi-Z/dsh-learn-wiki) | 1 | 2026-08-26 | 2026-09-12 | 边做边学知识库：CRAG 式纠错检索（L1 Markdown wiki + L2 Hindsight）。agent 反复撞同一堵墙时后台限流联网补料，蒸馏落 staged，两段式 commit 才进召回。DSH 插件。 |
| 19 | [fangwen9527/dsh-composer-ux](https://github.com/fangwen9527/dsh-composer-ux) | 1 | 2026-09-12 | 2026-09-12 | DSH Web 输入体验插件：发送/换行键位切换、右键菜单、面板滚动与尺寸记忆、OpenCode 请求头自动注入 |
| 20 | [GuoMonth/dsh-erp](https://github.com/GuoMonth/dsh-erp) | 1 | 2026-09-11 | 2026-09-12 | ERP learning and automation plugin targeting dsh 0.1.5 rc2, with evidence-backed knowledge and mandatory approval before ERP writes. |
| 21 | [jackeyunjie/dsh-rule-lens](https://github.com/jackeyunjie/dsh-rule-lens) | 1 | 2026-09-12 | 2026-09-12 | 规则透镜（RuleScope Lens）— DSH 本地插件：AGENTS.md/rules 加载可视化、预算治理、硬拦截、Lint、遵守率 \| Rule visibility, budget governance & hard guards for DeepSeek Harness |
| 22 | [Jackson-chen97/dsh-devops](https://github.com/Jackson-chen97/dsh-devops) | 1 | 2026-09-11 | 2026-09-12 | GitLab + Kubernetes monitoring plugin for DSH — track CI/CD pipelines and K8s cluster health in one place. |
| 23 | [jiale-li-orion/dsh-meshfin](https://github.com/jiale-li-orion/dsh-meshfin) | 1 | 2026-08-20 | 2026-09-12 | One agent across many devices — a multi-device capability runtime and personal workbench for persistent agents, built on DeepSeek Harness. |
| 24 | [lcestou/dsh-oh-my-claude](https://github.com/lcestou/dsh-oh-my-claude) | 1 | 2026-09-11 | 2026-09-12 | Claude Code CLI as an LLM provider for dsh (DeepSeek Harness): live model list, per-session resume, approval relay, images, a memory/rewind/changes panel, and workspaces on remote SSH boxes |
| 25 | [log-li/dsh-peakrate](https://github.com/log-li/dsh-peakrate) | 1 | 2026-09-11 | 2026-09-12 | Peak / off-peak rate badges for DeepSeek Harness — per provider, per model, in the model selector and the composer tool row. Judges each provider by its own time zone and schedule instead of DeepSeek-only hours. |
| 26 | [MurasakiIzumi/dsh-quake-alert](https://github.com/MurasakiIzumi/dsh-quake-alert) | 1 | 2026-09-07 | 2026-09-12 | Real-time Japanese earthquake, EEW, tsunami and JMA weather alerts for DeepSeek Harness (DSH) — matched against your watch regions and thresholds. |
| 27 | [rakibulrocky14/dsh-cli](https://github.com/rakibulrocky14/dsh-cli) | 1 | 2026-09-12 | 2026-09-12 | DeepSeek Harness in the terminal — Web-GUI-parity Cordis CLI plugin with full-screen TUI. |
| 28 | [shinzarou-eng/dsh-codebase-chat](https://github.com/shinzarou-eng/dsh-codebase-chat) | 1 | 2026-09-11 | 2026-09-12 | Multi-language codebase intelligence for DeepSeek Harness and MCP IDEs. Chat, search, audit, refactor, and board-ready reports from local code. |
| 29 | [tamashi486/dsh-openspec](https://github.com/tamashi486/dsh-openspec) | 1 | 2026-09-11 | 2026-09-12 | 把 OpenSpec（规范驱动开发）接入 DeepSeek Harness：内置六个 agent skill，并从插件自身依赖解析 openspec CLI，无需全局安装、无需按项目拷贝 .agents/skills ｜ OpenSpec (spec-driven development) for DeepSeek Harness: six bundled agent skills + CLI resolution from the plugin dependency. No global install. |
| 30 | [weibaohui/dsh-process](https://github.com/weibaohui/dsh-process) | 1 | 2026-09-08 | 2026-09-12 | dsh 插件 · 工艺管理：把 ntd 的「工艺」（Process，多阶段·多环节 agent 工作流模板）接进 dsh web——浏览/编辑/校验/导入导出/AI 生成，agent 可用 process_* 工具按工艺推进 |
| 31 | [yukitakasama/dsh-wsl-preset](https://github.com/yukitakasama/dsh-wsl-preset) | 1 | 2026-09-05 | 2026-09-12 | DeepSeek Harness plugin: installs the 'wsl' agent preset for Windows WSL |
| 32 | [zjuatri/dsh-terminal-plugin](https://github.com/zjuatri/dsh-terminal-plugin) | 1 | 2026-09-11 | 2026-09-12 | VS Code–style PTY terminal panel for the DeepSeek Harness Web UI, with tabs, reconnectable sessions, and xterm.js. |
| 33 | [1032740078/dsh-web-url-view](https://github.com/1032740078/dsh-web-url-view) | 0 | 2026-09-11 | 2026-09-12 | Shows the DSH Web GUI access URLs in Settings, including a stable fixed address that survives desktop restarts and is reachable from other devices on the same LAN. 在设置页显示固定的 Web 访问地址，局域网内其他设备也能直接打开。 |
| 34 | [1Vewton/dsh-edu](https://github.com/1Vewton/dsh-edu) | 0 | 2026-09-12 | 2026-09-12 | The educational version of deepseek harness |
| 35 | [233fxr-collab/dsh-launch-in-one-click](https://github.com/233fxr-collab/dsh-launch-in-one-click) | 0 | 2026-09-12 | 2026-09-12 | A DeepSeek Harness plugin for Windows: writes a self-contained one-click launcher, and refuses to start a second instance when the target port already serves one. / 一个 Windows 专用的 DeepSeek Harness 插件：写入自包含的一键启动器；目标端口已有 Harness 实例时拒绝启动第二个。 |
| 36 | [2432450223/dsh-image-governor](https://github.com/2432450223/dsh-image-governor) | 0 | 2026-09-12 | 2026-09-12 | Session image payload governor for DeepSeek Harness: audit which images a session still ships, pick the ones to keep, and move the rest out of the model context. |
| 37 | [3121455692atou-sudo/dsh-tavern-mode](https://github.com/3121455692atou-sudo/dsh-tavern-mode) | 0 | 2026-09-12 | 2026-09-12 | DSH 酒馆模式：角色卡、预设、独立角色记忆与共享头像 |
| 38 | [addie-ace/dsh-livebench-rankings](https://github.com/addie-ace/dsh-livebench-rankings) | 0 | 2026-09-06 | 2026-09-12 | LiveBench AI 能力排行榜 UI 插件 for DeepSeek Harness：拉取 livebench.ai 官方数据，筛选/对比 AI 模型并导出 CSV。 |
| 39 | [AGImentu/dsh-turn-chime](https://github.com/AGImentu/dsh-turn-chime) | 0 | 2026-09-12 | 2026-09-12 | DSH (DeepSeek Harness) Web 插件：任务完成后播放提示音（可开关、可调音量、可上传自己的音频；内置提示音由脚本合成） |
| 40 | [AkinoHaruka/companion-memory](https://github.com/AkinoHaruka/companion-memory) | 0 | 2026-09-12 | 2026-09-12 | 面向 AI 伴侣的长期记忆：受治理的准入、提及闸门与结构化边界保护 |
| 41 | [alcheme-labs/dsh-experience-map](https://github.com/alcheme-labs/dsh-experience-map) | 0 | 2026-09-12 | 2026-09-12 | dsh-experience-map |
| 42 | [AlienGene/dsh-llm-balance-siderbar](https://github.com/AlienGene/dsh-llm-balance-siderbar) | 0 | 2026-09-11 | 2026-09-12 | DeepSeek Harness plugin for querying LLM service provider usage: reads each configured provider's remaining balance or subscription quota and shows it in an always-visible card in the web GUI |
| 43 | [aliensweety/dsh-usage-dock](https://github.com/aliensweety/dsh-usage-dock) | 0 | 2026-09-12 | 2026-09-12 | DSH web plugin: per-session CNY cost pill that renders into the composer's shipped statistics row |
| 44 | [americanjeff/dsh-image-settings](https://github.com/americanjeff/dsh-image-settings) | 0 | 2026-09-12 | 2026-09-12 | User-tunable inline image display for dsh web sessions: larger, auto-unrolled read_image tool view with an Image settings card |
| 45 | [andrepontesmelo/deep-horizon](https://github.com/andrepontesmelo/deep-horizon) | 0 | 2026-09-10 | 2026-09-12 | Deep Horizon is a set an AI plugin for injecting long term goals |
| 46 | [andrepontesmelo/dsh-wayfinder-ui](https://github.com/andrepontesmelo/dsh-wayfinder-ui) | 0 | 2026-09-12 | 2026-09-12 | DSH plugin: spawns one live session per ready Wayfinder task and draws the dependency map in the chat GUI |
| 47 | [Artenx/dsh-honeybee](https://github.com/Artenx/dsh-honeybee) | 0 | 2026-09-03 | 2026-09-12 | 基于 deepseek-harness 的云端 Agent 工作台，随时随地开始实现你的想法 |
| 48 | [aytacbilgisayar-hub/dsh-locale-tr](https://github.com/aytacbilgisayar-hub/dsh-locale-tr) | 0 | 2026-09-11 | 2026-09-12 | Turkish (Türkçe) language pack for DeepSeek Harness (dsh) — client plugin registering the tr UI locale. |
| 49 | [caesarjue/dsh-audio-visualizer](https://github.com/caesarjue/dsh-audio-visualizer) | 0 | 2026-09-12 | 2026-09-12 | System-audio driven UI visualizer for DeepSeek Harness (dsh web / DSH Desktop): a draggable 48-band spectrum chip + frame-wide bass glow. |
| 50 | [Carrick-K7/dsh-keep-going](https://github.com/Carrick-K7/dsh-keep-going) | 0 | 2026-09-12 | 2026-09-12 | Restart DSH, then carry on: the answer in progress finishes, DSH closes in an orderly way, and every conversation the restart interrupted is woken. |
| 51 | [CCYellowStar2/astrbot_plugin_dsh](https://github.com/CCYellowStar2/astrbot_plugin_dsh) | 0 | 2026-09-12 | 2026-09-12 | AstrBot plugin: forward selected IM conversations to a local DeepSeek Harness agent (needs dsh-astrbot-ingress) |
| 52 | [CCYellowStar2/dsh-astrbot-ingress](https://github.com/CCYellowStar2/dsh-astrbot-ingress) | 0 | 2026-09-12 | 2026-09-12 | HTTP ingress plugin: let AstrBot (QQ / OneBot / official IM) drive a local DeepSeek Harness agent |
| 53 | [cheesewoo/dsh-qqbot-dafeiyu](https://github.com/cheesewoo/dsh-qqbot-dafeiyu) | 0 | 2026-09-12 | 2026-09-12 | QQ Bot IM channel plugin for DeepSeek Harness (dsh): per-peer sessions, image generation, TTS voice replies, attachments. |
| 54 | [chengyingshe/dsh-desktop-pet](https://github.com/chengyingshe/dsh-desktop-pet) | 0 | 2026-09-12 | 2026-09-12 | Interactive Shin-chan desktop pet plugin for the DeepSeek Harness Web GUI. |
| 55 | [cherrchen/dsh-plugin-multi-root-workspace](https://github.com/cherrchen/dsh-plugin-multi-root-workspace) | 0 | 2026-09-11 | 2026-09-12 | 多文件夹 workspace：让 DSH（DeepSeek Harness）的 Agent 不只能读写主目录，还能同时读写你添加的其他文件夹。Multi-folder workspace for DeepSeek Harness: let the agent read and write several folders at once, not just the primary one. |
| 56 | [CN-WenYu/dsh-live-model-catalog](https://github.com/CN-WenYu/dsh-live-model-catalog) | 0 | 2026-09-11 | 2026-09-12 | DSH 插件：让 llm-pi-ai 路由（含自定义服务商）的模型目录与推理档位跟着端点更新——补上新模型与 contextWindow/maxTokens/input/reasoningEfforts，端点给出推理信息即写入思考档位，并修好「获取可用模型」按钮；只走官方 settings 接缝，不打补丁、可卸载。\| DSH plugin: keeps llm-pi-ai routes (hand-written and custom providers included) in step with their own /models: new models, capabilities, reasoning levels, live fetch button. No patching. |
| 57 | [cnkids/dsh-office-toolkit](https://github.com/cnkids/dsh-office-toolkit) | 0 | 2026-09-12 | 2026-09-12 | DSH 宿主插件：给 AI 智能体增加读写 Word/Excel 的工具（docx/xlsx/xls/doc/rtf/odt，纯 JS 跨平台）｜ DSH host plugin: Word/Excel read & write tools for AI agents |
| 58 | [Dalcui/dsh-session-notice](https://github.com/Dalcui/dsh-session-notice) | 0 | 2026-09-12 | 2026-09-12 | DSH 会话 Bark 通知插件：会话头部按钮切换「会通知」状态（持久化），轮次停止时经 Bark 推送到手机；设置页配 server/key 并提供 ping→push→register 三步连通测试 |
| 59 | [Dayi-Z/dsh-safety-restart](https://github.com/Dayi-Z/dsh-safety-restart) | 0 | 2026-09-12 | 2026-09-12 | Safe, seamless restart for DeepSeek Harness: the agent can restart the host itself and resume afterwards. Four gates (restart-loop breaker, other sessions mid-turn, unresolvable profile bundles, unavailable app.relaunch) refuse with a reason instead of forcing it. |
| 60 | [devacc8/dsh-file-explorer](https://github.com/devacc8/dsh-file-explorer) | 0 | 2026-09-09 | 2026-09-12 | Vendored, hardened fork of dsh-file-explorer (DSH web file explorer): workspace confinement, argv-only launching, CSRF/header gate, English UI, theme-matched panel. |
| 61 | [dingguangyi0/dsh-plugin-migration-workbuddy](https://github.com/dingguangyi0/dsh-plugin-migration-workbuddy) | 0 | 2026-09-12 | 2026-09-12 | Migrate WorkBuddy sessions, memories, MCP drafts, and automation tasks into DSH — preview-first, read-only on the source |
| 62 | [DIV7NE/dsh-plugins](https://github.com/DIV7NE/dsh-plugins) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness (DSH) web plugins: a model-generated next prompt in the composer, and an integrated terminal for chat code blocks. |
| 63 | [DoctorxPriestess/dsh-llama-model-manager](https://github.com/DoctorxPriestess/dsh-llama-model-manager) | 0 | 2026-09-10 | 2026-09-12 | A DSH plugin that manages local llama.cpp GGUF model lifecycles, automatically loading and unloading models on demand through an OpenAI-compatible gateway. |
| 64 | [DoctorxPriestess/dsh-status-indicator](https://github.com/DoctorxPriestess/dsh-status-indicator) | 0 | 2026-09-12 | 2026-09-12 | A Windows system-tray indicator that monitors and controls a local DeepSeek Harness (DSH) web instance — the process started by dsh web |
| 65 | [Dragonk/dsh-locale-pl](https://github.com/Dragonk/dsh-locale-pl) | 0 | 2026-09-11 | 2026-09-12 | Polish (Polski) language pack for the DeepSeek Harness web UI — a community DSH client plugin adding pl to Settings → General → Language. |
| 66 | [duanyunlun/dsh-conversation-link](https://github.com/duanyunlun/dsh-conversation-link) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness（DSH）对话互通插件：同一进程里的对话可以互相发现、直接发消息、盯进度、设护栏——不用先绑定，也不用开子代理。多对话协作 / 跨会话通信 / 监工。Peer messaging, supervision & tool guards between conversations. |
| 67 | [ewoowe/session-messages-plugin](https://github.com/ewoowe/session-messages-plugin) | 0 | 2026-09-12 | 2026-09-12 | Searchable message overlay for DSH sessions: jump to any loaded message with the keyboard. |
| 68 | [fuguier001/dsh-imgview](https://github.com/fuguier001/dsh-imgview) | 0 | 2026-09-12 | 2026-09-12 | DSH 对话内图片卡插件：show_image 工具 + 同源图片路由 + 可点击放大灯箱卡片 |
| 69 | [Gan-lang/dsh-project-handbook](https://github.com/Gan-lang/dsh-project-handbook) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness plugin that generates a company-grade project handover and onboarding handbook from repository evidence. |
| 70 | [geoqiao/paseo-deepseek-harness](https://github.com/geoqiao/paseo-deepseek-harness) | 0 | 2026-09-12 | 2026-09-12 | Official DeepSeek Harness ACP runtime in Paseo 0.8: native context resume and complete tool output. |
| 71 | [gezi-wen/dsh-plugin-development](https://github.com/gezi-wen/dsh-plugin-development) | 0 | 2026-09-12 | 2026-09-12 | DSH plugin that ships a skill documenting how to build, debug and publish DSH plugins. Installing the plugin registers the skill. |
| 72 | [gezi-wen/sage-guikit](https://github.com/gezi-wen/sage-guikit) | 0 | 2026-09-12 | 2026-09-12 | Windows desktop-control tools for DeepSeek Harness (DSH): screen layout, annotated screenshots, click / type / key / scroll, window management, and UI Automation structured queries. Zero dependencies, no resident service, no API key. |
| 73 | [henrytian1998/dsh-doctor](https://github.com/henrytian1998/dsh-doctor) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness 诊断插件：把 home、进程、端口、大 session、版本问题收成一份可粘贴的报告。不替代 Desktop / TUI。 |
| 74 | [ice-ai-lab/dsh-plugin-codex-ui](https://github.com/ice-ai-lab/dsh-plugin-codex-ui) | 0 | 2026-09-12 | 2026-09-12 | Codex-style sidebar skin for the DeepSeek Harness Web GUI: a Projects + Recents browser, a New chat row that starts a session without picking a project and allocates its own working directory, and a draft composer that writes nothing until you send. |
| 75 | [inxups/dsh-memento-tab](https://github.com/inxups/dsh-memento-tab) | 0 | 2026-09-12 | 2026-09-12 | Session-scoped memory tab for DeepSeek Harness — a companion plugin to dsh-memento. |
| 76 | [JanisKroja/dsh-web-search-crw](https://github.com/JanisKroja/dsh-web-search-crw) | 0 | 2026-09-12 | 2026-09-12 | Self-hosted web search for DeepSeek Harness (dsh): a ctx.web provider plugin that routes web_search to your own CRW/Firecrawl-compatible server — no third-party API, no keys, no LLM tokens per search. Bring your own backend: CRW (Google via Camoufox) or any POST /v1/search implementation. |
| 77 | [jaxzhou/dsh-file-explorer](https://github.com/jaxzhou/dsh-file-explorer) | 0 | 2026-09-12 | 2026-09-12 | A [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) plugin that adds a **Files** tab to the Conversation View strip — the same level as **Chat** and **Trajectory** — showing the session workspace as a tree with a basic text preview beside it. |
| 78 | [jaxzhou/dsh-mathmatic-symbol](https://github.com/jaxzhou/dsh-mathmatic-symbol) | 0 | 2026-09-12 | 2026-09-12 | Three tools for DeepSeek Harness: typeset LaTeX formulas into images, draw mathematical figures from a declarative spec, and convert a formula or SVG into an image ready to embed in a document.  |
| 79 | [jh-Evil/dsh-music](https://github.com/jh-Evil/dsh-music) | 0 | 2026-09-12 | 2026-09-12 | 音乐播放器卡片插件 for DeepSeek Harness：对话内渲染可交互播放器，网易云/QQ 双后端，玻璃悬浮歌词、节拍气泡特效与多主题 |
| 80 | [jiumengya/dsh-computer-use](https://github.com/jiumengya/dsh-computer-use) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness desktop-control plugin (dsh-computer-use): virtual mouse/keyboard, screen capture, and driver-level input |
| 81 | [jiumengya/dsh-prompt-refine](https://github.com/jiumengya/dsh-prompt-refine) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness prompt-engineering plugin (dsh-prompt-refine): refine vague requests into precise instructions |
| 82 | [jiumengya/dsh-wallpaper](https://github.com/jiumengya/dsh-wallpaper) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness personalization plugin (dsh-wallpaper): Wallpaper Engine live-wallpaper integration |
| 83 | [joinsnow-star/dsh-agentic-proxy](https://github.com/joinsnow-star/dsh-agentic-proxy) | 0 | 2026-09-11 | 2026-09-12 | 给 DeepSeek Harness 的 按命令代理：Agent 自己决定哪条 shell 命令走代理，插件负责安装并托管它所需要的代理内核 —— 不依赖你机器上已装的任何代理软件。 |
| 84 | [justarook1e/dsh-ide-lite](https://github.com/justarook1e/dsh-ide-lite) | 0 | 2026-09-12 | 2026-09-12 | Lightweight IDE-in-the-sidebar plugin for the dsh web GUI: workspace file tree, agent-change review (accept/reject + undo), full editing with diff and rendered markdown, plus an integrated terminal view. |
| 85 | [KasenRi/dsh-orbit-browser-plugins](https://github.com/KasenRi/dsh-orbit-browser-plugins) | 0 | 2026-09-12 | 2026-09-12 | Orbit deterministic engineering orchestration and controlled browser automation plugins for DeepSeek Harness. |
| 86 | [killcerr/dsh-web-search-order](https://github.com/killcerr/dsh-web-search-order) | 0 | 2026-09-12 | 2026-09-12 | DSH plugin: ordered web-search provider fallback (omp-style webSearchOrder) over the providers already registered in ctx.web |
| 87 | [kim1232aa/dsh-mxpage](https://github.com/kim1232aa/dsh-mxpage) | 0 | 2026-09-11 | 2026-09-12 | DeepSeek Harness plugin: MxPage ecommerce product-image pipeline (analyze → plan → VPA → generate). |
| 88 | [Kirisame1969/dsh-project-based-learning](https://github.com/Kirisame1969/dsh-project-based-learning) | 0 | 2026-09-11 | 2026-09-12 | DeepSeek Harness (DSH) 项目制教学教练：学科无关的教学引擎 + 可替换领域包（Unity/C#）。A project-based learning coach shipped as a DSH skill and plugin bundle. |
| 89 | [kitterfast/dsh-ppt-maker](https://github.com/kitterfast/dsh-ppt-maker) | 0 | 2026-09-12 | 2026-09-12 | DSH (DeepSeek Harness) web plugin: adds a PPT 制作 entry to the composer + menu that kicks off a bundled, self-contained PPT workflow prompt. One menu pick, one short message, no repeated approval prompts. |
| 90 | [Koierrr/Thalamus](https://github.com/Koierrr/Thalamus) | 0 | 2026-09-12 | 2026-09-12 | θάλαμος —— 荷马史诗里屋子里最深处的那个房间，也是大脑中接住情绪的那枚丘脑。AI 陪伴微信机器人：DSH 插件，让一个独立的微信号成为一个有性格、有生活、对你特殊的她。 |
| 91 | [kp-z/dsh-mermaid-comm](https://github.com/kp-z/dsh-mermaid-comm) | 0 | 2026-09-12 | 2026-09-12 | DSH plugin: Make AI default to Mermaid diagrams in development conversations — prompt guidance, mermaid_validate syntax check, and output safety gate. Rendering via dsh-mermaid. |
| 92 | [L-ingqin12/dsh-redaction](https://github.com/L-ingqin12/dsh-redaction) | 0 | 2026-09-12 | 2026-09-12 | In-place redaction and prevention policy for DeepSeek Harness session logs - two Cordis plugins plus the platform research behind them |
| 93 | [lalilulelo3/dsh-notify](https://github.com/lalilulelo3/dsh-notify) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness plugin: Windows desktop notifications + sound when an agent turn finishes or the harness is waiting for you. |
| 94 | [Lbunc/dsh-composer-glass](https://github.com/Lbunc/dsh-composer-glass) | 0 | 2026-09-12 | 2026-09-12 | 把 DSH 的输入框变成一整块均匀半透明的毛玻璃面板 \| Turn DSH's input box into a uniform semi-transparent frosted glass panel. |
| 95 | [lengduan/dsh-usage-stats](https://github.com/lengduan/dsh-usage-stats) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness 用量统计插件：本地 SQLite 账本，按天 / 服务商 / 模型统计 token 用量 |
| 96 | [lengmoXXL/dsh-remote-ssh-worktree](https://github.com/lengmoXXL/dsh-remote-ssh-worktree) | 0 | 2026-09-11 | 2026-09-12 | A DeepSeek Harness (DSH) plugin that runs the harness's file, shell, and terminal tools inside a git worktree on a remote machine over SSH. The remote agent installs itself: it ships as a static Rust binary from GitHub Releases, listens on a random loopback port, and updates when the plugin does. |
| 97 | [leolee9086/dsh-session-title-refresh](https://github.com/leolee9086/dsh-session-title-refresh) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness 会话标题插件：在会话菜单中根据对话内容重新总结标题，零运行时依赖 |
| 98 | [leolee9086/SAC_search](https://github.com/leolee9086/SAC_search) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness 多引擎元搜索插件:约 200 个免 API key 搜索引擎,运行时零依赖 |
| 99 | [levodoubt/dsh-longtext-input](https://github.com/levodoubt/dsh-longtext-input) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness 长文本输入插件：把超长正文写进工作区 .dsh-longtext/ 下的 md 文件，输入框只留一个 @ 引用，保持聊天界面简洁。支持 Wallpaper Engine 毛玻璃。 |
| 100 | [lijunyu726/dsh-header-balance](https://github.com/lijunyu726/dsh-header-balance) | 0 | 2026-09-12 | 2026-09-12 | DSH Web GUI 会话页头部余额芯片：经宿主侧 Remote 用你的 API Key 查询 DeepSeek 账户余额，点击跳转充值，悬停可见赠送/充值拆分。API Key 不进浏览器。 |
| 101 | [lijunyu726/dsh-price-phase](https://github.com/lijunyu726/dsh-price-phase) | 0 | 2026-09-12 | 2026-09-12 | DSH Web GUI 峰谷时段徽标：显示 DeepSeek API 当前处于高峰还是空闲时段（周一至周五 9-12/14-18 为高峰，周末全天半价），含距下次切换的倒计时 |
| 102 | [Limbo-137/dsh-typst-preview](https://github.com/Limbo-137/dsh-typst-preview) | 0 | 2026-09-12 | 2026-09-12 | Live Typst preview in the DeepSeek Harness Web UI's native right Sidebar, rendered by a per-file tinymist preview server proxied over the app origin. |
| 103 | [liutian11451-png/dsh-plugin-compact-button](https://github.com/liutian11451-png/dsh-plugin-compact-button) | 0 | 2026-09-11 | 2026-09-12 | Composer compact control for the DeepSeek Harness web UI: a button beside the model selector that runs the deployment's own /compact command. |
| 104 | [liutian11451-png/dsh-plugin-model-config](https://github.com/liutian11451-png/dsh-plugin-model-config) | 0 | 2026-09-11 | 2026-09-12 | Full model-configuration editor for the DeepSeek Harness web Settings > Models page: every field the deployment's model-config schema declares. |
| 105 | [ljsysfurryACE/dsh-agentframe-plugins](https://github.com/ljsysfurryACE/dsh-agentframe-plugins) | 0 | 2026-09-12 | 2026-09-12 | AgentFrame plugin suite for DeepSeek Harness (dsh): memory / compaction / proactive scheduling. Fixed deps, arm64 verified. |
| 106 | [loyalchiiina/dsh-model-fold](https://github.com/loyalchiiina/dsh-model-fold) | 0 | 2026-09-12 | 2026-09-12 | Model picker grouped by source for DeepSeek Harness: source list with a slide-in side panel (or inline fold) for each provider's models |
| 107 | [Lumonote/lumo-harness](https://github.com/Lumonote/lumo-harness) | 0 | 2026-08-23 | 2026-09-12 | 基于deepseek-harness分布式智能体集群 |
| 108 | [luoshuai990529/dsh-context-snapshot-bar](https://github.com/luoshuai990529/dsh-context-snapshot-bar) | 0 | 2026-09-12 | 2026-09-12 | 一个用于观测 deepseek harness web 的运行时上下文快照和上下文轨迹的 dsh UI插件 |
| 109 | [lwy0v0/dsh-browser-agent](https://github.com/lwy0v0/dsh-browser-agent) | 0 | 2026-09-12 | 2026-09-12 | 这是一个Deepseek Harness项目。让模型能像人一样浏览网页 —— 点击、输入、hover、滚动、在页面里直接运行 JS，并配套「HTML 快照缓存 + CSS 选择器读取」「网络请求捕获」「控制台输出查看」。 |
| 110 | [lwy0v0/dsh-miao-vst3](https://github.com/lwy0v0/dsh-miao-vst3) | 0 | 2026-09-12 | 2026-09-12 | 这是一个deepseek harness项目。可以让模型操作vst3插件，注意：暂时不支持vst2。作为一个让模型捏音色的尝试性项目。目前针对serum与nexus做了适配性优化，其他插件可能存在适配性不足的情况。 |
| 111 | [LZG3530606141/dsh-wechat-bridge](https://github.com/LZG3530606141/dsh-wechat-bridge) | 0 | 2026-09-12 | 2026-09-12 | WeChat iLink channel, DSH session bridge, encrypted file delivery, and control CLI for DeepSeek Harness |
| 112 | [M0R1C/dsh-vision-fix-lmstudio](https://github.com/M0R1C/dsh-vision-fix-lmstudio) | 0 | 2026-09-12 | 2026-09-12 | Fixes the error “This turn failed400: 'url' field must be a base64 encoded image.” when using local vision‑enabled models from LM Studio. |
| 113 | [mafeis/dsh-image-guard](https://github.com/mafeis/dsh-image-guard) | 0 | 2026-09-12 | 2026-09-12 | DSH plugin: trims historical images to the provider image budget before sending, learns the image cap from HTTP 400 responses, and retries with fewer images. Reduces vision-token usage and prevents image-heavy sessions from failing. |
| 114 | [Mauit06/dsh-jinhsi-skin](https://github.com/Mauit06/dsh-jinhsi-skin) | 0 | 2026-09-11 | 2026-09-12 | DeepSeek Harness webGUI的今汐主题，Jinhsi (Wuthering Waves) theme for the DeepSeek Harness web GUI |
| 115 | [MichengAI/dsh-pua](https://github.com/MichengAI/dsh-pua) | 0 | 2026-09-12 | 2026-09-12 | PUA for DeepSeek Harness: task persistence, personas, and verification loops |
| 116 | [MrTrujay/dsh-weixin-minigame](https://github.com/MrTrujay/dsh-weixin-minigame) | 0 | 2026-09-11 | 2026-09-12 | Preview, develop, and debug (through logs and screenshots) WeChat Mini Games inside the dsh Web GUI |
| 117 | [mtr587/dsh-deepseek-tide](https://github.com/mtr587/dsh-deepseek-tide) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness Web GUI plugin: DeepSeek API peak/valley pricing indicator in the session header |
| 118 | [NaivG/dsh-network](https://github.com/NaivG/dsh-network) | 0 | 2026-09-12 | 2026-09-12 | Let Deepseek Harness access the internet seamlessly. |
| 119 | [new-Beginner/dsh-thought-fold](https://github.com/new-Beginner/dsh-thought-fold) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness ? Codex ????????????????????? |
| 120 | [nguyenduclong-ict/dsh-plugin-custom-css](https://github.com/nguyenduclong-ict/dsh-plugin-custom-css) | 0 | 2026-09-11 | 2026-09-12 | Custom CSS injection for DeepSeek Harness: a Settings section with an on/off toggle and a live CSS textarea |
| 121 | [NIGHT576/dsh-delete-session](https://github.com/NIGHT576/dsh-delete-session) | 0 | 2026-09-12 | 2026-09-12 | Real deletion for DSH Web conversations: a session-row menu action and a Workspaces-header batch dialog; removes each session's log directory and projection cache. 给 DSH Web 侧栏补上真正的会话删除：右键菜单删单条、区头批量删多条，删掉日志目录与投影缓存。 |
| 122 | [NightPainters/DSH-Ling](https://github.com/NightPainters/DSH-Ling) | 0 | 2026-09-10 | 2026-09-12 | 器灵，在你的DSH中培养具有可成长人格的助手和伴侣，最懂你的工作和生活。Artifact Spirit, Your partner and companion, the growth type personality that grows from your shared memories, understand you the most |
| 123 | [nirvanaslash/dsh-bat2exe](https://github.com/nirvanaslash/dsh-bat2exe) | 0 | 2026-09-12 | 2026-09-12 | Compile Windows .bat/.cmd launchers into real .exe shells from inside DeepSeek Harness: generated icon, C# wrapper, csc compile, optional shortcuts. |
| 124 | [NmouZh/dsh-mattpocock-skills](https://github.com/NmouZh/dsh-mattpocock-skills) | 0 | 2026-09-12 | 2026-09-12 | Matt Pocock's agent skills (mattpocock/skills 1.2.3) as a self-contained DeepSeek Harness plugin: 35 vendored skills + a DSH adaptation layer (58 hand-written rules, 29 mechanical slash normalisations, all occurrence-checked at load) + a model-facing dsh-workflow guide. |
| 125 | [nutsDad/dsh-plugin-vllm-ascend-profiler](https://github.com/nutsDad/dsh-plugin-vllm-ascend-profiler) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness plugin: parse vLLM-Ascend / Ascend NPU profiling artifacts, visualize Host/Device swimlanes plus cost shares, and emit structured, phase-aware optimization advice with Markdown/PDF export. |
| 126 | [openplancc/dsh-fuse](https://github.com/openplancc/dsh-fuse) | 0 | 2026-09-11 | 2026-09-12 | Cost policy plugin for DeepSeek Harness: per-call metering plus an offline fuse that enforces budget, model and reasoning-effort limits before any token is spent. |
| 127 | [ouli-1242/dsh-plugin-tool-management](https://github.com/ouli-1242/dsh-plugin-tool-management) | 0 | 2026-09-12 | 2026-09-12 | 一站式管理 DSH 的 MCP 服务与 Skills：工具级开关、密钥打码、技能回收站 \| Unified MCP & skills manager for DeepSeek Harness: per-tool toggles, secret masking, skill trash |
| 128 | [P02-1010751281/dsh-project-context](https://github.com/P02-1010751281/dsh-project-context) | 0 | 2026-09-12 | 2026-09-12 | dsh (DeepSeek Harness) plugins for project-level persistent context:  session archive with a mechanical index, memory consolidation (CONTEXT.md +  MEMORY.md), low-frequency skill autolearn, and automatic handoff. |
| 129 | [pekeyTeam/dsh-AGE](https://github.com/pekeyTeam/dsh-AGE) | 0 | 2026-09-12 | 2026-09-12 | dsh-AGE 是一个**无聊插件**，用来在 deepseek-harness 的网页界面里模拟「安全组件扫描时卡顿」的体验。 |
| 130 | [PerryLink/dsh-team-rooms](https://github.com/PerryLink/dsh-team-rooms) | 0 | 2026-09-11 | 2026-09-12 | Team rooms for DeepSeek Harness: persistent shared rooms across independent sessions - a message bus, a shared task board and a timeline. Extracted from dsh-background-agents, whose background-agent half is superseded by DSH's native continuable subagents. |
| 131 | [pgnqukezrdxmhjso/dsh-ui-fortifier](https://github.com/pgnqukezrdxmhjso/dsh-ui-fortifier) | 0 | 2026-08-30 | 2026-09-12 | DSH Web UI 强化插件：功能模块可开关，含提供方标签、级联模型选择器、设置面板拖动 等 |
| 132 | [pureexe/dsh-image-base64](https://github.com/pureexe/dsh-image-base64) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness plugin: transcodes images to a base64-safe format (PNG) before a vision request, so gateways like LM Studio (which only accept PNG/JPEG/GIF data URLs) do not reject WebP images. |
| 133 | [pureexe/dsh-mobile-topbar](https://github.com/pureexe/dsh-mobile-topbar) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness plugin: turns the sidebar into a compact top bar on mobile screens to save space |
| 134 | [QDchuan/dsh-github-toolkit](https://github.com/QDchuan/dsh-github-toolkit) | 0 | 2026-09-11 | 2026-09-12 | GitHub tools for DeepSeek Harness: 18 agent-facing github_* tools plus a Web settings page that keeps the PAT in the DSH credential store. |
| 135 | [QDchuan/dsh-voice-input](https://github.com/QDchuan/dsh-voice-input) | 0 | 2026-09-12 | 2026-09-12 | Voice input for DeepSeek Harness: a microphone seat in the composer and a Web settings page that transcribes through the browser or any OpenAI-compatible /audio/transcriptions endpoint, with a fully offline local Whisper server included. |
| 136 | [qgx1992/dsh-ui-tools](https://github.com/qgx1992/dsh-ui-tools) | 0 | 2026-08-27 | 2026-09-12 | DSH web 插件：模型选择双按钮（供应商+模型两级联动，含推理等级调节）+ 侧边栏工作区折叠/展开 |
| 137 | [qimen039-code/dsh-consumer-audit](https://github.com/qimen039-code/dsh-consumer-audit) | 0 | 2026-09-12 | 2026-09-12 | Audit a DSH profile for capabilities nothing consumes, and record completion claims with the evidence that supports them. |
| 138 | [Quimos-M/dsh-turn-cost](https://github.com/Quimos-M/dsh-turn-cost) | 0 | 2026-09-11 | 2026-09-12 | 适用于 DSH Web 的计价插件：按 DeepSeek 官方 API 价格统计并显示每轮 / 每会话花费，含子代理计价与分页明细 |
| 139 | [qzy033/dsh-astrbot-gateway](https://github.com/qzy033/dsh-astrbot-gateway) | 0 | 2026-09-12 | 2026-09-12 | 大肥鱼桥：DSH 与 AstrBot 之间的桥接插件，指令下行、结果只走文件交付，不直发用户 |
| 140 | [shuiiiiimu/dsh-stock-portfolio](https://github.com/shuiiiiimu/dsh-stock-portfolio) | 0 | 2026-09-11 | 2026-09-12 | DeepSeek Harness 中管理股票持仓的插件 |
| 141 | [shxiaooo/dsh-account-quota](https://github.com/shxiaooo/dsh-account-quota) | 0 | 2026-09-11 | 2026-09-12 | DeepSeek Harness web plugin: an ambient balance/usage reading under the composer, with a clickable per-provider detail panel. Every figure is upstream-reported. |
| 142 | [shxtmaker/dsh-token-quota](https://github.com/shxtmaker/dsh-token-quota) | 0 | 2026-08-26 | 2026-09-12 | DSH 用量监控插件：供应商周期限额显示（DeepSeek/OpenCode/Command Code）+ 自动探测 DSH 已添加供应商并自动填入 API Key |
| 143 | [SiriusWJ/dsh-restart-btn](https://github.com/SiriusWJ/dsh-restart-btn) | 0 | 2026-09-11 | 2026-09-12 | DSH 重启按钮插件：设置页一键重启 dsh web，复用桌面启动器机制（node + lib/bin.js、日志重定向、TCP 就绪轮询），修复非 ASCII 路径下计划任务静默失败的问题。 |
| 144 | [SiriusWJ/dsh-rp-tools](https://github.com/SiriusWJ/dsh-rp-tools) | 0 | 2026-09-11 | 2026-09-12 | 跑团 / DM 工具插件（DeepSeek Harness）：中立随机裁决 + 本地 ComfyUI 配图 + 按会话隔离的战役配置（角色卡 / 世界 / 随机表）。TTRPG/DM tools for dsh: dice, local ComfyUI illustrations, per-session campaign state. |
| 145 | [sky1ine139/dsh-plugin-screenshot-ask](https://github.com/sky1ine139/dsh-plugin-screenshot-ask) | 0 | 2026-09-12 | 2026-09-12 | DSH 截图提问插件：原生框选截图直接进输入框，全程不落盘（DeepSeek Harness plugin, Windows） |
| 146 | [tamashi486/dsh-plugins-hub](https://github.com/tamashi486/dsh-plugins-hub) | 0 | 2026-09-12 | 2026-09-12 | Third-party plugin hub for DeepSeek Harness — official/community grouped plugin list inside Settings → Plugins, with update checks, one-click update, uninstall, and live enable/disable. |
| 147 | [Tkingxiao/I-am-Yuike](https://github.com/Tkingxiao/I-am-Yuike) | 0 | 2026-09-11 | 2026-09-12 | 一个猫娘人格扮演插件（伪破限），去除dsh强制加入的附加提示词，只附带工具链和猫娘基准人格的插件 |
| 148 | [uckkk/dsh-live-data](https://github.com/uckkk/dsh-live-data) | 0 | 2026-09-12 | 2026-09-12 | 实时数据聚合插件（10 个工具 / 8 个免密钥公开接口）：汇率、天气、npm、GitHub、PyPI、B站、A股、大盘、金价（元/克）、IP 归属地。All-in-one live-data plugin for DeepSeek Harness. |
| 149 | [vansonffff/dsh-kdocs](https://github.com/vansonffff/dsh-kdocs) | 0 | 2026-09-12 | 2026-09-12 | 金山文档 (WPS 云文档) 接入 DeepSeek Harness：右栏面板 / 预览 / 引用到对话 / 4 个只读 Agent 工具。MIT |
| 150 | [vclike/dsh-delivery-cards](https://github.com/vclike/dsh-delivery-cards) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness 插件的独立交付卡片行：绕开 conversation.chat.turnTail 链被抢占导致的交付卡片消失；11 类文件类型图标、亮暗双主题、零依赖零构建 — DSH plugin: standalone delivery-cards row that renders presented files as cards with file-type icons, dual themes, zero dependencies. |
| 151 | [VviLliAm-qwq/dsh-open-terminal](https://github.com/VviLliAm-qwq/dsh-open-terminal) | 0 | 2026-09-12 | 2026-09-12 | dsh-TUI /term: open a system terminal in a workspace folder — blank opens the working-directory root, a fragment fuzzy-matches folders. |
| 152 | [W233666/dsh-composer-tabs](https://github.com/W233666/dsh-composer-tabs) | 0 | 2026-09-12 | 2026-09-12 | 按照插件分类添加tab页到技能菜单里 |
| 153 | [WangXuexin24/dsh-session-topics](https://github.com/WangXuexin24/dsh-session-topics) | 0 | 2026-09-12 | 2026-09-12 | Sidebar topic grouping plugin for DeepSeek Harness (DSH) - client-only, zero host-service dependency, with offline smoke tests. |
| 154 | [wannanbigpig/dsh-sidebar](https://github.com/wannanbigpig/dsh-sidebar) | 0 | 2026-09-01 | 2026-09-12 | 一个为 DeepSeek Harness 最新源码补齐工程能力的外置插件（Bundle），无需修改宿主源码。插件直接融合进宿主原生 Right Sidebar、文件资源标签和底部 Dock：复用宿主已有的文件树、标签页、拆分/悬浮布局，只补充可编辑高亮、Git Review/提交、Worktree 和交互式 PTY。所有项目操作以当前 Session 的 cwd 为边界 |
| 155 | [wanrenhuifu/NovelNovel](https://github.com/wanrenhuifu/NovelNovel) | 0 | 2026-08-20 | 2026-09-12 | DeepSeek Harness 插件：让 agent 用 novel_* 工具写小说（章节 / SillyTavern 角色卡 / 世界观词条 / 写作预设 / 上下文组装 / 导出），数据落工作区文件 |
| 156 | [weikangzeng07-ops/dsh-hmos-skills](https://github.com/weikangzeng07-ops/dsh-hmos-skills) | 0 | 2026-09-12 | 2026-09-12 | HarmonyOS (鸿蒙) development skills for DeepSeek Harness — 39 official hmos-* skill bundles ported to the DSH skill registry: ArkTS/ArkUI, multi-device adaptation, Kit integration, and DFX crash/leak analysis. |
| 157 | [whoiszzj/dsh-opencodego](https://github.com/whoiszzj/dsh-opencodego) | 0 | 2026-09-12 | 2026-09-12 | 在DSH中支持opencode支持GO订阅，包括模型获取以及能力设置、请求头自适应等 |
| 158 | [wings1848/dsh-rtk](https://github.com/wings1848/dsh-rtk) | 0 | 2026-09-12 | 2026-09-12 | RTK command rewriting and tool-output compaction for the DeepSeek Harness: rewrites bash commands to their rtk equivalents and compacts the result before the model sees it. |
| 159 | [woodfood111/dsh-token-live](https://github.com/woodfood111/dsh-token-live) | 0 | 2026-09-12 | 2026-09-12 | Composer readouts for the DeepSeek Harness: CJK-weighted draft token count, session spend at official peak/idle rates, context occupancy, and what the same usage would have cost on the costliest other model; client-only, with no host half and no credential access. |
| 160 | [WsTe47/dsh-step-clock](https://github.com/WsTe47/dsh-step-clock) | 0 | 2026-09-12 | 2026-09-12 | Live per-step elapsed clock for the DeepSeek Harness web GUI |
| 161 | [WuJiaoJue/dsh-later](https://github.com/WuJiaoJue/dsh-later) | 0 | 2026-09-12 | 2026-09-12 | DSH 会话内定时发送插件 |
| 162 | [WuTong1213/dsh-explorer-plugin](https://github.com/WuTong1213/dsh-explorer-plugin) | 0 | 2026-09-12 | 2026-09-12 | DSH Explorer: VS Code-style file tree + workspace-grouped session tabs |
| 163 | [wwwwangpengggg/dsh-api-balance](https://github.com/wwwwangpengggg/dsh-api-balance) | 0 | 2026-09-12 | 2026-09-12 | DSH 桌面插件：在桌面角落常驻一个置顶小窗，实时显示 DeepSeek API 余额与本次开机消耗的 token。七套配色、可用自己的图片当背景、× 收进托盘。 |
| 164 | [xiaoshengliang2002/dsh-prompt-boost-pro](https://github.com/xiaoshengliang2002/dsh-prompt-boost-pro) | 0 | 2026-09-12 | 2026-09-12 | Enhance the composer draft before sending: a sparkle button in the DSH web GUI rewrites your prompt in a structured or light mode, with an original-versus-enhanced preview. |
| 165 | [xichow0663-gif/yt-research-skill](https://github.com/xichow0663-gif/yt-research-skill) | 0 | 2026-09-11 | 2026-09-12 | An agent skill that batch-researches a YouTube channel's latest N videos — captions first, local ASR fallback — and writes one cross-video report instead of N summaries. Works in DSH, Codex, Claude Code, Hermes and WorkBuddy. |
| 166 | [yangyizhu8/dsh-unread-mark](https://github.com/yangyizhu8/dsh-unread-mark) | 0 | 2026-09-12 | 2026-09-12 | Session-row unread mark for DeepSeek Harness (dsh): Mark unread / Unmark in the session menu pins a red dot that survives reload until cleared. |
| 167 | [Ylight-cpu/dsh-creative-studio](https://github.com/Ylight-cpu/dsh-creative-studio) | 0 | 2026-09-12 | 2026-09-12 | Portable AI image-retouching and video-editing skill pack for DeepSeek Harness: matting with quality tiers, inpainting retouch, text/logo compositing, batch platform exports, footage review, timeline editing. |
| 168 | [Z-Asset/ZA_analysis](https://github.com/Z-Asset/ZA_analysis) | 0 | 2026-09-12 | 2026-09-12 | ZA Research analysis stage — end-to-end model training and estimation for asset pricing + ML/DL research. |
| 169 | [Z-Asset/ZA_data](https://github.com/Z-Asset/ZA_data) | 0 | 2026-09-12 | 2026-09-12 | ZA Research data stage — data discovery and quality assessment for asset pricing + ML/DL research. |
| 170 | [Z-Asset/ZA_literature](https://github.com/Z-Asset/ZA_literature) | 0 | 2026-09-12 | 2026-09-12 | ZA Research literature stage — search, synthesis, and citation-chain tracking for asset pricing + ML/DL research. |
| 171 | [Z-Asset/ZA_ppt](https://github.com/Z-Asset/ZA_ppt) | 0 | 2026-09-12 | 2026-09-12 | ZA Research PPT stage — presentation generation (Beamer/Quarto) from the paper. |
| 172 | [Z-Asset/ZA_report](https://github.com/Z-Asset/ZA_report) | 0 | 2026-09-12 | 2026-09-12 | ZA Research report stage — academic paper writing for asset pricing + ML/DL research. |
| 173 | [zgrajdnhj7806-svg/dsh-deepseek-web](https://github.com/zgrajdnhj7806-svg/dsh-deepseek-web) | 0 | 2026-09-12 | 2026-09-12 | DSH 插件：把 chat.deepseek.com 网页版接进 DeepSeek Harness（deepseek_web_ask / deepseek_web_analyze_lines / deepseek_web_status + 一键登录面板）。纯 Node，MIT License。 |
| 174 | [zhengjy01/dsh-restart](https://github.com/zhengjy01/dsh-restart) | 0 | 2026-09-12 | 2026-09-12 | One-click restart for DeepSeek Harness: a web button (plus a dsh_restart agent tool) hands the relaunch to a detached helper, the page reconnects by itself, and a recovery console shows the boot errors when the new host fails |
| 175 | [zhengjy01/dsh-zhihu](https://github.com/zhengjy01/dsh-zhihu) | 0 | 2026-09-12 | 2026-09-12 | 知乎 CLI 连接插件 for DeepSeek Harness：包装本机 pyzhihu-cli 为 zhihu_* 工具（18 个，写操作默认关闭），附 Web 可视化入口（侧栏「知」球 + 设置页卡片） |
| 176 | [zhiwuli0228/dsh-image-router](https://github.com/zhiwuli0228/dsh-image-router) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness plugin: digest prompt images through a vision model and expose a describe_image tool — without ever changing the session's model. |
| 177 | [zjuatri/dsh-browser-plugin](https://github.com/zjuatri/dsh-browser-plugin) | 0 | 2026-09-11 | 2026-09-12 | A DSH browser sidebar plugin with an isolated Chrome profile for every conversation, live interaction, and agent automation. |
| 178 | [zjuatri/dsh-feishu-plugin](https://github.com/zjuatri/dsh-feishu-plugin) | 0 | 2026-09-11 | 2026-09-12 | A DeepSeek Harness plugin for Feishu tasks, bot chat summaries, and AI-assisted follow-ups. |
| 179 | [zq0951/dsh-voice-gateway](https://github.com/zq0951/dsh-voice-gateway) | 0 | 2026-09-12 | 2026-09-12 | Voice Gateway client surface plugin for the DSH web client: mic status indicator, six-state machine, voiceprint enrollment, and auto-speak controls. |
| 180 | [zxr2115-1/dsh-anime-theme](https://github.com/zxr2115-1/dsh-anime-theme) | 0 | 2026-09-12 | 2026-09-12 | DeepSeek Harness (DSH) 二次元壁纸主题插件 · 随机动漫壁纸 / 四档铺满 / 边缘羽化 / 深浅色自适应 / 可拖动控制坞 ·  theme plugin for DeepSeek Harness |
| 181 | [zzdhsxk/dsh-session-migration-repair](https://github.com/zzdhsxk/dsh-session-migration-repair) | 0 | 2026-09-11 | 2026-09-12 | Repair legacy (format v0) DSH session logs that the current build refuses to migrate — scan, back up, fix, and verify offline against the real v0→v3 migration chain. |

## 从快照消失的已核准仓库 / Approved repositories missing from the snapshot

已核准但已不在当前快照中（删除或改名），核实后从 [data/approved.json](../approved.json) 移除或更新名称。

Approved but no longer present in the current snapshot (deleted or renamed) — after checking, remove them from [data/approved.json](../approved.json) or update the name.

- aiko-dsh-plugins/dsh-bid-studio
- aiko-dsh-plugins/dsh-ontology-kernel
- BaiLiang-233/dsh-off-peak-schedule-widget
- cjm-m/dsh-paste-code-block
- douzhenyu/oh-my-deepseek
- Eidosiny/dsh-accessory-hub
- jiale-li-orion/meshfin
- justarook1e/dsh-file-edit
- Kr-ATG/dsh-done-pill
- laodonge/col-dsh-plugin
- masquerator-coder/dsh-memory
- openplancc/dsh-plugin
- Paloma966/dsh-kaiju
- Paloma966/dsh-mem
- Paloma966/dsh-socrates
- reactive-resume/app
- shxtmaker/dsh-usage-monitor
