---
title: "Silent Leaks: Implicit Knowledge Extraction Attack on RAG Systems"
title_zh: 静默泄露：针对RAG系统的隐式知识窃取攻击
authors: "Yuhao Wang, Wenjie Qu, Shengfang Zhai, Yanze Jiang, Liu Zichen, Yue Liu, Yinpeng Dong, Jiaheng Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=zfVICPB5Sv"
tags: ["query:priv-sec"]
score: 10.0
evidence: IKEA：通过良性查询对RAG进行隐式知识窃取攻击
tldr: 本文提出隐式知识提取攻击IKEA，利用锚概念生成自然外观的查询，绕开基于输入输出检测的防御机制，从RAG系统的知识库中隐式窃取敏感或版权内容。实验表明，该方法在不易察觉的前提下实现了高效的知识提取，对RAG系统的隐私和版权保护构成新型威胁。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有RAG提取攻击依赖恶意提示，易被检测，需要更隐蔽的攻击方式。
method: 利用锚概念生成良性查询，设计两种机制引导模型泄露内部知识。
result: IKEA在隐蔽性高的同时实现了高效的知识提取。
conclusion: RAG系统面临来自隐式查询的新型隐私/版权泄露风险，需增强防御。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems enhance large language models (LLMs) by incorporating external knowledge bases, but this may expose them to extraction attacks, leading to potential copyright and privacy risks.
However, existing extraction methods typically rely on malicious inputs such as prompt injection or jailbreaking, making them easily detectable via input- or output-level detection. 
In this paper, we introduce **I**mplicit **K**nowledge **E**xtraction **A**ttack (**IKEA**), which conducts *Knowledge Extraction* on RAG systems through benign queries.
Specifically, **IKEA** first leverages anchor concepts—keywords related to internal knowledge—to generate queries with a natural appearance, and then designs two mechanisms that lead anchor concepts to thoroughly "explore" the RAG's knowledge:
(1) Experience Reflection Sampling, which samples anchor concepts based on past query-response histories, ensuring their relevance to the topic; 
(2) Trust Region Directed Mutation, which iteratively mutates anchor concepts under similarity constraints to further exploit the embedding space.
Extensive experiments demonstrate **IKEA**'s effectiveness under various defenses, surpassing baselines by over 80% in extraction efficiency and 90\% in attack success rate. Moreover, the substitute RAG system built from **IKEA**'s extractions shows close performance to the original RAG and outperforms those based on baselines across multiple evaluation tasks, underscoring the stealthy copyright infringement risk in RAG systems.

---

## 论文详细总结（自动生成）

# 论文深度分析总结：静默泄露——针对RAG系统的隐式知识窃取攻击

## 1. 研究动机与核心问题
- **背景**：检索增强生成（RAG）系统通过引入外部知识库显著提升了大语言模型（LLM）的能力，但知识库中的私密或受版权保护的内容面临被窃取的风险。
- **现有攻击的缺陷**：当前的知识窃取手段多依赖恶意注入或越狱提示，这些恶意查询在输入和输出层面极易被基于规则或模型的检测机制拦截。
- **研究问题**：如何在不触发安全告警的前提下，通过**看似正常的查询**从RAG系统的内部知识库中高效窃取敏感信息，从而揭示一种更隐蔽、更危险的隐私与版权侵权路径。

## 2. 方法论：隐式知识窃取攻击（IKEA）
- **核心思想**：摒弃明显的攻击性语言，利用与目标知识紧密相关的“锚概念”（anchor concepts）生成外观自然、语义连贯的查询，诱使RAG系统在回答中无意泄露知识片段。
- **关键技术机制**：
    - **经验反思采样**：根据历史查询与系统响应的交互历史，通过反馈机制采样与当前主题高度相关的锚概念，避免查询偏离知识库核心内容。
    - **信任区域定向变异**：在嵌入空间中，以相似性约束对锚概念进行迭代变异，确保查询在语义上保持平滑迁移的同时，尽可能全面地覆盖和挖掘知识库中的不同区域。
