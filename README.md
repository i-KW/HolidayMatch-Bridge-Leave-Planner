# HolidayMatch · Bridge Leave Planner 🗺️
跨国朋友/家庭一起规划假期：各自去找各国放假通知的麻烦？在群里敲一个个日期还对不上星期？不同国家的日历、假期混在一起、没有可视化参考让人眼花缭乱？这个项目致力于把多个国家的工作日和节假日按日历格式对照做成了一份好看的网页，附赠AI的拼假方案帮你请3休11，打印友好,截图友好,协作利器! HolidayMatch不是"AI生成日历"，是"自动化,多语言,本地化的跨国假期对齐规划家"——有简洁高效的SKILL自动化,防幻觉,产品和边界的设计!(English introduction on PART2)  
## 🧠 产品思维 & 防幻觉设计
| 层级 | 设计点 | 核心机制 | 防幻觉策略 | 用户价值 |
|:---|:---|:---|:---|:---|
| **⏰ 时间感知** | 动态年份搜索和判断 | 识别"下周出行"等模糊表述；≤1月默认今年；≥2月主动询问；12月提示跨年 | 避免LLM写死参数,遵循历史数据缺乏时间感 | 对齐用户需求和日程规划场景，减少无效输出 |
| **📅 标准底板** | ISO 8601 周历 + 公历校验 | WebSearch确认当年月份天数、星期对应、闰年处理 | 防止LLM的历史数据和幻觉，年份和星期对应、月份天数错误； | 年月星期准确，跨国对齐准确 |
| **🌍 特殊规则** | 分国别的边界条件库 | 中国调休/农历、英国顺延、伊斯兰浮动节日、日本黄金周、西班牙区域差异等 | 覆盖非标场景，各国本地化和特殊规则 | 真实可用，解决各国和本地化的特殊场景 |
| **📊 假期分级** | A/B/C 三级假期分类体系 | A类固定日期直接填入；B类规则推算并验证；C类待政府发布，用法定框架兜底 | 不猜测未发布数据，标注置信度，分类处理各类假期的不确定性 | 数据空缺时不产生幻觉，诚实展示待定状态 |
| **⚡ 并行架构** | 各国独立并行检索；分源独立检索 | 各国、假期信息 + 时间多源并发并发查询 | 多源交叉验证 | 速度×2，上下文干扰↓，准确性↑ |
| **🔍 验证兜底** | 置信度标记 + 来源透明 | 确认信息来源置信度，多源对比校验，主动标明AI生成等 | 不伪装确定性，诚实暴露边界 | 提高准确率，提示AI内容和易错场景 |
| **⚖️ 冲突仲裁** | 不投票，追源头 | 政府源一票否决；第三方源一致则采用；互相冲突则追加搜索或标记待确认 | 避免AI在数据冲突时"选边站"，透明展示各方来源 | 用户知悉信息可靠度，冲突时不下结论而是等待更多数据 |
| **🌸 增值和设计** | （待开发）导出和分享，丰富和自定义的样式 | 一键导出飞书表格/PDF/图片，富媒体样式如Notion，自定义背景图 | （待开发） | 方便分享和协作裂变，设计的情绪价值 |
<img width="1239" height="708" alt="image" src="https://github.com/user-attachments/assets/992293e2-0526-4d20-8ed7-2580d14f66c7" />

<img width="1031" height="531" alt="holidaymatchSnipaste_2026-06-18_23-28-21" src="https://github.com/user-attachments/assets/0bd064c7-e1da-47bb-b1d3-67703b6b7cde" />

## AI SKILL  
● .claude/skills/  
├── holiday-match-bridge-leave.md    ← SKILL for Claude Code/openCLAW. English version   
└── SKILL Chinese.md                 ← Chinese version  

## 怎么用
用浏览器打开对应的 HTML 就行。一个页面里：
- 几个国家各自的公众/银行假日（颜色区分）
- 几个国家共同放假的日期（紫色高亮）
- 全年假日汇总表（Bridge Leave Guide）
- AI 生成的拼假方案 —— 请几天年假能连成最长假期

打印友好,截图友好,适合直接丢到群里或家庭共享文档里一起看。(Good for Print, Screenshot and Sharing/Co-Work)

