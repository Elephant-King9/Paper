# 自己写的

​	感知加密是一种结合图像初始像素信息进行加密来保护图像视觉内容的有效方法。由于图像的信息具有连续性和高密度的特性，导致图像中会出现大量与主体无关的冗余信息。传统加密会不加区分的对图像的全部信息进行加密，并没有结合图像本身的属性，从而导致了大量冗余计算，与传统加密不同，感知加密根据图像的原始信息区分主体与冗余部分，将加密资源于图像关键主体的加密，可以保证用尽可能少的资源达到最好的加密效果。到目前为止，已经有许多工作针对图像进行感知加密【1,2,3,4,5】，这些方法宣称自己可以通过感知加密的方法来保护普通图像的安全性，但是本文提出的方法挑战了感知加密图像的安全性，【图1，画个原图->加密->恢复效果的图，同时对比现有的IR、SR网络的恢复结果】中的实例展示了我们的恢复结果，恢复图像在视觉上非常接近原始图像。从密码分析的角度出发，现有很多工作【6,7,8,9,10,11】已经从统计攻击、差异攻击和线性攻击等角度尝试分析感知加密图像的安全性，但是常规的密码分析需要严格的了解加密算法的每个细节，这会设计大量的人力与机器的计算资源，同时感知加密更关注图像本身的信息，会随着图像的改变而改变，而传统密码分析不是这样。

​	随着深度学习的发展与Transformer【12】架构的成熟，已经有许多基于CNN和Transformer的深度神经网络进行图像恢复工作【13,14,15,16,17,18】与超分辨率的工作【19,20,21,22,23,24】，并且在相应的领域取得了极大的进展，但是现有的基于图像恢复和超分辨率的网络仅限于恢复信息破坏程度较低的图像，如高斯噪声，运动模糊，雨雾天气等，对于感知加密这种信息破坏程度较高的图像，现有的恢复网络往往束手无策，详见【图1，画个原图->加密->恢复效果的图，同时对比现有的IR、SR网络的恢复结果】。目前也有工作专门针对信息破坏程度高的感知加密图像进行恢复【25,26】，但是这些网络仅使用CNN来进行图像恢复，没有结合Transformer进行大尺度图像捕捉的能力，同时这些工作针对的加密图像的尺寸较小，并不符合实际中使用图像的尺寸。在轻量化恢复大尺度感知加密图像的工作目前还鲜有人研究。

​	为了解决上述问题，在本文中，我们提出了一个【网络名】，旨在建立一个轻量化的恢复网络，用尽可能少的计算资源快速恢复大尺度的加密图像，【具体方法】





​	我们的主要贡献如下

	1. 我们提出了一个结合CNN和Transformer的端到端神经网络【】，不需要任何手工分析与对加密算法的先验知识，就可以破解大尺度感知加密图像中的信息。
	1. 我们提出了【】，来降低模型的参数量，实现了使用较少资源就可以部署的轻量化网络
	1. 我们提出的网络相较于现有的图像恢复网络，在感知加密领域取得了远远优于基线的性能

































































[1] Selective image encryption using a spatiotemporal chaotic system 

> Tao Xiang、Kwok-wo Wong、Xiaofeng Liao
>
> 2007
>
> >  提出了一种利用时空混沌系统对灰度级图像进行加密的通用选择性图像加密算法。为了解决安全性和性能之间的权衡，在仿真结果的基础上讨论了选择性加密的有效性。然后将该方案扩展到RGB彩色图像的加密。对两种场景的安全性分析表明，所提出的方案具有较高的安全性和效率。

[2] Selective image encryption based on pixels of interest and singular value decomposition

> STSF
>
> 加密方法
>
> 2012
>
> > 在本文中，提出了一种有效而简单的选择性加密技术，该技术是基于锯齿空间填充曲线，感兴趣的像素，非线性混沌图和奇异值分解的。所提出的方案的核心思想是通过使用感兴趣的像素方法选择锯齿齿空间填充曲线，然后选择重要像素。然后，使用从非线性混沌图和奇异值分解获得的秘密图像键在显着像素上进行扩散过程。最后，提出了一个可靠的解密过程，以从加密图像中构造原始图像。分析和实验结果表明，所提出的方案可以实现选择性加密的各种目的，并且在计算上是安全的。

