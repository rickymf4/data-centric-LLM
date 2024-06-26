# RAG Survey
https://github.com/hymie122/RAG-Survey?spm=5176.28575916.0.0.2d186db7GyG2Xl

摘要：人工智能生成内容（AIGC）的发展得益于模型算法的进步、可扩展的基础模型架构以及大量高质量数据集的可用性。虽然AIGC已经取得了显著的表现，但它仍然面临着挑战，例如维护最新的长尾知识的困难、数据泄露的风险以及与训练和推理相关的高成本。最近，检索增强生成（RAG）作为一种解决这些挑战的方法而出现。特别是，RAG引入了信息检索过程，通过从可用的数据存储中检索相关对象来提高AIGC的结果，从而实现更高的准确性和鲁棒性。在本文中，我们全面综述了现有将RAG技术整合到AIGC场景中的努力。首先，我们将根据检索器如何增强生成器对RAG进行分类。我们提炼出各种检索器和生成器的增强方法的基本抽象。这种统一的观点涵盖了所有RAG场景，揭示了有助于潜在未来进展的进步和关键技术。我们还总结了额外的RAG增强方法，以促进有效的工程和实施RAG系统。然后，从另一个角度，我们调查了RAG在不同模态和任务上的实际应用，为研究人员和从业者提供了有价值的参考资料。此外，我们介绍了RAG基准测试，并讨论了当前RAG系统的局限性，并提出了未来研究的方向。项目代码库：https://github.com/hymie122/RAG-Survey

