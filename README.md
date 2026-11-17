# Neverhash

Neverhash 是一套面向 AI Agent 的仓库组织与文档写作规范。它约束 Agent 如何设计目录、命名文件、组织说明，以及选择值得长期保留的项目内容。

现代 Agent 可以迅速生成大量代码、文档和实验记录。一个简单的功能可能伴随多份重复说明，一次测试可能留下整个输出目录，一项局部修改也可能引入新的脚本和 CI 工作流。这些额外内容增加了理解与维护项目的成本。

Neverhash 的目标是：**让初次接触项目的读者，以尽可能低的理解成本，获得尽可能多的有效信息。** 仓库应清楚地呈现当前成果。文档应完整而流畅。每个文件都应有明确用途。

## Philosophy

Neverhash 遵循六项理念。它们共同决定应当写什么、怎样写，以及哪些内容无需进入仓库。

- **Reader First** — 从读者需要理解的内容出发，优先介绍项目目的、功能和使用方式。
- **Fluency Over Accuracy** — **流畅性 > 准确性。** 当局部精确性打断整体叙述时，优先保证读者能够连续理解。主动概括或省略次要细节。
- **Information Has a Cost** — 每句话都应传递有效信息，每个文件都应值得长期维护。
- **One Purpose, One Place** — 每个主题有一个明确位置。相关信息集中组织，减少重复文档和跳转。
- **Explicit Meaning** — 使用直接陈述、肯定表达、一致术语和简洁句式，减少防御性修辞。
- **Examples Before Abstraction** — 使用完整、直观的实例解释规则与技术概念。

这些原则借鉴 [ASD-STE100 Skill](https://github.com/danyuchn/asd-ste100-skill) 的简洁、明确和有序表达，并将约束扩展到文档边界、仓库结构和提交管理。Neverhash 是独立规范，不宣称符合正式 ASD-STE100 标准。

## What It Covers

**仓库组织。** 使用语义明确、长期稳定的文件名。根据实际职责划分目录，避免无意义编号、日期文件名、过深层级和提前创建的模块。

**文档写作。** 先传达主要观点，再说明必要依据。使用短句与连贯段落，以实例解释抽象概念。每份文档承担独立职责，能够在一处讲清的内容集中说明。

**信息与证据。** 正文突出问题、方法和结论。提交历史保存变更，研究记录保存必要的证据。避免反复向正式文档加入哈希值、环境快照和运行流水账。

**提交管理。** 只保留有长期用途的代码、测试、配置和文档。未经明确要求，不提交 Agent 专属目录、本机脚本、临时日志或过大的实验数据。CI/CD 应解决实际且持续的问题，不能成为每次提交的默认附加工作。

**工作成果。** Agent 可以在内部进行审计、检查和验证，但这些过程应直接改善成果。最终文档应移除审计报告、检查清单和其他没有独立用途的工作脚手架。

完整规则、目录示例、正反例以及 Agent 执行流程均集中在 **[SKILL.md](SKILL.md)**。它是本仓库唯一的规范正文。

## Usage

在支持 Agent Skills 的工具中添加本仓库：

```bash
npx skills add ddy314/neverhash
```

随后可以直接要求 Agent 在编辑仓库时应用 Neverhash。例如：

> Apply Neverhash to this repository. Improve the README for a first-time reader, consolidate overlapping documents, use semantic filenames, and exclude temporary artifacts. Keep the final changes focused.

Neverhash 也适用于单独撰写 README、技术设计、论文说明或 Pull Request。无论任务大小，首先理解已有内容，尽量在原有结构中完成修改。

## Repository Contents

```text
neverhash/
├── README.md   # 项目介绍、理念与使用方式
└── SKILL.md    # 完整的 Agent 写作与仓库管理规则
```

README 负责让读者理解为什么需要 Neverhash，以及如何开始使用。SKILL.md 负责规定 Agent 的具体行为。两份文件各有职责，避免建立重复的规则集。
