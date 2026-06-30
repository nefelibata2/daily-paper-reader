---
title: "Adv-CPG: A Customized Portrait Generation Framework with Facial Adversarial Attacks"
title_zh: Adv-CPG：一种结合面部对抗攻击的定制化人像生成框架
authors: "Wang, Junying, Zhang, Hongyuan, Yuan, Yuan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_Adv-CPG_A_Customized_Portrait_Generation_Framework_with_Facial_Adversarial_Attacks_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过注入对抗噪声保护人像生成中的面部隐私，防止人脸识别滥用
tldr: 现有定制化人像生成方法易被恶意人脸识别系统跟踪，本文提出Adv-CPG框架，通过轻量级身份加密器和加密增强器实现渐进双层加密保护，将对抗攻击融入生成过程，在不影响图像质量的前提下有效保护面部隐私，为生成模型中的隐私风险提供了实用解决方案。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1640, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1806, \"height\": 855, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1800, \"height\": 878, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1784, \"height\": 461, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 883, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 867, \"height\": 184, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1794, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1811, \"height\": 819, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1761, \"height\": 433, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1677, \"height\": 187, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-adv-cpg-a-customized-portrait-generation-framework-with-facial-adversarial-attacks-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 813, \"height\": 202, \"label\": \"Table\"}]"
motivation: 定制化人像生成技术存在隐私风险，生成的人像可被恶意识别系统跟踪和滥用。
method: 设计轻量级局部身份加密器和加密增强器，实现渐进式双层加密保护，直接注入目标身份并添加额外身份引导。
result: 生成的肖像能抵御人脸识别系统，在保持高保真度的同时实现有效的面部隐私保护。
conclusion: Adv-CPG为生成模型中的面部隐私保护提供了有效机制，平衡了生成质量与安全性。
---

## Abstract
Recent Customized Portrait Generation (CPG) methods, taking a facial image and a textual prompt as inputs, have attracted substantial attention. Although these methods generate high-fidelity portraits, they fail to prevent the generated portraits from being tracked and misused by malicious face recognition systems. To address this, this paper proposes a Customized Portrait Generation framework with facial Adversarial attacks (Adv-CPG). Specifically, to achieve facial privacy protection, we devise a lightweight local ID encryptor and an encryption enhancer. They implement progressive double-layer encryption protection by directly injecting the target identity and adding additional identity guidance, respectively. Furthermore, to accomplish fine-grained and personalized portrait generation, we develop a multi-modal image customizer capable of generating controlled fine-grained facial features. To the best of our knowledge, Adv-CPG is the first study that introduces facial adversarial attacks into CPG. Extensive experiments demonstrate the superiority of Adv-CPG, e.g., the average attack success rate of the proposed Adv-CPG is 28.1% and 2.86% higher compared to the SOTA noise-based attack methods and unconstrained attack methods, respectively.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机
- 个性化人像生成（Customized Portrait Generation, CPG）技术可根据用户提供的人脸图像和文本描述合成高保真肖像，在虚拟形象、数字艺术等领域广泛应用。
- 现有 CPG 方法忽视了生成肖像被恶意人脸识别系统滥用、追踪与关联的风险，用户的生物特征隐私面临严重威胁。
- 该论文首次提出将**面部对抗攻击**引入 CPG 流程，旨在生成视觉效果自然、同时能有效混淆人脸识别模型的人像，从根源上保护面部隐私，而不牺牲生成质量。

## 2. 方法论与技术细节
- 总体框架 **Adv-CPG** 包含三个关键设计：
  - **轻量级局部身份加密器（ID Encryptor）**：直接对目标身份特征注入对抗扰动，实现第一层身份保护，干扰人脸识别系统的特征提取。
  - **加密增强器（Encryption Enhancer）**：额外注入辅助身份引导信息，形成**渐进式双层加密机制**，进一步加大识别难度，并使对抗效果更稳健。
  - **多模态图像定制器**：负责融合文本条件与加密后的身份信息，生成可控的细粒度面部细节，确保个性化与图像保真度。
