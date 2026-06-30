---
title: Adversaries Can Misuse Combinations of Safe Models
title_zh: 对手可利用安全模型的组合进行滥用
authors: "Erik Jones, Anca Dragan, Jacob Steinhardt"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=GCkhEPE1FG"
tags: ["query:priv-sec"]
score: 9.0
evidence: 单个安全模型的组合可被滥用于恶意任务
tldr: 当前 AI 安全评估单独测试每个模型，本文揭示了一种新威胁：即使每个模型单独安全，通过任务分解将智能任务分配给不同模型，攻击者可组合出恶意系统。研究考察人工与自动分解两种方式，证明这一漏洞普遍存在，呼吁更全面的系统性安全评估。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 单独测试无法发现组合模型中潜在的恶意协同风险。
method: 通过将恶意任务分解为子任务，分配给最适合的模型，演示组合滥用攻击。
result: 组合安全模型能成功执行原本单个模型无法完成的恶意任务。
conclusion: 安全评估必须考虑模型互操作带来的系统性漏洞。
---

## Abstract
Developers try to evaluate whether an AI system can accomplish malicious tasks before releasing it; for example, they might test whether a model enables cyberoffense, user manipulation, or bioterrorism. In this work, we show that individually testing models for such misuse is inadequate; adversaries can misuse combinations of models even when each individual model is safe. The adversary accomplishes this by first decomposing tasks into subtasks, then solving each subtask with the best-suited model. For example, an adversary might solve challenging-but-benign subtasks with an aligned frontier model, and easy-but-malicious subtasks with a weaker misaligned model. We study two decomposition methods: manual decomposition where a human identifies a natural decomposition of a task, and automated decomposition where a weak model generates benign tasks for a frontier model to solve, then uses the solutions in-context to solve the original task. Using these decompositions, we empirically show that adversaries can create vulnerable code, explicit images, python scripts for hacking, and manipulative tweets at much higher rates with combinations of models than either individual model. Our work suggests that even perfectly-aligned frontier systems enable misuse without ever producing malicious outputs, and that red-teaming efforts should extend beyond single models in isolation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：当前 AI 发布前的安全评估通常仅对单个模型进行恶意任务测试（例如能否协助网络攻击、用户操纵或生物恐怖主义）。然而，这种孤立测试可能忽略了多个模型协同工作时产生的全新滥用风险。
- **整体含义**：本文揭示了一种新的威胁模型——“组合滥用”。即使每个模型单独看都是安全的，攻击者仍可以通过将恶意任务分解为多个子任务，并分别交由最擅长该子任务的模型完成，最终组合出一个具备整体恶意能力的系统。这意味着，即使前沿模型被完美对齐、自身从不输出有害内容，其正常功能仍可能被恶意利用，形成系统性漏洞。因此，红队测试和安全评估必须超越单模型视角，转向考虑模型互操作带来的安全性问题。

## 2. 论文提出的方法论

- **核心思想**：攻击者不直接让单个模型完成整个恶意任务，而是**将复杂恶意任务分解**为多个子任务，每个子任务本身可能是良性的或危险性较低，然后调用最适合的模型分别解决。
- **两种任务分解方法**：
  - **人工分解**：由人类专家根据任务特性，识别出自然的分解结构，手动将恶意任务拆分为一系列子任务。
  - **自动分解**：利用一个较弱（或能力较低）的模型自动生成一系列看似良性的子任务，这些子任务交给对齐良好的前沿模型去执行；然后，弱模型会收集前沿模型给出的子任务解答，并将其作为上下文，用以最终完成原本的恶意任务。自动分解完全不需要人工介入，降低了攻击门槛。
- **关键技术流程**：
  - 给定恶意目标 \( T \)。
  - 分解模块（人或弱模型）输出子任务序列 \( \{t_1, t_2, ..., t_k\} \)。
  - 对于每个子任务 \( t_i \)，选择最优模型 \( M_i \) 执行（可能包括对齐的前沿模型、不可对齐的弱模型等）。
  - 将各子任务的输出组合，得到最终恶意结果 \( R \)。整个过程使得前沿模型输出的仅是良性中间结果，本身不违反安全策略，但组合后却构成有害输出。

