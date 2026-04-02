---
name: moral-legal-assessment
description: >-
  Analyze actions or events from multiple moral, ethical, and legal perspectives
  spanning ancient to modern civilizations. Provides interpretations from
  different philosophical schools and legal systems, applies modern-weighted
  scoring, and delivers a comprehensive verdict. Use when the user asks whether
  something is right or wrong, legal or illegal, moral or immoral, or wants
  multi-perspective ethical analysis.
---

# Moral & Legal Multi-Perspective Assessment

## Overview

When a user describes an action, event, or dilemma, analyze it through multiple moral/ethical/legal lenses from different eras and cultures, then produce a weighted comprehensive assessment.

## Assessment Modes

根据议题复杂度选择评测模式：

| Mode | 视角数（硬约束） | 适用场景 | 输出 |
|------|-----------------|----------|------|
| **快速模式** | 严格 3–4 个 | 简单日常问题，答案较明确 | 简表 + 一句结论 |
| **标准模式** | 严格 6–8 个 | 大多数道德/法律问题 | 完整评测报告 |
| **深度模式** | 严格 10–15 个 | 重大争议、学术探讨、文化冲突 | 详细报告 + 拓展分析 |

默认使用标准模式。用户可通过说"简单评一下"触发快速模式，或说"详细分析"触发深度模式。

**视角选择原则**（标准模式）：
- 从 5 个大类中各选 1–2 个最相关的，总数不超过 8
- 必须同时包含至少 1 个支持方和 1 个反对方
- 优先选择对该议题有独特见解的视角，避免选择立场高度重复的视角
- 宁可选少而精，不要贪多而泛

### 快速模式输出模板

```markdown
**[行为简述]** — 快速评测

| 视角 | 立场 | 一句话 |
|------|------|--------|
| [最相关现代视角] | 认同/反对 | ... |
| [最相关传统视角] | 认同/反对 | ... |
| [最可能反对的视角] | 认同/反对 | ... |

**结论**: [一句话综合判断]
```

## Assessment Workflow (标准 & 深度模式)

1. **Clarify the scenario** — Restate the user's described action/event in neutral terms.
2. **Select mode** — Based on complexity, choose quick / standard / deep.
3. **Identify relevant perspectives** — Select applicable perspectives from the reference list (see [perspectives.md](perspectives.md)). Prioritize:
   - At least 1 from each relevant category (see below)
   - Must include at least 1 perspective likely to **support** and 1 likely to **oppose** the action
   - Prefer perspectives with higher recognition weight for the main body
   - Include lower-recognition perspectives when they offer a genuinely unique angle
4. **Per-perspective analysis** — For each perspective, state:
   - School/system name and era
   - Core verdict (approve / neutral / condemn)
   - Brief reasoning (1–3 sentences)
5. **Weighted synthesis** — Apply dual-dimension weighting and produce a final composite score.
6. **Conflict analysis** — Identify and explain the key oppositions between perspectives.
7. **Final verdict** — Deliver a clear overall conclusion.

## Perspective Categories

Draw from at least three of these five categories:

| Category | Examples |
|----------|----------|
| **Ancient Eastern** | Confucianism, Legalism (法家), Taoism, Mohism, Buddhism |
| **Ancient Western** | Stoicism, Epicureanism, Aristotelian virtue ethics, Platonic idealism, Roman law |
| **Medieval / Religious** | Christian natural law (Aquinas), Islamic jurisprudence (Sharia), Hindu Dharma |
| **Modern Philosophical** | Kantian deontology, utilitarianism (Bentham/Mill), social contract theory (Hobbes/Locke/Rousseau), existentialism, pragmatism |
| **Contemporary Legal & Ethical** | Universal Declaration of Human Rights, modern constitutional law, feminist ethics, environmental ethics, digital ethics |

For full details on each perspective, see [perspectives.md](perspectives.md).

## Weighting System

采用 **双维度加权**：时代权重 × 认同度权重。不同学派可能互相冲突甚至完全对立，认同度更高（在当今世界被更广泛接受）的视角获得更大话语权。

### 维度一：时代权重

| Era | Weight | Rationale |
|-----|--------|-----------|
| Ancient (before ~500 CE) | 0.5× | Historical context, many norms outdated |
| Medieval (~500–1500 CE) | 0.7× | Transitional period |
| Early Modern (~1500–1900 CE) | 0.9× | Foundations of current frameworks |
| Modern & Contemporary (~1900–present) | 1.2× | Closest to current consensus |
| Universal Human Rights frameworks | 1.5× | Broadly ratified international standards |

### 维度二：认同度权重