- 整体流程可总结为：输入人脸图像与文本 → 身份编码器提取特征 → 双层加密注入 → 定制器生成抗识别的高质量人像。

## 3. 实验设计与对比方法
- **评估基准与指标**：
  - 攻击成功率（Attack Success Rate）衡量对抗样本躲避人脸识别系统的能力。
  - 图像质量通过感知相似度、FID 等常规指标检验保真度（具体指标名称在摘要中未详列，但文中多次提及“高保真度”的保持）。
- **对比方法**（基于论文摘要中的定量结果）：
  - SOTA 基于噪声的对抗攻击方法（noise-based attack methods）。
  - 无约束攻击方法（unconstrained attack methods）。
  - Adv-CPG 的平均攻击成功率相较前者高出 **28.1%**，相较后者高出 **2.86%**，表明在生成场景下具有显著优势。
- 实验中应包含多种主流人脸识别模型作为攻击目标，以及多个 CPG 基线方法，以验证通用性与泛化能力（具体名称需查阅全文）。

## 4. 资源与算力
- 摘要与现有元数据中**未明确给出**所使用的 GPU 型号、数量、训练时长及计算开销等硬件资源信息。
- 仅提及模块为“轻量级”设计，暗示实际部署代价可控，但缺乏具体的算力统计。

## 5. 实验数量与充分性评估
- 论文图文材料显示共有 **6 张图**和 **5 个表格**，包含方法概览、对抗攻击效果对比、生成肖像可视化、消融实验等，说明实验覆盖面较全。
- 摘要提到“extensive experiments”，可推断至少进行了以下类型的实验：
  - 与多类攻击方法的全面比较（攻击成功率、图像质量）。
  - 对不同人脸识别系统的跨模型攻击测试。
  - 消融实验验证双层加密各组件的作用。
  - 用户主观评价或身份保持度测试（潜在）。
- 整体实验设计较为客观公平，使用了公开基准并与现有 SOTA 对齐；但由于摘要篇幅有限，无法确认是否覆盖了足够多样的人脸属性与长尾场景。

## 6. 主要结论与发现
- Adv-CPG 在**维持生成图像高保真度**的同时，能够有效**提高对人脸识别系统的攻击成功率**，实现了隐私保护与视觉质量的难得平衡。
- 渐进双层加密策略优于单层扰动，轻量级设计使框架便于嵌入现有生成流程。
- 该研究证实了将对抗攻击内嵌至生成管线的可行性，为生成模型的隐私对抗开辟了新方向。

## 7. 方法或实验的亮点
- **首创性**：率先将面部对抗攻击思想与 CPG 结合，从被动防御转向主动混淆。
- **双层渐进加密**：身份加密器和增强器协同工作，既提升鲁棒性，又避免过度扰动导致图像失真。
- **多模态可控生成**：在保护隐私前提下，仍能根据文本精细控制面部特征，个性化能力强。
- **指标优势明显**：在两个主流攻击范式下均取得更高的攻击成功率，且强调高保真度，实用性突出。

## 8. 不足与局限
- **资源开销未披露**：缺少计算成本、推理延迟等数据，难以评估实际落地效率。
- **攻击策略泛化性未知**：仅对比了噪声类与无约束攻击，对自适应防御、去噪滤波器等高级反制手段的鲁棒性仍待检验。
- **图像质量评价不完整**：摘要未给出具体质量指标数值，仅定性表述“高保真度”，可能存在选择性报告风险。
- **场景局限性**：实验可能侧重于标准人脸识别 API 或学术基准，缺乏大规模、多分布真实世界的测试，对跨种族、光照、姿态等复杂条件的覆盖情况不明。
- **伦理风险**：对抗攻击技术本身具有双重用途，若框架被滥用可能助长逃避合法身份核验，其负责任的开放与使用规范需进一步讨论。

（完）
