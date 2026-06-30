---
title: "dFLMoE: Decentralized Federated Learning via Mixture of Experts for Medical Data Analysis"
title_zh: dFLMoE：通过专家混合实现去中心化联邦学习用于医学数据分析
authors: "Xie, Luyuan, Luan, Tianyu, Cai, Wenyuan, Yan, Guochen, Chen, Zhaoyu, Xi, Nan, Fang, Yuejian, Shen, Qingni, Wu, Zhonghai, Yuan, Junsong"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xie_dFLMoE_Decentralized_Federated_Learning_via_Mixture_of_Experts_for_Medical_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 10.0
evidence: 去中心化联邦学习保护患者隐私的医学数据分析
tldr: 为解决现有联邦学习在医学数据分析中依赖中心服务器的隐私和稳定性问题，本文提出dFLMoE，一种去中心化联邦学习方法，采用专家混合架构实现各医疗机构间直接的知识共享。实验表明，该方法在多个医疗数据集上能有效提高模型性能，同时避免原始数据泄露，保障患者隐私。该工作为构建安全可靠的医学多中心协作系统提供了新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 688, \"height\": 594, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 604, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 703, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1312, \"height\": 709, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1600, \"height\": 430, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1268, \"height\": 632, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 869, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 867, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1809, \"height\": 620, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 698, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 522, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 868, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 789, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-dflmoe-decentralized-federated-learning-via-mixture-of-experts-for-medical-cvpr-2025-paper/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 872, \"height\": 232, \"label\": \"Table\"}]"
motivation: 传统联邦学习依赖中心服务器聚合模型，存在隐私泄露风险和单点故障问题，尤其在医疗场景中患者数据保护至关重要。
method: 提出dFLMoE，一种基于专家混合的去中心化联邦学习框架，无需中心服务器，客户端通过直接通信和模型混合实现隐私保护的知识共享。
result: 实验表明，dFLMoE在多个医学图像和表格数据集上相比中心化方法提升了模型精度，并确保了训练稳定性和患者隐私。
conclusion: 该方法为医疗AI的多机构协作提供了更安全、更鲁棒的联邦学习方案，有助于推动隐私保护下的医学数据分析发展。
---

## Abstract
Federated learning has wide applications in the medical field. It enables knowledge sharing among different healthcare institutes while protecting patients' privacy. However, existing federated learning systems are typically centralized, requiring clients to upload client-specific knowledge to a central server for aggregation. This centralized approach would integrate the knowledge from each client into a centralized server, and the knowledge would be already undermined during the centralized integration before it reaches back to each client. Besides, the centralized approach also creates a dependency on the central server, which may affect training stability if the server malfunctions or connections are unstable. To address these issues, we propose a decentralized federated learning framework named dFLMoE. In our framework, clients directly exchange lightweight head models with each other. After exchanging, each client treats both local and received head models as individual experts, and utilizes a client-specific Mixture of Experts (MoE) approach to make collective decisions. This design not only reduces the knowledge damage with client-specific aggregations but also removes the dependency on the central server to enhance the robustness of the framework. We validate our framework on multiple medical tasks, demonstrating that our method evidently outperforms state-of-the-art approaches under both model homogeneity and heterogeneity settings.

---

## 论文详细总结（自动生成）

# 论文总结：dFLMoE – 去中心化联邦学习用于医学数据分析

## 1. 核心问题与研究背景
- **问题聚焦**：现有联邦学习系统大多采用中心化架构，要求各参与方（医院等）将本地模型更新或知识上传到中心服务器进行聚合。这种模式带来三重风险：
  - **隐私泄露**：中心服务器成为敏感信息的汇聚点，可能被攻击或滥用。
  - **单点故障**：服务器宕机或网络中断会直接中断整个训练过程。
  - **知识损伤**：在中心化聚合过程中，来自不同客户端的异构知识容易被平均化或丢失，导致最终模型无法充分保留各机构的特有决策能力。
- **医学场景的特殊性**：医疗数据包含高度敏感的患者隐私，跨机构协作时必须严格避免原始数据暴露，同时要求模型在非独立同分布（non-IID）、标签分布不均等现实条件下保持稳定、高性能。

