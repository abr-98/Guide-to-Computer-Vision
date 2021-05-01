There are some basic components which are very essential to build a convolutional network. We are going to talk about them.

![Schematic](https://www.researchgate.net/publication/336805909/figure/fig1/AS:817888827023360@1572011300751/Schematic-diagram-of-a-basic-convolutional-neural-network-CNN-architecture-26.ppm)

The above image gives a schematic representation of the parts and functioning of Convolutional Neural Networks. A CNN model consists of mainly two portions: 

1. A Convolution part to extract the features. 
2. A Fully Connected part to learn the features and deliver the final predictions.

The Fully connected layer units are different from the Convoluional layer units as they are dense artificial neurons to learn from 1-dimensional flattened features. 

For several problems like segmentation problems, we remove the Fully connected classification layers from the CNN architecture and replace it using 1x1 convolutional layer to coupled with a sigmoid or a softmax activation to provide the output on a pixel wise basis.

### 1. Convolutional layers:
As we have seen in the filter portion of the repository, filters are used to extract the features out of images. We have also seen, that different filters obtain different response from an image, thus highlighting different extracted features. Now, for different functions we need to extract different set of features, so we need different set of filters. Its practically impossible to select and tune the filter wieghts manually, so CNNs automates the tuning of the filter weights based on problem in hand and the dataset. 

So, in case of CNNs we initialize filters or kernels with random weights of size as decided by the designer, the filters extract features, which is used for predictions and the error in prediction is calculated, which backpropagates, The backpropagation is used to update the filter weights accordingly. 

![Diag](https://miro.medium.com/max/685/0*awD7_-Oxmz2O_0bD)

The diagram above showa the schematic flow of gradients in the layers. 

Till now we have used the terms "kernel" and "filter" for the same denotion, but at this stage the meanings are a bit different. Kernels are the weighted matrix like strutures that are convoluted with images. A group of kernel is called a filter. For convolutional layers,for each layer, a number of filter is passed to be convoluted with the image. The number and the dimension of the kernels building the filter at a certain layer is input from the user. Each of the kernels are different and they extract different feature maps (nD features) from an image. The dimension of all the feature maps are same as the dimension of the kernels are same. So, we stack the different feature maps obtained vertically, to create the actual output.

So, for a particular image, if the dimension of the obtained feature map is m x m and we got n kernels for that layer. The output becomes m x m x n. So, the spatial dimension of an image is m x m, and the third dimension n, we call it **channels.** The image is now said to have n channels. 

Now, for layer 2, where the 3d feature map of size m x m x n comes in, it already has n channels, which actually is n 2d feature maps stacked together. In such cases, 1 kernel convolutes with all the channels of the input 3d feature map, which are 2d each. So the new 2d feature maps obtained as a result of the convolution for all the channels of the input map is of same dimension, and the new 2d feature maps obtained for that particular kernel is added up pixelwise to obtain that one final single 2d feature map. Similarly for every kernel in the filter in layer 2, we get a 2d feature map. So, say for p kernels,we get p 2d feature maps, which we stack up to create a 3d output feature map. 

Now, the size of the feature maps, depend on the size and movement of kernels over the images. The mentioned factors are dependent on some user dependent paramaters, like: padding, stride, and size of the kernel. 

The stride defines how the kernel moves. If it is 1x1, the kernel moves 1 pixel each along x and y axis respectively. It's often seen the points on the edges of an image is not very well extracted by the kernels, for this we use a padding of pixel value 0 around the image. If we keep padding="Same", the size of the image remains same before and after the convolution operator.


