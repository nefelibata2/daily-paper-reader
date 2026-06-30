---
title: "CryptoMoE: Privacy-Preserving and Scalable Mixture of Experts Inference via Balanced Expert Routing"
title_zh: CryptoMoE：基于均衡专家路由的隐私保护可扩展混合专家推理
authors: "Yifan Zhou, Tianshi Xu, Jue Hong, Ye Wu, Meng Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=8pEqukyGrj"
tags: ["query:priv-sec"]
score: 10.0
evidence: 通过加密负载均衡实现MoE大模型的隐私保护推理
tldr: 现有加密大模型推理仅支持稠密结构，无法扩展到混合专家（MoE）架构，因为动态路由可能泄露输入隐私。本文提出CryptoMoE，首个支持MoE模型的隐私保护推理框架。通过平衡专家负载隐藏路由信息，并设计新颖的安全分派与组合协议，在保护隐私的同时保证了推理效率与精度。实验表明，CryptoMoE在多个MoE模型上取得了与明文推理相近的准确率，为大规模隐私保护AI服务提供了可行路径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有加密推理不支持MoE架构，动态路由会泄露敏感输入，急需隐私保护的MoE推理方案。
method: 提出CryptoMoE，通过平衡专家负载保护路由信息，并设计安全分派与组合协议。
result: 在MoE模型上实现了隐私保护推理，准确率接近明文，且具有可扩展性。
conclusion: CryptoMoE填补了MoE隐私推理的空白，为大规模模型的安全部署奠定了基础。
---

