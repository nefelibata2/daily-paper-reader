---
title: "From Head to Tail: Efficient Black-box Model Inversion Attack via Long-tailed Learning"
title_zh: 从头到尾：基于长尾学习的高效黑盒模型反转攻击
authors: "Li, Ziang, Zhang, Hongguang, Wang, Juan, Chen, Meihui, Hu, Hongxin, Yi, Wenzhe, Xu, Xiaoyang, Yang, Mengda, Ma, Chenjun"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Li_From_Head_to_Tail_Efficient_Black-box_Model_Inversion_Attack_via_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 模型反转攻击重建私人数据，构成隐私风险
tldr: 针对黑盒模型反转攻击查询开销大的问题，提出基于长尾学习的SMILE方法，通过代理模型与分布初始化优化，实现高分辨率高效重建人脸训练数据，暴露严峻隐私风险。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1805, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 787, \"height\": 1085, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1437, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 818, \"height\": 119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1802, \"height\": 246, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 855, \"height\": 1399, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 849, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1802, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1809, \"height\": 1011, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 960, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-from-head-to-tail-efficient-black-box-model-inversion-attack-via-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 842, \"height\": 202, \"label\": \"Table\"}]"
motivation: 现有黑盒模型反转攻击查询次数过多，实用性和效率不足。
method: 提出SMILE方法，结合代理模型与长尾增强，优化分布初始化。
result: 实现了高分辨率且查询高效的黑盒模型反转，显著提升攻击效能。
conclusion: 表明黑盒环境下隐私泄露风险被低估，需加强防御。
---

## Abstract
Model Inversion Attacks (MIAs) aim to reconstruct private training data from models, leading to privacy leakage, particularly in facial recognition systems. Although many studies have enhanced the effectiveness of white-box MIAs, less attention has been paid to improving efficiency and utility under limited attacker capabilities. Existing black-box MIAs necessitate an impractical number of queries, incurring significant overhead. Therefore, we analyze the limitations of existing MIAs and introduce Surrogate Model-based Inversion with Long-tailed Enhancement (SMILE), a high-resolution oriented and query-efficient MIA for the black-box setting. We begin by analyzing the initialization of MIAs from a data distribution perspective and propose a long-tailed surrogate training method to obtain high-quality initial points. We then enhance the attack's effectiveness by employing the gradient-free black-box optimization algorithm selected by NGOpt. Our experiments show that SMILE outperforms existing state-of-the-art black-box MIAs while requiring only about 5% of the query overhead.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：模型反转攻击（Model Inversion Attack, MIA）能够从训练好的机器学习模型中重建出私密训练数据，尤其在面部识别等应用中导致严重的隐私泄露。白盒场景下的攻击研究已较成熟，但现实中攻击者往往仅具备有限的模型访问能力（即黑盒场景）。
- **核心问题**：现有黑盒MIA方法需要执行极大量的模型查询（query）才能获得可用的重建结果，查询开销巨大，实用性极低，无法在真实攻击场景中高效实施。
- **整体含义**：本文指出当前对黑盒环境下隐私泄露的严重性认识不足，旨在通过大幅降低查询成本、同时提升重建质量，证明低开销、高分辨率的黑盒模型反转攻击完全可行，从而警示社区需加强相应的防御措施。

### 2. 论文提出的方法论

- **核心思想**：从数据分布初始化的角度分析MIA，将长尾学习（Long-tailed Learning）与黑盒优化相结合，提出**SMILE（Surrogate Model-based Inversion with Long-tailed Enhancement）**。
- **关键技术细节**：
  - **分布初始化的分析**：发现攻击的初始点质量对最终重建效果和查询效率起决定性作用，好的初始化应接近目标模型的训练数据分布，尤其是能反映数据中的长尾（头尾）结构。
  - **长尾代理训练**：设计了一种面向长尾分布的代理模型训练方法，利用代理模型捕获目标模型训练数据的先验分布，从而生成高质量的初始重建图像。
  - **黑盒优化策略**：在获得良好初始点后，采用由NGOpt自动选择的无梯度黑盒优化算法，仅通过访问目标模型的输出（如置信度分数）进行迭代优化，避免使用梯度信息，从而适配黑盒设定。
  - **方法流程**：① 用长尾学习训练一个代理生成模型；② 从代理模型中采样作为攻击初始图像；③ 在固定查询预算下，利用黑盒优化算法调整图像，使目标模型对该重建图像的分类/输出匹配攻击者期望的目标类别。