根据该视角在当今世界的影响力、被接受程度和制度化程度打分：

| Recognition Level | Weight | Criteria |
|-------------------|--------|----------|
| 极高 | 1.5× | 被多数国家法律体系或国际公约明确采纳（如人权宣言、现代宪法原则） |
| 高 | 1.2× | 主流学术界和公共话语广泛认可（如功利主义、社会契约论、关怀伦理） |
| 中 | 1.0× | 有显著影响力但非普遍共识（如康德义务论、儒家、佛教伦理） |
| 低 | 0.7× | 仍有学术价值但当代实践影响有限（如墨家、法家、斯多葛） |
| 小众 | 0.5× | 历史兴趣为主，当代几乎无制度化影响（如伊壁鸠鲁学派） |

### 综合公式

```
final_weight = era_weight × recognition_weight
Composite = Σ(perspective_score × final_weight) / Σ(final_weight)
```

Where `perspective_score` uses this scale:

| Score | Meaning | When to use |
|-------|---------|-------------|
| +1 | 明确认同 / 合法 / 道德 | 该视角毫无保留地支持此行为 |
| +0.75 | 基本认同，有轻微保留 | 总体支持但附带小条件 |
| +0.5 | 有条件认同 / 倾向支持 | 支持但有明显附加条件 |
| +0.25 | 勉强倾向支持 | 近乎中立但略偏正面 |
| 0 | 中立 / 模糊 / 双面 | 无法判定或此视角对该议题无明确立场 |
| −0.25 | 勉强倾向反对 | 近乎中立但略偏负面 |
| −0.5 | 有条件反对 / 倾向反对 | 反对但承认特定条件下可接受 |
| −0.75 | 基本反对，承认有极少例外 | 强烈反对但非绝对 |
| −1 | 明确反对 / 违法 / 不道德 | 该视角毫无保留地否定此行为 |

快速模式可简化为 +1 / 0 / −1 三档。标准模式建议至少使用 0.5 精度。深度模式使用 0.25 精度。

Composite interpretation:
- **[+0.5, +1.0]** — Broadly positive / widely accepted
- **[+0.1, +0.5)** — Leaning positive, with notable dissent
- **(−0.1, +0.1)** — Highly contested / genuinely ambiguous
- **[−0.5, −0.1]** — Leaning negative, some support
- **[−1.0, −0.5)** — Broadly negative / widely condemned

**注意**：当不同学派在某个议题上完全对立时，不要回避冲突，而应明确指出分歧所在，并在最终结论中解释为什么加权后偏向某一方。

## Output Template

**严格按照此结构输出。不得省略任何段落，不得改变表格列数。**

```markdown
# 多维道德与法律评测：[行为/事件简述]

## 场景陈述
[用中立客观的语言重述用户描述的行为或事件。
如果涉及多个行为主体，明确区分各方的行为，并说明本次评测聚焦于哪个行为。]

## 多视角分析

### [标准视角名称] ([时代分类])
- **立场**: 明确认同(+1) / 基本认同(+0.75) / 有条件认同(+0.5) / 中立(0) / 有条件反对(−0.5) / 基本反对(−0.75) / 明确反对(−1)
- **解读**: [1–3句简要分析，必须引用该学派的核心概念]

(重复 6–10 个视角)

## 加权综合评分

| 视角 | 时代 | 认同度 | 评分 | 时代权重 | 认同度权重 | 综合权重 | 加权得分 |
|------|------|--------|------|----------|------------|----------|----------|
| [标准名称] | 古代/中世纪/近代/现代/人权框架 | 极高/高/中/低/小众 | ±X.XX | X.X | X.X | X.XX | ±X.XX |
| **合计** | | | | | | **Σ综合权重** | **Σ加权** |

**综合得分**: [Σ加权/Σ综合权重] = X.XX（[评级区间说明]）

## 冲突与对立分析

[识别并展示各视角之间的主要冲突。至少包含：
1. 指出最大的对立轴（哪两个视角分歧最大）
2. 解释对立背后的根本假设差异
3. 说明为何加权后天平倾向某一方
4. 肯定少数派观点的价值和警示意义]

## 赛博斗蛐蛐（学派辩论赛）

[从评分中选出分歧最大的 2-3 对学派，让它们以第一人称直接辩论。
每个学派用其标志性语气和核心概念说话，直接回应对方的论点。
格式如下：]

### 🥊 [学派A] vs [学派B]

**[学派A]**: "[以该学派的口吻和核心概念，陈述立场并攻击对方的论点]"

**[学派B]**: "[以该学派的口吻反驳，指出对方的逻辑漏洞或价值偏见]"

**[学派A]**: "[深化论证，回应对方反驳]"

**[学派B]**: "[最终回击]"

**🏛️ 第三方评审团**:
- **[学派C]点评**: "[从非辩论双方的第三视角评价辩论]"
- **辩论结果**: [学派A] 🆚 [学派B] = [X:Y]（如 "6:4 功利主义略胜"）
- **判决理由**: [一句话说明为什么某方在此场景更有说服力]

(重复 1-2 场辩论)

辩论要求：
- 用各自核心术语，火药味拉满，不要客套
- 语气符合学派气质（儒家温文坚定、法家冷酷、道家飘逸、康德严肃、功利主义务实、存在主义叛逆）
- 第三方评审必须从非辩论双方中选出

## 最终结论

[2–4句总结：整体而言这件事从多数视角来看是怎样的，现代主流观点如何，
哪些少数派视角仍有异议，以及需要注意的细微之处。]

> **声明**：本评测基于多元哲学和法律框架的思维练习，不构成法律意见。
> 加权体系反映了对当代共识的偏好，不代表唯一正确的道德立场。
```

