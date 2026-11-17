---
name: neverhash
description: "Use when organizing repositories or writing technical documentation."
---

# NeverHash — Repository and Documentation Rules

NeverHash 规范 AI Agent 如何组织仓库、撰写技术文档和提交修改。它要求仓库让陌生读者迅速理解项目的目标、当前成果与使用方式。每份文档承担清楚的职责，每个文件具有长期用途。

## 1. Writing

### 1.1 Fluency Over Accuracy

**流畅性 > 准确性。**

这是强制性的写作优先级。局部准确性妨碍整体阅读时，优先保持叙述流畅。主动概括复杂条件、合并相近信息、删除次要数据。允许为更顺畅的表达牺牲部分局部精确度。

先陈述读者需要理解的结论，再介绍必要的方法与依据。不要为了保留所有例外、参数、限定词和技术细节而持续中断正文。证明、精确协议、关键实验条件和可执行要求可以在对应的专业内容中完整保留；概述负责传达它们的意义。

**Poor**

> 在特定编译器版本、选定测试集和多种构建参数的共同条件下，优化后的程序在部分输入规模上观察到了不同程度的执行时间变化。

**Good**

> 优化后的程序在测试中运行得更快。性能差异随输入规模变化。

每句话都应帮助读者理解事实、作出判断或执行操作。删除空泛评价、自我表扬、重复结论、无关背景、借鉴来源说明和作者对自身写作过程的解释。无法证明必要性的内容应当删除。

### 1.2 Sentences and Paragraphs

优先使用短句。每句话表达一个主要意思，具有明确的主语和动词。每个段落解释一个主题，将几句关系紧密的话连续组织。避免冗长复合句、整页大段文字，以及每句话独立成段的碎片化写法。

**Poor**

> 由于解析阶段需要在识别词法单元的同时判断其是否能够组成合法的表达式结构，因此系统在执行过程中使用不同的组件来进行相关处理。

**Good**

> 词法分析器将输入转换为词法单元。语法分析器使用这些单元构建表达式结构。

列表适合步骤、互不依赖的选项和并列规则。连续的解释应使用段落。避免把完整论述切成大量孤立的列表项。

### 1.3 Direct and Affirmative Language

直接说明行为、目的、事实和结论。优先使用肯定表达、主动语态与具体动词。需要说明范围或前提时，直接写出已测量的条件、数据集和适用边界。区分观察结果、推导和计划，不要将推测写成事实，也不要列举所有理论上可能的例外。

**严禁在任何项目文本（文档、注释、界面文案、Commit Message、PR 描述）中使用以下防御性、否定式或过程自证话术模式。** 按语义判断，不得用同义改写绕过；一旦出现，直接改写为正面事实陈述（代码关键字、公开接口字段、数学形式化命题与原样引文除外）：

