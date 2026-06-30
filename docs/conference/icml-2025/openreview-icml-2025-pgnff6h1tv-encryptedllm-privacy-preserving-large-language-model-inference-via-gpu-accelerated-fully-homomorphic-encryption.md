---
title: "EncryptedLLM: Privacy-Preserving Large Language Model Inference via GPU-Accelerated Fully Homomorphic Encryption"
title_zh: "EncryptedLLM: 基于GPU加速的全同态加密实现隐私保护大语言模型推理"
authors: "Leo de Castro, Daniel Escudero, Adya Agrawal, Antigoni Polychroniadou, Manuela Veloso"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=PGNff6H1TV"
tags: ["query:priv-sec"]
score: 10.0
evidence: 提出GPU加速的全同态加密保护大语言模型推理查询免遭云端泄露。
tldr: 为解决LLM推理外包至云端的隐私泄露风险，本文提出GPU加速的全同态加密实现，允许对加密查询直接进行模型计算。基准测试表明加密GPT-2前向传递速度比纯CPU基线快200多倍，初步达到实用水平，为在不可信云环境中安全部署大模型推理铺平道路。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: LLM推理外包至第三方云带来客户端查询隐私泄露风险，全同态加密是自然方案但计算开销巨大。
method: 实现GPU加速的全同态加密，并应用于加密GPT-2模型的端到端前向计算。
result: 加密推理速度相比CPU基线提升200倍以上，展示了实际应用的可行性。
conclusion: 为LLM的隐私保护推理提供了高效解决方案，推动了全同态加密在真实场景中的应用。
---

## Abstract
As large language models (LLMs) become more powerful, the computation required to run these models is increasingly outsourced to a third-party cloud. While this saves clients' computation, it risks leaking the clients' LLM queries to the cloud provider. Fully homomorphic encryption (FHE) presents a natural solution to this problem: simply encrypt the query and evaluate the LLM homomorphically on the cloud machine. The result remains encrypted and can only be learned by the client who holds the secret key. In this work, we present a GPU-accelerated implementation of FHE and use this implementation to benchmark an encrypted GPT-2 forward pass, with runtimes over $200\times$ faster than the CPU baseline. We also present novel and extensive experimental analysis of approximations of LLM activation functions to maintain accuracy while achieving this performance.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：随着大语言模型（LLM）能力增强，模型推理计算越来越多地外包给第三方云平台。此举虽节省客户端算力，却使客户查询（query）面临泄露给云提供商的风险。
- **整体含义**：该论文旨在利用全同态加密（FHE）技术解决 LLM 隐私推理问题，让云端直接对加密查询进行模型计算，结果依然保持加密状态，只有持有私钥的客户端才能解密。这为不可信云环境中的安全 LLM 部署提供了一种端到端隐私保护方案。
- **动机**：FHE 是实现隐私保护推理的自然路线，但此前因巨大的计算开销而难以实用，尤其在深层网络（如 GPT-2 级别）上前向计算极慢。本文试图通过 GPU 加速与激活函数近似，大幅降低延迟，使加密 LLM 推理初步接近实用水平。

## 2. 论文提出的方法论

- **整体思路**：设计并实现一个 GPU 加速的全同态加密库，并将其应用于加密的 GPT-2 前向传播过程。云端接收加密后的输入 token 序列，在不解密的条件下执行模型计算，最后输出加密的 logits。
- **关键技术细节**：
  - **GPU 加速的 FHE 实现**：将 FHE 中的核心操作（如多项式乘法、自举、密钥切换等）映射到 GPU 上进行并行计算，针对 LLM 推理的计算图进行优化。
  - **激活函数的近似处理**：由于 FHE 仅原生支持多项式和加性操作，而 Transformer 中的 GELU、Softmax 等非线性函数必须用低次多项式近似。本文提出新颖且广泛的实验分析，探究不同近似策略对最终模型精度的影响，以在精度和计算效率之间取得平衡。
  - **端到端加密推理流程**：客户端将查询加密发送至云端 → 云端加载加密权重（或由客户端加密发送）→ 执行密文域前向计算（包括注意力机制、前馈网络等层的 FHE 实现）→ 返回加密结果 → 客户端解密得到预测。
