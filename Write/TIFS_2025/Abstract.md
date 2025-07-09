# 1. 摘要

## 参考内容

>  ### PRNet
>
> 感知加密是一种有效的方法，仅通过选择性地加密部分图像中的一部分重要数据来保护图像内容。对感知加密的现有安全分析通常诉诸传统的密码分析技术，这些技术需要大量的手动工作和严格的加密方案知识。在本文中，我们介绍了一种新的端到端方法，用于分析感知加密图像的视觉安全性，而无需任何手动工作或了解加密方案的任何先验知识。具体而言，通过利用卷积神经网络（CNN），我们建议渐进恢复网络（PRNET）从感知加密的图像中恢复视觉内容。我们的PRNET堆叠着几个密集的注意恢复块（DARBS），其中每个DARB包含两个分支：特征提取分支和图像恢复分支。这两个分支合作恢复了更详细的视觉信息，并通过密集连接的结构和双重校正机制来产生有效的特征表示。我们进行了广泛的实验，以证明PRNET在具有不同设置的不同感知加密方案上起作用，结果表明，PRNET显着优于最先进的基于CNN的图像恢复方法。
>
> ### SwinIR
>
> 图像恢复是一个长期存在的低级视力问题，旨在从低质量图像（例如，缩小，嘈杂和压缩图像）恢复高质量的图像。尽管最先进的图像恢复方法是基于卷积神经网络的，但对于在高级视觉任务上表现出令人印象深刻的性能的变压器几乎没有尝试。在本文中，我们提出了一个强大的基线模型Swinir，用于基于Swin Transformer的图像恢复。 Swinir由三个部分组成：浅层提取，深度提取和高质量的图像重建。特别是，深色特征提取模块由几个残留的SWIN变压器块（RSTB）组成，每个型SWIN变压器块（RSTB）都有几个Swin Transformer层以及残留的连接。我们对三个代表性任务进行实验：图像超分辨率（包括经典，轻质和现实图像超分辨率），图像DeNoising（包括灰度和颜色图像DeNoising）和JPEG压缩工件减少。实验结果表明，Swinir在不同任务上的最先进方法高达0.14〜0.45dB，而参数的总数最多可以降低67％。
>
> ### RCAN
>
> 卷积神经网络（CNN）深度对于图像超分辨率（SR）至关重要。但是，我们观察到图像SR的更深层次的网络更难训练。低分辨率输入和特征包含丰富的低频信息，该信息在跨通道上平等处理，因此阻碍了CNN的代表性。为了解决这些问题，我们提出了非常深的残留渠道注意网络（RCAN）。具体而言，我们建议在残留（RIR）结构中的残留物形成非常深的网络，该网络由几个具有长跳连接的残差组组成。每个残留组都包含一些具有短跳连接的残差块。同时，RIR允许通过多个跳过连接绕过丰富的低频信息，从而使主要网络专注于学习高频信息。此外，我们提出了一种通道注意机制，以通过考虑频道之间的相互依赖性来适应频道的特征。广泛的实验表明，我们的RCAN可以针对最新方法实现更好的准确性和视觉改进。
>
> ### Resormer
>
> 由于卷积神经网络（CNN）在从LargesCale数据中学习可通用的图像先验方面表现良好，因此这些模型已广泛应用于图像恢复和相关任务。最近，另一类的神经体系结构，变形金刚显示出关于自然语言和高级视觉任务的显着性能。虽然变压器模型减轻了CNN的缺点（即，对输入含量的有限的可接受场和不适应能力），但其计算复杂性随空间分辨率而倍增，因此使其不可避免地适用于涉及高分辨率图像的大多数图像恢复任务。在这项工作中，我们通过在构建块（多头注意力和馈送前向网络）中制作多个关键设计来提出一个有效的变压器模型，以便它可以捕获远程像素交互，同时仍然适用于大图像。我们的模型称为Restoration Transformer（Restormer），在几个图像恢复任务上获得了最先进的结果，包括图像恢复任务，单位图，单位运动去除，Defocus DeBlurring（单形像和双像素数据）以及图像DeNoising（Gaussian Grayscale/color color colarescale/color colorscale/color deNoising和真实的图像DeNoising）。源代码和预培训模型可在https://github.com/swz30/restormer上找到。

