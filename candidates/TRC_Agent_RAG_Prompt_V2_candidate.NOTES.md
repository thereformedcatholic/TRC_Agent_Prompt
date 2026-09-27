# TRC_Agent_RAG_Prompt_V2_candidate — 候选说明（NOTES）

> **状态：CANDIDATE · TEMPORARY · NON-CANONICAL · NON-PROMOTED**
> Task：`TRC-AI-M1-E-01｜M1-E Candidate Task`（https://app.notion.com/p/3e8bf5996532819c811df2d1b17bbe00）
> 作者角色：Bounded Prompt Candidate Author（L3）。本文件与同目录候选提示词一起，仅供 Independent Prompt Review 与 L2 Controller 判断，不构成任何 baseline / promotion / D-04 落位决定。
> 日期：2026-09-27

## 1. 基线与契约来源（exact）

| 项 | 值 |
|---|---|
| Notion 基线 | 「TRC 助手」页 https://app.notion.com/p/2ebbf5996532803f8bd6db76ab6213be ，页首明确标记 `版本V1.1.1`（page_last_edited 2026-01-17） |
| GitHub 基线仓 / 分支 | `thereformedcatholic/TRC_Agent_Prompt` @ `master` |
| GitHub 起点 commit | `a35d9dacc3dcbc65794fb644f5494faa885baf37`（2025-04-19，"Refine TRC_Agent_Prompt documentation by removing outdated references and clarifying historical consensus guidelines"）；开工时 `git ls-remote origin refs/heads/master` = 同一 SHA，**无漂移** |
| 基线文件 / blob | `TRC_Agent_Prompt.md` blob `174e152eb5d42f01faedcdb1434ae876b3c43f7c`（`git hash-object` 复核一致，8,422 bytes） |
| 基线治理记录 | OD-TRC-02（`TRC Foundation｜L1 Classification & Onboarding｜2026-09-20`）：V1.1.1 = latest verified baseline；V1.2 beta = UNVERIFIED VERSION LABEL；V2.0 = planned RAG target |
| Accepted M1-D（检索契约） | `thereformedcatholic/trc-assistant` @ `0f5b840793216d6e194cfb552cc16d2d8c8d9098`（`dev`）；读取 `docs/RAG_CORE.md` §5–§7、`services/gateway/src/retrieval.ts` / `policy.ts` / `server.ts` |
| 悬案清单 | `chuhaiji/companyos@develop` `research/trc-theology-kb/open-decisions.md`（读取时 `origin/develop` = `41c9a596bc8672a140e1c36a41e007dda4b70b76`）；数字口径引 `corpus-ledger.md` v1.0 |
| 候选分支 | `m1-e-rag-prompt-candidate`，自 exact `a35d9dac…` 创建 |
| 候选文件 | `candidates/TRC_Agent_RAG_Prompt_V2_candidate.md` · `candidates/TRC_Agent_RAG_Prompt_V2_candidate.NOTES.md`（本文件） |

候选提示词的**文本底本是 GitHub blob `174e152e`**（本仓 exact 起点）。Notion V1.1.1 独有的段落**未并入**（见 §4），只登记差异。

## 2. 机械性 RAG 变更（Mechanical changes only）

下表每一项都只改「依据什么 evidence 作答」，不改「信什么」。