- **攻击流程（抽象化）**：
    1. **锚概念初始化**：选定与目标私密知识相关的若干关键词。
    2. **良性查询生成**：围绕锚概念组织语言，生成表面无恶意的查询。
    3. **获取响应并反馈**：将查询发送至RAG系统，收集回答；利用经验反思采样筛选出更有效的锚概念，再通过信任区域变异扩展新的概念。
    4. **迭代循环**：重复上述步骤，不断“漫游”知识空间，逐步拼接出完整的内部知识。

## 3. 实验设计
- **评估场景**：在多种不同的防御机制下（如输入过滤、输出审核等）测试攻击有效性。
- **核心指标**：
    - **知识窃取效率**：从知识库中复原目标内容的比例。
    - **攻击成功率**：成功绕开检测并获取有效信息的查询占比。
    - **重建RAG质量**：利用窃取出的知识重建一个替代RAG系统，并在多项下游评估任务上比较其与原系统及基于其他攻击方法重建的系统的性能。
- **对比基线**：现有的恶意注入类、越狱类知识窃取攻击方法。
- **实验所涉数据**：论文摘要与元数据中未具体列明所使用的基准数据集名称，但从“多评估任务”的表述推断，可能涉及知识密集型问答（如Natural Questions、TriviaQA）或事实一致性等通用评测任务。

## 4. 资源与算力
- 提供的论文截取内容（元数据与摘要）**未明确说明实验所需的计算资源**，如GPU型号、数量、训练或攻击时长等均未提及，无法就此给出详细描述。

## 5. 实验数量与充分性
- 从摘要中的“大量实验（Extensive experiments）”、“多种防御下（under various defenses）”和“多项评估任务（across multiple evaluation tasks）”可推断，作者进行了多组对比与消融实验。
- 提供了具体的量化提升数据（窃取效率提升>80%，攻击成功率提升>90%），表明实验具有一定的统计说服力。但受限于提供的摘要，**无法精确得知具体的实验组数、消融实验覆盖的组件及统计方差**，整体充分性基于现有文本只能做间接推断。

## 6. 主要结论与发现
- **隐蔽性强且高效**：IKEA成功实现了在不易被察觉的前提下，对RAG知识库进行高覆盖率窃取，攻击效率远超现有方法。
- **防御机制被绕过**：基于输入恶意性检测和输出异常检测的常见防御策略在面对隐式攻击时基本失效。
- **重建系统性能逼近原版**：利用IKEA窃取的知识拼凑出的替代RAG系统，其表现已接近原始RAG，且显著优于基于旧有攻击方法构建的系统，证实了严重的隐式版权侵犯可行性。
- **新型风险警示**：RAG系统需警惕来自表面合规查询的内部知识泄露风险，现有安全范式存在明显盲区。

## 7. 优点与亮点
- **攻击范式创新**：首次将隐式查询用于知识窃取，脱离了“提示注入/越狱”的旧框架，拓宽了RAG攻击面的认知边界。
- **机制设计精巧**：经验反思采样与信任区域定向变异分别从语义连贯性和空间探索广度两个维度协同优化查询，既有理论支撑又具备工程可操作性。
- **实验论证立体**：不仅测量攻击直接效果，还通过构建替代RAG系统评估窃取知识的实用价值，使版权风险论证更具说服力。
- **安全启示深刻**：直接动摇了依赖表面检测的防御逻辑，为下一代更鲁棒的RAG安全机制指明了方向。

## 8. 不足与局限
- **实验细节缺失**：基于现有摘要无法获知具体的评测数据集、RAG架构选择、知识库规模与类型，以及详细的消融实验设计，可复现性和结论外推性存疑。
- **攻击假设未明**：未阐明攻击所需的知识前提（如是否需要部分先验知识选定锚概念）、对RAG系统的访问权限（黑盒或灰盒），以及检索器的类型是否影响成功率。
- **实际部署挑战**：攻击可能依赖于目标知识库的静态性和一定的主题聚焦度，在知识频繁更新、跨语言、跨模态或高度泛化的场景下的有效性有待考证。
- **伦理讨论缺位**：文中着重描述攻击细节与效果，对如何负责任地披露漏洞及缓解措施的具体设计着墨较少。

（完）
