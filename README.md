# CMS-bjmu

### Health data science · Reproducible clinical prediction

This profile highlights a secondary analysis of the **PIC pediatric intensive care dataset**. The study asks how much early mortality prediction depends on bedside measurements, laboratory tests, and their combination.

## Featured project · PIC 患儿院内死亡预测

**研究问题：** 患儿入院后前 24 小时的床旁生命体征与实验室检查分别提供多少院内死亡预测信息？联合使用是否带来稳定的增量收益？

| 研究环节 | 本项目做法 |
| --- | --- |
| 数据与结局 | PIC 前 24 小时派生数据；结局为院内死亡 |
| 研究样本 | 13,258 次入院、12,690 名患儿；独立测试集 2,669 次入院，其中 157 次死亡 |
| 数据划分 | 按患儿编号隔离开发集与测试集，避免重复入院跨集合 |
| 特征与模型 | 开发集内处理缺失并进行极端随机树排序；固定年龄、性别及 9 项测量，比较三类信息来源的逻辑回归模型 |
| 稳健性分析 | 使用相同特征清单建立 XGBoost 模型；开展缺失阈值、首次入院、负年龄处理、类别权重及记录可获得性分析 |

### 独立测试集结果

| 信息来源 | 逻辑回归 AUROC / AUPRC | XGBoost AUROC / AUPRC |
| --- | ---: | ---: |
| 床旁生命体征 | 0.622 / 0.110 | 0.736 / 0.130 |
| 实验室检查 | 0.721 / 0.213 | 0.738 / 0.213 |
| 两类信息结合 | 0.713 / 0.192 | 0.781 / 0.229 |

两种算法均显示联合模型优于仅使用床旁数据的模型。联合模型与实验室模型的排序因算法而异：逻辑回归中实验室模型的点估计较高，XGBoost 中联合模型的 AUROC 较高。因此，信息增量的结论具有**算法敏感性**，不能概括为与模型无关。模型表现用于评价预测价值，不代表因果效应。

![三组模型的入模测量特征重要性排序](https://pic-information-sources-2026.robust-heron-5196.chatgpt.site/feature_importance.png)

**Explore:** [交互式研究网页](https://pic-information-sources-2026.robust-heron-5196.chatgpt.site/) · [主分析代码](https://pic-information-sources-2026.robust-heron-5196.chatgpt.site/analysis.py) · [XGBoost 代码](https://pic-information-sources-2026.robust-heron-5196.chatgpt.site/xgboost_robustness.py)

### 数据与学术归属

本项目是对 PIC 前 24 小时派生数据的二次分析。数据与基础代码来自 [hsd1503/PIC_mortality](https://github.com/hsd1503/PIC_mortality)；研究背景可参见 [Hong 等发表于 *Health Data Science* 的论文](https://doi.org/10.34133/2021/9365125)和 [PIC 数据库论文](https://doi.org/10.1038/s41597-020-0355-4)。项目字典、测量单位及模型外部适用性仍需进一步核查。

---

<sub>Public profile content contains aggregate results and figures only; no patient-level records are included.</sub>
