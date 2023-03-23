# LayoutLM-V2 (Document Foundation Model)
源代码复制:https://github.com/microsoft/unilm
## 基础知识
- VrDU 复文本文档理解
## 代码运行环境


## 论文理解
### 论文贡献
- 提出一个整合文本，布局和视觉信息的多模态Transformer模型。把空间自注意力机制整合到模型建构中？这一步是否有效，未知，因为代码中并没有开启这个配置？一个输入序列是512，抛除特殊字符，理论上是可以看到上下左右的字符的。但是这种注意力能否和语义关联起来？