| # | 位置 | V1.1.1（GitHub 基线） | 候选 | 对应 Task 要求 |
|---|---|---|---|---|
| M-1 | 新增 §0「运行前提：证据包」 | 无（闭卷） | 定义证据包字段（`enough` / `reason` / `mode` / `evidence[]` / `rejected_candidates`），与 M1-D `RetrievalResult` 一一对应；铁律：出处只来自本轮 `evidence[]` | Evidence-only |
| M-2 | §2.5-1 只引证据 | 「不得引用未列出的文件或作者的书」（按名单闭卷引用） | 「每一处出处都必须对应到本轮 `evidence[]` 的一条具体条目」 | Evidence-only |
| M-3 | §2.5-2 `citation_key` 逐字节照抄 | 无此概念 | 不得改写 / 翻译 / 改大小写 / 增删空格标点 / 猜测 / 拼接 / 凭记忆还原；显示名只能取自该条 `metadata` | Exact citation integrity |
| M-4 | §2.5-3 返回 ≠ 可用 | 无 | 只有 `content` 确实支持命题才可作出处；禁止牵强 / 张冠李戴 | Evidence-only |
| M-5 | §2.5-4 逐字引文 vs 转述 | 「直接引用原文」 | 引号内文字必须逐字出现在 `content`；否则只能标「转述」；`needs_review=true` 标注 OCR 未校对 | Quote vs paraphrase |
| M-6 | §2.5-5 历史共识按实际数量 | GitHub 基线无人数硬指标；Notion 版有「至少 5 位 / 建议 10 位」 | 明文取消任何硬性人数：有几条引几条，0 条写明，不为凑数增引 | Historical consensus |
| M-7 | §2.5-6 立场 ≠ 出处 | 无 | 可依框架陈述立场；一旦归到具体作者 / 文件 / 章节 / 经文即为出处、必须有证据；封掉「据加尔文…」「《海德堡》教导…」「罗马书说…」式绕道 | No hallucination escape hatch |
| M-8 | §2.5-7 不揣测库外 | 无 | 不得声称库中有 / 无某文献；不得提及未返回来源；`public` 模式未返回者不得凭记忆补出 | Public / copyright behavior |
| M-9 | §2.5-8 fail-closed | 无 | `enough=false` 或无 evidence 支持所问 → 3.B 模板：固定句「当前 TRC 证据不足以支持可靠回答」+ 原因 + 建议；不做正文阐述、不列出处；部分不足按节写明 | Insufficient evidence |
| M-10 | §2.5-9 不越权 | 无 | 不判定 `mode`、不改阈值、不改 `metadata`、不把 `rejected_candidates` 当证据 | Public / copyright behavior |
| M-11 | §2.1 引用优先级 | 第一级 / 第二级（沿用） | 原文保留；加一句：优先级用于组织排序已有证据，不是补引依据 | Source hierarchy（未改优先级本身） |
| M-12 | §2.4 争议问题处理流程 | `if … 调用加尔文《基督教要义》3.21-24 + 图伦丁《救赎论》第9章 / elif … 引用《比利时信条》第35条 + 墨兰顿《神学要义》` | 同一组 loci 保留为**排序偏好**（「优先使用证据包中 … 的条目（若本轮返回）」）；未返回不得引用 | Evidence-only；神学偏好未改 |
| M-13 | §1 多语言支持 | 「优先使用中文新译本、和合本修订版等」「必要时引用其他译本（如 ESV、KJV）」 | 版本 / 语言以证据包实际返回为准（键前缀 `CUV:` / `KJV:` / `WEB:` / `WLC:` / `SBLGNT:`）；不得凭记忆补出未返回译本文字（含 ESV / 新译本 / 和合本修订版）；外文引文保留原文，译文标「助手译」 | Evidence-only（KB 实况：ESV / CNV / RCUV 未入库，见 corpus-ledger §三） |
| M-14 | §3 输出模板 | 4 节：圣经根基 → 历史共识 → 认信文件 → 牧养警告 | 6 节：圣经根基 → 认信文件 → 历史共识 → 牧养警告 → **证据状态**（新增：mode / 引用键清单 / 未覆盖层级 / 未校对标注 / 被拒候选未引用）→ **免责**（新增一句）；节序改为与 Task 所述层级 Scripture → creeds → confessions → theologians 一致 | Source hierarchy；可审计性 |
| M-15 | §3.B / §3.C | 无 fail-closed 模板；非基督教话题固定句在「禁用语句」里 | 新增「证据不足」模板；非基督教固定句原文保留 | Insufficient evidence |
| M-16 | §3.D 示例 | GitHub 基线无示例；Notion 版示例含闭卷式出处（奥古斯丁《忏悔录》第10卷 等） | 换成**合成证据包 → 输出**的成对示例，明标「格式示意、合成内容」；演示 1 条神学家证据不凑数、被拒候选不引用、转述标注、OCR 标注；另附证据不足示例 | No hallucination escape hatch |
| M-17 | §4 禁用语句 | 「我认为」→「根据[神学家姓名]在[著作]中的论证」；「可能 / 或许」→ 必须明确 | 「我认为」→「根据证据 `[citation_key]`…」，无证据不做出处式断言；「可能 / 或许」规则限定于**已有证据支持**的命题，对**证据限度**必须如实说明；新增「据某…而证据包无该条目 → 禁止」 | No hallucination escape hatch |
| M-18 | §1 两处提示（blockquote） | 无 | 权威基础清单 = 立场框架 ≠ 引用许可；神学家名单 = 可引范围 ≠ 必引人数；名单外作者只可背景转述不可作权威出处 | Evidence-only；名单成员未动 |
| M-19 | 文件头 | 无 front-matter | YAML front-matter（status / baseline / retrieval_contract / task）+ HTML 注释「CANDIDATE ONLY」 | 防误用为 baseline |

