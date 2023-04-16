# LayoutLM-V2 (Document Foundation Model)
源代码复制:https://github.com/microsoft/unilm
## 基础知识
- 
## 代码运行环境


## 论文理解
## 摘要
使用了word-patch alignment objective 学习跨模态知识，预测文字对应的图片被遮盖。
### 论文贡献
1. 不使用cnn或者faster-rcnn 作为backbone提取特征减少模型参数和人工标注
2. 使用WPA实现模态对齐。

### 文本嵌入
使用了segment-level layout位置信息，表示那些单字共享语义。

### 图像嵌入
收到VIT和ViLT的影响，把图片切割成小的token，切割成pxp到校的patches。
使用1d相对坐标和2D位置坐标。

### 预训练的目的
#### MLM
采用span bert的泊松分布决定掩盖字数的机制。
在图像token和文字token的上下文下，可以预测被掩盖的内容。
#### MLM
采用BEiT的 blockwise masking strategy？一次性 Mask 掉相邻的多块 patch，这提高了重建任务的难度，
根据周围的图像和文字token，重新建立被掩盖的token。

###TODO
https://zhuanlan.zhihu.com/p/530902216