---
title: Distraction is All You Need for Multimodal Large Language Model Jailbreaking
title_zh: 分心即一切：多模态大语言模型越狱攻击
authors: "Yang, Zuopeng, Fan, Jiluan, Yan, Anli, Gao, Erdun, Lin, Xin, Li, Tao, Mo, Kanghua, Dong, Changyu"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yang_Distraction_is_All_You_Need_for_Multimodal_Large_Language_Model_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 10.0
evidence: 通过分心策略越狱多模态大语言模型
tldr: 提出对比子图分心越狱框架CS-DJ，通过结构化分心和交叉图像干扰策略破坏多模态大语言模型的视觉-文本对齐，从而绕过安全机制生成有害内容，揭示复杂视觉元素带来的新漏洞。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-distraction-is-all-you-need-for-multimodal-large-language-model-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1624, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-distraction-is-all-you-need-for-multimodal-large-language-model-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1606, \"height\": 868, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-distraction-is-all-you-need-for-multimodal-large-language-model-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 823, \"height\": 444, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-distraction-is-all-you-need-for-multimodal-large-language-model-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1470, \"height\": 977, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-distraction-is-all-you-need-for-multimodal-large-language-model-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 865, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-distraction-is-all-you-need-for-multimodal-large-language-model-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 724, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-distraction-is-all-you-need-for-multimodal-large-language-model-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 866, \"height\": 194, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-distraction-is-all-you-need-for-multimodal-large-language-model-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 868, \"height\": 183, \"label\": \"Table\"}]"
motivation: 多模态大语言模型中视觉元素与文本的复杂交互可能引入可绕过安全机制的漏洞。
method: 提出CS-DJ框架，通过子图对比分心策略扰乱模型对齐。
result: 实验证明，分心策略能有效越狱多模态大语言模型，无需特定内容。
conclusion: 图像复杂性而非内容导致安全漏洞，为防御提供新视角。
---

## Abstract
Multimodal Large Language Models (MLLMs) bridge the gap between visual and textual data, enabling a range of advanced applications. However, complex internal interactions among visual elements and their alignment with text can introduce vulnerabilities, which may be exploited to bypass safety mechanisms. To address this, we analyze the relationship between image content and task and find that the complexity of subimages, rather than their content, is key. Building on this insight, we propose the Distraction Hypothesis, followed by a novel framework called Contrasting Subimage Distraction Jailbreaking (CS-DJ), to achieve jailbreaking by disrupting MLLMs alignment through multi-level distraction strategies. CS-DJ consists of two components: structured distraction, achieved through query decomposition that induces a distributional shift by fragmenting harmful prompts into sub-queries, and visual-enhanced distraction, realized by constructing contrasting subimages to disrupt the interactions among visual elements within the model. This dual strategy disperses the model's attention, reducing its ability to detect and mitigate harmful content. Extensive experiments across five representative scenarios and four popular closed-source MLLMs, including \texttt GPT-4o-mini , \texttt GPT-4o , \texttt GPT-4V , and \texttt Gemini-1.5-Flash , demonstrate that CS-DJ achieves average success rates of 52.40% for the attack success rate and 74.10% for the ensemble attack success rate. These results reveal the potential of distraction-based approaches to exploit and bypass MLLMs' defenses, offering new insights for attack strategies.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：多模态大语言模型（MLLMs）通过融合视觉与文本信息实现了强大的跨模态理解与生成能力，在诸多场景中得到应用。
- **核心问题**：视觉元素与文本之间的复杂内部交互可能导致模型本身的安全对齐机制出现可被利用的脆弱点，攻击者可以绕过安全限制，使模型输出有害内容。
- **研究动机**：现有的越狱攻击往往依赖刻意构造的有害图像或文本，而本文发现**子图的复杂度（而非图像的具体内容）是导致模型安全防线失效的关键因素**，由此提出“分心假说”（Distraction Hypothesis），意图以一种更通用、更隐蔽的方式攻击 MLLMs 的安全性。
- **整体含义**：研究工作从注意力分散的角度揭示了一种新的攻击范式——通过结构化与视觉化的分心策略扰乱模型的跨模态对齐，从而在无需显式有害图像的情况下实现高效越狱，为多模态模型的安全性研究提供了新的攻击视角与防御思路。

## 2. 论文提出的方法论

- **核心思想**：基于“分心假说”，通过多层次的分心策略分散 MLLMs 的注意力，削弱其对有害内容的检测与防护能力，实现越狱。
- **框架名称**：对比子图分心越狱（Contrasting Subimage Distraction Jailbreaking, CS-DJ）。
- **两大组件**：
  - **结构化分心（Structured Distraction）**：
    - 方法：将原本完整的有害文本提示进行**查询分解（query decomposition）**，把一个统一的恶意请求切分成多个看似不相关的子查询。
    - 作用：制造**分布偏移（distributional shift）**，使模型难以将碎片化的子查询重新组合成有害语义，从而绕过安全校验。
  - **视觉增强分心（Visual-enhanced Distraction）**：
    - 方法：构造**对比子图（contrasting subimages）**，即在一张图像中引入多个在视觉特征或语义上相互矛盾的子区域，破坏视觉元素之间的一致性。
    - 作用：扰乱模型内部视觉元素的交互与对齐过程，进一步降低模型对潜在有害线索的捕捉能力。
