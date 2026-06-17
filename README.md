# HolidayMatch · Bridge Leave Planner 🗺️
跨国朋友/家庭一起规划假期：麻烦在各自去找放假通知？在群里打一个个日期还对不上星期？不同国家的日历、假期混在一起、没有可视化参考让人眼花缭乱？这个项目致力于把多个国家的工作日和节假日按日历格式对照做成了一份好看的网页，附赠AI的拼假方案帮你请3休11，打印友好,截图友好,协作利器! HolidayMatch不是"AI生成日历"，是"自动化,多语言,本地化的跨国假期对齐规划家"——有简洁高效的SKILL自动化,防幻觉,产品和边界的设计!(English introduction on PART2)  
## 🧠 产品思维 & 防幻觉设计 Product senese＆Anti-Hallucination
| 层级 | 设计点 | 核心机制 | 防幻觉策略 | 用户价值 |
|:---|:---|:---|:---|:---|
| **⏰ 时间感知** | 动态年份搜索和判断 | 识别"下周出行"模糊表述；≤1月默认今年；≥2月主动询问；12月提示跨年 | 避免LLM写死固定年份参数 | 对齐真实规划场景，减少无效输出 |
| **📅 标准底板** | ISO 8601 周历 + 公历校验 | WebSearch确认当年月份天数、星期对应、闰年处理 | 防止LLM的历史数据和幻觉，年份和星期对应、月份天数错误； | 年月星期准确，跨国对齐准确 |
| **🌍 特殊规则** | 分国别的边界条件库 | 中国调休/农历、英国顺延、伊斯兰浮动节日、日本黄金周、西班牙区域差异等 | 覆盖非标场景，各国本地化和特殊规则 | 真实可用，解决各国和本地化的特殊场景 |
| **⚡ 并行架构** | 各国独立并行检索；分源独立检索 | 各国、假期信息 + 时间多源并发并发查询 | 多源交叉验证 | 速度×2，上下文干扰↓，准确性↑ |
| **🔍 验证兜底** | 置信度标记 + 来源透明 | 确认信息来源置信度，多源对比校验，主动标明AI生成问题 | 不伪装确定性，诚实暴露边界 | 提示AI生成和易错场景 |
| **📊 数据可信** | 来源URL + 时间戳 + 版本号 | 每个假日可追溯，定期自动更新检测 | 防止"静态过期"幻觉 | 长期可用，随官方变动同步 |
| **🌸 增值和设计** | （待开发）导出和分享，丰富和自定义的样式 | 一键导出飞书表格/PDF/图片，富媒体样式如Notion，自定义背景图 |  | 方便分享和协作裂变，设计的情绪价值 |

<img width="1185" height="738" alt="image" src="https://github.com/user-attachments/assets/24905fbf-96d6-49aa-bfea-ac8630237707" />

## 怎么用
用浏览器打开对应的 HTML 就行。一个页面里：
- 几个国家各自的公众/银行假日（颜色区分）
- 几个国家共同放假的日期（紫色高亮）
- 全年假日汇总表（Bridge Leave Guide）
- AI 生成的拼假方案 —— 请几天年假能连成最长假期

打印友好,截图友好,适合直接丢到群里或家庭共享文档里一起看。(good for Print and Screenshot and Sharing/Co-Work)

<img width="1161" height="750" alt="image" src="https://github.com/user-attachments/assets/9874d77e-d3e4-49ce-b990-41c93f540014" />

## 技术栈

纯 HTML + CSS，不需要装任何东西，直接浏览器打开对应文件即可。打印友好（浏览器右键自助打印），截图友好，也可以直接当网页看。

## 已收录

| 文件 | 国家 | 说明 |
|------|------|------|
| `China＆Ireland_HolidayMatch_Calendar.html` | 🇨🇳 中国 · 🇮🇪 爱尔兰 | 含调休补班 + 拼假攻略 |
| `UK＆Spain_HolidayMatch_Calendar.html` | 🇬🇧 英国 · 🇪🇸 西班牙 | English + Los Puentes Bridge Leave |

请给星星⭐支持,可提issues需求来制作更多国家的日历。感谢Please provide me Star⭐ and create issues for HolidayMatch calendars for more countries. THX


Planning a vacation with friends or family across borders? Tired of hunting down public holiday notices for each country, typing dates into Group Chats that never align, or confusing without visual calendar reference? This project generates HTML calendar that maps workdays and holidays across multiple countries together, nice AI long holiday Bridge Leave Guide.
I wirite **SKILL for AI**, refined the SOP for AI-generated cross-border calendars, designed templates, and strategies for generating Bridge Leave Guide. SKILL help automatically generate collaborative calendars with the latest time and various country combinations, including differences rules across different countries, real-world and boundary conditions such as multiple languages and time parameters!
