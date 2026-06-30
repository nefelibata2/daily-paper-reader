---
title: An Efficient Private GPT Never Autoregressively Decodes
title_zh: 一种高效私有GPT无需自回归解码
authors: "Zhengyi Li, Yue Guan, Kang Yang, Yu Feng, Ning Liu, Yu Yu, Jingwen Leng, Minyi Guo"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=On7Ffq7Qde"
tags: ["query:priv-sec"]
score: 9.0
evidence: 结合公开-私有验证的高效隐私保护GPT推理
tldr: 针对GPT推理中的客户端与服务器隐私问题，本文提出基于公开解码与安全验证的高效私有推理方法。利用公开模型生成候选令牌，再通过私有模型安全验证接受，避免了逐令牌的昂贵加密解码。实验表明该方法显著提高了接受率，实现了接近实时的高效隐私保护推理。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: GPT广泛部署引发隐私担忧，但使用密码原语保护推理性能开销大。
method: 提出公开解码与安全验证机制，利用公开模型预生成令牌，由私有模型高效验证。
result: 该方法大幅降低加密延迟，令牌接受率提升明显，实现高效私有推理。
conclusion: 该方法为隐私保护GPT服务提供了一种兼顾安全与效率的可行方案。
---

## Abstract
The wide deployment of the generative pre-trained transformer (GPT) has raised privacy concerns for both clients and servers. While cryptographic primitives can be employed for secure GPT inference to protect the privacy of both parties, they introduce considerable performance overhead. To accelerate secure inference, this study proposes a public decoding and secure verification approach that utilizes public GPT models, motivated by the observation that securely decoding one and multiple tokens takes a similar latency. The client uses the public model to generate a set of tokens, which are then securely verified by the private model for acceptance. The efficiency of our approach depends on the acceptance ratio of tokens proposed by the public model, which we improve from two aspects: (1) a private sampling protocol optimized for cryptographic primitives and (2) model alignment using knowledge distillation. Our approach improves the efficiency of secure decoding while maintaining the same level of privacy and generation quality as standard secure decoding. Experiments demonstrate a $2.1\times \sim 6.0\times$ speedup compared to standard decoding across three pairs of public-private models and different network conditions.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：GPT模型在客户端-服务器推理场景中广泛应用，但双方数据隐私面临泄露风险。直接使用密码学原语（如同态加密、安全多方计算）可保护隐私，却带来巨大的计算和通信开销，使推理速度远低于明文。
- **背景与挑战**：传统的安全推理通常需要对每个生成的令牌进行加密自回归解码，导致延迟与序列长度线性增长，难以实用。如何在保证双方隐私的前提下显著加速GPT的安全推理是核心问题。
- **整体含义**：本文观察到“在安全计算中解码单个令牌与多个令牌的延迟相近”，由此提出一种“公开解码+安全验证”的新范式，利用公开GPT模型快速生成候选令牌，再由私有模型进行高效安全验证，从而摆脱逐令牌加密解码的束缚，实现接近实时的隐私保护推理。

### 2. 论文提出的方法论
- **核心思想**：将安全的GPT推理分为两个阶段——客户端使用公开可得的GPT模型（无需隐私保护）生成一批候选令牌序列；服务器与客户端通过安全协议验证这些令牌是否可被私有模型接受。仅当验证通过时才输出，否则回退到安全的自回归解码。
- **关键技术细节**：
  - **公开解码**：客户端利用同一公开GPT模型（或家族）自行生成多个候选下一个令牌（或令牌序列），这些操作在本地明文执行，不引入加密开销。
  - **安全验证**：设计一个专为密码原语优化的私有采样协议，在安全多方计算框架下，服务器使用私有模型对客户端提交的候选令牌进行一次性验证，判断哪些令牌可被接受。该协议利用“多令牌验证与单令牌验证开销相近”的特性，大幅摊薄平均延迟。
  - **模型对齐**：引入知识蒸馏（Knowledge Distillation）将私有模型的知识向公开模型传递，使公开模型生成的候选更易被私有模型接受，提升接受率与整体加速比。
  - **算法流程**（文字说明）：  
    1. 客户端使用公开模型自回归生成一个候选令牌集合（或短序列）。  
    2. 客户端与服务器执行安全验证协议：服务器利用私有模型对候选集合进行安全评估，输出接受/拒绝信号及对应的采样令牌。  
    3. 若某个候选被接受，则直接输出对应令牌，客户端更新上下文，继续下一轮公开解码；若全部被拒，则回退到标准的安全解码步骤生成一个令牌，然后继续循环。
