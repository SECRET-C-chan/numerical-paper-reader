# SAGA 单篇论文解读对照：无 skill 与 v3 skill

实验日期：2026-10-15。论文为 Defazio、Bach、Lacoste-Julien 的 [SAGA，arXiv:1407.0202v3](https://arxiv.org/abs/1407.0202v3)，15 页，主题是有限和优化；不属于 PWDFT、DGDFT、ISDF、CDFCI 相关工作。

## 完整报告

- [不加载 skill 的完整解读](baseline.md)
- [加载 numerical-paper-reader v3 的完整解读](with-skill.md)

两份报告均为对应 subagent 本轮生成的完整 Markdown 原稿，主代理没有润色、删节、纠错或选取较好的重试。它们是实验输出，不是经过独立同行评审的教程；公式与结论仍应对照论文检查。

报告长度与 SHA-256 见 [results.json](results.json)。按文件中的汉字统计，无 skill 组约 2,500 字，skill 组约 2,340 字；另有公式、数字及英文，不能将此统计直接当成阅读时间。两组均自报读取第 1–15 页并检查部分 PDF 原页；skill 组加载入口及四份参考。

## 共同条件与唯一预设差异

| 项目 | 设置 |
|---|---|
| 模型请求 | 两组均为 `gpt-6-sol`，推理强度 `high` |
| 上下文 | 两个独立 subagent，`fork_turns=none`，不继承本对话历史 |
| 论文材料 | 同一份 PDF 与带页码的全文提取文本；输入哈希见 experiment.json |
| 公共任务 | 同一份 [common-prompt.txt](common-prompt.txt)，自行安排完整中文解读 |
| 篇幅 | 相同软目标：正文 2500–4000 中文字，允许必要公式、表格与伪代码 |
| 外部信息 | 任务禁止联网、旧报告、旧 benchmark、其他代理输出和其他论文 |
| 无 skill 组 | 指令禁止加载任何 skill 正文或参考文件 |
| skill 组 | 使用冻结的 numerical-paper-reader v3，按需读取其参考文件 |
| 生成次数 | 每组一次，没有 best-of 筛选、修订重跑或种子控制 |
| 实验执行 | 只解读论文，没有运行 SAGA 或复现论文图表 |

skill 对应仓库提交 [6e1d8b1](https://github.com/SECRET-C-chan/numerical-paper-reader/tree/6e1d8b1c8a722540229ee501362fa62b1b2e616f)；快照各文件哈希记录在 [experiment.json](experiment.json)。

两组分组指令的实质差异仅是 skill 正文/参考的加载许可，另有各自输出路径。它们都读取相同公共任务和论文。加载了哪些参考、实际读到哪些位置、是否检查 PDF，见 [baseline-run.json](baseline-run.json) 与 [with-skill-run.json](with-skill-run.json)。这些是代理自报记录，不是独立的工具调用安全审计。

## 如何理解这次实验

这次选择论文是便利取样，并非随机抽样。SAGA 曾出现在早期 v1/v2 的语料中，但本轮代理没有获得那些解读或分数；此次是新的 v3 单篇生成。

“无 skill”准确地说是**不加载 skill 正文与参考**。subagent 仍共享宿主的基础规则、工具定义、可用技能目录元数据和预训练知识；文件可见性没有被单独操作系统沙箱隔离。因此不能把它描述成完全无系统影响的裸模型。相同材料也不保证两个代理实际读取的章节、展开篇幅完全相同，参考加载本身会增加 skill 组的上下文。

单篇、单次输出只能展示一个具体案例，不能证明平均质量、真人阅读速度或科研复现成功率提高。本次不额外打模型裁判分数；可直接并排阅读两份完整报告，关注能否重述核心创新、还原关键更新、识别存储/成本及适用边界。

论文 PDF、全文提取文本、私有聊天和底层执行日志不在公开目录中。重做时可从上述原文链接取得材料；抽取器和格式差异可能改变文本，所以输入哈希用于标识本轮材料，不承诺跨环境逐字复现。