## Abstract
Private large language model (LLM) inference based on cryptographic primitives offers a promising path towards privacy-preserving deep learning. However, existing frameworks only support dense LLMs like LLaMA-1 and struggle to scale to mixture-of-experts (MoE) architectures. The key challenge comes from securely evaluating the dynamic routing mechanism in MoE layers, which may reveal sensitive input information if not fully protected. In this paper, we propose CryptoMoE, the first framework that enables private, efficient, and accurate inference for MoE-based models. CryptoMoE balances expert loads to protect expert routing information and proposes novel protocols for secure expert dispatch and combine. CryptoMoE also develops a confidence-aware token selection strategy and a batch matrix multiplication protocol to improve accuracy and efficiency further. Extensive experiments on DeepSeekMoE-16.4B, OLMoE-6.9B, and QWenMoE-14.3B show that CryptoMoE achieves $2.8\sim3.5\times$ end-to-end latency reduction and $3\sim6\times$ communication reduction over a dense baseline with minimum accuracy loss. We also adapt CipherPrune (ICLR'25) for MoE inference and demonstrate CryptoMoE can reduce the communication by up to $4.3 \times$.

---

## 论文详细总结（自动生成）

# CryptoMoE 论文总结

## 1. 论文的核心问题与整体含义

- **核心问题**：现有基于加密原语的大型语言模型（LLM）隐私保护推理方案仅支持稠密结构（如 LLaMA‑1），无法扩展到混合专家（Mixture‑of‑Experts, MoE）架构。MoE 层中的动态路由机制会揭示输入的相关信息，若不加保护，会直接泄露用户隐私。
- **整体含义**：本文提出首个面向 MoE 模型的隐私保护推理框架 CryptoMoE，解决“在保护路由信息的前提下，实现高效、高精度 MoE 推理”这一空白，为大规模隐私保护 AI 服务铺平道路。

## 2. 论文提出的方法论

- **核心思想**：通过**平衡专家负载**来隐藏专家路由信息，同时围绕负载均衡设计安全分派（dispatch）与组合（combine）协议，在不泄露路由细节的条件下完成 MoE 层的密文计算。
- **关键技术细节**：
  - **负载均衡路由**：使不同专家接收的 token 数量趋于均衡，避免路由分布泄露原始输入特性。
  - **安全分派与组合协议**：设计新颖的加密协议，在密文域实现 token 到专家的分派以及专家输出组合。
  - **置信度感知的 token 选择策略**：根据置信度自动筛选需要计算的 token，提升效率并减少噪音。
  - **批量矩阵乘法协议**：优化密文下的矩阵运算吞吐，进一步降低计算与通信开销。
- **流程概览**（文字描述）：
  1. 输入 token 经过加密后传入 MoE 层；
  2. 在加密状态下执行负载均衡路由，生成隐藏路由信息的“均衡”调度；
  3. 依调度将 token 安全地分派到各专家（本地或远程计算）；
  4. 专家输出在密文下组合，并利用批量矩阵乘法加速；
  5. 仅最终结果解密给用户。

## 3. 实验设计

- **模型与数据集**（来自摘要与元数据）：
  - 模型：DeepSeekMoE‑16.4B、OLMoE‑6.9B、QWenMoE‑14.3B。
  - Benchmark/场景：隐私保护推理效率与准确度对比，与稠密基线、CipherPrune（ICLR’25）等方法的比较。
- **对比方法**：
  - 稠密（非 MoE）隐私推理基线，代表现有仅支持稠密模型的方案。
  - CipherPrune（ICLR’25）适配到 MoE 推理的方案，用于衡量通信压缩效果。

## 4. 资源与算力

- **论文原文未提供所需算力的具体说明**。摘要与元数据均未提及 GPU 型号、数量或训练/推理时长。仅给出了端到端延迟和通信量的相对提升倍数，不涉及硬件环境细节。

## 5. 实验数量与充分性

- **实验组数**（从已有信息推断）：至少包含 3 个不同规模（6.9B～16.4B）的 MoE 模型，与稠密基线、CipherPrune 的横向比较；评估指标涵盖端到端延迟、通信量、准确率损失等。
- **充分性与公平性**：
  - 从结果指标（延迟降低 2.8∼3.5×，通信降低 3∼6×，准确率损失最小）看，实验设计具有合理的覆盖度和对比度。
  - 但未提及消融实验细节，难以判断是否对负载均衡策略、token 选择、矩阵乘法等模块单独评估，因此暂时无法断言是否**完全充分**。
  - 对比对象选择了当前最相关的稠密隐私推理和压缩方法，比较**基本公平**。

## 6. 论文的主要结论与发现

- CryptoMoE 首次在 MoE 架构上实现了高效的隐私保护推理，填补了领域空白。
- 通过平衡专家负载，可以在不泄漏路由信息的前提下，取得与明文推理相近的准确率。
- 与稠密隐私推理基线相比，端到端延迟降低 2.8∼3.5 倍，通信量降低 3∼6 倍。
- 结合 CipherPrune 对 MoE 的适配，通信压缩可进一步提升至 4.3 倍，展现出良好的可扩展性和实用性。

## 7. 优点

- **首创性**：第一个专门解决 MoE 模型隐私推理的工作，问题定义清晰。
- **方法设计全面**：从路由保护到分派组合协议，再到 token 选择和批量运算优化，形成系统性的技术方案。
- **验证广泛**：在多个不同规模的 MoE 模型上进行评估，结果有说服力。
- **实用导向**：准确率损失小，延迟和通信降低显著，对真实场景的部署有直接价值。

## 8. 不足与局限

- **算力信息缺失**：全文可能未给出推理所需的硬件配置和具体算力开销，难以评估实际部署成本和资源门槛。
- **实验透明度受限**：仅从摘要和元数据无法看到消融实验、敏感性分析、不同安全参数的影响等细节，难以判断方法的鲁棒性边界。
- **应用限制**：方法依赖于负载均衡假设；若输入本身分布极端，可能影响隐藏效果或路由均衡程度。未讨论在极端负载不均或对抗性输入下的表现。
- **对比有限**：目前只见于两个基线（稠密隐私推理、CipherPrune），与更多可能的 MoE 推理优化方案（如非加密的负载均衡策略）的直接比较未知。

（完）
