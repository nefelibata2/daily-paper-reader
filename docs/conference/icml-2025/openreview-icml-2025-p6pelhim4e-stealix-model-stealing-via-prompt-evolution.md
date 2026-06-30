---
title: "Stealix: Model Stealing via Prompt Evolution"
title_zh: Stealix：通过提示进化的模型窃取
authors: "Zhixiong Zhuang, Hui-Po Wang, Maria-Irina Nicolae, Mario Fritz"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=p6PElhIM4E"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过自动提示进化的模型窃取对大语言模型构成安全威胁
tldr: 本文提出Stealix，一种无需预定义提示的模型窃取方法，通过进化提示来自动化攻击过程。该方法显著降低了对攻击者专业知识的要求，成功从黑盒模型中窃取模型功能，凸显了开放预训练模型面临的严重安全威胁，对LLM部署安全有警示意义。该工作还揭示了攻击者利用开源预训练模型进行知识迁移的风险，呼吁加强对模型访问的控制。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 模型窃取攻击威胁黑盒模型知识产权，现有方法依赖手工提示缺乏可扩展性。
method: 提出Stealix，利用提示进化在不预定义提示下实现模型窃取。
result: Stealix能有效窃取预训练模型，无需提示设计技能。
conclusion: 暴露了开放预训练模型的安全风险，需加强模型保护。
---

## Abstract
Model stealing poses a significant security risk in machine learning by enabling attackers to replicate a black-box model without access to its training data, thus jeopardizing intellectual property and exposing sensitive information.
Recent methods that use pre-trained diffusion models for data synthesis improve efficiency and performance but rely heavily on manually crafted prompts, limiting automation and scalability, especially for attackers with little expertise.
To assess the risks posed by open-source pre-trained models, we propose a more realistic threat model that eliminates the need for prompt design skills or knowledge of class names.
In this context, we introduce Stealix, the first approach to perform model stealing without predefined prompts. Stealix uses two open-source pre-trained models to infer the victim model’s data distribution, and iteratively refines prompts through a genetic algorithm, progressively improving the precision and diversity of synthetic images.
Our experimental results demonstrate that Stealix significantly outperforms other methods, even those with access to class names or fine-grained prompts, while operating under the same query budget. These findings highlight the scalability of our approach and suggest that the risks posed by pre-trained generative models in model stealing may be greater than previously recognized.

---

## 论文详细总结（自动生成）

# 论文总结：Stealix: Model Stealing via Prompt Evolution

## 1. 核心问题与研究意义
- **研究背景**：模型窃取攻击（Model Stealing）允许攻击者在无训练数据、仅通过查询接口的情况下复制一个黑盒模型，严重威胁模型的知识产权与敏感信息。
- **现有方法的局限**：近期利用预训练扩散模型进行数据合成的方法虽提升了效率与性能，但极度依赖人工设计的提示（prompt），难以自动化与规模化，对缺乏领域知识的攻击者尤为不友好。
- **本文动机**：为更真实地评估开放预训练模型带来的安全风险，本文重新定义了威胁模型——攻击者无需掌握提示设计技能或类别名称，仅凭开源预训练模型即可完成攻击，从而暴露了比以往认知更严重的安全缺口。

## 2. 方法论
- **核心思想**：提出 **Stealix**，一种在完全不依赖预定义提示的情况下执行模型窃取的自动化方法。它通过进化算法让提示“自我优化”，逐步逼近受害者模型的数据分布，合成越来越精准且多样的查询图像。
- **关键技术细节**：
    - 利用 **两个开源预训练模型** 协同推断受害者模型的数据分布，作为提示进化的起点与约束。
    - 采用 **遗传算法** 迭代优化提示：在每一代中，基于当前提示生成合成图像，查询受害者模型获取标签，根据响应质量评估提示的适应度（fitness），再通过交叉、变异操作产生新一代提示。
    - 整个过程无需人工介入，自动实现从模糊分布到高保真分布的跃迁，最大化合成数据的有效性与多样性。
