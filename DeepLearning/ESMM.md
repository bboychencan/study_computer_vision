# Entire Space Multi-task Model

2021-12-30
## 背景，主要是cvr预估，里面有几个问题
- Sample Selection Bias (SSB)问题，转化是在点击之后才有可能发生的动作，传统cvr模型通常以点击数据做训练集，
其中点击未转化为负例，点击并转化为正例。但是训练好的模型实际使用时，对整个空间的样本预估，而非只对点击样本
预估，即训练数据与实际预测的数据来自不同分布，这个偏差对模型的泛化能力构成了挑战。
- Data Sparsity （DS）问题，作为cvr训练数据的点击样本远小于ctr预估训练使用的曝光样本

对于上面的问题，有些缓和策略。但未实质解决这个问题
- 从曝光集中对unclicked的样本抽样做为负样本缓解SSB
- 对转化样本过采样缓解DS

点击 -》 转化，本身就是强相关的连续行为，作者希望在模型结构中显示考虑这种“行为链关系”，从而在整个空间上
进行训练预测。这里同时涉及到ctr与cvr两个任务，因此使用多任务学习MTL是自然的选择。

## Model
点击ctr，转化cvr，点击然后转化ctcvr，是三个不同的任务。
- pCTCVR   对于曝光样本x，点击且发生转化的预测概率
- pCTR     对于曝光样本x，预测点击发生的概率
- pCVR     对于假设曝光样本x且假设已点击，预测发生转化的概率
其中pCTR和 pCTCVR都是可以用全部样本空间来训练的，pCVR传统的方法是使用点击样本集，但是如果
同时计算出pCTCVR 和 pCTR 然后相除，就可以得到pCVR。等于先学习前面两个任务，隐式地学习cvr

