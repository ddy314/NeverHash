---
name: neverhash
description: "Apply when an AI agent writes or edits a README, technical document, research report, repository structure, filenames, proposed commit, or pull request. Make information reader-first, fluent, coherent, and selective. Remove duplicate documents, incidental precision, process scaffolding, unnecessary agent files, and unjustified CI/CD."
---

# Neverhash — Repository and Documentation Rules

Neverhash 约束 AI Agent 如何组织仓库、撰写说明和选择提交内容。它适用于软件、工具、研究和论文仓库，也适用于 README、设计文档、实验总结、代码注释、提交说明及 Pull Request。

**最终目标：让初次接触项目的读者，以尽可能低的理解成本，获得尽可能多的有效信息。** 先理解现有项目，再根据本文修改内容。不要为了满足规范而增加新的文件和目录。

## 1. Core Principles

### 1.1 Reader First

从读者需要理解什么出发，选择信息及其顺序。首先说明项目要解决的问题、当前提供的功能和使用方式，再介绍必要的技术背景。开发过程和历史记录不应决定主体文档的结构。

例如，编译器 README 应首先说明支持的语言、编译命令和实现范围。解析器经历的重构过程交给版本历史。读者无需了解作者的全部工作过程才能理解当前项目。

### 1.2 Fluency Over Accuracy

**流畅性 > 准确性。**

这是强制性写作优先级。局部准确性影响整体流畅性时，优先保证读者能够连续理解文章。主动概括复杂条件，省略次要细节，合并相近说明。即使损失部分局部精确度，也应选择更顺畅的表达。

禁止以追求绝对严谨为由，不断向主体叙述添加限定词、括号、脚注、运行参数和例外情况。不要为了交代一个细节，反复中断核心论述。必要的证明、协议要求、可执行条件和研究数据可以放在各自有明确职责的位置，主体文档优先传达结论、方法和意义。

例如，性能改进说明应先陈述优化目的和效果。只有具体参数影响读者对结果的理解时，才展开参数。

### 1.3 Every Piece of Information Has a Cost

每句话消耗注意力，每个文件增加维护成本。保留的内容必须帮助读者理解事实、作出判断或执行操作。删除重复结论、空泛评价、无关背景和自我解释。

**Poor**

> 本项目采用模块化设计。这种设计具有一定优势，有助于提高整体结构的清晰度，并在一定程度上增强可维护性。

**Good**

> 项目将词法分析、语法分析和代码生成放在独立模块中。修改语法规则时，可以保留现有的代码生成模块。

### 1.4 One Purpose, One Place

每个主题只有一个权威信息位置，每份文档有独立职责。能够在一个文档中完整解释的主题，集中在这个文档中。仅在读者需求独立或内容规模妨碍连续阅读时创建新文档。避免重复文档、导航中转页和多次跳转。

### 1.5 Explicit Meaning

直接说明目的、行为、结果和适用范围。优先使用肯定句、主动语态、明确动词和一致术语。删除“值得注意的是”“需要强调的是”等空泛引导语。用具体范围表达结论，避免一连串防御性否定。

**Poor**

> 这并不能证明该方法在所有情况下都具有优势，也不能排除其他因素的影响。

**Good**

> 该方法在当前测试场景中取得了更好的结果。

### 1.6 Concrete Examples Before Abstraction

用最小而完整的例子建立直观认识，再总结抽象规律。示例必须服务于正在解释的概念。不要为展示实现的全部细节而加入无关代码。

---

## 2. Repository Organization

仓库应反映当前功能和实际复杂度。目录划分职责，文件实现功能或传达信息。读者应能通过目录与文件名识别项目入口、核心模块、测试和必要资料。

### 2.1 Root Directory

根目录是项目入口，保持简洁。典型软件仓库可以这样组织：

