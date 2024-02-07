
# 用GPT-4合成数据来训练AI模型，实现SOTA！

https://mp.weixin.qq.com/s/Dzkg-GBYiekQknhF_Q6lgQ

RAG是未来LLMs应用的重要趋势之一。

论文标题:
Improving Text Embeddings with Large Language Models
论文链接:
https://arxiv.org/pdf/2401.00368.pdf
模型:
https://huggingface.co/intfloat/e5-mistral-7b-instruct
数据：
https://huggingface.co/datasets/andersonbcdefg/synthetic_retrieval_tasks

作者使用GPT-4集思广益产生一系列潜在的检索任务，然后为每个任务生成(查询,正例,困难反例)三元组。

这篇工作证明了通过LLMs技术，文本嵌入的质量可以得到显著提升。研究人员使用了专有的LLMs（如GPT-4），在多种语言环境下生成了多样化的合成数据，并结合Mistral模型强大的语言理解能力，在竞争激烈的MTEB基准测试中取得了SOTA。与现有的多阶段方法相比，既简单又高效，不再需要中间预训练的环节。
用网友的话说就是“Amazing Amazing Amazing!”，省去了人工采集数据的繁琐步骤，每个人都可以轻松地生成自己的数据集，并训练强大的嵌入模型。语义检索模型不给力导致生成模型性能受影响的局面，总算有希望翻篇儿了！