- **算法流程**（文字归纳）：
    1. 初始化：用预训练模型推断初始提示集合。
    2. 循环进化：生成图像 → 查询黑盒模型 → 计算适应度 → 选择、交叉、变异 → 更新提示池。
    3. 训练复制模型：用进化得到的最佳提示生成大规模数据集，训练一个功能近似的替代模型。

## 3. 实验设计
- **任务场景**：图像分类任务的模型窃取攻击。
- **基准方法（Benchmark）**：对比了其他需要手工提示的模型窃取方案，包括使用 **类别名称** 或 **细粒度提示** 的先前工作（摘要中未列出具体方法名，根据上下文可知为依赖预定义提示的生成式攻击）。
- **约束条件**：所有方法在 **相同的查询预算** 下进行比较，以确保公平。
- **数据集**：摘要未具体说明所用数据集，但通常涉及与预训练扩散模型兼容的标准分类数据集（如 ImageNet 子集等，需查阅正文以确认）。

## 4. 资源与算力
- 文中（提供的摘要及元数据）**未明确说明** 所使用的 GPU 型号、数量或训练时长。评估算力需求需参考正式论文的完整版本。

## 5. 实验数量与充分性
- 摘要仅展示了整体对比结果，指出 Stealix 在相同查询预算下“显著优于其他方法，包括那些有权使用类别名或细粒度提示的方法”。
- **实验覆盖度推测**：可能包含多组数据集、不同预算设置、消融实验（如验证提示进化各组件的作用）等，但 **当前提供的内容未详细展开**。
- **客观性评价**：比较对象均被置于同等查询预算下，且包括了享有更多先验知识的强基线，实验设计相对公平。但由于缺少具体实验规模、方差分析等细节，**无法完整评判其充分性**。

## 6. 主要结论与发现
- **有效性**：Stealix 无需任何提示设计技能，成功实现了高质量模型窃取，效果甚至超越了那些依赖人工提示或类别名称的现有方法。
- **安全警示**：该成果揭示了一个被低估的威胁——开放预训练生成模型极大降低了模型窃取的门槛，攻击者可利用现成的开源模型，以零专业知识完成攻击。
- **启示**：模型提供方需重新审视访问控制，加强对黑盒查询的防护，并认识到预训练模型生态中“知识迁移”可能带来的新型盗用风险。

## 7. 亮点与优点
- **高度自动化**：首次实现零提示设计的模型窃取，将攻击流程彻底自动化，可扩展性极强。
- **攻击能力超越基线**：在信息劣势（无类别名称、无手工提示）下，仍显著优于拥有更多先验知识的攻击方法，证明了提示进化策略的高效。
- **真实威胁模型**：贴合攻击者实际能力，为社区敲响警钟，推动防御技术的针对性研究。
- **方法论创新**：将遗传算法引入提示优化，摆脱对手工专家知识的依赖，思路新颖且可迁移至其他生成式攻击场景。

## 8. 不足与局限
- **黑盒依赖**：攻击效果受限于所采用的开源预训练模型质量与受害者模型数据分布的吻合程度，若分布偏差过大，进化可能难以收敛。
- **查询成本**：尽管在固定预算下效果最佳，但进化过程本身仍需要大量查询，对严格限次查询的场景可能不够隐蔽。
- **实验细节透明度**：从当前摘要无法获知实验的具体设置（数据集种类、预算范围、方差报告等），方法的鲁棒性和统计显著性尚需完整论文验证。
- **威胁范围**：主要针对使用预训练生成模型合成的图像分类任务，对于非图像模态或更复杂的模型结构的窃取能力未作探讨。
- **防御评估缺失**：摘要未涉及在有防御措施（如查询扰动、输出模糊）下的表现，现实部署中的可行性有待进一步分析。

（完）
