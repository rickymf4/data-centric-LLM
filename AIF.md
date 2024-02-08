RLAIF已经不是新鲜事了，之前包括Anthropic，谷歌都推出过自己的「AI训AI」的技术


# Meta提出自奖励语言模型

https://mp.weixin.qq.com/s/0Hd3VsmPVMXWATytZQuOiQ

Self-Rewarding Language Models : https://arxiv.org/pdf/2401.10020.pdf

然后研究人员建立一个模型，让它同时拥有两种能力：

指令遵循：给出描述用户请求的提示，能够生成高质量、有帮助（且无害）的响应。

自指令创建：能够按照示例生成和评估新指令，再添加到自己的训练集中。

这两个能力可以为了使模型能够执行自我对齐，即它们是用于使用人工智能反馈（AIF）迭代训练自身的组件。

研究人员使用同一模型的LLM-as-a-Judge能力来评估其自己的候选响应，得分为 r∈ [0, 5]

迭代训练

研究人员的整个过程训练一系列模型。其中每个连续模型t使用由t − 1模型创建的增强训练数据。
因此，研究人员将AIFT(M)定义为使用模型M创建的AI反馈训练数据。
M：基础预训练LLM，没有微调。
M1：用M初始化，然后使用SFT对IFT+EFT种子数据进行微调。
M2：用M1初始化，然后使用DPO用AIFT(M1)数据进行训练。
M3：用M2初始化，然后使用DPO用AIFT(M2)数据进行训练。

https://github.com/lucidrains/self-rewarding-lm-pytorch/tree/main

