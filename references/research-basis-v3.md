# v3 设计依据与阅读边界

检索日期：2026-10-15。使用英语、中文、法语、日语、意大利语、德语、俄语原语言查询，读取大学/研究者教程及原始论文。这是有目的的小样本，不代表各语言社区共识，不是阅读效果的受控验证。以下指令为综合设计，不冒称来源已有同一套路由。

## 多语言教程

| 语言与已读来源 | 采用的思想 | 适用边界 |
|---|---|---|
| 英语：[Mitzenmacher，How to read a research paper](https://www.eecs.harvard.edu/~michaelm/postscripts/ReadPaper.pdf)，全文两页 | 一两句话说明具体问题与回答，再展开关键贡献 | 不是固定字数或效果证明 |
| 英语：[Keshav](https://svr-sk818-web.cl.cam.ac.uk/keshav/papers/07/paper-reading.pdf)，§2.1–2.3；[Harvard CS290](https://harvard-cs290-2024-25.github.io/readings/how-to-read-a-research-paper/)，Guiding Questions / Critique | 深度随目的改变，理论/实验证据按贡献选择，核查收益归因 | 不强制三遍或固定分钟数 |
| 中文：[沈向洋、华刚演讲的厦大镜像](https://csrc.xmu.edu.cn/index_cn/info/1062/1720.htm)，三个层次/十个问题 | 问题、输入输出、核心贡献、证据、自己的话与实现区分 | 一手演讲转载，原微信访问失败；非厦大独立验证，偏视觉/ML |
| 法语：[Grenoble Alpes 教程](https://inspe-sciedu.gricad-pages.univ-grenoble-alpes.fr/rech-educ/tuto-lire-article.html)，CCC/QAMRI；[ENS Lyon 数学研究访谈](https://jmeenslyon.wordpress.com/wp-content/uploads/2022/11/pratique_de_la_recherche-2.pdf)，§2 Lecture | 问题、结果、推断分开；应用定理、找工具、理解证明是不同任务 | 前者教育研究；后者九人访谈，描述不等于普遍规范 |
| 日语：[筑波金森，論文の読み方・書き方](https://kanamori.cs.tsukuba.ac.jp/docs/how_to_read_and_write_papers.html)，概要/方法/结果；[东大 Morihata](https://www.graco.c.u-tokyo.ac.jp/labs/morihata/research_memo.htm)，技术问题/着想 | 先解释为什么，忠实区分旧新步骤，证据随主张选；不强造单一巧思 | 图形学及作者实验室视角，非通用理论 |
| 意大利语：[Pegaso 讲义](https://video.unipegaso.it/Post/DiMartino/ArticoloScientifico/ArticoloScientifico.pdf)，pp.3–18；[Bologna 课程说明](https://www.unibo.it/it/studiare/insegnamenti-competenze-trasversali-moocs/insegnamenti/insegnamento/2019/445001) | 摘要应被全文校正，具体基线/指标/复做条件，识别文种 | 临床/运动科学背景，只迁移通用原则，不移植临床清单 |
| 德语：[TU Dresden 讲义](https://tu-dresden.de/ing/informatik/smt/cgv/ressourcen/dateien/materialien/howto-abschlussarbeit.pdf)，§5.3–6 | 带读者问题选章节，用自己的话和短句复述 | 毕业论文写作训练，不以声望判断内容 |
| 俄语：[ITMO 研究者访谈](https://news.itmo.ru/ru/education/trend/news/12497/) | 摘要初筛，公式/图与关键结果帮助回溯方法 | 简短大学访谈，不采纳统一文章结构或声望替代证据 |

查询示例：`how to read research paper contributions`、`如何阅读论文 公式`、`lire article mathématiques preuve`、`論文の読み方 新規性 手法`、`come leggere articolo scientifico università`、`wissenschaftliche Paper lesen Methode`、`как читать научные статьи университет`。未能读取的页面未用来支撑具体规则。

## 原始论文如何校正问题清单

| 论文与已读位置 | 设计启发及防错 |
|---|---|
| [Shampoo](https://proceedings.mlr.press/v80/gupta18a/gupta18a.pdf)，§1.1 / Algorithm 1 / Theorem 7 | ICML 也可数学主线；明确参数形状、两侧预条件状态和真正基线。m²+n² 对 m²n² 指预条件器存储，不能说比 Adam 更省 |
| [THC-CCSD](https://arxiv.org/pdf/2111.11473)，§II / Algorithms 4–7 / 结论 | 解释积分和双激发振幅两者的分解及收缩；Algorithm 6 的 O(N_THC N_aux³) 保留辅助秩条件，形式四次不等于所有规模实测更快；能力扩展不是新物理发现 |
| [TT 振动光谱](https://arxiv.org/pdf/1605.08422)，§III / Algorithms 1–3 / §V | 波函数表示、内层解、外层特征迭代、谱精度连起来；存储随键秩增长；摘要与正文不同配置不能混合 |
| [DFT-FE](https://arxiv.org/pdf/1903.10959)，§3.7 / Fig.9 / §4 | 有限元、物理精度、多层并行共同构成贡献；空间域与 band 映射不同，正交化/投影仍需跨组通信 |
| [2.5D MM/LU](https://people.eecs.berkeley.edu/~demmel/Demmel_pubs_07_11_final/C81_Solomonik_Demmel_25D_MM_LU_EuroPar11.pdf)，§3.1 / Algorithm 2 / §4 / §7 | 矩阵数学对象不决定主线；复制、分层、归约体现内存换通信。LU 面板依赖不可继承 MM 的全部延迟结论 |
| [pipelined CG 精度修复](https://arxiv.org/pdf/1601.07068)，§1–4 / Algorithm 4 | HPC 开场但创新是残差 gap 与误差修复，应数学主、并行辅；不能声称修复全部正交性/收敛问题 |

以上读取支持针对性设计，不表示逐页重证或运行复现。论文案例不是固定分类标签：用户问的内容与正文证据可以改变主辅顺序。

## 与 v2 的关系

保留证据、成本口径、数值误差与复现层次；将通用长检查表改为短入口和按需的三条主线。开头从固定多项概览改为具体创新解释，避免复现入口挤占核心。路由是提示词中的判断流程，不更改模型或 agent，不需要 embedding/分类器服务。

v2 的既有评估不能证明 v3 更优；v3 的行为抽查也不等于真人阅读效率提升。后续可用未参与设计的论文和真人限时任务，检查核心机制复述、更新重建、误差/性能边界判断；同时控制输出长度和读取材料。
