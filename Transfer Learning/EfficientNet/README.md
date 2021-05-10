### Efficient Net

EfficientNet was proposed in 2019 by Google. The model was trained on the Imagenet dataset. The paper focused on two elements majorly:
1. To find a mobile-sized baseline architecture: EfficientNet-B0
2. It puts forward an effective compound scaling methods to achieve more robust model efficiency and performance.

It primarily focuses on reducing FLOPS (floating point operations per second) and the parameters used in the models. First, we need to look at the concept of scaling.

We have seen that previously, we have scaled up and down the models simply by stacking layers of convolutional modules on availablity of resource. The authors proposed a different concept of model scaling. They introduced three type of scaling:

1. Depth-wise scaling: The scaling in depthwise dimension is done by simply adding or removing convolutional layers. So, it concerns with the number of layers in the convolutions in the network. Deeper the network, more it can capture richer and more complex features. It is the common intution, but experiments show that it is not always true.

2. Width-wise scaling: The scaling in width or lateral-wise is done by adding more number of filters in the convolution layers. Width is represented by the number of filters. More wider the network, more fine-grained and localized features can be captured. Research has shown, after a certain increase the accuracy saturates.

3. Resolution scaling: The scaling deals with the dimension of the image input. The larger the dimension, more is the resolution, and it is said to better represent the fine-grained features. 

![scale](https://miro.medium.com/max/700/1*xQCVt1tFWe7XNWVEmC6hGQ.png)

The paper also showed that, increasing one of the three dimensions didn't have any effect on the accuracy. Intuitively, if we increase the width and not the depth, the network will not be able to learn the found features. So, we must gain a coumpound combined scaling, in all the fields together, to increase the accuracy. 

To achieve this, the authors framed the problem, as an effective scaling technique using a compound coefficient ɸ to uniformly scale network, as:

depth: d= α^ɸ
width: w= β^ɸ
resolution: r= γ^ɸ

such that, α x β^2 x γ^2 =2 (approx)
and all the parameters are greater than 1.

ɸ is a user-specified coefficient that controls how many resources are available whereas α, β, and γ specify how to assign these resources to network depth, width, and resolution respectively.

#### Architectiure
 
Now, for the providing the results of comparison of the different scaling, the authors needed to find a perfect base model which can be scaled to give the required results.

The authors used a Neural Architecture Search algorithm, M-NASNet to search the required model space and find the best fit model. 

![Arch](https://1.bp.blogspot.com/-DjZT_TLYZok/XO3BYqpxCJI/AAAAAAAAEKM/BvV53klXaTUuQHCkOXZZGywRMdU9v9T_wCLcBGAs/s640/image2.png)

The above architecture was proposed as the basic base architecture. The MBConv blocks are inverted Residual blocks as used in MobileNetV2 with squeeze and excite blocks.  Varying the parameters α, β, γ, and ϕ the versions of the Efficient nets were found from B1-B7. The best efficient net is found to be B0, with α =1.2, β = 1.1, ϕ =1 and γ = 1.15.

![Module](https://amaarora.github.io/images/mbconv.png)

The above image represents the MBConv module.

References:
1.https://arxiv.org/pdf/1905.11946.pdf\\ \
3.https://ai.googleblog.com/2019/05/efficientnet-improving-accuracy-and.html \
4.https://amaarora.github.io/2020/08/13/efficientnet.html \
5.https://medium.com/@nainaakash012/efficientnet-rethinking-model-scaling-for-convolutional-neural-networks-92941c5bfb95 \
6.https://arxiv.org/abs/1801.04381 \