[3] Period of a discrete cat mapping

> ARCM
>
> 加密方法
>
> 1992

[4]Partial multimedia encryption with different security levels

> GPGC
>
> 加密方法
>
> 2008
>
> > 他的论文介绍了新的广义P灰色代码（GPGC）上的三个多媒体加密算法基础，以保护国土安全应用程序中的监视数据。 GPGC是适用于任何碱的K数字参数序列。它也称为（n，k，p） - 格雷代码，其中p是一个允许用户更改距离以产生不同灰色代码序列的参数。基本N和参数P作为安全键具有许多选项，可以使加密的多媒体难以解码。这允许加密对象受到高度安全性的保护。实验结果验证了所提出的算法是无损的方法，并且在部分多媒体加密方面良好。引入了一种测量图像加密百分比的方法，还提供了量度结果以量化加密性能。实验表明，对于常见攻击，该算法表现出良好的性能。由于算法的复杂性较低，因此它们也适用于实时应用。提出的解决方案背后的原理可以应用于各种图像，音频和视频系统。

[5] A novel perceptual image encryption scheme using geometric objects based kernel

> GOPE
>
> 加密方法
>
> 2013
>
> > 在各种应用程序中，广泛使用数字图像和视频值得对当今的安全性和隐私问题进行认真关注。近年来，已经提出了几种加密技术，作为保护数字图像和视频的可行解决方案。在许多应用程序中，例如按观看付费视频，付费电视和视频按需，所需的功能之一是，仅通过某些加密技术部分将视频数据的质量降低，并且必须部分理解加密的数据。此功能称为“感知加密”是根据安全性或质量要求降低媒体内容质量的加密算法。在这项工作中，我们提出了一种简单而有效的技术，用于使用几何对象作为基于像素的内核来实现感知加密。所需的混淆方面是通过将内核插入图像上的，从而根据基于几何对象形成的内核进行像素的换位来实现的。几何对象的各种参数，对象的数量和图像中对象/内核的位置用作加密的键，然后用作解密。进一步选择图像质量所需的质量，即通过调整对象/内核的上述参数来提供不同级别的降解。从获得的结果可以明显看出，更倾向于感知加密的提议方法也可以有效地用于完整的图像加密，并可以接受。

[6] An efficient image homomorphic encryption scheme with small ciphertext expansion

> 传统密码分析(NLANet)
>
> 2013
>
> > 在加密域中的图像处理领域已越来越关注广泛的潜在应用程序，例如，在不受信任的环境中为隐私保护应用程序提供有效且安全的解决方案。广泛使用这些技术的一个障碍是由现有同构加密引起的高数数量级的密文扩展。在本文中，我们提供了一种解决此问题的方法，以用于加密域中的图像处理。通过使用图像格式的特征，我们开发了一个图像加密方案，以限制密文扩展，同时保留同构属性。提出的加密方案首先将图像像素与现有的概率同质密码系统进行加密，然后压缩整个加密图像以节省存储空间。与元素加密方案相比，我们的方案具有更小的密文扩展因子，同时保留同构特性。在将安全的信号处理工具应用于压缩的加密图像时，不必需要其他交互式协议。我们提出了一种快速算法，用于加密和压缩提出的图像加密方案，该方案加快了计算并使我们的方案更加有效。还进行了对安全性，密文扩展比和计算复杂性的分析。我们的实验证明了所提出的算法的有效性。提出的方案适合用作安全图像处理中应用程序的图像加密方法。

[7] An Image Encryption Algorithm Based on Autoblocking and Electrocardiography

> 传统密码分析(NLANet)
>
> 2015
>
> > 一种新型的图像加密算法使用心电图来生成初始键和自动块方法，以消除手动分配的需求。它已被证明是复杂，强大且灵活的，足以用于实际应用。

[8] Image scrambling encryption algorithm of pixel bit based on chaos map