<img width="1070" height="751" alt="image" src="https://github.com/user-attachments/assets/784e5e8c-cd32-4767-aaa8-028ad26e1d7c" />


## 技术栈

纯 HTML + CSS，不需要装任何东西，直接浏览器打开对应文件即可。打印友好（浏览器右键自助打印），截图友好，也可以直接当网页看。

## 已收录多国日历

| 文件 | 国家 | 说明 |
|------|------|------|
| `China＆Ireland_HolidayMatch_Calendar.html` | 🇨🇳 中国 · 🇮🇪 爱尔兰 | 含调休补班 + 拼假攻略 |
| `UK＆Spain_HolidayMatch_Calendar.html` | 🇬🇧 英国 · 🇪🇸 西班牙 | English and Spanish, Los Puentes Bridge Leave |


# PART2: English introduction
Planning a vacation with friends or family across borders? Tired of hunting down public holiday notices for each country, typing dates into Group Chats that never align, or confusing without visual calendar reference? This project generates HTML calendar that maps workdays and holidays across multiple countries together, nice AI long holiday Bridge Leave Guide.
I wirite **SKILL for AI**, refined the SOP for AI-generated cross-border calendars, designed templates, and strategies for generating Bridge Leave Guide. SKILL help automatically generate collaborative calendars with the latest time and various country combinations, including differences rules across different countries, real-world and boundary conditions such as multiple languages and time parameters!

## 🧠 Product senese＆Anti-Hallucination
| Tier | Design Principle | Core Mechanism | Anti-Hallucination Strategy | User Value |
|------|------------------|----------------|----------------------------|------------|
| ⏰ **Temporal Awareness** | Dynamic year inference & search | Resolves fuzzy expressions like "travel next week"; defaults to current year if ≤1 month away, proactively asks if ≥2 months; prompts for year-crossing in December | Prevents LLMs from hardcoding fixed year parameters | Aligns with real-world planning scenarios, reduces invalid output |
| 📅 **Standard Foundation** | ISO 8601 week calendar + Gregorian validation | WebSearch confirms month lengths, weekday mappings, and leap year handling for the target year | Prevents LLM hallucinations on historical data, year/weekday mismatches, and incorrect month lengths | Accurate year/month/weekday alignment, precise cross-border coordination |
| 🌍 **Special Rules** | Per-country boundary condition library | China: exchanged workdays/lunar holiday; UK: bank holiday deferrals; Islamic: floating festivals; Japan: Golden Week; Spain: regional variations, etc. | Covers non-standard scenarios with localized special rules for each country | Real-world applicability, solves localized edge cases across jurisdictions |
| 📊 **Data Tiering** | A/B/C holiday classification | Tier A (fixed dates): populate directly; Tier B (calculable): compute & verify; Tier C (pending): statutory framework fallback | Never fabricates unpublished data; marks confidence levels; handles uncertainty per tier | No hallucinations when data is missing; honestly shows pending status |
| ⚡ **Parallel Architecture** | Independent parallel retrieval per country; source-isolated querying | Concurrent queries for each country, holiday info, and temporal data from multiple sources | Cross-validation via multi-source verification | 2× speed, ↓ context interference, ↑ accuracy |
| 🔍 **Verification Fallback** | Confidence scoring + source transparency | Validates source confidence, cross-checks multiple sources, proactively flags AI-generated content | Does not feign certainty; honestly exposes boundaries | Warns users of AI-generated and error-prone scenarios |
| ⚖️ **Conflict Arbitration** | Don't vote — trace the source | Gov source vetoes all; third-party consensus accepted; conflicting sources trigger re-search or "needs verification" flag | Prevents AI from "taking sides" in data conflicts; transparently shows all sources | Users know reliability levels; conflicts are flagged as uncertain rather than silently resolved |
| 🌸 **Premium Features** *(WIP)* | Export, sharing, rich & customizable styling | One-click export to Feishu/Lark sheets, PDF, images; rich media styling like Notion; custom background images |*(wait for develop)*| Facilitates sharing and viral collaboration; delivers emotional design value |  

请给星星⭐支持,可提issues需求来制作更多国家的日历。感谢Please provide me Star⭐ and create issues for HolidayMatch calendars for more countries. THX