- **整体流程**：结合上述两种分心策略，将分散注意力的文本查询与对比子图一同输入 MLLMs，诱导其在注意力分散的状态下生成不安全回复，而不需要提供任何明文的禁止内容。

## 3. 实验设计

- **评估场景**：覆盖**五个代表性场景**（摘要未列出具体场景名称，但应包括常见的越狱测试任务，如生成暴力、歧视、非法建议等类别）。
- **目标模型**：四种流行的闭源 MLLMs：
  - `GPT-4o-mini`
  - `GPT-4o`
  - `GPT-4V`
  - `Gemini-1.5-Flash`
- **评估指标**：
  - **攻击成功率（Attack Success Rate, ASR）**：单次攻击中模型输出有害内容的比率。
  - **集成攻击成功率（Ensemble Attack Success Rate）**：综合多次攻击尝试后的总体成功率。
- **对比方法**：摘要未具体列出对比的基线攻击方法，但通常此类研究会与现有基于视觉的越狱攻击（如 typographic attack、adversarial image attack 等）以及纯文本越狱方法进行对比，以体现分心策略的优越性。

## 4. 资源与算力

- **论文中未明确提及使用的算力资源详情**，包括 GPU 型号、数量、训练时长等。由于攻击主要针对 API 可调用的闭源模型，推测实验中主要消耗的是推理查询的 API 调用次数，而非本地大规模训练或微调所需的计算资源。

## 5. 实验数量与充分性

- **实验规模**：
  - 在 **4 个主流闭源 MLLMs** 上进行了测试。
  - 覆盖 **5 个代表性攻击场景**，多维度评估攻击方法的泛化能力。
  - 给出了两个关键指标（ASR 与 ensemble ASR）的具体数值：平均攻击成功率 52.40%，集成攻击成功率 74.10%。
- **充分性与客观性**：
  - 多模型、多场景的实验设计较为充分，能够体现方法的通用性。
  - 使用了标准化的任务场景和客观的成功率指标，减少了人为评判偏差。
  - **潜在不足**：摘要未提及消融实验（验证各分心组件的独立贡献）以及对开源模型的测试，无法全面判断实验覆盖的完备程度。但仅从呈现的结果看，已具备一定的说服力。

## 6. 论文的主要结论与发现

- **分心策略的有效性**：通过结构化和视觉增强的双重分心，可显著提高越狱成功率，证明扰乱注意力是一种有效绕过安全机制的手段。
- **漏洞根源在于复杂性**：越狱成功的关键并非图像内容的“有害性”，而是子图的**结构复杂度和对比性**，这揭示了 MLLMs 安全对齐的薄弱点在于视觉‑文本交互的复杂性控制。
- **攻击范式创新**：CS-DJ 无需依赖显式的违禁内容，降低了攻击的隐蔽性与部署门槛，对现有防御机制构成新的挑战。
- **防御启示**：研究结论提示，未来的安全防御应更多地关注视觉输入的内部一致性和查询的结构完整性，而非仅仅过滤内容。

## 7. 优点

- **创新性强**：首次将“分心”作为核心攻击原理，打破了以往依赖有害图像或精心设计提示的越狱思路。
- **方法隐蔽高效**：通过查询分解和对比子图分散模型注意力，无需输入明显的违规信息，更难被内容过滤机制拦截。
- **实验扎实**：在多个主流闭源 MLLMs 上取得高成功率，且提出的集成攻击成功率进一步提升了攻击的稳定性。
- **视角独特**：从视觉‑文本对齐的脆弱性出发，给出了“复杂性导致漏洞”的新发现，为攻防双方均提供了有价值的新认知。

## 8. 不足与局限

- **模型覆盖面有限**：仅评估了闭源模型，未在开源 MLLMs（如 LLaVA、MiniGPT‑4 等）上验证，攻击的普适性有待进一步确认。
- **指标单一化**：仅以攻击成功率为衡量标准，缺乏对攻击隐蔽性、响应质量、攻击成本（如查询次数）等维度的评估。
- **场景细节缺失**：摘要未给出五个场景的具体定义及各类有害内容的分布，难以判断攻击在不同风险类别上的差异。
- **未考虑防御对抗**：实验未测试攻击在常见安全对齐增强（如系统提示、安全微调）下的鲁棒性，距离真实世界攻击尚有距离。
- **方法可解释性待加强**：虽然提出了分心假说，但对于模型内部注意力如何被具体扰乱缺乏深入的机制分析或可视化验证。

（完）