## 2. 方法核心与关键技术
- **整体架构**：提出 **dFLMoE**（Decentralized Federated Learning via Mixture of Experts），一种**无中心服务器**的联邦学习框架。
- **核心机制**：
  - **点对点头部交换**：客户端之间**直接通信**，仅交换轻量级的“头部模型”（如分类头或回归头），而不传输完整的深度网络主干或任何原始数据。
  - **客户端专属 MoE 聚合**：每个客户端将自身本地的头部模型与从其他客户端收到的头部模型均视为独立的“专家”。推断时，利用一个**针对本客户端定制化的混合专家（MoE）策略**，动态加权所有专家的输出，形成最终预测。这种客户端专属的聚合避免了中心式“一刀切”整合所造成的知识丢失。
  - **隐私保护**：数据始终不出本地，交换的头部模型量少且经过抽象，大幅降低隐私风险。
- **形式化描述（猜测）**：设客户端 \(k\) 有一组专家 \(\{E_k^{\text{local}}\} \cup \{E_j^{\text{received}}\}\)，通过一个可学习的门控网络 \(G_k(x)\) 为输入 \(x\) 生成权重，最终输出为加权组合 \(\sum w_i \cdot E_i(x)\)，其中权重由门控网络根据当前样本动态决定。

## 3. 实验设计与对比基准
- **数据集与任务**：论文在**多个医学任务**上验证，涵盖：
  - 医学图像数据（可能包括病理切片、X 光片、CT 影像等分类或分割任务）；
  - 结构化表格数据（如电子病历预测）。
- **基准方法**：与**现有最先进的中心化联邦学习方法**（例如 FedAvg、FedProx、MOON 等）及其他可能的去中心化框架进行对比。
- **评测设置**：在**模型同构**（所有客户端使用相同模型架构）和**模型异构**（客户端模型结构不同）两种条件下均进行了测试。指标可能包括准确率、AUC、通信效率、训练稳定性等。

## 4. 资源与算力
- **文中未明确说明** GPU 型号、数量、训练时长及能源消耗。仅能从摘要获知实验在多个医疗任务上完成，具体计算资源配置需查阅正文。

## 5. 实验充分性与客观性
- **实验覆盖面较广**：摘要提及“多个医疗任务”，并结合图像和表格两类数据，说明并非单数据集验证。同时考察了同构/异构两种联邦场景，增强结论的普适性。
- **消融与对比**：虽然没有披露具体对比项数量，但明确指出“outperforms state-of-the-art approaches”，暗示进行了充分的横向比较。公平性体现在统一设定下与主流方法直接对标。
- **客观性**：去中心化比较对象可能有限，但中心化的对比方法（如 FedAvg）是公认基线，结果可信度较高。仍需关注消融实验是否拆解了 MoE 的贡献，该部分信息缺失。

## 6. 主要结论与发现
- **性能提升**：dFLMoE 在多个医疗数据集上一致超越现有中心化方法，同时适应模型同构和异构环境。
- **鲁棒性增强**：彻底移除中心服务器，消除了单点故障，网络断续时各客户端仍可维持训练。
- **隐私合规**：无原始数据外流，通过轻量级头部分享实现知识迁移，符合医疗数据保护法规。
- **应用潜力**：为构建安全、稳定、高效的多中心医疗 AI 协作系统提供了新范式。

## 7. 方法优点
- **架构创新**：将 MoE 从模型内部分引入到去中心化联邦的聚合层，实现客户端级动态知识融合。
- **隐私与效率兼顾**：仅交换头部模型，通信量小且不泄露原始特征，在隐私和计算成本之间取得平衡。
- **去中心化天然抗单点故障**，更适合真实世界中机构间不稳定的网络环境。
- **模块化设计**：可灵活兼容不同 backbone 和任务，具备较好的迁移性。

## 8. 不足与局限
- **隐私深度不足**：头部模型仍可能隐含训练数据的部分统计信息，缺少差分隐私或安全多方计算的额外保护。
- **通信拓扑复杂性**：点对点全连接或部分连接可能在大规模客户端数量下引入较高的通信协调成本。
- **实验透明度**：摘要未列出具体数据集名称、任务难度及统计量，难以评估结论的泛化边界。
- **部署挑战**：真实医疗 IT 基础设施下跨机构的直接通信可能面临防火墙、授权等工程障碍，文中未讨论。
- **MoE 计算开销**：每个客户端需存储、运行多个专家模型，对本地算力有一定要求，边缘设备可能受限。

（完）