| Pattern | Forbidden Forms (Poor) | Affirmative Rewrite (Good) |
| --- | --- | --- |
| 范围与身份预否认 | `This is not …`、`This does not prove/imply/constitute …`、`这不是……`、`并不意味着……`、`不能证明……`、`不应解释为……`<br>例：`This is anomaly detection, not fault-ID classification.` | 直接定义系统执行的任务或作用范围。<br>例：`The monitor detects anomalies in process streams.` |
| 否定式对比转折 | `not X, but Y`、`rather than`、`instead of`、`不是……而是……`、`并非……而是……`、`不只是……更是……`<br>例：`这些贡献是统计残差权重，不是物理根因。` | 删去被否定的一侧，直接陈述实际含义。<br>例：`贡献分数度量各变量的统计残差权重。` |
| 免责承诺与模糊限定 | `does not guarantee`、`no generalization guarantee`、`may or may not`、`preliminary only`、`并不构成泛化保证`、`仅供参考`、`在一定程度上`<br>例：`Empirical calibration does not guarantee a target false-alarm rate.` | 写出具体的标定方式、评测数据集与观测指标。<br>例：`Thresholds are calibrated on the training split and evaluated on held-out test runs.` |
| 资质与成熟度免责 | `not production-ready`、`not safety-certified`、`not real plant measurements`、`非生产级`、`不属于安全认证工具`、`不是真实工厂数据`、`不是置信区间`<br>例：`不是工业真实数据，也不属于安全认证决策工具。` | 说明当前支持的工作流、运行环境或统计量定义。<br>例：`系统在 TEP 仿真数据上运行离线事件分析。` |
| 工程与历史自证 | `no files were overwritten`、`no other PR was merged`、`without relaxing validation`、`本次没有覆盖历史产物或放宽校验`、`本轮没有合并其他 PR`<br>例：`没有强推或删除历史分支，本轮没有合并其他 PR。` | 直接删除；版本变迁与合并范围由 Git 历史记录。 |
| 范围洗白与未完成播报 | `this change only …`、`outside the current scope`、`has not been uploaded/submitted`、`本次仅……`、`不在本次范围内`、`尚未上传/尚未独立验证`、`留待后续研究`<br>例：`此文件尚未上传 YouTube 或提交 Devpost。` | 只陈述当前已交付的成果与使用方式。<br>例：`演示视频保存在 video/ 目录，可由构建脚本生成。` |
| 展示型验证与哈希堆砌 | `all hashes remain unchanged`、`verification receipt`、`smoke test passed`、`57 个历史文件哈希不变`、`结构化验收回执`、`CI 全绿`、`详见审计文件`<br>例：`2,482 个原始与结果文件哈希保持一致，冒烟测试通过。` | 删除表面自证，用可执行的测试与核心实验结果支撑结论。 |
| 空泛引导与元叙述 | `it is worth noting that`、`to avoid confusion`、`for the avoidance of doubt`、`值得注意的是`、`需要强调的是`、`为避免误解`、`显而易见`<br>例：`值得注意的是，为避免误解，该算法并不在所有问题上最优。` | 删除引导语，直接陈述结论及测试范围。<br>例：`该算法在当前测试问题中表现更好。` |

### 1.4 Don't Repeat Yourself (DRY)

同一事实、规则、定义或结论只写一次：

- **不在同一处叠加多种形式**：用段落、列表或表格中的一种把问题讲清即可。禁止先罗列一遍，紧接着再用另一种形式重复同一批内容。
- **不维护简版与详版两套列表**：同一内容只保留唯一完整表述，不要在主文档写一部分，又在外部文件中重复维护扩充版本。
- **同一定义与符号只用一种形式**：任何概念、符号、指标或结构在全仓只定义一次，后续统一沿用首次确立的名称与记号。禁止在不同章节或文件中换用新名字、新记号将相同或高度相近的内容重新定义一遍。
- **不跨章节重复背景与前提**：共享的假设与实验条件在首次出现时集中说明，不在后续章节反复重申。
- **单一工作语言**：同一项目统一使用一种主语言撰写文档、注释与提交说明，不在正文中混用中英文或用双语并列重复同一句话。

### 1.5 Show a Concrete Example

解释复杂机制或架构设计时，先提供一个完整而简短的具体实例，再总结一般规律。实例只保留说明当前机制所需的部分。

例如，解释增量语法分析器如何在局部编辑后维持下游缓存命中时，可以先展示一次局部重解析前后的节点编号（Span）分配：

~~~text
Before edit:
Document [100..500]
├── Heading("Intro") [150]
├── Paragraph("Old text") [220..260]
└── Paragraph("Unchanged") [380..420]

After editing the first paragraph:
Document [100..500]
├── Heading("Intro") [150]
├── Paragraph("Updated longer text") [220..290]
└── Paragraph("Unchanged") [380..420]
~~~

读者可以直接看到局部编辑只重新分配 `[220..290]` 区间内的节点编号，后续段落的编号 `[380..420]` 保持稳定，因此以节点编号为键的增量缓存依然有效。随后再说明编号区间预留策略即可，无需贴出完整重解析代码。

## 2. Documents

### 2.1 One Purpose, One Place

每个主题只有一个权威信息位置。每份文档承担独立的阅读任务。优先完善现有文档；只有目标读者、用途或所需深度明显不同，才建立新文件。