## 3. 实验设计

- **评估场景/基准**：论文构建了多个具有代表性的恶意任务来测试组合滥用的成功率。具体包括：
  - 生成带有漏洞的代码
  - 生成露骨/色情图片
  - 生成用于黑客攻击的 Python 脚本
  - 生成具有操纵性的社交媒体推文
- **对比方法**：主要比较以下三种设置下的任务成功率：
  - 仅使用单个安全模型（例如对齐的前沿模型）直接完成恶意任务。
  - 仅使用单个不安全模型（例如能力较弱但缺乏对齐的模型）直接完成。
  - **组合方案**：将任务分解后，部分子任务用安全模型处理，部分用不安全模型处理，最后组合。
- **核心指标**：恶意任务成功执行的比率，用以证明组合方式显著优于任何单一模型。

## 4. 资源与算力

- 论文摘要及元数据中**未明确给出**所使用的 GPU 型号、数量、训练或推理时长等信息。由于该项研究侧重于评估现有模型的组合行为，而非从头训练，所需算力主要来自对黑盒 API 模型的调用，具体消耗未详细披露。

## 5. 实验数量与充分性

- **实验组数**：根据摘要描述，实验覆盖了至少四种不同类型的恶意任务（漏洞代码、色情图片、黑客脚本、操纵推文），并在人工分解和自动分解两种模式下均进行了测试。虽然未列出具体消融实验细节，但多任务、多分解方式的设计已能支撑核心主张。
- **充分性与客观性**：实验通过对比单模型与组合模型的成功率，直观展示了组合滥用的有效性。任务选择横跨代码、图像、文本等多种模态，增强了结论的普适性。但摘要未提及是否进行了统计学显著性检验，也未明确任务样本量，因此严谨性需待全文验证。整体设计较为客观，对比基线合理。

## 6. 论文的主要结论与发现

- 单独测试模型的安全性是不充分的：即使每个模型在独立测试中都不会产生有害输出，通过组合，攻击者仍可达成恶意目的。
- 成功演示了利用“安全模型”完成部分子任务来间接实现整体恶意任务：前沿模型从未直接生成恶意内容，但输出了足以被滥用的中间结果。
- 自动分解方法的可行性意味着，这种组合滥用攻击可以低成本、规模化地实施，不需要使用者具备高深的领域知识。
- 该发现呼吁 AI 社区重新思考安全性评估的标准：红队测试和相关政策必须将系统的多模型互操作性纳入考虑，否则会形成巨大的安全盲区。

## 7. 优点

- **视角新颖**：首次系统性地提出并验证了“组合安全模型可用于恶意目的”这一威胁，跳出了单一模型安全的传统框架。
- **方法简洁有力**：任务分解与模型分配的逻辑清晰，特别是自动分解方法降低了对人工攻击者的技能要求，现实威胁性更高。
- **实验多样性强**：覆盖了多种恶意任务类型和两种分解策略，增强了说服力。
- **实际意义显著**：直接挑战了当前业界普遍采用的“逐个模型红队测试”的范式，对安全评估实践有指导意义。

## 8. 不足与局限

- **技术细节披露有限**：从现有摘要无法得知自动分解的具体实现算法、提示词设计、以及弱模型与前沿模型的具体配置，这影响了方法的可复现性判断。
- **算力与资源限制未说明**：缺乏对实验规模的描述，难以评估结论在不同规模模型上的泛化性。
- **攻击防御措施的探讨欠缺**：论文主要揭露了漏洞，但未深入讨论可能的缓解方法（如输出监控、组合行为检测），实践指导有待完善。
- **任务范围可能受限**：虽已覆盖多种任务，但恶意任务空间极大，现实中更复杂的多步攻击是否同样有效尚待验证。
- **组合方式的局限性**：实验假设攻击者能够自由组合不同模型，但在部分实际部署环境中（如仅开放单一 API），该攻击的可行性会下降，论文尚未讨论这种环境约束。

（完）
