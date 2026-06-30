---
title: Exploring and Mitigating Adversarial Manipulation of Voting-Based Leaderboards
title_zh: 探究及缓解基于投票的排行榜的对抗操纵
authors: "Yangsibo Huang, Milad Nasr, Anastasios Nikolas Angelopoulos, Nicholas Carlini, Wei-Lin Chiang, Christopher A. Choquette-Choo, Daphne Ippolito, Matthew Jagielski, Katherine Lee, Ken Liu, Ion Stoica, Florian Tramèr, Chiyuan Zhang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=zf9zwCRKyP"
tags: ["query:priv-sec"]
score: 8.0
evidence: 揭示并缓解了对基于投票的LLM排行榜的对抗操纵
tldr: 针对LLM社区依赖的基于人工投票的排行榜，本研究发现其面临对抗操纵的风险，攻击者可系统性地影响排名结果。作者在展示攻击可行性的同时，提出了一系列防护措施以加强排行榜的公正性。实验表明，若无适当防御，排行榜容易受到严重操纵，该工作为LLM评估生态的安全性提供了重要警示和改进方向。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 基于人工投票的LLM排行榜被认为是公平准确的，但其易受恶意操纵的漏洞未被充分研究。
method: 揭示攻击者可利用漏洞人为改变排行榜排名，并提出相应的防御措施。
result: 实验显示攻击可有效操纵排行榜顺序；所提防御能显著减轻操纵影响。
conclusion: 该研究揭示了LLM评价系统的新安全威胁，强调了加强排行榜完整性的必要性。
---

## Abstract
It is now common to evaluate Large Language Models (LLMs) by having humans manually vote to evaluate model outputs, in contrast to typical benchmarks that evaluate knowledge or skill at some particular task. Chatbot Arena, the most popular benchmark of this type, ranks models by asking users to select the better response between two randomly selected models (without revealing which model was responsible for the generations).  These platforms are widely trusted as a fair and accurate measure of LLM capabilities. In this paper, we show that if bot protection and other defenses are not implemented, these voting-based benchmarks are potentially vulnerable to adversarial manipulation. Specifically, we show that an attacker can alter the leaderboard (to promote their favorite model or demote competitors) at the cost of roughly a thousand votes (verified in a simulated, offline version of Chatbot Arena). Our attack consists of two steps: first, we show how an attacker can determine which model was used to generate a given reply with more than $95\%$ accuracy; and then, the attacker can use this information to consistently vote for (or against) a target model. Working with the Chatbot Arena developers, we identify, propose, and implement mitigations to improve the robustness of Chatbot Arena against adversarial manipulation, which, based on our analysis, substantially increases the cost of such attacks. Some of these defenses were present before our collaboration, such as bot protection with Cloudflare, malicious user detection, and rate limiting. Others, including reCAPTCHA and login are being integrated to strengthen the security in Chatbot Arena.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：当前评估大语言模型（LLM）的一种主流方式是基于人工投票的排行榜（如 Chatbot Arena），用户从匿名成对的回答中选出更优者，以此生成排名。这类平台被广泛视为公平、准确的模型能力衡量标准。
- **核心问题**：论文揭示了此类排行榜在缺少有效的 bot 防护及其他防御机制时，极易遭受**对抗性操纵**——攻击者能够系统性地操控投票结果，抬高自己的模型或打压竞争对手。
- **整体含义**：研究并非否定投票式评测本身，而是强调其完整性高度依赖底层安全防御；若防御缺位，排行榜的公正性将受到严重威胁，从而动摇 LLM 评价生态的可信度。

### 2. 论文提出的方法论
- **攻击方法（操纵排行榜）**：
  - 攻击分为两个阶段：
    1. **模型归属推断**：攻击者首先需要识别出匿名回答是由哪个模型生成的。论文实现了一种方法，可以达到 **超过 95% 的准确率**。
    2. **定向投票**：在掌握模型归属信息后，攻击者持续为目标模型投出赞成票（或给对手投反对票），从而达到人为操纵排名的目的。
  - **攻击成本**：在模拟的离线版 Chatbot Arena 中，仅需大约**一千次投票**即可显著改变排行榜顺序。
