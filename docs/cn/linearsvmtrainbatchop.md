# 支持向量机算法

## 功能介绍
* 支持向量机是一个二分类算法
* 支持向量机组件支持稀疏、稠密两种数据格式
* 支持带样本权重的训练

## 参数说明

<!-- This is the start of auto-generated parameter info -->
<!-- DO NOT EDIT THIS PART!!! -->
| 名称 | 中文名称 | 描述 | 类型 | 是否必须？ | 默认值 |
| --- | --- | --- | --- | --- | --- |
| C | 惩罚项系数 | 支持向量机算法参数 | Double |  | 1.0 |
| optimMethod | 优化方法 | 优化问题求解时选择的优化方法 | String |  | null |
| withIntercept | 是否有常数项 | 是否有常数项，默认true | Boolean |  | true |
| maxIter | 最大迭代步数 | 最大迭代步数，默认为 100 | Integer |  | 100 |
| epsilon | 收敛阈值 | 迭代方法的终止判断阈值，默认值为 1.0e-6 | Double |  | 1.0E-6 |
| featureCols | 特征列名数组 | 特征列名数组，默认全选 | String[] |  | null |
| labelCol | 标签列名 | 输入表中的标签列名 | String | ✓ |  |
| weightCol | 权重列名 | 权重列对应的列名 | String |  | null |
| vectorCol | 向量列名 | 向量列对应的列名，默认值是null | String |  | null |
| standardization | 是否正则化 | 是否对训练数据做正则化，默认true | Boolean |  | true |<!-- This is the end of auto-generated parameter info -->



## 脚本示例
#### 运行脚本
```python
import numpy as np
import pandas as pd
data = np.array([
    [2, 1, 1],
    [3, 2, 1],
    [4, 3, 2],
    [2, 4, 1],
    [2, 2, 1],
    [4, 3, 2],
    [1, 2, 1],
    [5, 3, 2]])
df = pd.DataFrame({"f0": data[:, 0], 
                   "f1": data[:, 1],
                   "label": data[:, 2]})

input = dataframeToOperator(df, schemaStr='f0 int, f1 int, label int', op_type='batch')
dataTest = input
colnames = ["f0","f1"]
svm = LinearSvmTrainBatchOp().setFeatureCols(colnames).setLabelCol("label")
model = input.link(svm)

predictor = LinearSvmPredictBatchOp().setPredictionCol("pred")
predictor.linkFrom(model, dataTest).print()
```
#### 运行结果
f0 | f1 | label | pred 
---|----|-------|-----
2|1|1|1
3|2|1|1
4|3|2|2
2|4|1|1
2|2|1|1
4|3|2|2
1|2|1|1
5|3|2|2



## 备注

1. 该组件的输入为训练数据，输出为SVM模型。
2. 参数数据库的使用方式可以覆盖多个参数的使用方式。



