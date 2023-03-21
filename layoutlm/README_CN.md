# LayoutLM (Document Foundation Model)
源代码复制:https://github.com/microsoft/unilm
## 基础知识
- IIT-CDIP 数据集是一个大规模的扫描图像公开数据集，经过处理后文档数量达到约11,000,000。
  - https://ir.nist.gov/cdip/ 
  - https://paperswithcode.com/dataset/rvl-cdip
- Robert 比原有的bert数据量更大，参数调优更精细化
- 数据预处理部分：对原来的页面进行了缩放，调整为1000x1000的页面
- 

## 运行环境准备

~~~bash
conda create -n layoutlm python=3.9
conda activate layoutlm
conda install pytorch==1.13.1 torchvision==0.14.1 torchaudio==0.13.1 pytorch-cuda=11.6 -c pytorch -c nvidia
conda install tensorboardX lxml transformers  -y
pip install seqeval
~~~
## 代码更新
- `layoutlm/deprecated/layoutlm/modeling/layoutlm.py` 使用troch自带的LayerNorm
- `layoutlm/deprecated/examples/classification/run_classification.py` 使用pytroch的tensorboard
## 和论文不一致的地方

### 输入编码

- 增加的text区域对应的宽度和高度 `h_position_embeddings w_position_embeddings`

- [ ] position_ids  对应的数据格式不清楚,应该是为了保留bert的position信息，实际情况使用的是bbox的坐标信息
- [ ] token_type_ids 对应的数据格式不清楚,似乎是用来区分填充的数据还是非填充的数据。对应的segment——id，用来做NSP？存疑

## 论文中的预训练
### Task1 MVLM任务
训练的时候，把文字遮盖掉，但是保留bbox的坐标信息，然后标签用来预测被遮盖掉的内容。
### Task2 MDC分类
这块儿，没有从代码中读到哪里是预测的特征，
### 训练配置和时间
- 8块32GBV100 ，整体的batch是80，平均一块10个size
- base模型，80个小时一个epoch，价格，平均租用一块V100是2.8元/小时，训练一个epoch的价格是:2.8*8*80 大概是1792，不一定能保证一次训练成功，五次训练成功的话，大概租用GPU的价格就要1w元。太贵了。
- large模型，170个小时一个epoch 
## 模型的缺点
预训练的时候，只是使用了模型的坐标，没有使用图像的信息，图像的信息是在下游任务的时候，结合fast rcnn提取的特征，再用神经网络进行判定的。