- **防御方法（与开发者合作提出并实施）**：
  - **原有防护**：在合作之前，平台已部署 Cloudflare 的 bot 保护、恶意用户检测、速率限制等。
  - **新增/强化防护**：引入 **reCAPTCHA** 验证、**强制用户登录** 等机制，结合原有防御，大幅提高了攻击方的执行成本和被检测风险。

### 3. 实验设计
- **评估场景与数据集**：实验在**模拟的离线版 Chatbot Arena** 中进行，该环境忠实复现了真实平台的成对投票与排名机制。论文未提及外部独立的数据集或 benchmark。
- **对比方法**：攻击评估主要对比**有无防御措施**下的操纵效果，例如观察攻击所需投票数、排名被改变的程度。防御层面则为一系列方案（bot 检测、登录、验证码等）的组合与叠加效果，而非与其他学术性防御框架的横向比较。

### 4. 资源与算力
- 论文摘要及提供的元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长等信息。从任务性质推断，模型归属推断可能涉及对 LLM 输出的分类或比对，但所需算力未被量化；攻击和防御的主要开销在于模拟投票与判定的流程，并非大规模模型训练，因此可能对计算资源要求较低。

### 5. 实验数量与充分性
- **实验数量**：从现有信息推测，实验主要包括：
  - 模型归属推断准确率的验证实验；
  - 在不同票数下操纵排行榜效果的模拟实验（展示 ~1000 票即可篡改排名）；
  - 防御措施启用前后攻击成功率的对比实验。
- **充分性与公平性**：
  - **充分性**：基于离线模拟平台的实验能够控制变量并重复验证，较为严谨地证明了攻击的可行性与防御的有效性。但真实线上环境存在更多噪声和未知变量，模拟实验的结论仅为参考。
  - **公平性**：对比主要围绕“无防御 vs. 有防御”，属自对比较，未涉及其他攻击类型或第三方防御方案，客观性受限于平台合作背景。

### 6. 论文的主要结论与发现
- 在缺乏适当防御时，基于投票的 LLM 排行榜是**高度可操纵的**，仅需约一千次定向投票便可颠覆排名。
- 通过多层次的防御组合（Bot 检测、速率限制、验证码、登录机制等）能够**大幅度提高攻击的成本与复杂度**，显著加强排行榜的稳健性。
- 该研究为 LLM 评估社区敲响了安全警钟：对排行榜的信任必须以坚实的安全措施为前提，不能将投票完整性视为理所当然。

### 7. 优点
- **问题现实且紧迫**：直指当前 LLM 评估生态中被忽视的安全盲点，与时下热门的排行榜实践高度相关。
- **攻击方法清晰，成本量化**：将攻击分解为两步，并给出具体的准确率和票数门槛，直观展示了漏洞的严重性。
- **实际影响力**：与 Chatbot Arena 开发团队直接合作，部分防御措施已在实际系统中部署或计划集成，研究直接推动了平台的加固。
- **兼顾攻防**：既展示了攻击的威胁，也提出了相应的缓解方案，构成完整的“发现问题-解决问题”链路。

### 8. 不足与局限
- **实验环境与真实环境的差距**：所有实验均在离线模拟环境完成，真实世界的攻击者可能采用更隐蔽、更复杂的策略（如分布式僵尸网络、社会工程学等），模拟结果未必能完全反映线上防御的实际有效性。
- **防御方案的泛化性**：提出的防御措施（如登录、reCAPTCHA）依赖特定平台实现，未讨论这些措施对用户体验、平台开放性带来的潜在影响，也未探讨攻击者针对这些单项防御的绕过技术。
- **缺乏同类方法的横向比较**：未将所提攻击与其他可能的排行操纵攻击（如模型输出注入、合谋刷票）进行对比，也未比较不同的抗操纵框架。
- **算力细节缺失**：无法判断攻击所需的计算开销，尤其模型归属推断模块的实际训练或推理成本未知。
- **范围局限于投票式排行榜**：结论是否可推广到其他类型的众包评估（如评分制、Elo 变体等）没有展开讨论。

（完）
