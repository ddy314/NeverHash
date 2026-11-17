# NeverHash

NeverHash 规范 AI Agent 如何组织仓库、撰写技术文档和提交修改。它希望一个第一次接触项目的读者，能够迅速理解项目的用途、当前成果和使用方式。

AI Agent 经常为一项简单任务生成多个说明文件、临时脚本和冗长的运行记录。这些内容会掩盖实际成果，也会让后续维护变得困难。NeverHash 要求每个文件承担明确的职责，让重要信息集中呈现，减少读者寻找答案的成本。

## What Changes

随着项目规模扩大，缺乏规范的仓库常在根目录堆积阶段性报告、临时脚本、版本号后缀目录与散乱测试：

~~~text
compiler/
├── README.md
├── project-overview.md
├── architecture-v2.md
├── audit-report.md
├── experiment-2026-11-17.py
├── run-output.txt
├── parser_new/
├── layout_final/
└── scripts/
    ├── smoke_test.sh
    └── check_hashes.py
~~~

应用 NeverHash 后，根目录保持精简，子系统按处理阶段与职责横向扩展，文档与测试同构对齐：

~~~text
compiler/
├── Cargo.toml
├── README.md
├── crates/
│   ├── compiler/
│   ├── compiler-cli/
│   ├── compiler-syntax/
│   ├── compiler-eval/
│   ├── compiler-layout/
│   └── compiler-pdf/
├── docs/
│   ├── dev/
│   │   └── architecture.md
│   └── reference/
├── tests/
│   ├── ref/
│   ├── src/
│   └── suite/
└── tools/
~~~

README 直接解释项目用途、核心能力与使用入口。子模块按职责边界平铺拆分，架构文档交代全局目录与数据流阶段，测试集按功能域组织。临时运行记录由开发过程管理，重复说明被整合或删除。

NeverHash 优先追求顺畅阅读与完整叙述，并明确采用 **流畅性 > 准确性** 的写作优先级。

## Usage

在支持 Agent Skills 的工具中安装：

~~~bash
npx skills add ddy314/NeverHash
~~~

也可以直接要求 Agent：

> Apply NeverHash to this repository. Make the README useful to a new reader, combine overlapping documentation, keep meaningful filenames, and submit the changes through a pull request.

[SKILL.md](SKILL.md) 给出了完整的规则、正反例以及 PR 提交流程。

## License

[MIT](LICENSE)
