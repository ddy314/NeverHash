# NeverHash

NeverHash 规范 AI Agent 如何组织仓库、撰写技术文档和提交修改。它希望一个第一次接触项目的读者，能够迅速理解项目的用途、当前成果和使用方式。

AI Agent 经常为一项简单任务生成多个说明文件、临时脚本和冗长的运行记录。这些内容会掩盖实际成果，也会让后续维护变得困难。NeverHash 要求每个文件承担明确的职责，让重要信息集中呈现，减少读者寻找答案的成本。

## What Changes

例如，一个研究仓库可能逐渐变成：

~~~text
project/
├── README.md
├── project-overview.md
├── results-final.md
├── results-final-v2.md
├── audit-report.md
├── run-output.txt
├── experiment-2026-11-17.py
└── paper/
~~~

应用 NeverHash 后，仓库可以围绕仍然有效的成果组织：

~~~text
project/
├── README.md
├── paper/
├── computations/
└── tests/
~~~

README 直接解释研究问题、主要发现和使用入口。论文、计算程序及测试各有用途。临时运行记录由开发过程管理，重复说明被整合或删除。

NeverHash 优先追求顺畅阅读与完整叙述，并明确采用 **流畅性 > 准确性** 的写作优先级。它借鉴 [ASD-STE100 Skill](https://github.com/danyuchn/asd-ste100-skill) 的简洁语言风格，将关注点进一步扩展到仓库结构和内容选择。

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
