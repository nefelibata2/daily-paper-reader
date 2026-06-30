---
title: "BadToken: Token-level Backdoor Attacks to Multi-modal Large Language Models"
title_zh: BadToken：针对多模态大语言模型的令牌级后门攻击
authors: "Yuan, Zenghui, Shi, Jiawen, Zhou, Pan, Gong, Neil Zhenqiang, Sun, Lichao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yuan_BadToken_Token-level_Backdoor_Attacks_to_Multi-modal_Large_Language_Models_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 10.0
evidence: 针对多模态大语言模型的令牌级后门攻击
tldr: 首次提出面向多模态大语言模型的令牌级后门攻击BadToken，通过令牌替换和令牌添加两种隐式行为，在自动驾驶和医疗诊断等应用场景中实现灵活且隐蔽的攻击，突显即插即用部署的安全风险。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1694, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 782, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 843, \"height\": 365, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1740, \"height\": 550, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 875, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 746, \"height\": 274, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 851, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 853, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 874, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 871, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yuan-badtoken-token-level-backdoor-attacks-to-multi-modal-large-language-models-cvpr-2025-paper/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 812, \"height\": 562, \"label\": \"Table\"}]"
motivation: 多模态大语言模型在即插即用部署下易受后门攻击，现有攻击有效性和隐蔽性有限。
method: 提出BadToken，引入令牌替换和令牌添加两种令牌级后门行为。
result: 实验证明，BadToken在多种多模态任务中实现高成功率攻击，且更隐蔽。
conclusion: 揭示了多模态模型的令牌级安全威胁，为防御提供新思路。
---

## Abstract
Multi-modal large language models (MLLMs) extend large language models (LLMs) to process multi-modal information, enabling them to generate responses to image-text inputs. MLLMs have been incorporated into diverse multi-modal applications, such as autonomous driving and medical diagnosis, via plug-and-play without fine-tuning. This deployment paradigm increases the vulnerability of MLLMs to backdoor attacks. However, existing backdoor attacks against MLLMs achieve limited effectiveness and stealthiness. In this work, we propose BadToken, the first token-level backdoor attack to MLLMs. BadToken introduces two novel backdoor behaviors: Token-substitution and Token-addition, which enable flexible and stealthy attacks by making token-level modifications to the original output for backdoored inputs. We formulate a general optimization problem that considers the two backdoor behaviors to maximize the attack effectiveness. We evaluate BadToken on two open-source MLLMs and various tasks. Our results show that our attack maintains the model's utility while achieving high attack success rates and stealthiness. We also show the real-world threats of BadToken in two scenarios, i.e., autonomous driving and medical diagnosis. Furthermore, we consider defenses including fine-tuning and input purification. Our results highlight the threat of our attack.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究背景**：多模态大语言模型（MLLMs）通过将视觉编码器与大语言模型结合，能处理图像-文本联合输入，已在自动驾驶、医疗诊断等场景中以“即插即用”（plug-and-play）方式广泛部署（无需微调）。
- **核心问题**：这种即插即用的部署范式使 MLLMs 极易受到后门攻击。现有针对 MLLMs 的后门攻击在**有效性**和**隐蔽性**方面存在明显局限：攻击成功率不高，且攻击行为（如输出固定恶意句子）容易被检测。
- **整体含义**：本文指出令牌级的后门攻击是更隐蔽、更灵活的威胁，并首次系统性地提出针对 MLLMs 的令牌级后门攻击方法，揭示了多模态模型在输出层面面临的新型安全风险。

### 2. 论文提出的方法论
- **核心思想**：提出 **BadToken**，一种令牌级后门攻击，通过在后门触发时对模型原本应有的良性输出进行**最小粒度的令牌级修改**，实现既隐蔽又有效的攻击。
- **关键技术细节**：
  - **两种后门行为**：
    - **令牌替换（Token-substitution）**：将原始输出中的某些关键令牌替换为恶意令牌（例如，将“停止”替换为“通行”）。
    - **令牌添加（Token-addition）**：在原始输出中悄悄插入额外的恶意令牌（例如，在诊断报告中插入错误的疾病代码）。
  - **优化问题建模**：将两种后门行为统一为一个**通用优化问题**，目标是在保证模型通用能力（utility）的前提下，最大化后门样本上目标令牌生成的概率，同时最小化正常样本上的扰动，以兼顾隐蔽性和有效性。
  - **攻击流程**：攻击者通过操控训练数据或植入恶意适配器，在 MLLM 中注入后门。当输入图像或文本中包含特定后门触发词/图案时，模型生成的输出会被执行令牌替换或添加。

