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

## 自己写的v1

感知加密作为一种高效的加密方法，通过区分输入信息中的重要信息与非重要信息并进行选择性加密，实现了加密效率与信息保护的平衡，目前已经被广泛的运用在了图像与视频加密中。然而，现有的图像恢复网络已经证明在小尺度图像上可以被轻易破解，但在大尺度加密图像中的视觉信息仍无法被正常恢复，我们的工作证明了即使是在大尺度感知加密图像中的视觉信息也是可以被恢复的。在本文中，我们提出了一种全新的模型(xxx)，用于基于Transformer的图像恢复。我们的(xxx)使用编码器-解码器结构，其中每个xxx拥有xxx，用于捕获加密图像中的信息，同时xxx拥有全新的视觉信息提取模块，即使在大尺度图像上也能恢复出良好的视觉效果，并且拥有很高的训练效率。大量的实验结果表明，xxx拥有远超现有基于Transformer图像恢复网络的性能。代码和预训练模型可以在xxx找到。



## GPT润色v1

感知加密作为一种高效的信息保护策略，通过区分输入图像中的重要区域与非重要区域并施加选择性加密操作，有效实现了加密强度与计算效率之间的权衡。该技术已广泛应用于图像与视频加密任务。然而，现有研究表明，针对小尺寸感知加密图像，深度图像恢复网络已经可以较为轻松地实现视觉内容重建。但对于高分辨率加密图像，图像恢复的性能仍面临显著挑战。本文提出了一种全新的基于Transformer架构的感知加密图像恢复模型（简称：xxx），首次在大尺度感知加密图像上实现了高质量的视觉内容重建。所提模型采用编码器-解码器结构，编码器模块xxx用于充分捕获密文图像中的全局上下文信息，解码器则集成了我们设计的新型视觉信息提取模块，显著增强了对重要视觉语义的还原能力。该方法在多个大规模图像数据集上均表现出优越的恢复效果，同时保持了较高的训练效率。大量实验表明，xxx在多个评价指标上均显著优于现有的Transformer图像恢复基线方法。代码与预训练模型已公开发布，地址为：xxx。

## 人工修改GPTv2

感知加密作为一种高效的信息保护策略，通过区分输入图像中的重要区域与非重要区域并施加选择性加密操作，有效实现了加密强度与计算效率之间的权衡。该技术已广泛应用于图像与视频加密任务。然而，现有研究表明，针对小尺寸感知加密图像，深度图像恢复网络已经可以较为轻松地实现视觉内容重建。但对于高分辨率加密图像，图像恢复的性能仍面临显著挑战。本文提出了一种全新的基于Transformer架构的感知加密图像恢复模型（xxx1），首次在大尺度感知加密图像上实现了高质量的视觉内容重建。所提模型采用编码器-解码器结构，**(xxx1)中的模块(xxx2)用于充分捕获密文图像中的全局上下文信息，同时集成了我们设计的新型视觉信息提取模块(xxx3)，**显著增强了对重要视觉语义的还原能力。该方法在多个大规模图像数据集上均表现出优越的恢复效果，同时保持了较高的训练效率。大量实验表明，(xxx1)在多个评价指标上均显著优于现有的Transformer图像恢复基线方法。代码与预训练模型已公开发布，地址为：xxx。

## GPT翻译

Perceptual encryption has emerged as an efficient strategy for information protection by distinguishing between visually important and unimportant regions within an image and applying selective encryption accordingly. This approach enables a desirable balance between encryption strength and computational efficiency, and has been widely applied in image and video encryption tasks.While prior studies have shown that deep image reconstruction networks can effectively recover visual content from perceptually encrypted images of small resolution, restoring semantic information from high-resolution encrypted images remains a significant challenge.In this paper, we propose a novel Transformer-based model(xxx1), for perceptually encrypted image restoration. To the best of our knowledge, this is the first work that successfully achieves high-fidelity reconstruction from large-scale perceptually encrypted images. The proposed architecture follows an encoder-decoder paradigm, where the (xxx2) module in (xxx1) is responsible for capturing global contextual information from the encrypted inputs. In addition, we integrate a newly designed visual information extraction module(xxx3), which substantially enhances the model’s capability to recover semantically important content,and the results show that (xxx1) consistently outperforms existing Transformer-based baselines in terms of both reconstruction quality and computational efficiency. The code and pre-trained models are publicly available at: (xxx).

## 翻译软件翻译回来

感知加密已经成为一种有效的信息保护策略，通过区分图像中视觉上重要和不重要的区域，并相应地应用选择性加密。该方法在加密强度和计算效率之间取得了理想的平衡，已广泛应用于图像和视频加密任务中。虽然先前的研究表明，深度图像重建网络可以有效地从小分辨率的感知加密图像中恢复视觉内容，但从高分辨率加密图像中恢复语义信息仍然是一个重大挑战。在本文中，我们提出了一种新的基于transformer的感知加密图像恢复模型，xxx1。据我们所知，这是第一个从大规模感知加密图像中成功实现高保真重建的工作。所建议的体系结构遵循编码器-解码器范例，其中xxx1中的xxx2模块负责从加密输入中捕获全局上下文信息。此外，我们集成了一个新设计的视觉信息提取模块xxx3，大大增强了模型对语义重要内容的恢复能力，结果表明，xxx1 *在重建质量和计算效率方面始终优于现有的基于transformer的基线。代码和预训练的模型可以在xxx上公开获得。