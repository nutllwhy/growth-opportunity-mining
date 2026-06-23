---
name: growth-opportunity-mining
version: 1.0.0
description: "增长机会挖掘研究工作流：从用户评价、公开讨论、评测与竞品证据中识别用户需求、痛点、目标人群、传播卖点和产品增长机会。当用户需要对某个品类/产品/竞品做评价收集、需求归因、增长机会分析、报告和可视化网页时使用。"
metadata:
  requires:
    skills: ["research-synthesis", "data-dashboard"]
---

# Growth Opportunity Mining｜增长机会挖掘

用于把"公开评价/讨论/评测/竞品资料"转化为可执行的增长判断，包括：

- 用户为什么买
- 高频使用场景是什么
- 用户满意/不满意什么
- 哪些吐槽是共性问题，哪些只是个别反馈
- 哪些需求值得产品投入
- 哪些卖点值得市场传播
- 哪些目标用户最值得争取
- 是否值得进入某个品类，以及进入方式
- 最终生成研究报告和可视化网页

## 触发场景

当用户提出以下需求时使用本 Skill：

- "帮我分析某类产品的增长机会/市场机会"
- "收集用户评价并分析需求/痛点"
- "对比几款竞品，找产品机会"
- "从小红书/电商/社区/评测里总结用户真实反馈"
- "判断某个品类值不值得做/怎么切入"
- "输出报告和可视化网页/看板"

## 核心原则

1. **证据优先，不编造评论**
   遇到登录限制、反爬限制、动态加载或样本不足时，不虚构结果；改用其他公开可访问来源，并明确标注限制。

2. **原始数据与分析结论分离**
   原始评价、公开摘要、链接、来源类型、置信度单独保存；分析表、结论报告、网页另存。

3. **重要结论至少双来源支撑**
   关键判断至少引用 2 条不同来源/不同类型证据，如用户评价 + 媒体评测、社区讨论 + 电商评价、品牌资料 + 第三方评测。

4. **阶段性汇报**
   每完成一个阶段，向用户简短说明：已完成什么、当前发现、限制或下一步。

5. **先确认报告结构与核心结论，再做网页**
   如果用户需要最终网页，应先展示报告结构和核心结论预览，待用户确认后再生成可视化网页。

6. **网页不仅放结论，还要放证据**
   可视化网页必须保留代表性用户评论/公开观点摘要，并支持按产品、情绪、主题等筛选。

## 推荐目录结构

在当前工作区或用户指定目录下创建研究目录，例如：

```text
<研究主题>/
  data/
    raw/
      <product-a>-reviews.csv
      <product-b>-reviews.csv
    processed/
      all-reviews-combined.csv
      source-sample-summary.json
      sentiment-by-product.csv
      source-distribution.csv
      theme-frequency.csv
      product-comparison.csv
      user-needs-priority-matrix.csv
  evidence/
    <product-a>-findings.md
    <product-b>-findings.md
  reports/
    growth-opportunity-report.md
  web/
    growth-opportunity-dashboard.html
```

## 原始数据字段规范

每条评价/观点/证据至少包含：

```csv
product,source_type,source_name,date,url,raw_summary,sentiment,topic_tags,evidence_quote_or_summary,confidence
```

字段说明：

| 字段 | 说明 |
|---|---|
| product | 产品/品牌/竞品名称 |
| source_type | 来源类型，如 user_review、community_post、media_review、brand_doc、complaint、app_store、ecommerce 等 |
| source_name | 来源名称，如 App Store、京东、小红书、Reddit、B站、媒体名 |
| date | 发布时间或抓取日期，未知可留空 |
| url | 可回溯链接 |
| raw_summary | 原始评价/公开摘要/页面内容摘要 |
| sentiment | positive / negative / mixed / neutral |
| topic_tags | 主题标签，如 续航、佩戴、价格、AI能力、拍摄、翻译、连接稳定 |
| evidence_quote_or_summary | 关键证据摘录或准确摘要 |
| confidence | high / medium / low。逐条可验证原文优先 high；搜索摘要或二手归纳一般 medium/low |