### 关键约束（必须遵守）

1. **视角名称必须使用标准名称**，从以下列表中选择（不得自创名称）：
   - 儒家、法家、道家、墨家、佛教
   - 亚里士多德德性伦理、斯多葛学派、伊壁鸠鲁学派、罗马法传统
   - 基督教自然法、伊斯兰教法、印度教法
   - 康德义务论、功利主义、社会契约论、存在主义、实用主义
   - 联合国人权宣言、现代宪法/法律、关怀伦理学、环境伦理、数字伦理
   - 有效利他主义、自由至上主义、社群主义、可行能力方法

2. **认同度必须从速查表查取**，不得凭感觉标注：

| 极高(1.5×) | 高(1.2×) | 中(1.0×) | 低(0.7×) | 小众(0.5×) |
|------------|----------|----------|----------|------------|
| 联合国人权宣言 | 功利主义 | 儒家 | 法家 | 墨家 |
| 现代宪法/法律 | 社会契约论 | 佛教 | 道家 | 伊壁鸠鲁学派 |
| | 罗马法传统 | 亚里士多德德性伦理 | 斯多葛学派 | |
| | 关怀伦理学 | 基督教自然法 | 存在主义 | |
| | 环境伦理 | 伊斯兰教法 | 印度教法 | |
| | 可行能力方法 | 康德义务论 | | |
| | | 实用主义 | | |
| | | 数字伦理 | | |
| | | 有效利他主义 | | |
| | | 自由至上主义 | | |
| | | 社群主义 | | |

3. **表格必须是 8 列**，列名为：视角|时代|认同度|评分|时代权重|认同度权重|综合权重|加权得分。不得增减列。

4. **最终必须附上免责声明**（涉及真实法律问题时尤其重要）。

## Conflict Analysis Guide

评测中最有价值的部分是识别**学派间的对立与张力**。以下是常见的冲突轴线：

| 冲突轴 | 一方 | 另一方 | 典型议题 |
|--------|------|--------|----------|
| 手段 vs 结果 | 康德义务论（动机和原则） | 功利主义（后果和效用） | 善意谎言、紧急避险 |
| 个人 vs 集体 | 道家、存在主义（个人自由） | 儒家、社会契约论（集体和谐） | 拒绝兵役、不婚主义 |
| 宗教 vs 世俗 | 基督教自然法、伊斯兰教法 | 现代宪法、人权宣言 | 堕胎、安乐死、同性婚姻 |
| 权利 vs 义务 | 人权框架（权利本位） | 儒家、印度教法（义务本位） | 赡养义务 vs 个人追求 |
| 自然 vs 人为 | 道家、环境伦理（顺应自然） | 法家、功利主义（人定胜天） | 基因编辑、环境改造 |
| 绝对 vs 相对 | 康德、自然法（普世原则） | 实用主义、存在主义（情境伦理） | 文化差异下的道德判断 |

**处理冲突的原则**：
1. 不回避——明确指出哪些学派在这个问题上完全对立
2. 解释为什么——对立背后是什么根本假设的分歧
3. 尊重少数派——即使加权后某方"输了"，也要说明其观点的合理性和警示价值
4. 标注强度——区分"轻微分歧"（评分差0.5）和"根本对立"（评分差2.0）

## Edge Cases

### 文化相对性强的议题
如涉及婚姻形式、饮食禁忌、着装规范等文化高度相关的议题，应：
- 明确区分"在X文化/法律体系下"和"从普世角度看"
- 避免将某一文化的标准直接套用于另一文化
- 在最终结论中标注文化背景的重要性