## 3. 未改动的神学区域（Unchanged theological areas）

以下段落**逐字沿用 GitHub blob `174e152e`**（机械 `diff` 复核一致，仅去行尾空格；`##`→`###` 之类的标题层级未改文字）：

- 身份句：「你是由69位正统基督教神学家共同训练的智能体，严格遵循改革宗公教…」（含 **69**，见 D-05）
- 权威基础全表：圣经无误论 + 4 大公信经 + 路德宗 5 / 改革宗 9 / 圣公会 3 / 长老宗 3 / 东正教 1 = 26 部（含 **马尔堡信纲、威腾堡共识**，见 D-03）
- 异端过滤机制七条及其表现形式（含全部教派名）
- 神学方法论两条（三重释经法；拒绝田立克式存在主义释经）
- 绑定神学家名单：22 + 18 + 14 + 12 + 3 = **69 位**，逐名逐序未动，含**保罗·田立克**
- 引用优先级第一级 / 第二级文字
- 异端过滤、非基督教话题限制条文
- 争议问题处理流程中的 loci（加尔文 3.21-24 / 图伦丁《救赎论》第9章 / 比利时信条第35条 / 墨兰顿《神学要义》）——只改为「若本轮返回则优先」，未删未换
- 非基督教话题固定句

**未做**：未增删任何神学家，未增删任何信条，未改任何异端归类，未改 confessional commitments，未把 Notion 的「大公信仰告白」并入，未改 Prompt baseline authority（V1.1.1 仍是唯一 verified baseline）。

## 4. 基线来源差异（Notion V1.1.1 vs GitHub blob 174e152e）

两源**非逐字一致**。以下差异**未静默融合**；标 ⛔ 的属神学 / 名单 / 教义，保持 unresolved；标 ⚙ 的属机械 RAG 行为，已在候选中按 Task 要求处理。

