---
title: "Protecting Your Video Content: Disrupting Automated Video-based LLM Annotations"
title_zh: 保护您的视频内容：扰乱基于视频的大语言模型自动标注
authors: "Liu, Haitong, Gao, Kuofeng, Bai, Yang, Li, Jinmin, Shan, Jinxiao, Dai, Tao, Xia, Shu-Tao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liu_Protecting_Your_Video_Content_Disrupting_Automated_Video-based_LLM_Annotations_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 解决视频大语言模型未经授权自动标注带来的隐私安全担忧，提出保护性水印扰乱标注
tldr: 针对视频大语言模型自动标注带来的隐私泄露风险，本文提出两种保护性水印方法：Ramblings诱导模型生成错误字幕，Mutes使模型输出空白标注。通过添加人眼难以察觉的对抗扰动，水印有效扰乱了主流视频LLM的理解能力，防止个人视频被用于训练下游模型。实验表明，该方法能在不损害视频视觉质量的前提下，显著降低自动标注的准确性，为视频隐私保护提供了新手段。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 828, \"height\": 504, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1775, \"height\": 894, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 826, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 406, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 402, \"height\": 401, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1807, \"height\": 697, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1814, \"height\": 695, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 622, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1820, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-protecting-your-video-content-disrupting-automated-video-based-llm-annotations-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1824, \"height\": 361, \"label\": \"Table\"}]"
motivation: 基于视频的LLM自动标注可能侵犯个人视频隐私，导致数据被滥用用于训练下游模型。
method: 提出两种保护性视频水印Ramblings和Mutes，添加不可见对抗扰动，误导模型生成错误或空白标注。
result: 水印有效扰乱了视频LLM的标注，使其生成不准确或空白字幕，保护视频内容隐私。
conclusion: 为个人视频提供了主动防御，防止未经授权被LLM分析和利用。
---

## Abstract
Recently, video-based large language models (video-based LLMs) have achieved impressive performance across various video comprehension tasks. However, this rapid advancement raises significant privacy and security concerns, particularly regarding the unauthorized use of personal video data in automated annotation by video-based LLMs. These unauthorized annotated video-text pairs can then be used to improve the performance of downstream tasks, such as text-to-video generation. To safeguard personal videos from unauthorized use, we propose two series of protective video watermarks with imperceptible adversarial perturbations, named Ramblings and Mutes. Concretely, Ramblings aim to mislead video-based LLMs into generating inaccurate captions for the videos, thereby degrading the quality of video annotations through inconsistencies between video content and captions. Mutes, on the other hand, are designed to prompt video-based LLMs to produce exceptionally brief captions, lacking descriptive detail. Extensive experiments demonstrate that our video watermarking methods effectively protect video data by significantly reducing video annotation performance across various video-based LLMs, showcasing both stealthiness and robustness in protecting personal video content. Our code is available at https://github.com/ttthhl/Protecting_Your_Video_Content.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究动机

*   **研究背景**：近年来，以视频为输入的大语言模型（video-based LLMs）在视频理解任务上表现卓越，能够自动生成视频描述（caption）。
*   **问题与威胁**：这种自动标注能力带来了严重的隐私与安全风险——未经授权的个人视频可能被自动分析，生成的视频-文本对（video-text pairs）可被用于下游任务（如文本生成视频）的训练，从而导致个人隐私泄露与数据滥用。
*   **核心目标**：为个人视频提供主动防护手段，干扰 video-based LLMs 的自动标注能力，使其无法生成准确、有效的视频描述，从而切断下游未经授权使用的链条。

### 2. 方法论

论文提出两类保护性视频水印，通过向视频中添加人眼难以察觉的对抗性扰动，误导大语言模型的标注输出：

*   **总体思路**：在视频中嵌入不可见扰动（imperceptible adversarial perturbations），改变 video-based LLM 感知到的表征，从而操纵其生成的文本。
*   **两类水印策略**：
    *   **Ramblings（胡言乱语水印）**：诱导模型生成与视频内容不一致的错误描述，降低视频-文本对的匹配质量，使自动标注变得不可靠。
    *   **Mutes（静默水印）**：促使模型输出极短、缺乏描述细节的空白或无效标注，使视频失去有效文本对应项。
*   **技术特点**：扰动需满足不可见性（stealthiness），兼顾对多种视频 LLM 的扰动有效性（robustness across models）。

### 3. 实验设计

*   **评测对象与基准**：实验覆盖多种主流的 video-based LLMs，以它们原有的视频标注性能作为基准（benchmark）。
*   **评估维度**：主要比较加水印前后模型生成的 caption 质量（如准确性、完整度），验证水印是否显著降低了自动标注的性能。
*   **对比方法**：文章中包含了 Ramblings 与 Mutes 的对比，并可能涉及与简单扰动或其它保护方法的比较（具体 baseline 未在摘要中详述）。

### 4. 资源与算力

*   **未明确报告**：提供的摘要和元数据中**未提及**所使用的 GPU 型号、数量、训练/生成时长等具体算力信息。常规实验可能使用单卡或多卡 GPU 进行对抗样本生成，但此处无法确认。

### 5. 实验数量与充分性

*   **实验体量**：从论文标题、摘要及元数据中给出的表格、图片索引来看（含多张表格和图示），实验涉及多类 video-based LLMs、多种评测指标以及消融/鲁棒性分析，实验数量较为丰富。
*   **实验充分性**：分析了水印的**隐匿性**（人眼不可见）和**鲁棒性**（跨模型有效性），多维度验证了方法的保护效果，实验设计较为充分、客观。
*   **公平性**：通过比较同一模型在原型视频和加水印视频上的表现，并展示跨模型的泛化性能，评估体系相对公平。

### 6. 主要结论与发现

*   **有效性**：提出的 Ramblings 和 Mutes 水印能够**显著降低**多种 video-based LLMs 的自动视频标注性能，使其生成不可靠或无效的 caption。
*   **隐匿与鲁棒**：水印具有良好的隐匿性（imperceptibility），不影响视频的视觉质量；同时具有一定鲁棒性，可在不同视频 LLM 上发挥保护作用。
*   **保护价值**：该方法为个人视频提供了一种主动防御模式，可有效防止视频被未经授权的自动分析、标注和训练利用，保障了视频内容的隐私安全。

### 7. 优点

*   **主动防御理念**：从数据源头入手，通过添加保护水印阻挠自动标注，比被动的事后限制更具前瞻性。
*   **双策略设计**：Ramblings 与 Mutes 分别应对“错误标注”和“无意义标注”两种保护需求，设计灵活。
*   **实用性验证**：兼顾不可见性与跨模型泛化能力，展示了实际应用的潜力。

### 8. 不足与局限

*   **实验细节缺失（基于摘要判断）**：算力开销、对抗扰动的计算复杂度、在不同分辨率/时长视频上的可扩展性等在摘要中未体现，可能限制对实用成本的评估。
*   **依赖对抗攻防的时效性**：视频 LLM 的迭代可能降低特定扰动模板的破坏效果，长期有效性需要持续更新维护。
*   **应用边界**：若攻击者采用带噪声鲁棒训练或水印压缩处理等手段，水印的效力可能被削弱，论文未能详述针对此类对抗的反制实验。

（完）