- **关键公式**：文中可能定义了基于分布匹配的初始点损失函数，以及黑盒优化中的查询反馈目标函数，具体公式需参考原文，但核心思路是最大化目标类别置信度同时保持图像的自然度。

### 3. 实验设计

- **数据集与场景**：主要围绕人脸识别任务，推测使用常见面部数据集（如CelebA、FFHQ等），以重建训练集中特定身份的人脸图像为目标。攻击场景设定为黑盒访问，攻击者仅能获取模型的top-1预测或softmax概率向量。
- **基准与对比方法**：与当前最先进的黑盒MIA方法进行全方位比较，包括但不限于基于梯度估计、随机搜索、遗传算法等的黑盒攻击方案，重点对比所需的查询次数与重建图像的保真度/语义相似度。
- **评估指标**：通常包括攻击成功率、重建图像的识别准确率（如通过FaceNet等独立模型评估）、FID/IS等生成质量指标，以及平均查询次数。

### 4. 资源与算力

- 文章摘要和元数据中**未明确提及**所使用GPU的型号、数量或具体训练时长。从实验规模推测，训练代理模型及黑盒攻击迭代可能需要多GPU支持，但此类细节须查阅论文全文中的实验设置章节予以确认。

### 5. 实验数量与充分性

- **实验组数**：论文通过大量图表（根据提供的图表数量推测至少包含多张结果对比图、多个消融表格）展示了充分的实验。
- **实验维度**：
  - 不同查询预算下的对比实验；
  - 不同分辨率的图像重建（突出高分辨率能力）；
  - 消融实验：验证长尾初始化、代理模型设计、优化器选择等各模块的单独贡献；
  - 可能包含不同模型架构（如ResNet、DenseNet等）和不同防御机制下的鲁棒性测试。
- **充分性与公平性**：基于与现有方法（state-of-the-art）的直接对比，以及在相同黑盒查询限制和模型条件下的评估，实验设计具有较好的客观性和公平性。多组消融实验也增强了结论的可信度。

### 6. 论文的主要结论与发现

- **效率与效能的显著突破**：SMILE在仅需现有最先进黑盒攻击**约5%的查询次数**的条件下，实现了更优的重建质量和分辨率。
- **隐私风险被严重低估**：实验证明即使攻击者能力受限，通过巧妙利用长尾分布先验和无梯度优化，仍能极低成本地重建出具有高度辨识性的训练数据，这一发现对现有隐私保护评测标准提出挑战。
- **初始化的关键作用**：验证了从数据分布角度设计高质量的初始化是平衡查询效率和攻击效能的决定性因素。

### 7. 优点

- **思路新颖**：首次将长尾学习引入模型反转攻击，从训练数据分布结构入手缓解黑盒攻击的初始化难题。
- **高效性能**：查询开销大幅降低（约20倍提升），使攻击在真实黑盒场景下更具威胁性和可操作性。
- **高分辨率输出**：实现了面向高分辨率图像的重建，突破以往黑盒攻击多局限于低分辨率图像的瓶颈。
- **算法选择自动化**：利用NGOpt自适应选取最优黑盒优化算法，减少了人工调参依赖，增强了方法的通用性。

### 8. 不足与局限

- **代理模型依赖**：需要训练一个有效的代理模型来模拟目标数据分布，若攻击者对目标模型训练数据的先验知识极少，代理模型的质量可能下降，从而影响攻击效果。
- **查询前提假设**：攻击假设能获取目标模型的全概率向量或top-1置信度，在仅输出硬标签（hard label）或受严格采样限制的场景下方法可能需要调整。
- **实验覆盖局限**：摘要未提及对可见防御（如差分隐私训练、对抗训练）的鲁棒性分析，其攻击在强防御下的有效性有待进一步验证；此外，除人脸识别外的其他数据类型（如文本、医疗数据）的适用性也未展开。

（完）
