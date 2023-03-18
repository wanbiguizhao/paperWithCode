# LayoutLM (Document Foundation Model)
# LayoutLM (Document Foundation Model)
源代码复制:https://github.com/microsoft/unilm
## 运行环境准备

~~~bash
conda create -n layoutlm python=3.9
conda activate layoutlm
conda install pytorch==1.13.1 torchvision==0.14.1 torchaudio==0.13.1 pytorch-cuda=11.6 -c pytorch -c nvidia
conda install tensorboardX lxml transformers  -y
pip install seqeval
~~~