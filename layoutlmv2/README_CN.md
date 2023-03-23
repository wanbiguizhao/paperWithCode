# LayoutLM-V2 (Document Foundation Model)
源代码复制:https://github.com/microsoft/unilm
## 基础知识
- VrDU 复文本文档理解
## 代码运行环境


## 论文理解
### 论文贡献
- 提出一个整合文本，布局和视觉信息的多模态Transformer模型。把空间自注意力机制整合到模型建构中？这一步是否有效，未知，因为代码中并没有开启这个配置？一个输入序列是512，抛除特殊字符，理论上是可以看到上下左右的字符的。但是这种注意力能否和语义关联起来？
- MVLM 抹掉token，然后预测token？TIA text-image alignment TIM text-image matching 实现文档和图片align（对齐）我个人文档和图片对齐这个太大的，这个图片有若干部分被替换例如70%，然后cls变成一个回归任务，对齐上，会不会更好一些？