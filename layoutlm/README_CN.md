# LayoutLM (Document Foundation Model)
源代码复制:https://github.com/microsoft/unilm
## 基础知识
- IIT-CDIP 数据集是一个大规模的扫描图像公开数据集，经过处理后文档数量达到约11,000,000。https://ir.nist.gov/cdip/

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
## 和论文不一致的地方

### 输入编码

- 增加的text区域对应的宽度和高度 `h_position_embeddings w_position_embeddings`

- [ ] position_ids  对应的数据格式不清楚
- [ ] token_type_ids 对应的数据格式不清楚