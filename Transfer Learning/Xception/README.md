### Exception

Exception stands for "extreme inception". It was first proposed by Google Researchers in the year 2017, in the imagenet challenge. 

The Exception network takes on the Inception network one step further. As we have already seen, the inception module uses a 1x1 convolutional layer for dimensionality reduction, the exception network, implements a depthwise seperable convolutional layers in place of the inception modules.

The idea behind **depthwise seperable convolution** is that it seperates the convolutions in a spatial and a cross-channel or depthwise operation. In the original seperable convolution process, we have a depthwise convolution followed by a pointwise convolution.

![depsep](https://miro.medium.com/max/770/1*VvBTMkVRus6bWOqrK1SlLQ.png)

As the above image shows, the depthwise convolution is the spatial convolution, so, 1 filter is convoluted with 1 channel at a time. So, for z channels in the image, we will have z nxn spatial convolutions. It is followed by pointwise convolutions, for changing the dimension, so, nxnxz shape is convoluted with 1x1xy filters to be converted to nxnxy. So, basically it deals with the cross-channel or depthwise convolutions. This seperation boosts performance and decreases the number of parameters and makes the model lighter.

Now the exception model slightly modified the architecture of the original depth seperable convolution. The original has depthwise convolution has depthwise followed by pointwise convolutions, which was reversed in exception. It has been proved that, it doesnot bring much change in the result. Another point of modification is, the exception module has no intermediate non-linearity unit or RelU activation function unlike Inception. 

#### Architecture

![Arch](https://miro.medium.com/max/770/1*hOcAEj9QzqgBXcwUzmEvSg.png)

The overall architectiure of Exception network has 3 different stage, Entry flow, Middle Flow and Exit flow. It applies seperable convolutions in addition to Residual skip connections. The architecture is similar to inception networks, with inception modules being replaced.

References: /

1. https://arxiv.org/pdf/1610.02357.pdf  /
2. https://towardsdatascience.com/an-intuitive-guide-to-deep-network-architectures-65fdc477db41
3. https://towardsdatascience.com/review-xception-with-depthwise-separable-convolution-better-than-inception-v3-image-dc967dd42568
4. https://maelfabien.github.io/deeplearning/xception/#the-limits-of-convolutions



