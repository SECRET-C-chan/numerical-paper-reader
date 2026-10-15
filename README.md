# numerical-paper-reader

面向计算数学、优化、计算物理与并行/分布式计算论文的 Codex skill。先点明具体创新，再依据摘要和正文中的贡献证据选择阅读主线，按需解释数学对象、公式与算法、成本、物理意义或分块/调度/通信。

An evidence-oriented paper-reading skill for numerical mathematics, optimization, and scientific computing. Chinese instructions; responses follow the user's language.

## 关注什么

- 问题、输入输出、假设与适用边界。
- 算法状态、关键更新、一轮流程、终止条件，以及相对基线究竟改了哪一步。
- 数学结构、证明条件、误差与数值稳定性。
- 每步和总计算量、存储、达到目标精度的成本。
- 计算图、work/span、同步、数据布局、通信轮数和数据量。
- 实验公平性、最小验证，以及从原型到论文实验的复现缺口。

覆盖 arXiv、数学期刊、算法会议、JCTC、CPC 等来源；按论文贡献选择模块，不把期刊标签当成分析结论。

## 安装与使用

将本仓库放到 Codex 的个人 skill 目录下，目录名为 `numerical-paper-reader`，确保其下直接包含 `SKILL.md`、`agents/` 和 `references/`。常见路径是 `~/.codex/skills/numerical-paper-reader`；自定义环境请使用自己的 skill 目录。重新开启会话后显式调用：

```text
$numerical-paper-reader 精读这篇论文：[论文链接或本地文件]。
先让我快速理解问题、核心算法和相对基线的改进，再分析复杂度、计算图、分布式通信及最小复现方案。
```

也可以把完整目录交给其他能读取文件的 agent，要求先读 `SKILL.md` 并按需读取参考文件。只复制入口文本会丢失详细分析模块。此项目是阅读指令与参考材料，不包含论文下载器或自动执行实验的程序。

## 文件结构

入口为 [SKILL.md](SKILL.md)，详细模块位于 [references/](references/)。[设计与参考来源](references/sources-and-design.md)记录了 Paper-Agent 等公开项目、期刊资料和方法文献带来的启发；未复制这些项目的实现代码。

## 评估与边界

当前文件为修订版 v3：新增基于贡献证据的主辅线判断，以及数学、物理、并行三个独立提示模块；不按 arXiv 分区或期刊强制分类。设计参考了七种语言的阅读教程及跨领域原始论文，详见 [v3 依据](references/research-basis-v3.md)。六篇设计内论文与摘要场景的行为抽查不构成效果对照试验。

历史受控评估针对 v1/v2：20 篇论文的无 skill / v1 配对解读，以及 10 篇留出论文的 v1 / v2 比较。它支持更完整的成本、并行性和复现准备分析，但**不能证明真实读者理解更快，或完整实验复现成功率更高，也不能将其分数归给 v3**。

见 [评估摘要](benchmark/README.md)和[评分标准](benchmark/rubric.json)。模型仍可能误读符号、实验数值和实现条件；研究结论须回到原文核查。

## 贡献与许可

欢迎通过 issue 提供论文定位、当前解读、错误原因和建议修订。改进应优先修复可验证的理解缺口，避免增加无用栏目或强制篇幅。

本仓库原创内容使用 [MIT License](LICENSE)。所链接论文与第三方项目仍受各自许可及版权约束。