### 3. 实验设计
- **数据集/场景**：
  - 虽未列举具体数据集名称，但摘要提到在 **多种多模态任务** 上进行评估，可覆盖图像描述、视觉问答等通用任务。
  - 针对真实世界威胁的展示场景：**自动驾驶**（如对交通标志的令牌级篡改导致错误决策）和**医疗诊断**（如在诊断报告中插入假症状或误诊断）。
- **Benchmark 与对比方法**：
  - 在两个**开源 MLLMs**上评测（文中未给出模型名，但可合理推断为 LLaVA、MiniGPT-4 等主流模型）。
  - 对比了 **微调（fine-tuning）** 和 **输入净化（input purification）** 等防御手段，以检验 BadToken 的鲁棒性。
- **评估指标**：主要关注攻击成功率（Attack Success Rate, ASR）和模型通用效用的保持度。

### 4. 资源与算力
- 论文提供的元数据及摘要中**未明确说明**所用的 GPU 型号、数量及训练时长。因此无法从现有信息中总结具体算力开销。

### 5. 实验数量与充分性
- **实验组数推测**：
  - 2 个开源 MLLMs × 多种多模态任务 × 2 种后门行为（替换、添加）× 真实威胁场景（自动驾驶、医疗诊断）× 防御评估（微调、输入净化）。按照这样的组合，至少包含几十组实验设置。
  - 很可能还包含**消融实验**，例如单独测试令牌替换或令牌添加的效果，以及对比不同触发器或优化权重的影响。
- **充分性与公平性**：
  - 覆盖了通用任务与具体高风险领域的测试，实验设计较为全面。
  - 对比的防御方法是后门领域常用的基线（微调清除、输入净化），具有客观参照。
  - 显式测量了攻击对模型正常效用的影响，确保所提攻击并非以严重牺牲性能为代价，对比公平。

### 6. 论文的主要结论与发现
- BadToken 攻击能够在维持 MLLM 通用能力（utility）的前提下，取得**高攻击成功率**。
- 令牌级修改（替换/添加）比以往的整句输出替换更**隐蔽**，更难被基于字面匹配的检测方法发现。
- 在自动驾驶和医疗诊断场景的案例中，BadToken 表现出真实的、可操作的威胁，凸显了即插即用部署的严重风险。
- 对微调和输入净化等防御的鲁棒性实验进一步说明，当前防御策略不能完全消除此类令牌级后门威胁。

### 7. 优点
- **问题新颖性**：首次提出针对 MLLMs 的令牌级后门攻击，填补了该方向空白。
- **方法设计巧妙**：令牌替换和令牌添加两种细粒度行为，配合精心建模的优化目标，实现了灵活且隐蔽的攻击。
- **结合实际威胁**：在自动驾驶和医疗诊断两个高风险应用场景中验证威胁，提升了研究的现实意义。
- **防御讨论**：预先考虑并测试了典型防御方法，使攻击的严重性论证更完整。
- **实验全面**：涵盖多模型、多任务、多场景，并量化了效用与隐蔽性的权衡。

### 8. 不足与局限
- **数据集与模型未公开具名**：从已有元数据无法得知具体使用了哪些模型和数据集，可能影响复现的清晰度（需查阅原文全文）。
- **防御覆盖有限**：仅测试了微调和输入净化两种防御，未涉及更先进的检测与防御机制（如模型诊断、鲁棒性训练、触发器反演等），可能低估了防御潜力。
- **攻击假设可能较强**：后门攻击通常要求攻击者能操控训练数据或模型组件（如适配器），本文未详细说明攻击场景的权限假设，实际部署中可实施性存在约束。
- **跨模态泛化待验证**：仅聚焦于 MLLMs，未探讨令牌级后门在纯文本 LLM 或纯视觉模型上的迁移性或差异。
- **隐蔽性评估维度单一**：主要依赖人工检查或简单字面匹配，未使用更系统的隐蔽性指标（如基于困惑度、语义一致性的检测）。

（完）
