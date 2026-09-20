# 日语口语训练系统

这是一个“ChatGPT 项目负责每日陪练，Codex 负责安装引导和周度复盘”的日语口语训练 Skill。

它融合了原版英语 Speaking System 的闭环：

```text
Input → Chunk → Retrieval → Output → Correction → Retest
```

但把内容改成了适合中国学习者、A2 / JLPT N4、以日常交流为目标的日语训练流程。

## 它解决什么问题

- 每天知道先学什么、怎么开口、怎么复盘；
- 让助词、动词活用、固定搭配进入滚动重测，而不是当天纠正后就遗忘；
- 区分“提示后会说”和“自由表达时自发会用”；
- 每周把 ChatGPT 项目中的多次练习整理成一篇可复习的 Markdown 周报；
- 摘出本周重点语法、重点词汇和表达，方便下一周复习。

## 安装与首次使用

用户不需要手动下载、解压或复制 Skill 文件夹。推荐把 GitHub 上的
`AGENT-SETUP.md` **raw 链接**交给一个拥有本地文件和网络权限的 Agent，让 Agent
自己读取安装说明、下载仓库、安装并校验 Skill。

在 Codex 或其他本地 Agent 中发送：

```text
请读取并严格执行这个 Agent 安装文档，帮我安装日语口语训练 Skill：
https://raw.githubusercontent.com/joey-41/japanese-speaking-system/main/AGENT-SETUP.md
```

Agent 应当完成以下工作：

1. 读取 raw 链接指向的完整 `AGENT-SETUP.md`；
2. 从同一 GitHub 仓库下载 Skill；
3. 安装到 `$CODEX_HOME/skills/japanese-speaking-system/`，未设置时使用 `~/.codex/skills/`；
4. 检查 `SKILL.md`、`README.md`、`AGENT-SETUP.md` 和 `references/` 是否完整；
5. 读取已安装的 Skill，生成 ChatGPT 项目提示词。

用户不应被要求手动下载或复制 Skill。本 Skill 的公开仓库地址是：

<https://github.com/joey-41/japanese-speaking-system>

如果以后迁移仓库，需要同步更新上面的 raw 链接；不要把本地路径伪装成 GitHub 链接。

安装完成后仍有一个明确的产品边界：Agent 不能假装替用户创建或修改 ChatGPT 项目。
用户只需要手动完成最后这一步：

1. 在 ChatGPT 中创建项目，名称建议为 `日本語`；
2. 打开项目设置中的 Instructions；
3. 将 Agent 生成的完整提示词粘贴进去；
4. 回到项目内输入 `今日预习` 验收第一步。

这一步是“配置 ChatGPT 项目”，不是“安装 Skill”；Skill 的下载、安装和校验应由 Agent 完成。

## 每日 SOP

### 1. 文字预习

在 ChatGPT 的 `日本語` 项目中输入：

```text
今日预习
```

会得到：

- 一篇约 350–500 日语字符的生活类短文；
- 5 个重点表达；
- 8–10 个重点单词；
- 2–3 个重点语法；
- 朗读和语音练习的材料。

读熟预习卡后，打开语音。

### 2. 语音练习

在语音对话中输入或说：

```text
开始口语练习
```

流程固定为：

1. 预告主题；
2. 完整朗读课文；
3. 逐个解释 5 个表达；
4. 一次练一个表达，中文给情境，用户用日语产出；
5. 完成内容理解、生活观点和课文复述三问；
6. 继续错误重测、表达重测、任务卡和当日输出任务。

如果已经读完预习卡，可以说 `今日已预习`，直接进入朗读和语音操练。

### 3. 当天复盘

语音练习结束后切回文字输入：

```text
按模板复盘
```

每日复盘继续保留在 ChatGPT 项目中，不需要每天复制到本地。

### 4. 结束训练

只有在用户说：

```text
今天到这
```

时才结束完整训练流程。某个环节提前完成时，应增加追问、换说法、举反例或重造句，不要直接询问“还要继续吗”。

## 每周 SOP

每周在 Codex 中输入：

```text
生成本周日语复盘
```

Skill 会读取 ChatGPT `日本語` 项目中本周可见的实际对话，并生成：

```text
Japanese-Speaking-Review/weekly/YYYY-W##.md
```

周报包含：

- 每日主题、时长、评分和缺失日期；
- 本周进步和重复错误；
- 助词、活用、固定搭配、句型组织等错误趋势；
- 重点语法复习表；
- 重点词汇与表达复习表；
- 表达自发使用和毕业状态；
- 下周不超过 3 个训练重点；
- 每日摘要。

其他指令：

```text
生成上周日语复盘
刷新本周日语复盘
```

周报以每日复盘为事实来源，不重新替用户评分，也不虚构不可见的聊天记录。

## 月度复盘

在 ChatGPT 项目中输入：

```text
月度模考
```

进行日常问答、生活角色扮演和连续表达，并生成日语口语复盘以及 CEFR / JLPT 参考判断。

JLPT 没有正式口语考试，因此报告中的 JLPT 只能作为语法词汇水平参考，不能称为正式成绩。

## 推荐目录

```text
japanese-speaking-system/
├── SKILL.md
├── README.md
├── AGENT-SETUP.md
├── agents/
│   └── openai.yaml
└── references/
    ├── japanese-project-instructions.md
    └── weekly-report-template.md
```

运行后产生的学习资料建议独立放在当前工作区：

```text
Japanese-Speaking-Review/
└── weekly/
    ├── 2026-W38.md
    └── 2026-W39.md
```

## 核心设计原则

1. 先输入，再提取，再输出；只读课文不等于会说。
2. 搭配操练和错误重测即时纠正；自由表达等用户说完再集中纠正。
3. 同一个表达在自由输出中无提示、正确使用两次，才算毕业。
4. 日语重点优先级是助词、动词活用、固定搭配和自然度，而不是堆高级单词。
5. 每周报告既看分数，也看错误率、连续输出时长和表达自发使用情况。
6. 每周复盘保留为 Markdown，不依赖 Obsidian、数据库或后台同步。

## 当前限制

- Codex 只能读取当前应用暴露出来的 ChatGPT 项目和对话；报告会明确写出可见范围。
- 对话标题不一定等于练习日期，周报以每日复盘正文中的日期为准。
- 日语转写没有天然空格，词数和 WPM 只能作为近似记录。
- 发音如果无法从转写可靠判断，不应虚构发音错误。
