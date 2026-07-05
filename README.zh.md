# 受 Thariq 启发的智能体未知项指南

[![skills.sh](https://skills.sh/b/Yevanchen/thariq-shihipar-skills)](https://skills.sh/Yevanchen/thariq-shihipar-skills/find-unknowns)

一个单一的 `CLAUDE.md` 文件，用于改善智能体式编码行为，源自 [Thariq Shihipar 的实践指南](https://x.com/trq212/status/2073100352921215386)：在实现前、实现中、实现后持续发现未知项。

[English](./README.md) | 简体中文

## 问题所在

来自 Thariq 的文章：

> 你交给智能体的 prompt、skill 和上下文，只是工作的地图。

> 真正的领土是代码库、产品、现实世界，以及实现过程中才会出现的约束。

> 当地图和领土不一致时，智能体只能猜测你想要什么。

## 解决方案

四个原则，集中在一个文件中，直接解决这些问题：

| 原则 | 解决什么问题 |
|-----------|-----------|
| **标出未知项** | 缺失上下文、隐藏假设、模糊任务边界 |
| **编码前发现** | 未知的未知、"看到才知道" 的需求 |
| **实现中记录** | 中途偏离、边界情况、静默转向 |
| **闭环交付** | 评审困惑、交接薄弱、实现上下文丢失 |

## 四个原则详解

### 1. 标出未知项

**prompt 是地图。代码库、产品、用户和约束是领土。先把差距说清楚。**

实现前，拆解任务：

- **已知的已知** — prompt、规格、代码或已声明约束中已有的事实
- **已知的未知** — 你知道必须回答的问题
- **未知的已知** — 只有看到原型、diff、设计或行为后才会识别的标准
- **未知的未知** — 盲点、既有方案、边界情况、隐藏风险或更好的可能结果

如果未知项主导任务，不要立刻让智能体执行。先让它发现、访谈、原型或检查参考资料。

### 2. 编码前发现

**先低成本发现未知项，避免它们变成高成本代码。**

使用能暴露不确定性的最小工件：

- **盲点扫描** — 在不熟悉的领土里，请求相关 unknown unknowns
- **教我我的未知项** — 当你还无法判断 "好" 是什么时，请求领域词汇、质量标准和失败模式
- **头脑风暴或原型** — 当你只有看到后才知道答案时，生成多个具体选项
- **访谈** — 一次问一个问题，优先问那些会改变架构、API、数据模型、UX 或安全边界的问题
- **参考资料** — 当语言太模糊时，指向源代码、示例、截图、文档或旧实现
- **可调整计划** — 把用户最可能修改的决策放在前面，把机械工作放在后面

**检验标准：** 这个工件是否在实现前暴露了一个决策、风险或质量标准？

### 3. 实现中记录

**有些未知项只会在领土里出现。记录它们，不要让它们消失。**

在模糊或长时间任务中：

- 维护一个 `implementation-notes.md` 或 `.html` 草稿工件
- 当现实迫使计划改变时，在 `Deviations` 下记录偏离
- 如果必须在没有用户输入时继续，选择保守路径
- 如果新未知项推翻计划，停止并暴露决策，不要静默转向
- 把发现的事实转化为下一轮 prompt、规格、检查清单、测试或项目指令

**检验标准：** 下一次尝试是否能从更好的地图开始？

### 4. 闭环交付

**发布意味着别人会继承你的未知项。让它们可评审。**

合并、交接或审批前：

- 把原型、规格、决策、实现笔记和证据打包成简洁解释文档
- 先展示 demo 或行为，再回答评审者可能提出的反对意见
- 当变更太大、无法只靠 diff 理解时，请求测验或评审指南
- 只有 owner 理解改了什么、为什么改、剩余风险是什么时才合并

**检验标准：** 评审者能否不靠自己从 diff 里重建未知项，也能理解这项工作？

## 安装

**选项 A：skills.sh / Agent Skills**

用 Skills CLI 安装可复用 skill：

```bash
npx skills add Yevanchen/thariq-shihipar-skills --skill find-unknowns
```

不安装直接使用：

```bash
npx skills use Yevanchen/thariq-shihipar-skills --skill find-unknowns
```

**选项 B：Claude Code 插件**

在 Claude Code 中，首先添加插件市场：

```
/plugin marketplace add Yevanchen/thariq-shihipar-skills
```

然后安装插件：

```
/plugin install thariq-shihipar-skills@thariq-skills
```

这会将指南安装为 Claude Code 插件，使其在你的项目中可用。

**选项 C：CLAUDE.md（按项目）**

新项目：

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/Yevanchen/thariq-shihipar-skills/main/CLAUDE.md
```

已有项目（追加）：

```bash
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/Yevanchen/thariq-shihipar-skills/main/CLAUDE.md >> CLAUDE.md
```

## 在 Cursor 中使用

本仓库包含一个已提交的 Cursor 项目规则 ([`.cursor/rules/find-unknowns.mdc`](.cursor/rules/find-unknowns.mdc))，因此在 Cursor 中打开项目时同样适用这些指南。详情请参见 **[CURSOR.md](CURSOR.md)**，包括如何在其他项目中使用该规则，以及它与 Claude Code 的关系。

## 核心洞察

强编码智能体的质量瓶颈，很多时候不是生成能力，而是人和智能体是否已经把未知项降到足够少，使智能体不必靠猜来做关键决策。

"Find Unknowns" 原则捕捉的就是这一点：把模糊任务上下文转化为工件、问题、计划、笔记和解释文档，让地图持续贴近领土。

## 如何判断它在起作用

如果你看到以下情况，说明这些指南正在发挥作用：

- **静默假设更少** — 未知项在实现前被暴露
- **计划更好** — 计划把用户可能调整的决策放在前面
- **长任务更稳** — 偏离被记录，而不是被隐藏
- **评审更顺畅** — 评审者理解改了什么、为什么改、剩余风险是什么

## 定制

这些指南设计用于与项目特定指令合并。将它们添加到现有 `CLAUDE.md` 或创建一个新的。

对于项目特定规则，添加如下章节：

```markdown
## 项目特定未知项

- 修改 billing 代码前先请求 blindspot pass
- 视觉改动先做原型，再接后端行为
- 多小时任务如果偏离计划，记录到 `implementation-notes.md`
```

## 权衡说明

这些指南倾向于**澄清而非速度**。对于琐碎任务、简单拼写修复和显而易见的一行修改，请自行判断。不是每个改动都需要完整的未知项流程。

目标是减少模糊工作中的高成本错误，而不是拖慢简单任务。

## 许可

MIT
