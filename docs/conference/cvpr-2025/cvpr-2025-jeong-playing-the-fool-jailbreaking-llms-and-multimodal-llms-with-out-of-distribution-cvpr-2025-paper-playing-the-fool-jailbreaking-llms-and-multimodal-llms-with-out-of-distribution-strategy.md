---
title: "Playing the Fool: Jailbreaking LLMs and Multimodal LLMs with Out-of-Distribution Strategy"
title_zh: 装傻：利用分布外策略越狱大语言模型和多模态大语言模型
authors: "Jeong, Joonhyun, Bae, Seyun, Jung, Yeonsung, Hwang, Jaeryong, Yang, Eunho"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Jeong_Playing_the_Fool_Jailbreaking_LLMs_and_Multimodal_LLMs_with_Out-of-Distribution_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 10.0
evidence: 利用安全对齐漏洞对大语言模型进行越狱攻击
tldr: 针对现有安全对齐的大语言模型仍存在越狱漏洞，本文提出一种分布外策略，通过构造特殊输入绕过安全防护，使模型生成有害内容。实验表明，该方法能有效突破安全防线，揭示当前对齐技术的脆弱性，为构建更鲁棒的模型安全机制提供启示。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jeong-playing-the-fool-jailbreaking-llms-and-multimodal-llms-with-out-of-distribution-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1809, \"height\": 858, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jeong-playing-the-fool-jailbreaking-llms-and-multimodal-llms-with-out-of-distribution-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 855, \"height\": 969, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jeong-playing-the-fool-jailbreaking-llms-and-multimodal-llms-with-out-of-distribution-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 884, \"height\": 978, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jeong-playing-the-fool-jailbreaking-llms-and-multimodal-llms-with-out-of-distribution-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 915, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jeong-playing-the-fool-jailbreaking-llms-and-multimodal-llms-with-out-of-distribution-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 811, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jeong-playing-the-fool-jailbreaking-llms-and-multimodal-llms-with-out-of-distribution-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 797, \"height\": 475, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-jeong-playing-the-fool-jailbreaking-llms-and-multimodal-llms-with-out-of-distribution-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1826, \"height\": 887, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-jeong-playing-the-fool-jailbreaking-llms-and-multimodal-llms-with-out-of-distribution-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1615, \"height\": 240, \"label\": \"Table\"}]"
motivation: 尽管大型语言模型经过安全对齐，但仍存在被越狱攻击诱导生成有害内容的风险，而目前针对这一脆弱性的研究尚不充分。
method: 提出一种分布外策略，构造与模型训练分布差异大的输入，绕过安全防护生成有害输出。
result: 在多个主流大模型上的实验证明，该方法能显著提高越狱成功率，暴露安全对齐的脆弱性。
conclusion: 该工作揭示了大模型安全机制的潜在漏洞，为开发更鲁棒的对齐方法提供了测试基准和新的研究方向。
---

## Abstract
Despite the remarkable versatility of Large Language Models (LLMs) and Multimodal LLMs (MLLMs) to generalize across both language and vision tasks, LLMs and MLLMs have shown vulnerability to jailbreaking, generating textual outputs that undermine safety, ethical, and bias standards when exposed to harmful or sensitive inputs. With the recent advancement of safety alignment via preference-tuning from human feedback, LLMs and MLLMs have been equipped with safety guardrails to yield safe, ethical, and fair responses with regard to harmful inputs. However, despite the significance of safety alignment, research on the vulnerabilities remains largely underexplored. In this paper, we investigate the unexplored vulnerability of the safety alignment, examining its ability to consistently provide safety guarantees for out-of-distribution(OOD)-ifying harmful inputs that may fall outside the aligned data distribution. Our key observation is that OOD-ifying the vanilla harmful inputs highly increases the uncertainty of the model to discern the malicious intent within the input, leading to a higher chance of being jailbroken. Exploiting this vulnerability, we propose JOOD, a new Jailbreak framework via OOD-ifying inputs beyond the safety alignment. We explore various off-the-shelf visual and textual transformation techniques for OOD-ifying the harmful inputs. Notably, we observe that even simple mixing-based techniques such as image mixup prove highly effective in increasing the uncertainty of the model, thereby facilitating the bypass of the safety alignment. Experiments across diverse jailbreak scenarios demonstrate that JOOD effectively jailbreaks recent proprietary LLMs and MLLMs such as GPT-4 and o1 with high attack success rate, which previous attack approaches have consistently struggled to jailbreak. Code is available at https://github.com/naver-ai/JOOD.

---

## 论文详细总结（自动生成）

# Playing the Fool: 利用分布外策略越狱大语言模型和多模态大语言模型 详细总结

## 1. 核心问题与整体含义（研究动机和背景）
*   **研究背景**：大语言模型和多模态大语言模型虽通过基于人类反馈的偏好调优实现了安全对齐，但仍存在“越狱”漏洞，即在特定输入下会生成违反安全、伦理和偏见准则的有害内容。
*   **核心问题**：现有研究对安全对齐在面对“分布外”有害输入时的脆弱性探索不足。安全对齐机制能否在输入偏离其训练分布时持续提供安全保障，是一个尚未被充分解答的关键问题。
*   **整体含义**：本文旨在揭示安全对齐的OOD脆弱性，并通过提出一种基于“装傻”的越狱框架，暴露出当前模型安全防线的薄弱环节，从而为构建更鲁棒的对齐方法提供警示和新思路。