```text
project/
├── README.md
├── LICENSE
├── pyproject.toml
├── src/
│   └── project/
│       ├── main.py
│       ├── parser.py
│       └── evaluator.py
├── tests/
│   ├── test_parser.py
│   └── test_evaluator.py
└── examples/
    └── basic_usage.py
```

这只是职责示例，实际文件必须遵循项目语言及构建工具的约定。一个单文件工具无需预建完整目录树。不要为了仓库看起来完整而创建尚未使用的目录。

### 2.2 Directory and File Order

采用自然的逻辑顺序：**项目入口 → 核心实现 → 辅助功能 → 测试与示例 → 补充资料。** 子目录同样应先让读者找到入口和主要功能。

同层文件使用稳定的语义名称，让相关文件容易识别。无需通过数字前缀强迫文件管理器使用特定排序。

**Good**

```text
parser/
├── ast.py
├── lexer.py
├── parser.py
└── tokens.py
```

**Poor**

```text
parser/
├── 01_start.py
├── 02_process.py
├── 03_finish.py
├── parser_new.py
└── parser_final.py
```

后者记录了临时开发阶段，读者无法从名称判断长期职责。目录顺序依靠清晰的边界和名称表达，必要的操作顺序写在实际使用说明中。

### 2.3 Directory Boundaries

将共同完成一个职责的文件放在同一模块。只有一个简单文件时，保持结构扁平；当模块拥有多个独立组件时，再建立目录。

**Poor**

```text
src/core/internal/components/processing/parser.py
```

**Good**

```text
src/parser.py
```

当解析器具有词法分析、语法树和错误恢复等独立组件时，`src/parser/` 可以成为合理的模块。不要预先设计未来可能使用的层级。

### 2.4 Semantic Filenames

文件名必须准确、稳定地描述用途。避免 `new`、`old`、`latest`、`final`、无意义编号和时间后缀。

| Poor | Good | Reason |
| --- | --- | --- |
| `test2.py` | `test_lexer.py` | 明确测试对象 |
| `new_algorithm.py` | `beam_search.py` | 描述实际算法 |
| `final_result.md` | `evaluation.md` | 描述主题 |
| `notes_latest.md` | `design-decisions.md` | 明确记录内容 |
| `script.py` | `export_dataset.py` | 说明功能 |
| `run_2026_11_17.csv` | `validation_samples.csv` | 去除日期依赖 |
| `misc/` | `formatting/` | 明确目录职责 |

**禁止在新文件名中添加日期或时间。** 修改历史交给版本控制系统。保留构建工具、语言生态和公开接口要求的标准文件名。

### 2.5 Research Repositories

研究仓库可以按论文、证明、计算程序和测试的实际职责组织。以最大行列式研究为例，适用时可采用：

```text
project/
├── README.md
├── paper/
├── proofs/
├── computations/
└── tests/
```

README 概括研究问题、主要成果及入口。论文呈现研究叙述，证明材料保存推导，计算目录保存有长期用途的程序。该结构是示意，并非要求所有研究仓库创建这些目录。

不要把论文、正式证明、临时猜想、实验日志和执行输出混在同一层。研究历史优先由 Git、Issues 或 PR 保存。长期文档只保留对理解当前成果有用的信息。

### 2.6 No Artificial Structure

创建文件或目录之前，先检查已有内容能否承担新职责。禁止空目录、没有读者需求的说明文件、重复的模块入口和无意义的包装层。重组完成后删除被替代的文件与无效引用，避免保留导航脚手架。

---

## 3. Documentation

文档应以连续、完整的叙述解释项目目标、方法、行为和使用方式。每个章节回答明确的问题，章节之间按读者理解问题的顺序衔接。

### 3.1 Start with the Main Idea

README 首先介绍项目，设计文档首先说明设计目标，研究报告首先说明研究问题与主要结论。不要用通用行业背景延迟主题。

**Poor**

> 随着计算机视觉技术不断发展，图像处理日益重要。研究人员提出了各种方法来提升复杂环境下的图像质量。