## 标准执行步骤

### Step 0｜确认研究范围

向用户确认或主动整理：

- 研究对象：品类、产品、竞品名单
- 地域/语言范围：国内、海外或全球
- 时间范围：近 30 天、近 1 年、上市以来等
- 目标输出：报告、表格、网页、内容选题、进入建议等
- 是否需要先确认结构再生成网页

若用户已明确确认对象，则直接进入采集。

### Step 1｜建立研究目录与文件结构

创建 `data/raw`、`data/processed`、`evidence`、`reports`、`web` 等目录。

阶段汇报示例：

> 阶段 0 完成：已建立研究目录，原始数据会放在 data/raw，分析结果会放在 data/processed 与 reports。

### Step 2｜评价与证据采集

按产品/竞品拆分采集，优先并行处理。推荐来源：

- 电商评价：Amazon、京东、天猫、淘宝、BestBuy 等
- 应用商店：App Store、Google Play
- 社区讨论：Reddit、小红书、微博、知乎、NGA、雪球、什么值得买等
- 视频/内容平台：B站、YouTube、抖音、视频号等
- 媒体评测：专业媒体、科技媒体、测评博客
- 投诉/售后：黑猫投诉、消费保、论坛售后反馈
- 品牌/官方资料：发布会、产品页、FAQ、更新日志

采集要求：

- 不绕过登录或付费限制。
- 不编造不可访问评论。
- 受限来源可记录为"公开摘要/搜索摘要/二手归纳"，并降低 confidence。
- 每个产品单独保存 raw CSV 和 findings.md。

阶段汇报示例：

> 阶段 1 完成：三款产品的原始评价/证据文件已生成。部分中文平台存在登录或动态加载限制，已用公开可访问来源补充，并在 confidence 字段标注。

### Step 3｜合并清洗与样本质量评估

生成：

- `all-reviews-combined.csv`
- `source-sample-summary.json`
- `source-distribution.csv`
- `sentiment-by-product.csv`

检查：

- 各产品样本量是否大致均衡
- 来源类型是否过度集中
- high / medium / low 置信度比例
- 是否存在重复、空链接、缺字段
- 是否需要补采

阶段汇报示例：

> 阶段 2 完成：共合并 N 条观点/证据记录。A 产品可逐条验证评价最多；B/C 产品部分来源受限，后续结论会按置信度分层。

### Step 4｜主题归因与需求聚类

从原始评价中抽取并归一化主题标签：

- 购买动机
- 使用场景
- 满意点
- 不满意点
- 退货/弃用原因
- 价格/价值感
- 版本/地区/系统差异
- 未满足需求

常见归一化标签：

- 续航
- 佩戴舒适
- 价格/价值感
- AI能力/可靠性
- 第一视角拍摄
- 音频/通话
- 显示/HUD
- 翻译/导航
- 连接稳定
- App/生态
- 隐私/社交接受度
- 退货/弃用

输出：

- `theme-frequency.csv`
- 每个产品的 findings.md 更新

### Step 5｜横向对比与机会矩阵

生成：

- `product-comparison.csv`
- `user-needs-priority-matrix.csv`

对比维度建议：

| 维度 | 说明 |
|---|---|
| 核心定位 | 用户把它当成什么工具 |
| 目标人群 | 最容易被打动的人群 |
| 购买动机 | 为什么买 |
| 高频场景 | 买后怎么用 |
| 核心优势 | 用户真正认可的点 |
| 高频槽点 | 重复出现的问题 |
| 未满足需求 | 产品机会 |
| 传播卖点 | 最适合营销表达的利益点 |
| 风险 | 退货、弃用、舆情、替代品等 |

机会矩阵字段：

```csv
需求/机会,频率,情绪强度,影响人群,购买决策影响,优先级,说明,证据来源1,证据来源2
```

优先级建议：

- P0：高频、高情绪强度、强影响购买/留存/退货
- P1：中高频，影响增长或传播
- P2：低频或细分需求，可作为后续验证

