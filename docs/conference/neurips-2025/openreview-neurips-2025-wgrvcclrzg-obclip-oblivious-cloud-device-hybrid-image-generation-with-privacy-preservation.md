---
title: "ObCLIP: Oblivious CLoud-Device Hybrid Image Generation with Privacy Preservation"
title_zh: ObCLIP：具有隐私保护的不经意云端-设备混合图像生成
authors: "Haoqi Wu, Wei Dai, Ming Xu, Wang Li, Qiang Yan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=WgrVccLRzG"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过提示混淆实现隐私保护图像生成
tldr: 针对扩散模型云推理中用户提示可能泄露敏感信息的问题，本文提出ObCLIP，一种即插即用的保护机制。它通过将输入提示转换为语义相似但敏感属性不同的候选提示，实现不经意云端-设备混合生成。实验验证了其在保护隐私的同时保持生成质量的有效性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 扩散模型云端推理存在提示泄露敏感信息的风险。
method: 提出ObCLIP，将提示转换为语义相似但属性不同的候选集。
result: 在多个数据集上平衡了隐私保护和图像生成效果。
conclusion: ObCLIP为生成模型隐私保护提供了实用方案。
---

## Abstract
Diffusion Models have gained significant popularity due to their remarkable capabilities in image generation, albeit at the cost of intensive computation requirement. Meanwhile, despite their widespread deployment in inference services such as Midjourney, concerns about the potential leakage of sensitive information in uploaded user prompts have arisen. Existing solutions either fail to strike an effective balance between utility and efficiency, or lack rigorous privacy guarantees. 

To bridge this gap, we propose ObCLIP, a plug-and-play safeguard that enables oblivious cloud-device hybrid generation scheme.
By oblivious, each input prompt is transformed into a set of semantically similar candidate prompts that differ only in sensitive attributes (e.g., gender, ethnicity). The cloud server processes all candidate prompts without knowing which one is the real one, thus preventing any prompt leakage. To mitigate server cost, only a small portion of denoising steps is performed upon the large cloud model. The resulting intermediate latents are then transmitted back to the device, which selects the targeted latent and completes the remaining denoising using a small local model to obtain the final image. Additionally, we analyze and incorporate several cache-based accelerations that leverage temporal and batch redundancy, effectively reducing computation cost with minimal utility degradation. Extensive experiments across multiple datasets demonstrate that ObCLIP provides rigorous privacy and comparable utility to large cloud models with slightly increased server computation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **问题背景**：扩散模型（Diffusion Models）在图像生成领域表现突出，但云端推理服务（如 Midjourney）部署时，用户上传的文本提示（prompt）可能包含敏感隐私信息（如性别、种族等），存在泄露风险。
- **现有方法不足**：已有方案无法在生成质量（utility）、计算效率与严格隐私保障之间取得有效平衡。
- **研究动机**：提出一种即插即用（plug-and-play）的保护机制，实现**不经意的云端-设备混合生成**，既能防止提示信息在云端泄露，又能维持接近云端大模型的高生成质量。

## 2. 方法论
- **核心思想**：ObCLIP，将原始提示转换为**语义相似但敏感属性不同的候选提示集**，云端对所有候选进行部分去噪，设备端再完成后续步骤并筛选出目标图像。
- **关键技术细节**：
  - **提示混淆**：用户输入的真实提示被扩展为 \(K\) 个候选提示，各候选在敏感属性（如性别、族裔）上不同，但整体语义高度相似。云端无法区分哪个是真实提示，从而实现**不经意性（oblivious）**。
  - **云端-设备混合去噪**：
    - 云端大模型仅执行**少量前向去噪步骤**（例如占总步骤的一小部分），处理所有 \(K\) 个候选提示，得到中间潜在表示（intermediate latents）。
    - 这些潜在表示传回本地设备后，设备端识别并选择与真实提示对应的潜在表示，再利用**本地小模型**完成剩余去噪步骤，生成最终图像。
  - **缓存加速**：利用时序和批次冗余设计缓存机制，减少重复计算，降低云端开销。
- **算法流程概括**：
  1. 用户输入原始提示 \(p\)。
  2. 设备端生成语义相似但属性改变的候选提示集 \(\{p_1, ..., p_K\}\)。
  3. 云端大模型对所有 \(p_i\) 进行早期去噪，得到 \(\{z_i\}\)。
  4. 设备接收 \(\{z_i\}\)，选择 \(z_{target}\)，用本地小模型完成剩余去噪，输出图像。

## 3. 实验设计
- **数据集/场景**：论文在**多个数据集**上进行实验（摘要中未列出具体名称，可能包括人脸生成、通用图像生成等常见评测集）。
- **评价基准**：以**云端大模型（无隐私保护）的生成质量**作为 utility 基准，同时衡量隐私保护程度和服务器计算开销。
- **对比方法**：与现有未能同时满足效用与严格隐私的方案进行比较（具体方法名未给出）。

## 4. 资源与算力
- 摘要及元数据中**未明确提及**所用 GPU 型号、数量或训练时长。仅提及“slightly increased server computation”表明云端计算量略有增加，但无量化算力指标。

## 5. 实验数量与充分性
- 摘要提到“extensive experiments across multiple datasets”，说明在不同数据集上进行了**多组实验**，可能包含：
  - 不同隐私保护强度下的生成质量对比。
  - 消融实验：候选集大小 \(K\)、云端去噪步数、缓存机制对性能的影响。
- 但摘要未给出具体实验组数，无法判断是否覆盖足够多的场景。从“rigorous privacy and comparable utility”的表述看，实验在保护效果和生成质量之间取得了均衡，具有一定说服力。

## 6. 论文的主要结论与发现
- ObCLIP 能够在**提供严格隐私保障**（云端无法获取真实提示）的同时，实现**与云端大模型相当**的生成质量。
- 混合生成策略和缓存加速有效控制了云端计算开销，仅带来轻微增加。
- 该方法是一种即插即用的隐私保护方案，可方便集成到现有扩散模型推理服务中，平衡隐私、效率与实用性。

## 7. 优点
- **隐私保障严谨**：提示混淆结合不经意性，杜绝云端直接获取真实敏感信息。
- **实用性强**：即插即用设计，无需重新训练云端模型。
- **计算成本可控**：通过仅执行少量云端去噪和本地模型补全，避免全量云端计算，辅以缓存进一步降本。
- **生成质量维持**：在多个数据集上验证了与无保护大模型可比的效果。

## 8. 不足与局限
- **实验细节缺失**：摘要未列出具体数据集、对比基线方法及量化指标，难以评估覆盖广度和公平性。
- **敏感属性定义**：候选提示的生成依赖对敏感属性的预定义，可能无法覆盖所有潜在敏感维度。
- **本地小模型依赖**：设备端需具备一定的本地推理能力（小模型），可能对低端设备仍存在门槛。
- **通信开销**：需传输 \(K\) 个中间潜在表示，当 \(K\) 较大时可能带来额外带宽消耗。
- **缓存限制**：缓存加速效果受用户请求的时序和批量相似性影响，极端不重复场景下收益可能有限。

（完）