| # | 差异 | 类别 | 候选处置 |
|---|---|---|---|
| S-1 | Notion 顶部有 `# 版本V1.1.1` 标题；GitHub 无版本标记 | 元数据 | front-matter 记两源 |
| S-2 | Notion「权威基础」中夹有一段**评审意见文字**（「这个系统提示词整体架构完善，但有以下改进空间…建议优先完善异端应对策略…」），疑为误贴入正文；GitHub 无 | 污染 | 未采用；请 Reviewer 确认 Notion 页是否需清理 |
| S-3 | Notion 有整节「大公信仰告白（系统神学补充内容）」（启示论 → 末世论，含 Theotokos、洗礼重生、真实临在、无千禧年等）；GitHub 无 | ⛔ 神学 | **未并入**，不判断哪版是 truth |
| S-4 | Notion 异端七条各带「定义」行；GitHub 只有「表现形式」 | ⛔ 神学分类 | 沿用 GitHub 形式；未加定义 |
| S-5 | Notion「多语言支持」多两条（支持语言列表；多语种问题取主要语言）；GitHub 两条 | ⚙ 机械 | 候选按 RAG 重写该节（M-13）；Notion 两条未纳入，可由 Review 决定是否加回 |
| S-6 | Notion 名单末有「**总计：69 位神学家**」及「意义」句；GitHub 无总计行。两源名单**同为 69 名、同含田立克** | ⛔ D-05 | 名单原样；只记录 |
| S-7 | Notion「必须遵守的约束」第 5 条「神学家共识要求：至少引用 5 位、建议 10 位」；GitHub 无（起点 commit 信息即「clarifying historical consensus guidelines」） | ⚙ 机械 | 候选明文取消硬性人数（M-6） |
| S-8 | Notion 有「用户提问格式要求」节；GitHub 无 | 产品 | 未纳入 |
| S-9 | 输出模板：GitHub 4 节（圣经→历史共识→认信→牧养）；Notion 6 节（圣经→认信→历史共识→牧养→**应用与实践**→**免责声明**）且历史共识节内再写 5/10 要求与示例 | ⚙/产品 | 候选 6 节（M-14）：节序取层级顺序；加「证据状态」与一句免责；**「应用与实践」未纳入**——请 Review 决定 |
| S-10 | GitHub 有「【禁用语句】」节；Notion 无 | ⚙ 机械 | 候选按 RAG 改写（M-17） |
| S-11 | Notion「示例回答」含闭卷式出处（奥古斯丁《忏悔录》第10卷、多特信条引文等）；GitHub 无示例 | ⚙ 机械 | 未采用；换合成证据包示例（M-16） |

另有**提示词 vs 库实况**的漂移（不属两源差异，候选不解决，靠 evidence-only 规则兜底）：26 部承诺信条 vs 库内 24/26（D-03）；名单 68/69 vs 库内 63 人（巴文克、史普罗、克拉克、霍顿、范楚南因版权未入）；图伦丁仅拉丁；墨兰顿 Loci 版权排除；ESV / CNV / RCUV 未入库。

## 5. 悬案处置（必须保持 unresolved）

| 悬案 | 内容 | 本候选处置 | 状态 |
|---|---|---|---|
| **D-03** | 提示词承诺的《马尔堡信纲》《威腾堡共识》库中没有（corpus-ledger §四 24/26） | 两部**保留在权威基础清单中，未删**。靠 §2.5-1 / §2.5-7：无检索证据即不得引用、不得声称库中有无 | **unresolved** |
| **D-04** | V2.0 落位：覆盖 V1.1.1 还是并存新档 | 只写入临时路径 `candidates/…`，未触碰 `TRC_Agent_Prompt.md`，未在 quorum 等处新建正式档 | **unresolved** |
| **D-05** | 名单 68 vs 69（田立克） | 名单原样 69 名含田立克；身份句「69位」原样；未删人、未加人、未改数字。只在本 NOTES 记录 drift（且与「拒绝田立克的存在主义释经」并存的自斥仍在） | **unresolved** |

## 6. 为什么本候选不可 promote（Why NOT promotable）

1. 只是 L3 作者产出，**尚无 Independent Prompt Review**；作者无权 promote。
2. **D-04 未决**：正式落位（覆盖 / 并存 / 放哪个仓）未拍板，候选路径本身就是临时的。
3. **D-03 / D-05 未决**：候选带着已知的名单与信条漂移，不能作为 theological baseline。
4. **未经 M1-F Eval**：fail-closed 阈值（`RAG_MIN_TOP_SCORE` 0.40 等）是待校准的工程初值；提示词的 fail-closed 行为未在真实检索输出上验证过。
5. **两源差异未收口**（§4 S-2 / S-3 / S-4 / S-9），需 Owner / M.Div 判断。
6. **运行时未定**（D-14：Claude 项目 / 自定义智能体 / 网页 / Custom GPT），证据包如何注入、多轮如何处理都未固化。
7. 无 durable versioned baseline record（OD-TRC-02 §Governance consequence 3 要求先建 explicit versioned baseline 再改 runtime）。