### Step 6｜报告结构与核心结论预览

先给用户看，不直接进入网页制作。

报告结构建议：

1. 研究范围与方法
2. 样本与来源说明
3. 用户心智概览
4. 购买动机分析
5. 高频使用场景分析
6. 最受认可的功能
7. 高频负面问题
8. 退货、弃用与低频使用原因
9. 价格与付费接受度
10. 版本/地区/系统差异
11. 未满足需求
12. 竞品横向对比
13. 共性需求 vs 个别吐槽
14. 用户需求优先级矩阵
15. 产品增长机会
16. 市场传播卖点
17. 目标用户
18. 内容选题
19. 是否值得进入该品类
20. 风险与待验证问题

核心结论必须包含：

- 3-7 条主结论
- 每条主结论的证据基础
- 明确区分"已确认""倾向判断""待验证"
- 数据限制说明

### Step 7｜生成正式报告

在用户确认结构和核心结论后，生成完整报告：

- `reports/growth-opportunity-report.md`

报告要求：

- 结论前置
- 每个重要结论附至少 2 个不同来源证据
- 把共性问题和个别吐槽分开
- 明确增长建议、传播建议、目标用户和风险

### Step 8｜生成可视化网页

网页应包含：

- 研究结论首页
- 样本量/来源/置信度说明
- 情绪分布图
- 主题频次图
- 竞品横向对比表
- 用户需求优先级矩阵
- 产品机会/传播卖点/目标用户
- **真实评论证据卡片**
  - 按产品筛选
  - 按情绪筛选
  - 可按主题/关键词搜索（可选）
  - 显示 source_type、source_name、date、url、confidence

网页不得只展示结论，必须能回看代表性评论或观点摘要。

### Step 9｜网页验收与修复

必须做基础前端验收，尤其当网页包含图表、筛选器、评论卡片时：

- 控制台无关键 JS 错误
- 图表容器高度正常，无异常大留白
- 页面无横向溢出：`document.documentElement.scrollWidth <= document.documentElement.clientWidth + 1`
- 评论卡片长文本、长链接不出框
- 筛选器可用
- 图表 canvas 有明确高度/最大高度
- 移动端或窄屏布局可读
- 外部 CDN 失败时应有基本降级说明或避免核心信息依赖单一外链

常用 CSS 约束：

```css
.chart,
canvas.chart {
  height: 300px !important;
  max-height: 320px !important;
  width: 100% !important;
  display: block;
}

.card,
.comment,
td,
th {
  min-width: 0;
  max-width: 100%;
  overflow-wrap: anywhere;
  word-break: break-word;
}

.comment a,
.src a {
  word-break: break-all;
}

.block {
  overflow: hidden;
}
```

### Step 10｜最终交付说明

最终回复应包含：

- 已生成文件清单
- 原始数据位置
- 分析数据位置
- 报告位置
- 网页位置
- 样本量与数据限制
- 已做的验收检查
- 后续可选动作，如部署到可分享链接、补采某平台、做 PPT、做内容日历

## 阶段性汇报模板

```text
阶段 X 完成：已完成 <动作>。
当前发现：<1-3 条发现>。
限制/风险：<如果有>。
下一步：<下一阶段动作>。
```

## 最终判断模板

```text
我的判断是：<值得/不值得/谨慎进入>。

依据：
1. <证据支持的需求>
2. <证据支持的市场/用户行为>
3. <证据支持的风险>

建议进入方式：
- <垂直场景>
- <目标用户>
- <MVP/试点方式>
- <需要验证的指标>

不建议：
- <不要基于未经验证的大众刚需假设>
- <不要过度依赖概念传播>
```

## 质量红线

- 不把搜索结果少等同于事实不存在。
- 不把品牌宣传当用户评价。
- 不把单一爆款评论当共性结论。
- 不隐藏反爬、登录、动态加载导致的限制。
- 不在用户确认前直接跳到最终网页。
- 不交付未验收的网页，尤其避免图表异常留白、评论出框、筛选不可用等基础问题。