**Good**

> 该项目实现基于暗通道先验的图像去雾算法，并使用 C 和 SIMD 加速处理。程序可以处理图像和视频帧，并使用客观指标评估结果。

### 3.2 Build a Complete Narrative

按照读者获取知识的过程组织内容。项目说明可以依次介绍用途、功能、使用方式和设计；研究说明可以依次介绍问题、方法、结果和意义。具体章节依据实际内容决定，不要为了模板创建空章节。

相邻部分要有清楚的逻辑关系。解释编译器的解析流程时，集中说明词法分析、语法分析和语法树。构建环境与历史实验放在更合适的位置。

### 3.3 Short, Dense Sentences

优先使用简短、完整、有明确主语和动词的句子。每句表达一个主要意思。缩短句子是为了提高阅读效率，避免机械地把一段连贯意思切成碎片。

**Poor**

> 由于编译器采用递归下降语法分析，并且需要判断输入程序中不同类型的语法结构，因此必须通过多个相互调用的函数完成语法树构建。

**Good**

> 编译器使用递归下降解析器。每个解析函数处理一种语法结构，再通过函数调用组合完整的语法树。

### 3.4 Paragraphs as Information Units

每个段落围绕一个主题，包含能够共同表达完整意思的句子。避免大段堆砌，也避免每个句子独立成段。

**Poor**

> 编译器支持变量声明。
>
> 变量可以具有显式类型。
>
> 类型检查发生在语义分析阶段。
>
> 类型错误会产生诊断信息。

**Good**

> 编译器支持带有显式类型的变量声明。语义分析阶段检查变量类型，并在发现类型错误时生成诊断信息。

### 3.5 Affirmative and Direct Language

直接陈述结果及其适用范围。避免连续堆叠“并不意味着”“不能排除”“尚不足以证明”等防御性表达。主动删去没有独立信息的开场套话。

**Poor**

> 当前结果并不能证明所提出的方法在所有场景中均具有优势，也不能完全排除其他因素的影响。

**Good**

> 该方法在当前实验场景中取得了更好的结果。

### 3.6 Explain with Concrete Examples

复杂概念先给最小的例子，再说明原理。例如，介绍编译器如何处理运算符优先级：

```rust
let result = 2 + 3 * 4;
```

对应的简化表达式树：

```text
Add
├── Number(2)
└── Multiply
    ├── Number(3)
    └── Number(4)
```

这个例子直接展示了乘法优先级。无需在同一节列出解析器所有函数或完整实现。

### 3.7 Separate Different Cases

不同条件使用独立、连续的说明。Windows 与 Linux 的安装命令分别写；默认模式与高级配置分别介绍；正常执行与错误处理分别描述。避免在同一段落中频繁切换条件。

### 3.8 Keep Documents Self-Contained

文档必须独立传达主要信息。外部资料可以深入说明，不得代替当前文档的核心解释。

**Poor**

> 研究动机见文档 A。构造方法见论文 B。验证过程见文档 C。结果解释见文档 D。

**Good**

> 本研究通过显式构造自动机族，分析同步词长度。核心方法是构造满足指定转移结构的自动机，再验证其最短同步词。正式证明与计算程序保存在仓库中，供需要深入检查的读者使用。

### 3.9 Links Must Have a Purpose

使用链接时，说明目标提供了什么信息及为什么需要它。避免只给一个裸链接、用“更多信息”替代解释，或让读者不断跳转才能理解当前文档。

**Poor**