# 自己写的

感知加密作为一种高效的加密方法，通过区分输入信息中的重要信息与非重要信息并进行选择性加密，实现了加密效率与信息保护的平衡，目前已经被广泛的运用在了图像加密中。然而，现有的图像恢复网络已经证明在小尺度图像上可以被轻易破解，但在大尺度加密图像中的视觉信息仍无法被正常恢复，我们的工作证明了即使是在大尺度感知加密图像中的视觉信息也是可以被恢复的。具体而言，【xxx】使用了基于空洞窗口的Transformer结构，通过创新的上下采样模块与轻量化设计，能够以较少的资源完成对大尺度感知加密图像的恢复，大量实验表明，【xxx】在多个评价指标上均显著优于现有的感知加密图像恢复的基线方法。代码与预训练模型已公开发布，地址为：【xxx】。

# GPT润色

感知加密作为一种高效的加密方法，通过区分输入信息中的关键信息与非关键内容并进行选择性加密，有效实现了加密效率与信息保护之间的平衡，目前已被广泛应用于图像加密任务中。尽管现有研究表明，小尺度感知加密图像中的视觉信息可被现有图像恢复网络轻易还原，但在处理大尺度加密图像时，其视觉信息的有效恢复仍面临显著挑战。本研究表明，即使是在大尺度感知加密图像中，潜在的视觉信息同样可以被成功还原。具体而言，【xxx】采用了基于空洞窗口的 Transformer 架构，并引入了创新的上下采样模块与轻量化设计，使得模型能够以较低的资源开销完成对大尺度感知加密图像的高质量恢复。大量实验证明，【xxx】在多个主流评价指标上均显著优于现有感知加密图像恢复的基线方法。相关代码与预训练模型已公开发布，地址为：【xxx】。

# GPT翻译

Perceptual encryption has emerged as an efficient encryption paradigm that selectively encrypts critical visual information while preserving non-essential content, thereby achieving a desirable trade-off between computational efficiency and information security. It has been widely adopted in image encryption tasks. Although prior studies have demonstrated that visual information in small-scale perceptually encrypted images can be easily reconstructed using existing image restoration networks, recovering high-fidelity content from large-scale perceptually encrypted images remains a significant challenge.In this work, we show that the underlying visual content of large-scale perceptually encrypted images can still be effectively restored. Specifically, **【xxx】** employs a Transformer architecture with dilated window attention, and incorporates a novel upsampling and downsampling mechanism alongside a lightweight design. This enables high-quality restoration of large-scale perceptually encrypted images with minimal computational overhead.Extensive experiments on multiple benchmarks demonstrate that **【xxx】** consistently outperforms existing state-of-the-art baselines for perceptually encrypted image reconstruction across several widely-used evaluation metrics. The source code and pretrained models are publicly available at: **【xxx】**.

# 翻译软件根据GPT翻译回来

感知加密已经成为一种有效的加密范式，它可以选择性地加密关键的视觉信息，同时保留非必要的内容，从而在计算效率和信息安全之间实现理想的权衡。它已被广泛应用于图像加密任务中。尽管先前的研究表明，使用现有的图像恢复网络可以很容易地重建小规模感知加密图像中的视觉信息，但从大规模感知加密图像中恢复高保真内容仍然是一个重大挑战。在这项工作中，我们证明了大规模感知加密图像的底层视觉内容仍然可以有效地恢复。具体而言，**【xxx】**采用了扩展窗口注意力的Transformer架构，并结合了新颖的上采样和下采样机制以及轻量级设计。这使得大规模感知加密图像的高质量恢复具有最小的计算开销。在多个基准测试上进行的大量实验表明，**【xxx】**在几个广泛使用的评估指标中，始终优于现有的最先进的感知加密图像重建基线。源代码和预训练模型可在**【xxx】**公开获取。