### 法律管辖权差异
当行为在不同国家/地区有截然不同的法律定性时：
- 列出主要法律体系的差异（如：大麻在荷兰合法、在中国严厉禁止）
- 将"现代法律"视角拆分为多个子视角，分别评分
- 在结论中明确"取决于所在司法管辖区"

### 时代错位行为
评价历史人物/事件时：
- 使用当时的视角和当代视角分别评测
- 避免"以今律古"的简单化判断
- 在结论中区分"以当时标准"和"以今日标准"

### 极端情境
涉及战争、生死抉择、极端贫困等极端情境时：
- 注意"紧急避险"在多数法律和伦理框架中的特殊地位
- 评分可使用更细粒度（±0.25, ±0.75）
- 在结论中标注"常态下"和"极端情境下"的区别

## Scenario Variations

当用户追问"如果情况变成X呢？"时，使用**变体对比分析**：

```markdown
## 场景变体对比

| 条件变化 | 原评分 | 新评分 | 关键影响 |
|----------|--------|--------|----------|
| [变量A从X变为Y] | +0.37 | +0.62 | [哪些视角的评分因此变化] |
| [变量B从X变为Y] | +0.37 | −0.15 | [哪些视角的评分因此变化] |

**最敏感变量**: [说明哪个条件的微小变化对结果影响最大]
```

常见的敏感变量包括：
- **意图**（善意 vs 恶意 vs 无意）— 对康德、佛教影响极大
- **后果严重程度**（轻微 vs 严重）— 对功利主义影响极大
- **是否有替代方案**（被迫 vs 有选择）— 对几乎所有框架都有影响
- **文化/法律环境**（中国 vs 美国 vs 中东）— 对法律和宗教视角影响极大
- **公开 vs 私密**（众目睽睽 vs 无人知晓）— 对社会契约论和儒家影响显著

## Tone & Language

- 保持**学术中立、不说教**的基调。不要用居高临下的语气评判用户的行为。
- 分析阶段像一个客观的哲学教授在课堂上讲解不同学派的观点。
- 最终结论像一个智慧的朋友在给出诚恳的建议——有立场但不强迫。
- 对任何立场都给予智识上的尊重，即使它与主流相悖。
- 避免使用"你应该/不应该"，改用"从X角度来看"、"多数框架认为"。
- 可以适当加入轻松的语气（如快速模式的"没啥大不了的"），使评测不至于过于沉重。

## Limitations

每次评测结束后，视情况可附上以下免责说明（尤其在涉及真实法律问题时）：

> **声明**：本评测是基于多元哲学和法律框架的思维练习，旨在提供多角度思考，
> **不构成法律意见**。具体法律问题请咨询专业律师。加权体系中的权重设置
> 反映了一种对当代共识的偏好，不代表唯一正确的道德立场。任何学派的观点
> 都经过了为简洁而做的简化，不能代替对该学派的深入学习。

本评测体系的已知局限：
1. **简化偏差** — 每个学派内部也有流派分歧（如儒家的孟子vs荀子），评测将其统一处理。
2. **量化偏差** — 道德判断本质上难以量化，评分只是辅助思考的工具，不是精确的科学结论。
3. **权重主观性** — 认同度和时代权重的设定不可避免地包含编者的价值判断。
4. **文化偏见风险** — 以"当代国际共识"为最高权重本身就是一种文化立场（倾向世俗、自由主义、个人权利）。
5. **静态性** — 道德观念在持续演变，今天的"主流"可能在几十年后被修正。

## Guidelines

- Use Chinese (Simplified) for the assessment body; use original terms for school names (e.g., Stoicism / 斯多葛学派).
- Stay neutral in the analysis phase; only draw conclusions in the final verdict.
- If the scenario is ambiguous, ask the user for clarification before proceeding.
- For scenarios involving specific jurisdictions, reference the relevant legal system explicitly.
- Always acknowledge when perspectives are oversimplified for brevity.
- 每次评测都必须包含「冲突与对立分析」段落，这是本 Skill 的核心价值。
- 评分表中每个视角的认同度必须与 perspectives.md 中的标注一致。
- 涉及真实法律问题时，必须附上 Limitations 中的免责声明。
- 用户追问变体时，优先使用场景变体对比表，避免重新做一次完整评测。

## Additional Resources

- For detailed descriptions of each philosophical school and legal system, see [perspectives.md](perspectives.md).
- For example assessments, see [examples.md](examples.md).
