### Pyramid Scene Parsing Network (PSPNet)

PSPNet focussed on the idea of using the multiple scaling to extract and capture finer features and information. 

![Arch_PSP](https://miro.medium.com/max/2608/1*IxUlWP8RBtxNS1N6hyBAxA.png)

As shown in the figure, the PSPNet primarily focused on extracting the information from the images using a Resnet  or Dilated convolution based deep architecture. After obtaining the feature maps, as shown, it uses 4 different average pooling operation with 4 different window sizes and strides. This creates 4 different scaling of the same image. Now, a 1x1 convolution is used on all the 4 scaled images, in order to reduce dimension. 

Finally the Resultant from all the 4 different scaled images are concatenated with the extracted feature maps. Bilinear Transformation is applied on the concatenated result in order to upsample the feature map, and finally 1x1 convolution is applied to obtain the predictions.

References:

1. https://arxiv.org/pdf/1612.01105.pdf
2. https://towardsdatascience.com/review-pspnet-winner-in-ilsvrc-2016-semantic-segmentation-scene-parsing-e089e5df177d


### Fast FCN

Fast FCN proposed the replacement of the dilated convolution with **Joint Pyramid Upsampling(JPU).** 

![Arch](https://miro.medium.com/max/700/1*qIjtbbsVYqRwpTs6-7_i8Q.png)

The differences between Fast FCN's backbone and DilatedFCN's lies in the last two convolution stages. Typically, the input feature map is first processed by a regular convolution layer, followed by a series of dilated convolutions. Fast FCN conceptually processes the input feature map with a strided convolution and then employs several regular convolutions to generate the output.  

![JPU](https://miro.medium.com/max/700/0*YrT7w4KaIPPUGsgt.png)

Each feature map is passed through your regular convolutional block. Afterwards, the feature maps are upsampled and concatenated which then is passed through four convolutions with different dilation rates. Finally, the convolution's results are concatenated again and passed through a final convolution layer. JPU extracts multi-scale context information from multi-level feature maps, which leads to a better performance.

References:

1. https://arxiv.org/pdf/1903.11816.pdf
2. https://flonelin.wordpress.com/2019/11/17/fastfcn/
3. https://github.com/wuhuikai/FastFCN

