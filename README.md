# Moral Compass AI

###  赛博清汤大老爷

**多维道德与法律评测框架** — 从古至今 26 个哲学/法律视角，对任何行为进行加权综合评判。

> 告诉 AI 你做了什么，它会从儒家、佛教、康德、功利主义、人权宣言等 26 个视角告诉你——这件事到底对不对、合不合法、被谁认同、被谁反对，以及为什么。

## 特性

- **26 个视角** — 覆盖古代东方、古代西方、中世纪宗教、近代哲学、当代法律与伦理
- **双维度加权** — 时代权重 × 认同度权重，现代主流观点话语权更大
- **三种模式** — 快速(3-4视角)、标准(6-8视角)、深度(10-15视角)
- **冲突分析** — 不回避学派间的对立，揭示根本分歧
- **场景变体** — 追问"如果条件变了呢"，快速对比分析
- **经过 GPT-5.4 实测验证** — 5 轮迭代优化，A 级评测质量

## 快速开始

### 方式一：Cursor / Codex Skill（推荐）

将 `skill/` 目录复制到你的 Cursor Skills 目录：

```bash
# macOS
cp -r skill/ ~/.cursor/skills/moral-legal-assessment/

# Linux
cp -r skill/ ~/.cursor/skills/moral-legal-assessment/

# Windows (CMD)
xcopy /E skill\ %USERPROFILE%\.cursor\skills\moral-legal-assessment\

# Windows (PowerShell)
Copy-Item -Recurse skill\ "$env:USERPROFILE\.cursor\skills\moral-legal-assessment\"
```

或者使用 `git clone` 后复制：

```bash
git clone https://github.com/kobolingfeng/moral-compass-ai.git
cp -r moral-compass-ai/skill/ ~/.cursor/skills/moral-legal-assessment/
```

之后在 Cursor 对话中直接问"帮我评测一下：[描述你的行为]"即可自动触发。

### 方式二：API 调用（System Prompt）

将 [`system-prompt.md`](system-prompt.md) 的内容作为 `system` 消息传入任何 OpenAI 兼容 API：

```python
import openai

client = openai.OpenAI(
    api_key="your-api-key",
    base_url="https://api.openai.com/v1"
)

# 读取 system prompt
with open("system-prompt.md", "r", encoding="utf-8") as f:
    system_prompt = f.read()

response = client.chat.completions.create(
    model="gpt-4o",  # 或 gpt-5.4 等
    messages=[
        {"role": "system", "content": system_prompt},
        {"role": "user", "content": "帮我评测一下：我上班迟到了10分钟但没有跟领导说"}
    ],
    max_tokens=4000,
    temperature=0.7
)

print(response.choices[0].message.content)
```

### 方式三：直接复制提示词

如果你使用 ChatGPT、Claude 等对话式 AI，可以直接将 [`system-prompt.md`](system-prompt.md) 的内容粘贴为第一条消息（或自定义指令），然后正常对话即可。

## 项目结构

```
moral-compass-ai/
├── README.md                # 本文件
├── system-prompt.md         # 精简版提示词，可直接用于 API 调用
├── skill/                   # Cursor / Codex Skill 标准格式
│   ├── SKILL.md             # 主框架：评测流程、加权体系、输出模板
│   ├── perspectives.md      # 26 个视角详细参考 + 认同度速查表 + 话题速配表
│   └── examples.md          # 5 个完整评测示例（标准/深度/快速/变体分析）
└── assets/                  # 赞助相关图片
```

## 评测示例

### 快速模式

> 用户：简单评一下：我上班摸鱼看了半小时短视频

| 视角 | 立场 | 一句话 |
|------|------|--------|
| 现代法律 | 认同 | 通常不违法，但可能违反劳动纪律 |
| 功利主义 | 偏反对 | 若影响产出则总体效用下降 |
| 儒家 | 偏反对 | "贪小便宜"不符合君子之德，但程度极轻 |

**结论**: 法律上没问题，道德上属极轻微的"小错"——没啥大不了的。

### 标准模式

> 用户：帮我评测一下：我的好朋友借了我5000块钱一直不还，已经拖了半年了，我把这件事告诉了我们的共同朋友圈。

综合得分: **+0.12**（倾向正面有异议）

关键冲突：正当维权 vs 名誉隐私保护。前提是你说的是真实事实、范围适度、目的偏向维权而非羞辱。

*完整示例见 [skill/examples.md](skill/examples.md)*

## 覆盖的 26 个视角

| 类别 | 视角 |
|------|------|
| **古代东方** | 儒家、法家、道家、墨家、佛教 |
| **古代西方** | 亚里士多德德性伦理、斯多葛学派、伊壁鸠鲁学派、罗马法传统 |
| **中世纪宗教** | 基督教自然法、伊斯兰教法、印度教法 |
| **近代哲学** | 康德义务论、功利主义、社会契约论、存在主义、实用主义 |
| **当代** | 联合国人权宣言、现代宪法/法律、关怀伦理学、环境伦理、数字伦理、有效利他主义、自由至上主义、社群主义、可行能力方法 |

## 加权体系

采用双维度加权，确保认同度更高的视角获得更大话语权：

**综合权重 = 时代权重 × 认同度权重**

| 维度 | 最低 | 最高 |
|------|------|------|
| 时代权重 | 古代 0.5× | 人权框架 1.5× |
| 认同度权重 | 小众 0.5× | 极高 1.5× |

例如：联合国人权宣言的综合权重为 1.5 × 1.5 = **2.25×**（最大话语权），而墨家为 0.5 × 0.5 = **0.25×**。

## 社区

- [Linux.do 社区](https://linux.do) — 欢迎来 Linux.do 交流讨论

## 声明

本项目是基于多元哲学和法律框架的**思维练习工具**，旨在提供多角度思考，**不构成法律意见**。加权体系反映了对当代共识的偏好，不代表唯一正确的道德立场。

## 赞助支持

如果这个项目对你有帮助，欢迎赞助支持：

| 微信赞赏 | 链动小铺 |
|:--------:|:--------:|
| <img src="assets/wechat-sponsor.png" width="200"> | <img src="assets/shop-qr.png" width="200"> |

- [链动小铺](https://pay.ldxp.cn/item/gwd2qo)
- [PayPal](https://paypal.me/koboling)

## License

MIT