根据检索器如何增强生成器，我们将 RAG 基础范式分为四个不同的类别，如图 6 所示。
基于查询的 RAG：基于查询的 RAG 也称为提示增强。它直接在语言模型输入的初始阶段将用户查询与检索过程中获取的文档中的见解相结合。这种范式是在 RAG 应用程序中广泛采用的方法。一旦检索到文档，其内容就会与原始用户查询合并以创建复合输入序列。然后将此增强序列馈送到预训练的语言模型以生成响应。
[! https://github.com/hymie122/RAG-Survey/blob/main/RAG_Overview.jpg]


### D. 图像的 RAG
图像生成：RAG 通过引入一个信息检索系统来增强生成模型。对于图像生成，这意味着利用检索的数据来产生高保真度和逼真的图像，即使对于稀有或未见过的对象也是如此。同时，这种方法还可以减少生成模型的参数数量和计算成本。
RetrieveGAN [43] 使用可微分检索过程从其他图像中选择兼容的补丁作为生成的参考。它采用 Gumbel-softmax 技巧使检索过程可微分，从而实现端到端训练和嵌入函数优化。它还通过额外的目标函数来鼓励选择彼此兼容的补丁。RetrieveGAN 可以根据场景描述生成逼真且多样的图像，其中检索到的补丁合理且连贯。IC-GAN [137] 将数据分布建模为每个训练示例周围的条件分布混合。它在生成器和判别器上都施加了实例特征约束，这些特征由预训练的特征提取程序获得。它还将条件实例的最近邻用作判别器的正样本。IC-GAN 既适用于带标签的数据集也适用于不带标签的数据集，并且可以通过更改条件实例来转移到未见过的数据集。IC-GAN 还可以控制生成图像的语义和风格，方法是交换类标签或实例特征。然而，使用训练数据本身进行检索可能会限制其泛化能力。KNN扩散 [149] 使用大规模检索方法在没有任何文本数据的情况下训练一个基于扩散的模型。该模型以两个输入为条件：由CLIP提取的文本或图像嵌入，以及来自大型图像数据库中k个最近邻居的嵌入。k近邻嵌入有助于弥合文本和图像分布之间的差距，并通过简单地交换数据库来生成不同域中的图像。该模型还能够通过微调模型以预测从a操纵版本。RDM [150] 将一个小扩散或自回归模型与一个大型外部图像数据库结合起来，构成一个半参数化模型。在训练过程中，该模型为每个训练图像从数据库中检索一组最近邻，并根据它们的 CLIP 编码对生成模型进行条件设置。这样，模型就可以学习根据检索到的视觉内容来构建新的场景。在推理过程中，该模型可以通过更改数据库或检索策略来推广到新颖领域、任务和条件。Re-imagen [148] 从外部多模态知识库检索信息以产生逼真且忠实的图像，特别是对于罕见或未见过的实体。它基于一个级联扩散模型，其生成取决于文本提示和检索到的图像文本来进行条件设置。它还提出了一种交替分类器免费指导时间表来平衡文本和检索条件之间的对齐。Re-imagen 在 COCO 和 WikiImages 数据集上实现了最先进的性能，并显著提高了生成图像的新基准 EntityDrawBench 的保真度。X&Fuse [233] 是一种用于从文本生成图像时对视觉信息进行条件设置的一般方法。它通过在 U-Net 架构中的每个注意力块之前连接经过条件设置的图像和噪声图像，并通过自我注意机制使它们之间可以相互交互来实现这一点。Retrieve&Fuse 是 X&Fuse 的一个特例，其中根据文本或图像索引从大量图像库中检索出经条件设置的图像。X&Fuse 相较于替代方法具有几个优势，例如对空间差异的鲁棒性、没有信息损失等。RPG [77] 检索代表性图像以构造信息丰富的上下文示例（即图像区域对），并利用多模态连锁思维推理[234] 来规划复合文本到图像扩散的互补子区域。


# 𝗦𝘂𝗽𝗲𝗿 𝗡𝗘𝗪 𝗥𝗔𝗚 𝘁𝗲𝗰𝗵𝗻𝗶𝗾𝘂𝗲𝘀 𝘄𝗶𝘁𝗵 𝗣𝗿𝗮𝗰𝘁𝗶𝗰𝗮𝗹:- 20240406

## 1. 𝗖𝗵𝗮𝗶𝗻 𝗼𝗳 𝗡𝗼𝘁𝗲

Steps in CoN involve Generating notes for documents that have been retrieved, which result in a more factually correct answer and also because Notes are generated at steps that have been used to break the problem in the final step trustworthiness of the answer also increases.

Practical - https://lnkd.in/gpSzmrWu

## 2. 𝗖𝗼𝗿𝗿𝗲𝗰𝘁𝗶𝘃𝗲 𝗥𝗔𝗚

This RAG technique breaks the problem into a binary step if the retrieved answer is Ambiguous --> Then the query is passed to Search and then search results are taken and finally LLM is triggered again to look at the query keeping in mind both RAG document and Search results.

Practical - https://lnkd.in/g_MKJWsB

## 3. 𝗥𝗔𝗚 𝗙𝘂𝘀𝗶𝗼𝗻 

A Query is broken into small sub-queries in this approach. Then these queries are given to a vector DB to retrieve the most relevant documents for each query. Finally, using the Reciprocal rank fusion algorithm, the most relevant information is prioritized.
( In LlamaIndex When I used the combination of Recursive Retrieval and Semantic Chunking + Pinecone as VectorDB results came out best for our RAG application)
Practical:-
1. LangChain - https://lnkd.in/gCuJJm4t
2. LlamaIndex - https://lnkd.in/gtUBq3_J

## 4. 𝗘𝗺𝗼𝘁𝗶𝗼𝗻𝗣𝗿𝗼𝗺𝗽𝘁 

In this prompting technique researchers have shown how adding a few lines to the prompt can improve the performance of RAG.
Practical - https://lnkd.in/gimGJa_U

## 5. 𝗦𝗲𝗹𝗳-𝗥𝗔𝗚 

A self-rag technique where LLMs can do self-reflection for dynamic retrieval, critique, and generation.

Practical - https://lnkd.in/gWa6GFJB
Thanks, Roie Schwaber-Cohen for your awesome work at Pinecone blog and
I would also like to thank Pratik Bhavsar for his blog at 🔭 Galileo and Cobus Greyling


