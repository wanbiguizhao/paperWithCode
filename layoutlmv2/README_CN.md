# LayoutLM-V2 (Document Foundation Model)
源代码复制:https://github.com/microsoft/unilm
## 基础知识
- VrDU 富文本文档理解
## 代码运行环境


## 论文理解
### 论文贡献
- 提出一个整合文本，布局和视觉信息的多模态Transformer模型。把空间自注意力机制整合到模型建构中？这一步是否有效，未知，因为代码中并没有开启这个配置？一个输入序列是512，抛除特殊字符，理论上是可以看到上下左右的字符的。但是这种注意力能否和语义关联起来？
- MVLM 抹掉token，然后预测token？TIA text-image alignment TIM text-image matching 实现文档和图片align（对齐）我个人文档和图片对齐这个太大的，这个图片有若干部分被替换例如70%，然后cls变成一个回归任务，对齐上，会不会更好一些？

### 文本嵌入
格式:[cls][T1][..][T9][SEP][T10][...][T23][SEP][PAD][PAD] 
三部分组成：
- TOKEN对应的向量编码
- 1D位置的编码
- 不能的文本块[SEG]对应的编码
segment embedding is used to distinguish different text segments。 text segments 应该是和OCR做文字切割时相关。
### 图像嵌入
1. resize 224x224
2. 放入到backbone中，输出WH的feature map
3. 展平后，通过一次线性映射，映射后的维度和文字的token的维度一样
4. 位置编码：1D编码是类似于1，2，3，4的编码,值域[0,WH]
5. segment编码固定的值[C]用来编辑这部分是文字编码。
### 布局编码
对于boxPAD的bbox为=(0,0,0,0,0,0)
i-th (0 ≤ i < W H + L) 的i表示文本和图像token之后的下标记，
在注意力中，原来只是关注i作为token的输入，现在还引入了j-i以及j和i的bbox,x,y坐标的相对距离。