README 介绍项目的用途、主要功能与使用入口。架构说明解释系统结构及设计选择。接口文档规定调用方式。研究论文提出研究问题、方法、结果与论证。只有项目确实需要这些独立内容时，才创建相应文件。

**Poor**

~~~text
docs/
├── introduction.md
├── background.md
├── overview.md
├── project-summary.md
└── design-overview.md
~~~

若这些文件都在介绍相同的项目目标与设计，应将其合并为一个完整的说明。必要的架构细节可以拥有独立文档。

### 2.2 Self-Contained Without Duplication

文档应独立完成自己的阅读任务。README 应让陌生读者理解项目，但无需重复架构文档的全部内容。概述可以简要说明结论；规则、参数定义与完整证明应各有唯一权威位置。

出现冲突时，**优先保留理解当前文档所需的最小上下文，再消除跨文档的重复解释。** 不要为追求自包含而复制整节规则，也不要为了减少重复把核心解释全部替换成链接。

例如，NeverHash 的 README 展示一个使用前后的仓库示例，说明这套规范能带来什么变化。本文件集中规定 Agent 的具体行为。读者能够从 README 理解项目，再按需阅读规则。

### 2.3 Natural Reading Order

按照读者理解问题的过程组织章节。项目说明先介绍用途、功能和使用方式，再进入设计。架构文档先给出顶层目录职责图谱，再按系统核心处理阶段（例如 `Parsing → Evaluation → Layout → Export`）依次说明每一阶段的输入输出、关键数据结构与模块位置。研究说明先提出问题与主要发现，再解释方法和证据。依据实际内容决定章节，禁止为了迎合模板而创建空章节。

同一章节围绕一个主题展开。构建环境、历史实验和发布计划应在各自合适的位置说明。

### 2.4 Purposeful Links

链接应提供原始材料、必要背景或深入内容。给出链接时，说明目标内容及作用。

**Poor**

