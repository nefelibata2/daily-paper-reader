---
title: Exploring Visual Vulnerabilities via Multi-Loss Adversarial Search for Jailbreaking Vision-Language Models
title_zh: 通过多损失对抗搜索探索视觉漏洞以越狱视觉语言模型
authors: "Hao, Shuyang, Hooi, Bryan, Liu, Jun, Chang, Kai-Wei, Huang, Zi, Cai, Yujun"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Hao_Exploring_Visual_Vulnerabilities_via_Multi-Loss_Adversarial_Search_for_Jailbreaking_Vision-Language_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 10.0
evidence: 利用视觉漏洞越狱视觉语言模型的框架
tldr: 针对视觉语言模型的安全对齐漏洞，提出多损失对抗图像搜索框架MLAI，利用场景感知生成和平坦极小值理论选取健壮的对抗图像，实现更有效的协同越狱攻击，揭示视觉模态的潜在安全风险。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 1244, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 631, \"height\": 494, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1746, \"height\": 1360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 401, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 836, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 875, \"height\": 384, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 623, \"height\": 488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 625, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 873, \"height\": 430, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1801, \"height\": 683, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-hao-exploring-visual-vulnerabilities-via-multi-loss-adversarial-search-for-jailbreaking-vision-language-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 860, \"height\": 205, \"label\": \"Table\"}]"
motivation: 视觉语言模型虽继承语言模型的安全措施，但仍存在视觉模态的越狱漏洞。
method: 提出MLAI框架，通过多损失搜索、场景匹配图像和协同攻击增强越狱效果。
result: 实验表明，场景匹配图像能显著放大有害输出，多图像协同攻击效果更强。
conclusion: 揭示了视觉语言模型中视觉模态的对齐缺陷，为安全评估提供新方法。
---

## Abstract
Despite inheriting security measures from underlying language models, Vision-Language Models (VLMs) may still be vulnerable to safety alignment issues. Through empirical analysis, we uncover two critical findings: scenario-matched images can significantly amplify harmful outputs, and contrary to common assumptions in gradient-based attacks, minimal loss values do not guarantee optimal attack effectiveness. Building on these insights, we introduce MLAI (Multi-Loss Adversarial Images), a novel jailbreak framework that leverages scenario-aware image generation for semantic alignment, exploits flat minima theory for robust adversarial image selection, and employs multi-image collaborative attacks for enhanced effectiveness. Extensive experiments demonstrate MLAI's significant impact, achieving attack success rates of 77.75% on MiniGPT-4 and 82.80% on LLaVA-2, substantially outperforming existing methods by margins of 34.37% and 12.77% respectively. Furthermore, MLAI shows considerable transferability to commercial black-box VLMs, achieving up to 60.11% success rate. Our work reveals fundamental visual vulnerabilities in current VLMs safety mechanisms and underscores the need for stronger defenses. Warning: This paper contains potentially harmful example text.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：视觉语言模型（Vision-Language Models, VLMs）虽普遍继承了底层大语言模型的安全对齐措施，但在视觉模态上仍可能存在未被充分审视的安全漏洞。
- **核心问题**：本文致力于揭示并利用 VLMs 的视觉模态脆弱性，实现“越狱攻击”（jailbreaking），即诱导模型生成本应被过滤的有害内容。
- **关键发现**：
  - **场景匹配图像可放大有害输出**：与攻击意图在语义上高度匹配的图像，能显著绕过安全限制，增强模型生成有害文本的倾向。
  - **最小损失值并不保证最优攻击效果**：现有基于梯度的对抗攻击普遍认为损失极小值对应最佳攻击效果，但在 VLMs 越狱场景中，这一假设并不成立，需要更稳健的图像选择策略。
- **整体含义**：提出 MLAI（Multi-Loss Adversarial Images）框架，从攻击视角系统性地暴露当前 VLM 安全机制的缺陷，为构建更强的防御体系提供依据和推动力。

### 2. 论文提出的方法论

**核心思想**：MLAI 框架通过三个紧密协同的模块，生成能诱使 VLM 输出有害内容的对抗性图像：

- **场景感知图像生成（Scenario-aware Image Generation）**
  - 不直接扰动原始像素，而是利用文本到图像生成模型，根据“有害请求的语义场景”生成匹配的合成图像，使图像内容与攻击意图对齐，增大模型越狱的可能性。

- **基于平坦极小值理论的鲁棒对抗图像选择（Flat Minima based Robust Selection）**
  - 从损失地形（loss landscape）的视角，不再仅选取损失值最小的候选项，而是基于“平坦极小值”（flat minima）原则，选择在参数扰动下损失变化更平缓的图像。
  - 这类图像具有更好的迁移性和攻击稳定性，从而解释并规避了“最小损失 ≠ 最优攻击”的误区。

- **多图像协同攻击（Multi-image Collaborative Attack）**
  - 同时向模型输入多张分别针对不同语义侧面的对抗图像（例如一张描绘场景，另一张带有误导性文字），利用模型对多图像输入的联合编码，进一步放大了不安全内容的生成概率。