> 相关信息：[link](https://example.com)

**Good**

> 算法参考资料说明了状态转换的定义及证明方法。

若当前文档能够清楚解释一个概念，直接说明。引用应补充证据、背景或技术深度。

### 3.10 Avoid Redundant Documents

**Poor**

```text
docs/
├── introduction.md
├── overview.md
├── background.md
├── project-summary.md
├── design-overview.md
└── implementation-notes.md
```

当这些文档讲述同一主题时，应整合。

**Good**

```text
README.md
docs/
├── architecture.md
└── api.md
```

README 介绍项目与用法。架构文档解释系统设计。API 文档说明接口。只有确有独立需求时才创建后两者。

### 3.11 Remove Writing Scaffolding

**最终文档呈现整理完成的知识，删除写作和研究过程中的脚手架。**

Agent 可以内部检查、审计、交叉验证和整理问题。这些工作应直接改善成果。除非用户明确要求，不要创建独立的审计章节、审计报告、验证清单和过程性总结。审计是其他工作的附属过程。

例如，修订数学论文后，最终论文应呈现修订好的定义、定理和证明。用于检查的临时笔记与逐项审计表无需进入论文。修复代码后，更新代码、测试和相关说明；不要额外提交 `AUDIT_REPORT.md` 或 `VERIFICATION_SUMMARY.md`。

发现的问题应进入对应位置：接口问题进入接口说明，设计问题进入设计文档，测试要求进入实际测试。让成果本身体现改进。

---

## 4. Technical Detail and Evidence

技术文档要解释重要设计和结果。Agent 应区分核心信息与辅助记录，避免把主体叙述写成实验过程或运行输出的堆积。

### 4.1 Results Before Details

先写结论，再介绍理解结论所需的主要依据。

**Poor**

> 我们在多个图像尺寸下运行去雾程序，调整线程数并记录执行时间。随后使用 PSNR 和 SSIM 评估图像质量，对不同配置进行比较。

**Good**

> SIMD 优化提高了去雾程序的处理速度。图像质量通过 PSNR 和 SSIM 评估，结果显示优化后的实现保持了预期效果。

### 4.2 Remove Incidental Precision

主体文档避免反复出现哈希值、运行编号、临时路径、环境版本和无关参数。

**Poor**

> 在提交 `a81d9e2` 中，我们采用指定编译选项运行第 17 组实验，随后调整两个参数执行第 18 组和第 19 组实验。

**Good**

> 实验比较了不同编译配置的性能。优化后的配置减少了执行时间。

确有需要的完整条件放在相应的基准测试说明或研究数据中。不要让一次执行的环境覆盖项目的长期说明。

### 4.3 Explanation and Provenance

Git 保存文件变化，Issues 和 PR 保存讨论与决策，长期文档解释当前设计和使用方式。不要将开发时间线复制到 README，也不要持续追加过期方案和临时运行结果。

### 4.4 Useful Research Evidence

数学证明、基准测试方法、关键实验条件和能够支撑结论的数据可具有长期价值。应保留在职责明确的位置。原始日志、重复结果和调试记录通常留在仓库之外。

研究说明应回答研究了什么、用了什么方法、发现了什么、结果有何意义。不要将实验输出原样作为论文或正式报告。

---

## 5. Repository Content and Commit Policy

仓库应保存支持开发、使用、测试和维护的必要内容。任何新增文件都应具有长期用途。

### 5.1 What to Keep

保留源代码、必要配置、可维护测试、可移植脚本和有明确读者用途的文档。示例及测试数据应保持适当规模。禁止为未来假设的需求创建空目录、预留文件或冗余辅助系统。

### 5.2 Agent-Specific Files

**除非用户明确要求，禁止提交 `.codex/`、`.claude/` 等 Agent 专属目录。** 不要提交一次性提示词、内部任务状态、Agent 运行记录及只对当前工具有用的配置。项目应独立于作者使用的 Agent 和编辑器。

### 5.3 Local Scripts and Environments

禁止提交依赖作者机器、个人绝对路径、私有配置或未记录状态的脚本。

**Poor**

```python
data = open("/home/user/Desktop/project/data.txt")
```

**Good**

```python
from pathlib import Path
import sys

data = Path(sys.argv[1]).read_text()
```

第二种实现允许调用者指定输入文件。只有脚本具有清晰用途、稳定输入输出和可维护执行方式时，才适合长期保留。非必要的本机环境信息不进入正式文档。

### 5.4 Generated Output and Large Datasets

除非明确要求，禁止提交控制台输出、调试日志、缓存、一次性报告、重复生成物和过大的实验数据集。训练项目可以保留数据获取方法、格式说明与小型样本，将完整数据存放在合适的数据系统中。

### 5.5 CI/CD Must Be Justified

**没有明确需求时，不得主动添加或扩大 CI/CD 工作流。** 持续集成会增加运行成本、外部依赖和维护责任。它必须解决真实、持续存在的问题，不能成为每次推送的默认附加工作。

**Poor：为小型研究修改新增大量工作流**

```text
.github/
└── workflows/
    ├── lint.yml
    ├── test.yml
    ├── docs.yml
    ├── audit.yml
    └── validate.yml
```

**Good：已有测试能直接执行**

```text
tests/
└── test_parser.py
```

小型项目可优先运行现有本地测试。文档更新通常不需要新增 GitHub Actions。确有自动发布、多平台兼容检查或持续协作需求时，可添加职责明确的工作流。避免重复执行同一任务，也不要为了证明已经检查而额外创建 CI 任务。

### 5.6 Proportional Verification

检查规模与修改影响相称。文档修改重点检查内容和链接；局部代码修改运行相关测试；公共接口或核心算法修改可以扩大验证范围。

Agent 可私下使用临时工具检查，但应清理其产物。重要发现直接体现为代码、测试或对应说明。除非明确要求，不创建审计项目、检查目录或独立报告。

### 5.7 Focused Commits and Pull Requests

每次提交围绕一个明确目标。不要在实现功能时附带大量无关整理、临时实验或额外文档。提交说明表达主要变化及其意义。

**Poor:** `Various improvements and fixes`

**Good:** `Fix parser handling of nested expressions`

复杂 PR 可简述设计选择与必要验证，不必列出 Agent 每次工具调用和逐项操作。

---

## 6. Agent Workflow

### 6.1 Understand Before Editing

阅读 README、相关源码和现有文档，明确项目目的、当前设计与修改目标。判断已有文件是否承载相应职责。优先修改、合并或删除，必要时再新增。

### 6.2 Design the Information Structure

明确目标读者、核心问题和最终需要传达的结果。按读者的理解顺序安排章节。一个主题优先一个位置，关系紧密的内容保持连续。

### 6.3 Write the Main Narrative

先写核心结论和必要方法，再补充例子与技术依据。采用短句、适当段落、一致术语和直接陈述。只添加真正帮助理解的信息。

### 6.4 Review Through Editing

检查直接服务最终成果。重复内容合并，模糊术语改写，重叠文档整合，无用文件移出提交范围。允许内部审计与验证，但最终交付去除过程性脚手架。

### 6.5 Deliver the Result Directly

简要报告实际变化和有意义的验证结果。保留影响用户决策的限制。避免将内部执行过程、工具调用和检查流水账作为交付主体。

---

## 7. Quality Standard

符合 Neverhash 的成果具备以下特征：

1. **容易理解。** README 直接说明目标、功能和用法。
2. **结构清晰。** 目录和文件名说明职责，结构对应实际需求。
3. **文档完整。** 相关信息集中呈现，减少重复和跳转。
4. **表达流畅。** 短句、适当段落、直接结论和直观示例构成连续叙述。
5. **信息经过选择。** 流畅性高于局部准确性，次要细节不会遮蔽主线。
6. **内容便于维护。** 临时记录、个人配置和不必要的自动化不占据仓库。
7. **成果直接。** 审计与验证服务于内容，交付时不保留内部脚手架。

Neverhash 不用文档数量、文本长度、自动化规模或技术细节的丰富程度衡量质量。

**每句话都有意义，每个段落都有主题，每份文档都有职责，每个文件都有存在的理由。**