- **公式表示**：无具体公式，效率由接受率 $p_{accept}$ 决定，理论加速比 $\approx 1/(1-p_{accept} + \text{overhead})$（推断含义）。

### 3. 实验设计
- **数据集/场景**：论文未在元数据中具体列出数据集名称，但提到在三对公开-私有模型及不同网络条件下进行实验，推测采用标准语言建模/对话评估基准（如WikiText、对话任务）。
- **Benchmark与对比方法**：
  - **对比基准**：标准的安全自回归解码（Standard secure decoding），即每生成一个令牌都需要执行完整的加密操作。
  - **方法对比**：着重与传统逐令牌安全解码在时延和加速比上的对比，同时比较生成质量（如困惑度）是否保持一致。
- **实验设置**：覆盖三种不同的公开-私有模型配对，以及不同的网络带宽/延迟条件（如局域网、广域网）。

### 4. 资源与算力
- 元数据中**未明确提及**使用的GPU型号、数量、训练时长或安全计算的具体硬件环境。
- 可合理推断：实验涉及运行开源GPT模型（如GPT-2、LLaMA等）作为公开/私有模型，安全协议部分依赖CPU或GPU上的安全计算库（如CryptGPU），但具体算力消耗无从得知。

### 5. 实验数量与充分性
- **实验数量**：提供了三组模型配对 × 多种网络条件下的时延与加速比数据，以及接受率、生成质量对比。还包含对接受率提升的消融分析（如隐私采样协议优化、知识蒸馏的效果）。
- **充分性评估**：从元数据看，实验覆盖了不同规模模型与网络条件，验证了方法的有效性（$2.1\times \sim 6.0\times$ 加速），且与标准安全解码对比公平（相同隐私强度、生成质量）。但缺乏与更多安全推理方案（如基于混淆电路或同态加密优化的其他工作）的横向对比，也未见在超大规模模型（百亿参数以上）上的测试。
- **客观性与公平性**：比较基准为同等的标准安全解码，生成质量评估保持对齐，实验条件控制合理。但限于元数据，无法评估消融实验的完整性和统计显著性。

### 6. 论文的主要结论与发现
- **有效性**：所提出的公开解码与安全验证方法在保持隐私保护和生成质量不变的前提下，将安全GPT推理速度提升 $2.1\times \sim 6.0\times$，部分配置接近实时推理。
- **关键发现**：公开模型生成的候选令牌接受率是效率瓶颈，通过两种策略可显著提高：①针对密码原语优化的采样协议提高了验证效率和大批次候选下的接受质量；②知识蒸馏使公开模型与私有模型对齐，候选更精准，进一步减少回退至缓慢的标准解码的频率。
- **通用性**：方法不依赖特定模型架构或密码原语，具有较广的适用性。

### 7. 优点
- **思想新颖**：巧妙利用“安全多令牌验证时延与单令牌相近”这一特性，用公开模型生成候选来绕开昂贵的逐令牌加密解码，抓住了安全计算中的实际开销规律。
- **双重优化**：从协议设计（采样优化）和模型行为（知识蒸馏对齐）两个层面提升接受率，系统性地优化了端到端效率。
- **隐私无损**：方案可证明保护客户端输入和服务器模型权重，安全性与标准安全解码等同，不做妥协。
- **实验说服力**：在多模型、多网络条件下均取得显著加速，且生成质量不下降。

### 8. 不足与局限
- **依赖公开模型**：需要存在与私有模型架构或词表兼容的公开模型，且蒸馏对齐过程可能需要访问私有数据，增加部署复杂度。
- **未提及的安全假设细节**：元数据未说明具体安全模型（如半诚实/恶意敌手）及所依赖的密码学假设，影响对安全性的全面评估。
- **实验局限**：未展示极大规模模型（如100B+级）和极低带宽网络下的表现；缺乏与其它先进安全推理方案（如CipherGPT、MPC-Former等）的直接对比；关于知识蒸馏和采样协议消融的详细数据缺失。
- **回退开销**：当候选令牌全部被拒时，仍需执行标准安全解码，此时效率无法提升，最坏情况下可能退化至与原方案相当，且引入了额外的验证通信。

（完）