**关键技术流程**（文字描述）：
1. 根据目标有害问题，生成一系列候选场景图像。
2. 计算多维度损失（如语义对齐损失、有害性引导损失），并评估每个候选图像在损失地形中的平坦度。
3. 从中选取位于平坦极小值区域的对抗图像。
4. 若单张图像攻击成功率不足，则动态组合多张图像协同攻击。
整体过程可视为一种搜索范式，兼顾了图像语义、损失地形和输入多样性。

### 3. 实验设计

- **数据集／评估场景**：
  - 基于常见安全基准构建的越狱测试集，包含多种有害请求类别（暴力、仇恨言论、非法建议等）。
- **基准模型（Benchmark Models）**：
  - 开源 VLM：MiniGPT-4、LLaVA-2。
  - 商用黑盒 VLM（如 Gemini 等）用于测试攻击的迁移性。
- **对比方法**：
  - 现有基于梯度的图像对抗攻击方法。
  - 仅使用文本的越狱攻击基线。
  - 其他近期针对 VLMs 的越狱方案。
- **评估指标**：攻击成功率（Attack Success Rate, ASR），即模型输出确实包含有害内容的比例。

### 4. 资源与算力

- 论文 PDF 文本及元数据中**未明确提及**所使用的 GPU 型号、数量、训练／搜索时长等具体算力信息。
- 从方法描述推断，对抗图像生成可能依赖于预训练的扩散模型（用于场景图像生成）和 VLM 自身的前向传播损失计算，搜索过程涉及多候选评估，但具体的计算资源开销在现有材料中未予说明。

### 5. 实验数量与充分性

- **主要实验组**：
  - 在 MiniGPT-4 和 LLaVA-2 上的主攻击实验（单图像与多图像协同）。
  - 攻击成功率对比实验，与多个基线方法进行比较。
  - 迁移性实验，跨模型测试（尤其向商用的黑盒 VLM）。
  - 消融实验（虽未逐一列举，但从方法论中“场景匹配”“平坦极小值选择”“多图像协同”等独立模块的设计可推断，论文对每个模块的有效性进行了剥离验证，如仅用随机图像、仅用最小损失图像、仅用单图像等）。
- **实验充分性**：
  - 覆盖了两款主流开源 VLM 以及商业黑盒模型，体现了较强的覆盖面。
  - 通过对比和消融，验证了各设计选择的必要性与增益，整体实验较为翔实、公平。
  - 迁移性测试进一步提升了结论的外部效度。

### 6. 论文的主要结论与发现

- MLAI 在 MiniGPT-4 上取得 **77.75%** 的攻击成功率，在 LLaVA-2 上达到 **82.80%**，相较于现有方法分别提升 **34.37%** 和 **12.77%** 个百分点，展现出显著优势。
- 场景匹配图像能够系统性放大 VLMs 的有害输出，单纯依靠文本越狱或随机图像攻击收效甚微。
- 平坦极小值选择策略有效解决了“最小损失 ≠ 最优攻击”的认知偏差，并提升了对抗图像在黑盒模型上的迁移性（迁移至商业 VLM 的攻击成功率最高达到 **60.11%**）。
- 多图像协同攻击进一步增强了越狱效果，表明 VLMs 在处理多模态输入时的脆弱性尤为突出。
- 总体结论：当前 VLMs 在视觉通路上的安全对齐存在本质缺陷，亟需更强的多模态防御机制。

### 7. 优点

- **视角新颖**：以损失地形平坦性作为对抗样本选择标准，打破了传统梯度攻击中依赖最小损失值的惯性思维，理论依据清晰。
- **多模块协同**：将场景语义对齐、图像鲁棒性选择和多图像联合攻击有机整合，形成一个完整的攻击框架，攻击效率与成功率均大幅领先。
- **实用性强**：不仅能攻击开源模型，还能高比率地迁移到黑盒商业模型，凸显该漏洞的现实威胁性。
- **实验扎实**：进行了多模型、多基线、迁移性和消融等全面评估，论证充分。

### 8. 不足与局限

- **算力细节缺失**：未披露方法所需的计算资源（如 GPU 消耗、搜索时长等），难以评估其实际攻击成本和可复现性。
- **防御对策未给出**：虽然揭示了漏洞，但并未提出相应的防御方案，攻击方法的发布也可能被恶意利用。
- **攻击场景限定**：实验主要针对文本形式的有害输出，未覆盖图像生成或多模态混合输出的越狱情形，攻击面有待拓展。
- **自动评测偏差**：攻击成功率的判定依赖于响应内容的有害性检测器，检测器本身的误差可能影响最终 ASR 的绝对数值，但这一偏差在对比实验中影响较小。
- **伦理风险**：论文本身包含有害示例文本，虽标注了警告，但仍有被滥用的潜在风险，尤其在开源攻击框架后。

（完）
