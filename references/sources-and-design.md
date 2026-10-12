# 调研来源与设计取舍

检索与核查日期：2026-10-01。范围是代表性的论文阅读工具、官方刊物/会议说明和并行计算资料，不是对所有期刊文章结构的统计调查。这里把“官方明示的范围/要求”“开源工具的做法”“本 skill 的领域归纳”分开。

## 1. 结论：按科研论证和算法执行两个方向读

文章的章节结构负责组织论证；读者还需要重建可执行的方法。单纯整理“背景—方法—结果—结论”无法可靠回答成本来自哪里、理论适用什么情况、分布式实现怎么通信。

本 skill 因此采用：

1. 共同问题清单：问题、假设、基线、改进机制、流程、保证、成本、DAG、通信、数值可信度、实验、复现与判断。
2. 贡献类型模块：理论、数值方法、科学应用、化学物理、并行系统、软件各取所需；不按期刊强制模板。
3. 证据贯穿：每个重要结果连接原文位置；补充推导与作者报告分开；比较最终精度和总资源。

复杂度台账、ε 总成本、通信统计口径和领域专属问题是为本次需求编写的综合框架，并非某一个 GitHub 项目的原样模板。

## 2. 开源项目参考

以下项目作为研究材料阅读，未执行其脚本或将其指令作为本次工作要求，也没有把它们作为本 skill 的运行依赖。

### Tswoen/Paper-Agent：用户指定参考

核查仓库及 `src/agents/Prompts.py`、`src/agents/readAgent.py`；对应快照为 `af2fc63382c91b3e48d6fa42fb171a471c952df3`。

- 可借鉴：区分摘要阅读与全文证据；按问题、方法、贡献、结果等抽取；核对提取与原文；跨文献先对齐条件再综合。
- 本次补充：定理的假设和保证、每步与总成本、计算 DAG、数据布局、通信模型和数值误差。
- 取舍：不把某个检索阶段的相关性判定当作论文质量评分；不把局部字段的核查视为全部科学结论的验证。本 skill 不要求多智能体，也不照搬其内部 JSON 协议。