- **公式/算法流程**（文字描述）：
  - 加密：$c = \text{Enc}(pk, x)$，其中 $x$ 为输入 token 序列，$pk$ 为公钥。
  - 密文计算：$\hat{y} = \text{Eval}(c, \text{EncryptedModel})$，其中 $\text{Eval}$ 为基于 FHE 的电路求值，对应 GPT-2 的各层操作（线性层通过多项式计算实现，激活函数通过近似多项式实现）。
  - 解密：$y = \text{Dec}(sk, \hat{y})$，客户端用私钥 $sk$ 获得明文输出。

## 3. 实验设计

- **模型与场景**：以 GPT-2 模型的端到端前向传播作为评测对象，模拟 LLM 推理外包场景。
- **基准对比**：
  - 纯 CPU 实现的 FHE 推理（作为基线），对比本文 GPU 加速实现的速度提升。
  - 激活函数近似带来的精度变化（可能对比不惜代价的高精度近似或明文模型的精度）。
- **评价指标**：主要关注推理延迟（运行时），兼考虑激活函数近似对模型准确率的影响。
- **数据集说明**：摘要及元数据未明确提及使用的具体数据集（如用于评估精度损失的评测集）。仅指出对加密 GPT-2 前向传递进行基准测试，可能使用随机或标准推理样本，但未披露细节。

## 4. 资源与算力

- **算力使用**：文中明确提到“GPU-accelerated implementation”和“比 CPU 基线快 200 倍以上”，但摘要和元数据**未提供所用 GPU 的具体型号、数量、运行时长**等细节。因此无法从现有信息中精确总结合理卡、时长或总成本。
- **指出缺失**：需要查阅完整论文获取关于 GPU 配置（如 NVIDIA A100/H100、显存、并行策略）、加密参数规模及基准测试时长的具体数据。

## 5. 实验数量与充分性

- **估计实验量**：摘要提及主要进行加密 GPT-2 前向传递的基准测试，并“对 LLM 激活函数近似进行了新颖且广泛的实验分析”。由此推测至少包含：
  - 不同激活函数近似方法的对比（组数未知）。
  - 加密推理速度对比（GPU vs. CPU）。
  - 精度与速度的权衡实验。
- **充分性与公平性**：
  - 定性描述为“广泛的”，说明实验有一定规模。
  - 作为会议论文（ICML 2025 已接收），通常须满足一定的实验充分性和可比性要求。但本文摘要未提供具体的实验表格、消融变量或统计检验，故无法外部评估是否客观公平。
  - **局限**：未披露数据集、不同模型规模、不同 FHE 方案等的消融。

## 6. 论文的主要结论与发现

- **速度大幅提升**：通过 GPU 加速，加密 GPT-2 前向传播的运行时间相比纯 CPU 基线提升超过 **200 倍**，使 FHE 推理初步达到实用水平。
- **精度可保持**：通过精心设计的激活函数近似方法，可以在实现上述加速的同时，维持模型的输出准确率。
- **可行路径**：该工作证明全同态加密在真实 LLM（如 GPT-2）上的隐私保护推理是可行的，并为在不可信云环境中安全部署大型模型铺平道路。

## 7. 优点

- **系统级贡献**：首次展示 GPU 加速的全同态加密应用于完整 GPT-2 前向传播，将理论方案推向工程实用。
- **性能突破**：200 倍以上的加速比极具说服力，显著缩小了 FHE 与明文推理的差距。
- **激活函数近似研究**：对 LLM 中非线性函数近似进行深入实验分析，为该方向的后续研究提供了实践指导。
- **问题聚焦**：紧扣当前 LLM 部署中最急迫的隐私痛点，方案直接且通用。

## 8. 不足与局限

- **算力与细节缺失**：摘要未说明 GPU 型号、算力消耗、推理单次延迟的绝对值，难以评估其真实部署成本和吞吐量。
- **模型单一**：仅测试了 GPT-2，未扩展到更大或更新的模型（如 LLaMA、GPT-3 等），通用性有待验证。
- **数据集与精度评估不详**：未给出激活函数近似后的具体精度指标（如困惑度、下游任务得分），无法判断性能损失是否在应用可接受范围内。
- **仅覆盖推理**：未涉及加密训练或微调，应用场景限定于仅推理。
- **安全模型与参数未说明**：摘要没有提及 FHE 方案的具体参数、安全等级、密钥规模和噪声管理，这些对实际安全强度判断至关重要。
- **比较对象有限**：仅与 CPU 基线比较，未与其他隐私推理技术（如安全多方计算、可信执行环境）进行综合权衡分析。

（完）
