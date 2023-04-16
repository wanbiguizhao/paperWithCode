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
#### MIM
采用BEiT的 blockwise masking strategy？一次性 Mask 掉相邻的多块 patch，这提高了重建任务的难度，
根据周围的图像和文字token，重新建立被掩盖的token。

###TODO
https://zhuanlan.zhihu.com/p/530902216
#### WPA 
预测预测文本对应的图片是否被mask掉了。
文本和对应的图片都没有被遮盖，才可以认为只对齐了。 
𝐶 × 𝐻 × 𝑊 = 3 × 224 × 224, 𝑃 = 16, 𝑀 = 196.  token的size是16*16,M表示图片token的长度。

### 模型实验
使用CogView替代attention的softmax计算分数。
### 视觉任务微调
LayoutLMV3作为backbone，FPN网络选取4，6，8，12层的输出为为铁证。
batch_size 32 ，60000步训练。
并没有使用数据增强。
参考了DIT
相对位置坐标？

