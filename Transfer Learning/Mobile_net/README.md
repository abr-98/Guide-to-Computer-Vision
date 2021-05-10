### Mobile Net:

Mobile net has been proposed by Google in two versions, V1 and V2 correspondingly in the years 2017 and 2018. The MobileNet are designed to be light-weight, and very cost efficient to be used on-device use like mobile devices and cloud APIs. 

### MobileNet-V1 

The MobileNet-V1 uses Depthwise Seperable Convolutions. It has much fewer parameters and reduced number of mathematical operaions. The MobileNet-V1 also introduces, a Width Multiplier α for Thinner Models and Resolution Multiplier ρ for Reduced Representation. These two parameters are provided by the user to control the weight or resource consumed by the model.

The idea behind **depthwise seperable convolution** is that it seperates the convolutions in a spatial and a cross-channel or depthwise operation. In the original seperable convolution process, we have a depthwise convolution followed by a pointwise convolution.

![depsep](https://miro.medium.com/max/770/1*VvBTMkVRus6bWOqrK1SlLQ.png)

As the above image shows, the depthwise convolution is the spatial convolution, so, 1 filter is convoluted with 1 channel at a time. So, for z channels in the image, we will have z nxn spatial convolutions. It is followed by pointwise convolutions, for changing the dimension, so, nxnxz shape is convoluted with 1x1xy filters to be converted to nxnxy. So, basically it deals with the cross-channel or depthwise convolutions. This seperation boosts performance and decreases the number of parameters and makes the model lighter.

As we have already seen, if we use depthwise seperable convolutions, we perform depthwise convolutions, followed by pointwise convolutions. For depthwise convolutions, we require in total **n x n x z x k x k** mathematical operations where z: Number of input channels, n: Kernel size, and k: Feature map size. For the pointwise cnvolutions, we use **1 x 1 x y x k x k x z** where, y is the number of output channels. So, in total number of operations are:

**total= n x n x z x k x k + 1 x 1 x y x k x k x z**

![Unit-1](https://miro.medium.com/max/408/1*XFvQWA4VESeQIcxzXMHCAg.png) 

The 1st unit shows the normal convolutional unit and the second unit shows the modified depthwise seperable convolutions. 

Now, the width control parameter α is introduced to control the number of channels or channel depth. So, the modified number of operations become:

**total= n x n x αz x k x k + 1 x 1 x αy x k x k x αz**

α is kept always in the interval (0,1], the typical values being 0.25, 1, 0.75 and 0.5. The baseline has α=1.

Next, the paper introduces Resolution Multiplier ρ to control the input image resolution of the network. So, it gets multiplied with the feature maps. So, the modified number of operations become:

**total= n x n x αz x ρk x ρk + 1 x 1 x αy x ρk x ρk x αz**

ρ varies between 0 and 1, with 1 as the baseline.

Thus the parameters decrease or increase with value of rho and alpha.

### MobileNet-V2:

The MobileNet-V2 modified the MobileNet-V1's basic convolutional block module as shown:

![update](https://miro.medium.com/max/770/1*bqE59FvgpvoAQUMQ0WEoUA.png)

The V2 has two types of modules, 1 with stride=1, that keep the dimension unaltered and with dimension stride=2, to reduce the size of the image. The module with stride 1 uses a Residual skip connection structure, while the 2nd block is relatively simple. 

The V2 module brought 1 major change, that is the last layer of the block is a 1x1 convolution layer with linear activation. The paper claimed that if ReLU is used again, the deep networks only have the power of a linear classifier on the non-zero volume part of the output domain. 


The V2 model gave a much higher performances compared to other models. 

References:  \n

1. https://arxiv.org/pdf/1704.04861.pdf   \n
2. https://arxiv.org/pdf/1801.04381.pdf   \n
3. https://ai.googleblog.com/2018/04/mobilenetv2-next-generation-of-on.html \n
4. https://towardsdatascience.com/review-mobilenetv1-depthwise-separable-convolution-light-weight-model-a382df364b69
5. https://towardsdatascience.com/review-mobilenetv2-light-weight-model-image-classification-8febb490e61c
6. https://analyticsindiamag.com/why-googles-mobilenetv2-is-a-revolutionary-next-gen-on-device-computer-vision-network/