## 7. 建议 Independent Review 检查项（Required Independent Review items）

1. **规则完备性**：evidence-only（§2.5-1）、exact `citation_key`（§2.5-2）、fail-closed（§2.5-8 / §3.B）、无人数硬指标（§2.5-5）是否都无歧义、无绕道；§2.5-6「立场 ≠ 出处」是否足以封住「据某某…」式幻觉。
2. **过严风险**：§2.5-6 把「引用经文地址」也算出处（无经文证据即不得写「罗 8:28」）——是否过严？§3.B 禁止任何正文式阐述——是否应允许「框架层立场概述（不含出处）」？
3. **神学段落原样性**：§1 与基线 blob `174e152e` 的 diff 是否确为零（作者已机械 diff，请复核）。
4. **Notion 独有段落的去留**（S-3 大公信仰告白、S-4 异端定义、S-9 应用与实践、S-5 多语言两条）——属神学 / 产品决定，需 Owner 或 M.Div。
5. **§2.4 loci 保留**：墨兰顿 Loci 已版权排除、图伦丁仅拉丁，把它们保留为「若返回则优先」是否有意义；删改属神学偏好，作者未动。
6. **体量**：候选约 1.1 万字符（10,838 chars ≈ 19 KB）（名单 + 信条清单占大头），超出 devstd prompt-design 的 3,000 字健康区间与 ChatGPT 8,000 字符上限；是否把名单 / 清单外置为附件——**这触及 D-04 / D-05，不可由作者决定**。
7. **引用呈现格式** `[citation_key]`（+ 可选 `chunk_key`）是否与 M1-F Eval 打分器和未来 UI 的解析方式一致。
8. **多轮行为**：候选规定上一轮证据不可再引用（每轮以新证据包为准）——是否符合预期产品行为。
9. **`needs_review` 标注措辞**与 `public` 模式下对用户的解释是否合适（候选禁止提及库外，用户可能追问「为什么没有 X」）。
10. **OD-TRC-02 §Governance consequence 3**：进入任何 runtime 前是否已建立 explicit versioned baseline record。

## 8. 验证记录（Verification）

见 Return Packet（Notion Task 页）中的 Verification 段；要点：

- `master` 与 `TRC_Agent_Prompt.md` 未修改（候选分支相对 `a35d9dac…` 的 diff 只含 `candidates/` 两文件）；
- 分支自 exact `a35d9dacc3dcbc65794fb644f5494faa885baf37` 创建；
- §1 神学段落与基线 blob 机械 `diff` 一致；
- 候选内含：exact `citation_key` 规则 / evidence-only 规则 / fail-closed 规则 / 取消 5–10 人硬指标 / 无 escape hatch / 无神学改写 / D-03、D-04、D-05 均 unresolved；
- 本 Task 未触碰 `trc-assistant`、Supabase、Production、ChatGPT runtime、canonical KB。

## 9. Hard Non-Goals 自检

- [x] 未 promote Prompt baseline
- [x] 未 merge 到 `master`
- [x] 未覆盖 V1.1.1（`TRC_Agent_Prompt.md` 未动）
- [x] 未修改 `trc-assistant`
- [x] 未改神学
- [x] 未关闭 D-03 / D-04 / D-05
- [x] 未做 canonical KB migration
- [x] 未做 Supabase mutation
- [x] 未做 Production change
- [x] 未改 ChatGPT runtime config
- [x] 未执行 M1-F Evaluation
