### Deeplab Family

Google proposed a family of papers in the field of semantic segmemtation. The papers brought a set of new ideas in the field. The set of 4 papers: DeepLab V1, DeepLab V2, DeepLab V3, DeepLab V3+ consecutively outperformed the previous one and all the contemporary algorithms. 

Concpts Proposed:
1. Version 1: Atrous/Dilated convolutions, Conditional Random Fields (CRF)
2. Version 2: Atrous Spatial Pyramidal Pooling 
3. Version 3: Parallel processing approach on Atrous Spatial Pyramidal Pooling 
4. Version 3+: Normalization and decoder unit on Version 3, and atrous seperable convolutions

### Version 1:

Deeplab V1 first proposed Atrous/ Dilated convolutions. The problem seen in FCN was, it needed a 32x upsampling, as we needed to go deep in the network to obtain finer features, which requires downsampling of the image. The downsampling is actually required because in order to obtain global information, we need to capture the larger context in the image, which either requires, excessive downsampling or larger kernels, which hugely increases the number of parameters. So, we usually go with the first one, which causes loss in local information due to the downsapling. But in case of segmentation, we need both global and local information. 

So, dilated or atrous convolutional was introduced. Atrous convolution or the hole convolution or dilated convolution which helps in getting an understanding of large context using the same number of parameters. Dilated convolution works by increasing the size of the filter by appending zeros(called holes) to fill the gap between parameters. The number of holes/zeroes filled in between the filter parameters is called by a term dilation rate. When the rate is equal to 1 it is nothing but the normal convolution. When rate is equal to 2 one zero is inserted between every other parameter making the filter look like a 5x5 convolution. Now it has the capacity to get the context of 5x5 convolution while having 3x3 convolution parameters. Similarly for rate 3 the receptive field goes to 7x7.

![Dilated](https://nanonets.com/blog/content/images/2020/08/main-qimg-d9025e88d7d792e26f4040b767b25819.png)

The deeplab replced the pooling and the some convolutional layers with Dilated convolutions, with stride 1. This helped to obtain larger context, thus better global features, and also restricts the downsampling to 8x, which prevents huge loss of local features. The 8x upsampling was possible using bilinear upsampling. [WIKI](https://en.wikipedia.org/wiki/Bilinear_interpolation)

Next, it was seen that the often the output by bilinear interpolation was coarse in nature, in such circumstances, CRF or conditional Random Fields were used to smoothen out the output. 

![CRF](https://miro.medium.com/max/1284/1*r7dUU5Gb3LaWCr7tnKYm2w.png)

The idea behind CRF is to minimize a randomness or an energy function, which is a summation of the log proabability of the prediction, and an weighted sum of results of a bilinear filter and a gaussian filter. The idea is to penalize the model for predicting different labels for pixels very close to each other (Focused by the gaussian kernel) and the pixels which are close to each other having similar intensity values (Focused on by the Bilinear Kernel). The first term in the loss function depicts the log probability, and the second term focuses on the discussed penalties.

![Res](https://miro.medium.com/max/729/1*0omVBDSf5sucAqsFBastiQ.png)

### Version 2:

Deeplab V2 introduced Atrous Spatial Pyramidal Pooling layers, inspired from Spatial Pyramidal Pooling layers, which captured multi-scale information, from single input images, using 1x1, 2x2, and 4x4 convolutional layers and finally concatenated the feature maps as 1d vectors. 

ASPP takes the concept of fusing information from different scales and applies it to Atrous convolutions. The input is convolved with different dilation rates and the outputs of these are fused together.

![ASPP](https://nanonets.com/blog/content/images/size/w1000/2020/08/deeplab_aspp.jpg)

The input is convolved with 3x3 filters of dilation rates 6, 12, 18 and 24 and the outputs are concatenated together since they are of same size. A 1x1 convolution output is also added to the fused output. The multi-scale information from ASPP helps in improving the results.

CRF is used here also as a post processing step to improve results.

### Version 3: 

Version 3 introduced a parallel processing measure for atrous convolutions and also introduced batch normalization.

It focused on the fact that using Atrous convolutions, we can actually stack layers, without decreasing the resolution of the image.

![Version3](https://miro.medium.com/max/2566/1*8Lg66z7e7ijuLmSkOzhYvA.png)

It removed the CRF post processing and used the ASPP idea combined with a global Average Pooling just to have a better global feature based idea. 

### Version 3+

The Deeplab V3+ combined the ideas of the encoder-decoder limb and ASPP net to create a new ASPP Encoder-Decoder based network. 

![Comp](https://nanonets.com/blog/content/images/size/w1000/2020/08/1_Llh9dQ1ZMBqPMOJSf7WaBQ.png)

Its main idea was to build a decoder limb on the output of the ASPP layer of Deeplab V3, and remove the biliear interpolation method for upsampling.

![ARCH_V3+](https://miro.medium.com/max/770/1*MFchBd4c8ZEgE3qtbnTznw.png)

DeepLabV3+ proposes to add an intermediate decoder module on top of the DeepLabV3. After processing via DeepLabV3, the features are then upsampled by x4. They are then further processed along with the original features from the feature extraction frontend, before being upscaled again by x4. This lightens the load from the end of the network and provides a shortcut path from the feature extraction frontend to the near end of the network.

References:

1. https://arxiv.org/pdf/1606.00915.pdf
2. https://arxiv.org/pdf/1412.7062.pdf
3. https://arxiv.org/pdf/1706.05587.pdf
4. https://arxiv.org/pdf/1802.02611.pdf
5. https://arxiv.org/pdf/1502.03240.pdf
6. https://sh-tsang.medium.com/review-deeplabv3-atrous-separable-convolution-semantic-segmentation-a625f6e83b90
7. https://towardsdatascience.com/review-deeplabv3-atrous-convolution-semantic-segmentation-6d818bfd1d74
8. https://towardsdatascience.com/review-deeplabv1-deeplabv2-atrous-convolution-semantic-segmentation-b51c5fbde92d
9. https://developers.arcgis.com/python/guide/how-deeplabv3-works/