> 传统密码分析？(NLANet)
>
> 2010
>
> > 本文介绍了基于混乱图的像素位的图像加密算法。该算法利用了混乱图的最佳特征，例如其伪界属性，系统参数，对初始条件和非周期性的敏感依赖性以及像素值位结合使用。新算法仅使用一次混乱映射一次来实现图像的灰色争夺加密，其中均匀分布在0到255的像素值均匀分布，所有像素的位置也被排列。通过这种方式，提出的方法彻底改变了原始图像信息的统计特征，因此，它增加了未经授权的人打破加密的困难。最后，数值实验结果表明，图像加密算法建议具有完美的隐藏能力，包括大钥匙空间，对初始条件的敏感钥匙，高灰色的拼凑型学位，并且适合于通过Internet保护数字图像信息的安全性。

[9] Cryptanalyzing an image-scrambling encryption algorithm of pixel bits

> 传统密码分析（PRNet）
>
> 2017
>
> >  一种有效的方法可以披露通过仅限文化攻击方案中典型的图像加密算法隐藏的重要视觉信息。实验还表明，攻击者可以使用真实的拼凑域来支持有效的已知或选定式攻击。

[10] Cryptanalyzing an image encryption algorithm based on autoblocking and electrocardiography.

> 传统密码分析（PRNet）
>
> 2018
>
> > 本文从现代密码学的角度对基于自动阻塞和心电图的混沌图像加密算法进行了彻底的安全分析。该算法使用心电图（ECG）信号生成混沌系统的初始键，并应用一种自动块方法将纯图像划分为适合后续加密的某些尺寸的块。设计师声称，所提出的算法“对于实际应用来说足够强大，足够灵活”。我们发现它很容易受到已知的明文攻击：基于一对已知的纯图像及其相应的密码图像，对手能够得出一个掩码图像，可以将其用作同样的秘密键，以成功地将其他密钥在相同的密钥中加密使用，该密钥在相同的密钥中使用不合格的概率为1/1/1/1/1/1/1/1/256。以此为典型的反例，我们总结了许多图像加密算法中存在的一些安全缺陷。

[11] Ciphertext-only attack on an image homomorphic encryption scheme with small ciphertext expansion.

> 传统密码分析（PRNet）
>
> 2015
>
> > 该论文“具有较小密码扩展的有效图像同态加密方案”（在Proc。ACMMM’13，pp.803-812中）提出了一种新型的图像同构加密方法，可实现大幅度减少密码扩展。在当前的工作中，我们研究了只有密文的攻击（COA），该加密系统的安全性。我们表明，我们提出的COA有效地产生了原始图像的忠诚度的草图。提供实验结果以验证拟议攻击策略的有效性。

[12] Attention is all you need

> Transformer
>
> 2017

[13] Uformer: A general U-shaped transformer for image restoration

> Uformer(IR)
>
> 2021

[14]SwinIR: Image restoration using swin transformer

> SwinIR(IR)
>
> 2021

[15] Restormer: Efficient transformer for high-resolution image restoration

> Restormer(IR)
>
> 2022

[16] Cross aggregation transformer for image restoration

> CAT(IR)
>
> 2023

[17] Adapt or perish: Adaptive sparse transformer with attentive feature refinement for image restoration

> AST(IR)
>
> 2024

[18] Accurate image restoration with attention retractable transformer

> ART(IR)
>
> 2023

[19] Transcending the limit of local window: Advanced super-resolution transformer with adaptive token dictionary

> ADT(SR)
>
> 2024

[20] Swift parameter-free attention network for efficient super-resolution

> SPAN(SR)
>
> 2024

[21] SRFormer: Permuted self-attention for single image super-resolution

> SRFormer(SR)
>
> 2023

[22] Multi-scale attention network for single image super-resolution

> MAN(SR)
>
> 2024

[23] Lightweight image super-resolution with superpixel token interaction

> SPIN(SR)
>
> 2023

[24] Image Super-Resolution Using Very Deep Residual Channel Attention Networks

> RCAN(SR)
>
> 2018

[25] The illusion of visual security: Reconstructing perceptually encrypted images

> NL-ANet(方法对比)
>
> Ying Yang 、Tao Xiang 、 Xiao Lv 、Shangwei Guo、Tieyong Zeng
>
> 2024

[26] PRNet: A Progressive Recovery Network for Revealing Perceptually Encrypted Images

> PRNet(方法对比)
>
> 2021