> 详细信息请看[这里](https://example.com)。

**Good**

> [接口说明](https://example.com)列出了输入参数、返回值和错误代码。

当当前文档能够简洁解释一个概念时，直接说明。减少读者必须依次打开多个文件才能理解主题的情况。

## 3. Repository Structure

### 3.1 Scale Horizontally with a Flat Root

无论项目规模如何增长，仓库根目录始终保持精简，只放置入口文档（`README.md`、`CONTRIBUTING.md`、`LICENSE`）、工作区构建配置，以及少数几个顶层职责目录（如源码子包目录 `crates/` 或 `packages/`、文档目录 `docs/`、测试目录 `tests/`、辅助工具目录 `tools/`）。禁止把新增模块、阶段脚本或实验目录直接堆在根目录。

当系统规模扩大时，**按处理阶段或独立职责在子包目录内横向平铺拆分**，不要向深处堆叠多层抽象目录（如 `src/core/internal/engine/v2/`）：

- **主入口与薄封装层分离**：核心库编排完整流程，CLI 或 IDE 服务作为薄封装层置于同级子包。
- **处理流水线分包**：词法与语法树、语义求值、排版或核心计算、各类导出后端各自成为同级子包，并以统一前缀命名。
- **子包内部先平铺、按需建子目录**：子包内优先将单文件模块平铺（如 `ast.rs`、`lexer.rs`、`parser.rs`、`span.rs`）；只有当某个子领域（如排版中的 `flow/`、`grid/`、`inline/`、`math/`、`pages/`）确实包含多个紧密协作的实现文件时，才向下建立一层子目录。

**Good：随规模横向扩展的多子系统仓库**

~~~text
compiler/
├── Cargo.toml
├── README.md
├── crates/
│   ├── compiler/          # 顶层编译入口与主流程编排
│   ├── compiler-cli/      # 命令行薄封装层
│   ├── compiler-syntax/   # 词法、无类型语法树、类型化 AST 与增量重解析
│   │   └── src/
│   │       ├── ast.rs
│   │       ├── lexer.rs
│   │       ├── lib.rs
│   │       ├── node.rs
│   │       ├── parser.rs
│   │       ├── reparser.rs
│   │       └── span.rs
│   ├── compiler-eval/     # 虚拟机、作用域栈与模块求值
│   ├── compiler-layout/   # 排版引擎：简单模块平铺，复杂模式单建一层子目录
│   │   └── src/
│   │       ├── flow/
│   │       ├── grid/
│   │       ├── inline/
│   │       ├── math/
│   │       ├── pages/
│   │       ├── lib.rs
│   │       ├── lists.rs
│   │       └── shapes.rs
│   ├── compiler-pdf/      # PDF 导出后端
│   ├── compiler-svg/      # SVG 导出后端
│   └── compiler-utils/    # 跨模块通用工具
├── docs/
│   ├── dev/
│   │   └── architecture.md
│   └── reference/
├── tests/
│   ├── ref/               # 基准参考输出
│   ├── src/               # 测试驱动与校验器
│   └── suite/             # 按功能域划分的集成测试集
│       ├── layout/
│       ├── math/
│       ├── scripting/
│       └── syntax/
└── tools/                 # 开发与调试辅助工具
~~~

**Poor：根目录膨胀与纵向嵌套失控**

~~~text
compiler/
├── README.md
├── ARCHITECTURE_V2.md
├── stage1_summary.md
├── run_all_checks.sh
├── pdf_export_new/
├── src/
│   └── core/
│       └── internal/
│           └── engine/
│               ├── 01_tokenize.rs
│               ├── 02_parse_new.rs
│               ├── parser_final.rs
│               └── math_layout_v2.rs
├── scripts/
│   ├── smoke_test_2026.py
│   └── verify_hashes.py
└── test_outputs_backup/
~~~

### 3.2 Align Tests and Tooling with Domain Boundaries

随着功能增加，测试与文档应与核心子模块保持同构：

- **测试套件按功能域分目录**：在 `tests/suite/` 下按系统功能域（如 `syntax/`、`scripting/`、`layout/`、`math/`、`pdf/`）组织测试用例，将测试运行器（`tests/src/`）与参考输出（`tests/ref/`）分离。禁止按开发批次、Issue 编号或临时验证堆积 `test_stage1`、`smoke_test`、`regression_new`。
- **同层文件按职责命名排序**：目录内使用统一的领域名词命名，让文件按字母序自然呈现模块结构，不依赖 `01_`、`02_` 等序号前缀编码执行顺序。

### 3.3 Semantic Names

目录、子包与文件名应准确描述职责或领域概念，长期保持稳定。避免使用 `new`、`old`、`latest`、`final` 和无意义的数字后缀。

| Poor | Good | Reason |
| --- | --- | --- |
| `compiler_v2/` | `compiler-layout/` | 标明子系统职责而非迭代代数 |
| `parser_final.rs` | `reparser.rs` | 区分增量重解析与全量解析职责 |
| `test2.py` | `tests/suite/syntax/` | 按被测功能域归类 |
| `results_final.md` | `docs/dev/architecture.md` | 明确文档受众与主题 |
| `run_2026_11_17.csv` | `validation_samples.csv` | 名称不依赖运行日期 |
| `misc/` | `compiler-utils/` | 明确跨模块基础工具边界 |

**新文件名禁止包含具体日期和时间。** 修改时间由 Git 保存。保留构建工具、语言生态与公共接口要求的标准名称。

### 3.4 Research and Benchmark Repositories

大型研究与基准评测仓库同样保持精简根目录，按论文（`paper/`）、形式化证明（`proofs/`）、核心算法与评测实现（`benchmarks/` 或 `src/`）及测试（`tests/`）划分顶层目录：

~~~text
study/
├── README.md
├── pyproject.toml
├── paper/
│   ├── main.tex
│   └── sections/
├── proofs/
│   └── theorem_bounds.lean
├── benchmarks/
│   ├── datasets/
│   ├── methods/
│   ├── metrics.py
│   └── runner.py
└── tests/
    ├── test_methods.py
    └── test_metrics.py
~~~

新增对比算法、数据集或实验工况时，将其作为同级模块并入 `benchmarks/methods/` 或 `benchmarks/datasets/`，由统一的 `runner.py` 调度并更新权威结果表。禁止每做一轮实验就在 `docs/` 或根目录新建 `stage-one-validation.md`、`benchmark-expanded.md`、`integration-2026-10-23.md` 等阶段性报告。

## 4. Technical Detail and Evidence

### 4.1 State the Finding First

实验与研究说明应先给出结果，再介绍读者评估该结果所需的方法。不要按照实际执行顺序列出全部命令、参数、日志和截图。

**Poor**

> 我们先运行程序，再调整线程数，然后测试不同输入尺寸，记录执行时间，并使用 PSNR 和 SSIM 进行比较。

**Good**

> SIMD 优化提高了图像去雾的处理速度。PSNR 和 SSIM 测试用于评估优化后的图像质量。

让主体文档解释研究发现。完整执行细节应保存在需要它们的复现材料中。

### 4.2 Keep Provenance in Its Place

Git 历史记录版本变化，Issues 与 PR 记录讨论及决策，测试程序记录可执行的行为预期。长期文档描述当前有效的设计、方法和结果。

避免在 README 中反复引用提交哈希、运行编号、临时路径、本机环境和调试过程。证明、基准测试的关键条件与复现所需参数应保存在对应的专业材料中，避免反复出现在概述中。

## 5. Changes and Delivery

### 5.1 Keep Durable Content

提交具有明确长期用途的源代码、构建配置、测试、可移植脚本与文档。小型样本可用于展示格式或验证行为。体积过大的实验数据应保存在适合的数据存储中，并提供必要的获取说明。

**除非用户明确要求，禁止提交** Agent 专属目录（如 `.codex/` 和 `.claude/`）、一次性提示词、个人工作状态、硬编码本机绝对路径的脚本、控制台输出、缓存、临时报告和重复生成结果。脚本与工具应通过命令行参数、配置文件或相对工作区路径接收输入，不得将个人桌面或本机目录作为运行前提。

### 5.2 Add CI/CD Only for a Real Need

**没有明确要求或持续性需求时，不得新增或扩大 CI/CD。** 自动化工作流会增加维护责任、运行成本和外部依赖。一个小型研究修改可以使用已有测试和本地验证，普通文档修改也无需新建 GitHub Actions。

**Poor：为一项局部修改增加多套工作流**

~~~text
.github/workflows/
├── audit.yml
├── docs.yml
├── lint.yml
├── test.yml
└── validate.yml
~~~

持续发布、多平台兼容性检查或多人协作中的重复验证可以构成合理需求。新增工作流前，确认现有工作流和测试工具无法满足该需求。

### 5.3 Always Submit Changes Through a Pull Request

**任何仓库修改都必须先建立独立分支，通过 Pull Request 提交。禁止直接推送到主分支。**

按以下顺序操作：

1. 检查仓库当前状态与已有 PR，确认本次修改的目标。
2. 创建或使用本次修改的工作分支。
3. 在工作分支提交修改。
4. 为新任务创建 PR；若任务已存在对应 PR，则更新同一 PR。
5. 将最终成果交给用户审阅，由用户决定是否合并。

即使只有一个文件、一句话或一次小修复，也遵守这一流程。不要绕过 PR 直接修改 `main`、`master` 或仓库的其他默认分支。

**Good**

~~~text
main
└── docs/improve-readme
    └── Pull Request → review → merge
~~~

**Poor**

~~~text
main ← direct push
~~~

### 5.4 Verification Serves the Result

检查工作的规模应与修改影响相称。文档修改检查内容和链接，局部代码修改运行相关测试，关键接口与核心算法修改可以进行更深入的验证。

Agent 可以在内部审计、交叉验证与记录问题。**最终交付应呈现完成的成果，清除与结果无关的过程性脚手架。** 除非用户明确要求，不要创建独立的审计章节、审计报告、检查清单与验证总结。

例如，修订数学论文后，论文应呈现修改后的定义、定理和证明。临时审计笔记应清理。发现接口问题则直接更新接口说明；发现测试问题则直接修正测试。

提交说明与 PR 描述应概括主要变化、影响和必要验证结果。避免逐项记录 Agent 的工具调用与执行流水账。

**每句话都有意义，每个段落都有主题，每份文档都有职责，每个文件都有存在的理由。**
