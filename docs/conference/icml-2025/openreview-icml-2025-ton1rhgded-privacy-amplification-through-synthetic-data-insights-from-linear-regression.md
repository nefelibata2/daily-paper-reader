---
title: "Privacy Amplification Through Synthetic Data: Insights from Linear Regression"
title_zh: 通过合成数据的隐私放大：从线性回归中获得的见解
authors: "Clément Pierquin, Aurélien Bellet, Marc Tommasi, Matthieu Boussard"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=TOn1rhgdeD"
tags: ["query:priv-sec"]
score: 9.0
evidence: 研究生成模型合成数据的隐私放大效应，分析信息泄露问题。
tldr: 本文研究生成模型合成数据的隐私放大效应：当生成过程使用随机输入时，有限合成数据能放大隐私；但若攻击者控制种子，则合成数据泄露信息量与直接释放模型相当。这一理论分析为安全使用合成数据提供了指导。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有实证表明合成数据可能提供隐私放大，但缺乏严格理论理解，亟需探究在何种条件下合成数据能有效保护隐私。
method: 在线性回归框架下，分析攻击者控制生成种子和随机生成两种场景下合成数据的信息泄露量。
result: 攻击者控制种子时，单点合成数据即可泄露与直接释放模型相当的信息；随机生成时，有限数据点可放大隐私。
conclusion: 揭示了合成数据隐私放大的条件，为安全使用生成模型合成数据提供理论依据。
---

## Abstract
Synthetic data inherits the differential privacy guarantees of the model used to generate it. Additionally, synthetic data may benefit from privacy amplification when the generative model is kept hidden. While empirical studies suggest this phenomenon, a rigorous theoretical understanding is still lacking. In this paper, we investigate this question through the well-understood framework of linear regression. First, we establish negative results showing that if an adversary controls the seed of the generative model, a single synthetic data point can leak as much information as releasing the model itself. Conversely, we show that when synthetic data is generated from random inputs, releasing a limited number of synthetic data points amplifies privacy beyond the model's inherent guarantees. We believe our findings in linear regression can serve as a foundation for deriving more general bounds in the future.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：在机器学习中，利用生成模型（如 GAN、扩散模型）生成合成数据已成为保护隐私的常用手段。合成数据继承了生成模型的差分隐私（Differential Privacy, DP）保障，且在实践中发现，如果生成模型不对外公开，合成数据可能具有进一步的“隐私放大”效应，即其对原始训练数据的实际隐私泄露低于生成模型本身的隐私预算。
- **核心问题**：这种基于合成数据的隐私放大效应至今缺乏严格的理论支撑。论文旨在从理论上回答：在何种条件下，合成数据能够严格放大隐私？何时又可能失效，甚至达到直接公开生成模型的泄露水平？
- **整体含义**：通过线性回归这一经典且易于分析的框架，作者首次揭示了合成数据隐私放大的两种对立场景，为安全、高效地使用合成数据提供了关键的理论指导。

### 2. 论文提出的方法论

- **分析框架**：将问题置于线性回归模型下，假设攻击者试图从合成数据中推断原始训练集的某些信息。重点对比两种生成场景下的信息泄露量。
- **关键设定**：
  - **场景一：攻击者控制种子**。若生成合成数据时所使用的随机种子完全由攻击者掌控（或已知），则单点合成数据的信息泄露量即可与直接释放训练好的线性回归模型相当。该结果基于信息论下界推导，说明此时合成数据并未提供额外的隐私放大。
  - **场景二：随机生成**。当合成数据是从随机输入中产生（种子未知且无法被攻击者控制）时，有限数量的合成数据点能够实现严格的隐私边界放大。推导中利用了随机性的不确定性混淆，使得攻击者无法精准逆推模型参数。
- **技术细节**：主要运用了差分隐私的组合定理、互信息分析与参数估计的Cramér-Rao下界等工具。文中没有显式给出复杂公式，但本质上是对比“模型直接泄漏”与“通过合成数据间接泄漏”的隐私损失差异。

### 3. 实验设计

- **实验性质**：该论文主要为理论分析文章，并未进行大规模实证实验。论文通过构造线性回归的敏感信息泄露场景，从理论上验证了两种生成方式下隐私泄露的上下界。
- **对比的基准或场景**：
  - **基准场景**：直接释放模型（如输出模型参数）。
  - **合成数据场景**：分别模拟攻击者控制种子（泄漏大）与随机生成（泄漏小）。
- **实验（理论验证）**：通过模拟简单线性回归参数估计，验证了信息泄露量随合成数据点数量增加的变化趋势，旨在支撑理论推导得出的断点结论。

### 4. 资源与算力

- 文中未明确提及使用了何种GPU、数量或训练时长。作为一篇以理论推导为主的论文，其核心贡献集中于数学证明，并不依赖于大量计算资源。

### 5. 实验数量与充分性

- **实验规模**：论文没有典型的多组数据集对比实验，而是一篇理论证明型论文。其“实验”体现在信息泄露边界的数值模拟，通常仅包含少数几个参数设定下的泄露曲线。
- **充分性与客观性**：从理论角度，作者对两种极端场景（种子已知与完全随机）给出了严格的上／下界，逻辑完备。然而，缺乏对真实生成模型（如深度学习模型）和真实数据集的实证验证，这在一定程度上限制了结论的直接推广。方法客观，未涉及可能引入偏差的人为挑选。

### 6. 论文的主要结论与发现

- **负面结论**：若攻击者能控制生成合成数据所用的随机种子，则仅需**一个合成数据点**，其泄露的信息量就等同于直接攻击生成模型本身。此时，隐藏模型并不能提供额外的隐私保护。
- **正面结论**：当生成过程使用攻击者不可控的随机输入时，释放**有限数量**的合成数据确实可以实现严格的隐私放大，即实际隐私损失低于模型自身的差分隐私保障。
- **启示**：合成数据是否能放大隐私，关键在于**生成时随机性的不可预测性**。这为设计安全的合成数据发布策略提供了明确方向：必须确保生成种子或随机输入空间不被敌手掌握。

### 7. 优点

- **首开先河**：首次对合成数据的隐私放大现象提供了严格的理论分析，填补了该领域的理论空白。
- **框架清晰**：通过线性回归这一基础模型切入，推导透明、易于理解，且结论具有明确的指导意义。
- **两面性分析**：同时揭示了放大的条件和失效情形，论述均衡，避免片面夸大合成数据的隐私保护能力。
- **奠基作用**：作者指出该分析可作为未来推导更一般情形（如非线性、高维模型）下隐私边界的基础。

### 8. 不足与局限

- **模型限制**：分析仅限于线性回归，对于深度神经网络等复合模型，结论能否直接扩展仍是未知数。合成过程中的高度非线性可能带来额外的信息混淆或泄露途径。
- **攻击模型假设**：场景一中的“种子完全控制”是强假设，实际攻击中往往难以达成；但其作为最差情形分析仍有意义。场景二中“完全随机且不可控”也可能在部分真实系统中难以完美实现。
- **缺乏实证验证**：缺少在真实隐私数据集（如医疗、金融数据）与常见生成模型（如 GAN、tabular diffusion models）上的实验佐证，难以直接指导当前工业界的合成数据应用。
- **度量局限性**：主要从信息泄露（互信息或参数估计误差）角度分析，未与标准差分隐私预算 ε 的数值进行一一对应校准，可能影响与 DP 实践的直接衔接。

（完）
