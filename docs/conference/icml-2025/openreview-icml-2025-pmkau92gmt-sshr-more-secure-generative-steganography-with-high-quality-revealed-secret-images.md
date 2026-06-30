---
title: "SSHR: More Secure Generative Steganography with High-Quality Revealed Secret Images"
title_zh: SSHR：更高安全性的生成式高保真秘密图像隐写
authors: "Jiannian Wang, Yao Lu, Guangming Lu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=PMKAu92gMT"
tags: ["query:priv-sec"]
score: 4.0
evidence: 关注生成式隐写术的安全性，该技术可能被利用为漏洞。
tldr: 本文针对生成式隐写术安全性不足的问题，提出SSHR方法，通过改进扩散模型控制与中间状态一致性，增强隐写图像的抗检测性和秘密图像恢复质量，提升信息隐藏的安全性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有生成式隐写方法易被检测且秘密图像恢复质量差。
method: 设计SSHR，优化扩散模型提示控制与反演一致性，增强隐写安全性。
result: 实验表明生成的隐写图像更自然，抗检测性更强，恢复质量更高。
conclusion: 为基于扩散模型的隐写提供了更安全的方案，可能催生新的防御需求。
---

## Abstract
Image steganography ensures secure information transmission and storage by concealing secret messages within images. Recently, the diffusion model has been incorporated into the generative image steganography task, with text prompts being employed to guide the entire process. However, existing methods are plagued by three problems: (1) the restricted control exerted by text prompts causes generated stego images resemble the secret images and seem unnatural, raising the severe detection risk; (2) inconsistent intermediate states between Denoising Diffusion Implicit Models and its inversion, coupled with limited control of text prompts degrade the revealed secret images; (3) the descriptive text of images(i.e. text prompts) are also deployed as the keys, but this incurs significant security risks for both the keys and the secret images.To tackle these drawbacks, we systematically propose the SSHR, which joints the Reference Images with the adaptive keys to govern the entire process, enhancing the naturalness and imperceptibility of stego images. Additionally, we methodically construct an Exact Reveal Process to improve the quality of the revealed secret images. Furthermore, adaptive Reference-Secret Image Related Symmetric Keys are generated to enhance the security of both the keys and the concealed secret images. Various experiments indicate that our model outperforms existing methods in terms of recovery quality and secret image security.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
关注生成式隐写术的安全性，该技术可能被利用为漏洞。

### 2. 核心内容
本文针对生成式隐写术安全性不足的问题，提出SSHR方法，通过改进扩散模型控制与中间状态一致性，增强隐写图像的抗检测性和秘密图像恢复质量，提升信息隐藏的安全性。

### 3. 对应检索需求
security vulnerabilities of generative models。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=PMKAu92gMT](https://openreview.net/forum?id=PMKAu92gMT)