## 2. 论文提出的方法论：核心思想、关键技术细节
*   **核心思想**：通过对原始有害输入施加分布外化变换，刻意制造与安全对齐训练数据分布差异巨大的“怪异”输入。这种OOD化操作会显著增加模型辨别恶意意图的不确定性，使其难以正确调用安全护栏，从而大幅提升越狱成功率。
*   **框架名称与研究假设**：所提方法命名为JOOD——Jailbreak via OOD-ifying inputs。其核心假设是，安全对齐模型在面临偏离分布的有害输入时，其安全识别能力会下降。
*   **关键技术细节**：
    *   JOOD框架探索了多种即插即用的视觉和文本变换技术，用于对原始有害输入进行OOD化处理。
    *   **多模态场景**：对于图文输入，采用简单的混合类技术或图像变换，在保持有害语义的同时扭曲输入的分布特性。
    *   **纯文本场景**：同样应用相应的分布外化文本变换策略。
    *   **关键发现**：即使是极其简单的混合技术，也被证明能有效提高模型的不确定性，从而轻松绕过安全对齐防护。
    *   **流程**：整体而言，JOOD相当于一个输入预处理器，在保持恶意查询核心意图的前提下，向输入中注入“无害”或“噪声”特性，使模型在识别恶意内容时产生混淆，最终输出有害回复。

## 3. 实验设计：数据集/场景、基准、对比方法
*   **数据集与场景**：实验覆盖了多种越狱攻击场景，主要针对标准有害指令数据集，重点验证了多模态和纯文本场景下的攻击效果。
*   **基准模型**：选择了近年具有代表性的专有闭源大模型作为攻击对象，包括但不限于GPT-4和o1。这些模型被认为具有当前最强的安全对齐能力，也是此前许多攻击方法难以攻破的目标。
*   **对比方法**：将JOOD与已有的越狱攻击方法进行了横向对比，特别强调它在那些此前攻击手段持续失利的模型上取得了高攻击成功率，以此突显其优越性。
*   **评价指标**：以攻击成功率作为核心评估指标。

## 4. 资源与算力（GPU、数量、时长等）
*   **文中未明确提及**：提供的论文摘要与元数据中，均未说明JOOD方法所需的GPU型号、数量、训练/推理时长或具体的计算开销。
*   **方法特性推断**：由于JOOD主要依赖对输入进行即用型变换实现越狱，不涉及模型的微调或重训，其算力主要消耗在API调用和输入变换上，相对传统对抗攻击方法而言算力需求较低。但具体数字尚未在提供的内容中披露。

## 5. 实验数量与充分性（实验组数、消融、公平性）
*   **实验覆盖度**：实验涵盖了多个主流闭源大模型、多种越狱场景以及不同的OOD化变换技术，展示出较高的覆盖度。
*   **消融与分析**：文中重点对简单的混合类技术进行了有效性验证与分析，观察其对模型不确定性的影响，这构成了一类内部的消融研究。
*   **公平性**：实验在与现有攻击方法的直接对比中，选取统一标准的有害指令集和攻击成功率指标，评估过程较为客观。结论得出JOOD能突破此前攻击方法无法攻破的模型，对比相对公平。
*   **充分性判断**：基于现有信息，实验设计在证明核心论点方面是充分的，但由于未获取全文，无法确认是否对每种变换、每个模型均做了详尽、多轮次的统计显著性检验。

## 6. 主要结论与发现
*   **漏洞证实**：大语言模型与多模态大语言模型的安全对齐确实存在显著的OOD脆弱性。通过将有害输入进行分布外化，即可大幅降低模型的恶意识别能力。
*   **攻击有效性**：提出的JOOD框架能有效利用该漏洞，成功越狱包括GPT-4和o1在内的最先进的闭源模型，且攻击成功率较高。
*   **简单方法的高效性**：即使是最简单的输入变换技术，也能对安全对齐造成严重威胁，表明当前对齐方法的鲁棒性有巨大提升空间。
*   **研究意义**：该工作不仅揭示了新的攻击面，更为后续开发更鲁棒的安全对齐算法提供了直接的测试基准和明确的研究方向。

## 7. 优点：方法或实验设计亮点
*   **问题新颖性**：首次系统性地从OOD鲁棒性角度探究大模型安全对齐的脆弱性，视角独特。
*   **方法简洁高效**：利用现成的、甚至极其简单的视觉/文本变换即实现了对顶尖模型的成功越狱，执行简单且攻击效果显著。
*   **突破性强**：成功攻破了GPT-4、o1等此前诸多攻击方法难以撼动的目标，证明了方法的实际威力和潜在风险。
*   **启示价值高**：研究结论直接指明了安全对齐未来需要重点强化的方向——提升对分布外输入的鲁棒泛化能力。
*   **可复现性**：公布了代码仓库，有利于社区的后续跟进与防御研究。

## 8. 不足与局限：实验覆盖、偏差风险、应用限制等
*   **防御考虑不足**：研究重心在攻击，尚未探讨如何从根本上修补此类OOD脆弱性，给出的防御启示较为宏观。
*   **攻击可察觉性**：部分OOD化操作可能会产生明显异常的模式，未来若部署输入检测器等外围防御，此类攻击的隐蔽性可能受到挑战，文中未加以探讨。
*   **实验广度**：虽测试了多个顶尖闭源模型，但受限于可获得的信息，无法评估对更多开源模型、更多样变换组合以及不同安全对齐版本的完整消融覆盖。
*   **伦理风险**：作为一种有效的越狱攻击方法，论文方法的公开必然带来潜在的恶意滥用风险，但作为安全性研究，其警示作用大于工具本身的风险。
*   **长期有效性**：文章未讨论该方法在模型安全对齐技术迭代更新后的持续有效性。

（完）