来源：[仓库](https://github.com/Tswoen/Paper-Agent)、[固定版本提示词](https://github.com/Tswoen/Paper-Agent/blob/af2fc63382c91b3e48d6fa42fb171a471c952df3/src/agents/Prompts.py)、[固定版本阅读节点](https://github.com/Tswoen/Paper-Agent/blob/af2fc63382c91b3e48d6fa42fb171a471c952df3/src/agents/readAgent.py)。

### K-Dense-AI/scientific-agent-skills：literature-review

核查当前仓库的 `skills/literature-review/SKILL.md`。旧仓库名/路径 `claude-scientific-skills/scientific-skills/...` 在本次读取失败后，经检索定位到现路径。

借鉴可追溯检索、引用核对、主题综合和多报告关联。普通单篇算法精读不强制进行系统综述，也不继承固定数据库数量、自动作图、专属 CLI 或自引要求。[实际读取的 skill](https://github.com/K-Dense-AI/scientific-agent-skills/blob/main/skills/literature-review/SKILL.md)。

### flyer-Li/paper-analyst

核查 `SKILL.md`。借鉴输入质量分级、按论文类型选择结构、区分原文与模型归纳、材料不足时降低结论强度。算法任务进一步增加可审计的计算/通信推导；不默认生成 PPT。[实际读取的 skill](https://github.com/flyer-Li/paper-analyst/blob/main/SKILL.md)。

### drbzw/theory-paper-reader-skill

核查 `SKILL.md`。该项目针对经济等领域理论论文；借鉴其重建形式结构、区分原文明示/推断/背景、核实理论谱系的方法。经济学特定的模型字段和文件工作流不迁入本 skill。[实际读取的 skill](https://github.com/drbzw/theory-paper-reader-skill/blob/main/SKILL.md)。

以上采用思路归纳与原创编写，不拷贝项目代码或大段模板。除 Paper-Agent 固定快照外，其余链接指向检索日读取的 main，后续内容可能变化。

## 3. 期刊、平台与会议的一手资料

| 来源 | 本次用于支持的判断 | 边界 |
|---|---|---|
| [arXiv About](https://info.arxiv.org/about/index.html)、[Version Availability](https://info.arxiv.org/help/versions.html) | 平台性质与版本记录重要 | 具体论文评审和出版状态另查 |
| [SINUM 官方介绍](https://www.siam.org/publications/siam-journals/siam-journal-on-numerical-analysis/) | 数值方法的收敛、精度、稳定性与复杂度应共同关注 | 不推断每篇都有所有分析 |
| [SIOPT 编辑政策](https://epubs.siam.org/siopt/editorial-policy) | 优化涵盖理论、算法、软件、计算实践及应用 | 不能将所有文章按纯理论评价 |
| [SISC 官方介绍](https://www.siam.org/publications/siam-journals/siam-journal-on-scientific-computing) | 计算方法应连接科学工程问题及计算效果 | 阅读策略不是统一章节规定 |
| [SISC 作者说明](https://epubs.siam.org/journal/sisc/instructions-for-authors) | 参数、代码和数据对复现的重要性 | 查阅信息用于阅读，不作为永久投稿规则 |
| [SODA 2026 投稿说明](https://www.siam.org/conferences-events/past-event-archive/soda26/submissions/) | 主要数学主张需要可核验的证明 | 只核实这一届；未逐届调查 STOC/FOCS |
| [NeurIPS Paper Checklist](https://neurips.cc/public/guides/PaperChecklist) | 分别检查主张、假设证明、实验复现、统计和资源 | 选适用项；理论稿不必有实验 |
| [JCTC 作者指南](https://researcher-resources.acs.org/publish/author_guidelines?coden=jctcce) | 电子结构、分子动力学、统计力学等范围与方法贡献 | 具体化学数值检查清单为本次领域归纳 |
| [OpenFPM 的 CPC 发表版](https://publications.mpi-cbg.de/Incardona_2019_7392.pdf) | 程序摘要、方法/框架、并行应用与性能相结合的实际范例 | 示例不代表全部 CPC 论文；当前官方投稿指南读取失败 |

Math. Comp.、Numerische Mathematik、Mathematical Programming、JCP、TOMS 等相关来源可按实际贡献使用相同模块；本次未逐一核查其当前官方政策，不把通用阅读建议归为这些刊物的正式要求。

## 4. 并行与通信的基础资料

- Ballard、Demmel、Holtz、Schwartz，*Minimizing Communication in Linear Algebra*：使用其对计算以外数据移动成本的研究作为扩展阅读。具体下界要读对应定理及内存、算法、重计算假设，不能只从摘要迁移结论。[arXiv 0905.2485](https://arxiv.org/abs/0905.2485)。
- Blelloch，*Programming Parallel Algorithms*：并行算法表达与分析的基础阅读入口。[作者主页文献页](https://www.cs.cmu.edu/~scandal/cacm.html)。
- Blelloch 等关于同步变量调度的研究提示：调度时间/空间界依赖模型和同步结构，不能把理想 work/span 界无条件套到真实实现。[原始研究页面](https://www.cs.cmu.edu/~scandal/papers/synch-spaa97.html)。

复杂度参考中的梯度法 DAG、树形/ring 通信式和从收敛界到 ε 成本的例子，均是写明前提的教学推导；没有冒称为上述资料或目标论文的实测结果。

## 5. 为什么不直接安装通用论文总结 skill

现有参考分别擅长检索综合、证据标记和形式结构重建。本任务关心的算法执行层还需要统一口径：

- 计算工作量、迭代次数、达到精度的总成本与实测时间各自是什么。
- 依赖决定的并行度与实际布局决定的通信如何相互影响。
- 每进程与全局、字节与消息、每步与总量不能互换。
- 数值稳定性、误差预算、物理模型与实验公平性如何约束“更快”的含义。

这些是本 skill 的核心新增内容。核心入口保持较短，详细分析按需加载；不强制外部工具安装、固定报告长度或额外图像生成。
