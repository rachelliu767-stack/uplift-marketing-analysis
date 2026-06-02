# 电商营销干预效果优化：Uplift 增量模型分析

## 项目背景

在电商、外卖、本地生活等业务中，优惠券、满减、买一送一等营销干预很常见。但传统做法如果只按照“购买概率”或“流失风险”筛选用户，可能会把优惠券发给本来就会购买的用户，造成营销成本浪费。

本项目基于公开电商营销实验数据，模拟优惠券干预场景，使用 Uplift Model 分析营销干预的增量效果，尝试识别“因为营销干预才会转化”的用户群体。

## 分析目标

- 评估营销干预对整体转化率的平均影响。
- 构建用户特征，训练 Two-Model Uplift 模型。
- 使用 Qini 曲线评估模型对增量用户的排序能力。
- 对比随机触达、流失概率、转化概率和 Uplift 策略。
- 基于业务假设进行 ROI 离线模拟测算。
- 总结 Two-Model 方法在该数据集上的效果局限和优化方向。

## 数据说明

数据集：Hillstrom Marketing Dataset

数据规模：64,000 条用户营销实验记录，9 个原始字段。

主要字段：

- `recency`：最近一次购买间隔
- `history`：历史消费金额
- `used_discount`：是否使用过折扣
- `used_bogo`：是否使用过买一送一
- `zip_code`：地区类型
- `channel`：购买渠道
- `offer`：营销干预类型，包括 Discount、Buy One Get One、No Offer
- `conversion`：是否转化

## 技术栈

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Random Forest
- Two-Model Uplift
- Qini 曲线
- ROI 离线模拟

## 项目流程

1. 数据加载与探索性分析
2. 缺失值检查与目标变量分布分析
3. 干预组与对照组转化率对比
4. 特征工程
5. 训练集/测试集划分
6. Two-Model Uplift 建模
7. Qini 曲线评估
8. 策略对比分析
9. ROI 离线模拟测算
10. 用户分群与运营建议

## 核心结果

- 整体转化率约为 14.68%。
- 干预组相比对照组的平均处理效应（ATE）约为 6.09 个百分点，说明营销干预在平均层面有效。
- Treatment 模型 AUC 约为 0.65，Control 模型 AUC 约为 0.71，整体预测 AUC 约为 0.62。
- Qini 评估结果显示 Two-Model 在该数据集上的增量排序效果有限。
- ROI 离线测算显示，在当前业务假设下，各策略收益表现不理想，说明优惠券成本、毛利率和目标人群选择会显著影响营销收益。

## 业务结论

营销干预平均有效，并不代表所有用户都值得触达。Uplift 分析的价值在于帮助业务方从“谁可能购买”转向“营销是否真正改变了用户行为”。

本项目中 Two-Model 方法完整跑通了增量建模流程，但模型排序效果一般。因此更适合作为 Uplift 分析流程和评估方法的学习项目，而不是一个已经证明线上收益显著提升的成功案例。

## 优化方向

- 尝试 Single-Model / Class Transformation 方法。
- 尝试 Causal Forest、X-Learner、T-Learner 等因果推断模型。
- 增加更多用户行为特征，如购买频次、品类偏好、最近访问、生命周期阶段。
- 在真实业务中通过小流量 A/B 测试验证模型排序效果。
- 使用真实优惠券成本、毛利率、订单利润等业务参数重新评估 ROI。

## 项目文件

```text
uplift-marketing-analysis/
├─ README.md
├─ requirements.txt
├─ data/
│  └─ data.csv
├─ notebooks/
│  └─ uplift_marketing_analysis.ipynb
└─ docs/
   └─ interview_cheatsheet.md
```




