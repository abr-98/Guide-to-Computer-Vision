### Fully Convolution Networks

Fully convolutional Networks was proposed by Jonathan Long, Evan Shelhamer from UC Berkeley in the paper titled "Fully Convolutional Networks for Semantic Segmentation". 

The idea behind the Fully Convolutional Network evolved from the previously used image classification methods, which used a convolutional network, a corresponding Fully connected layer and finally a softmax layer for prediction. Now, in image classification we did a single prediction.

The authors replaced the dense layers using 1x1 convolutional layer, with a softmax activation instead of ReLU activation. Now, we need dense predictions, in order to do that, we need to predict for each pixel. But we know, to extract finer features, we must go deep in tha convolutional net, and apply Maxpooling, which decreases the resolution of the image. So, the size of the final feature map is less than the original image. To make pixelwsie predictions, we need the feature map on which we will predict the output, of the same resolution as the input image, so we upsample the feature map to accomplish it. 

![Network](https://miro.medium.com/max/559/1*NXNGhfSyzQcKzoOSt-Z0Ng.png)

The paper replaced the upsampling layers with deconvolutional layers, in order to make the model learn in a better way, as upsampling usage has an aliasing effect. 

It is known that, we need to use deeper network to learn finer features, which decreased the feature map resolution, so the authors needed to upsample 32x times, in order to predict. This is why, it was called FCN 32. The output was found to be very coarse and rough. 

It was discovered that, the location information which is mostly spatial localized information was lost, which prevented the model from giving fine-grained predictions. So, the deep model actually, got better at global information, but lost local information, and both of them are necessary for Segmentation problem. 

The authors found that the feature maps, found in the shallower layers of the convolutional networks had better spatial information owing the higher resolution of the maps compared to the deeper layer ones, So, the authors devised a skip connection strategy. 

The authors combined feature maps from the shallower pool layers with the upsampled feature maps, just to provide the spatial local informations better and upsampled from those feature maps to have better information.

![FCN](https://miro.medium.com/max/770/1*lUnNaKAjL-Mq10v3tIBtJg.png)

As we can see, instead of directly upsampling 32x times, we upsample it 2x times and then combine with feature map from the corresponding pooing layer. Then, that feature map is upsampled 16x, and the predictions are made on that map. This model was termed as FCN-16. Similarly, we obtain FCN-8.

The later modellings were known to obtain much better segmentation results.

![FCN_res](https://miro.medium.com/max/630/1*tcYqvV0KHjK2ANBGe8GpjQ.png)

References:
1. https://arxiv.org/pdf/1411.4038.pdf
2. https://towardsdatascience.com/review-fcn-semantic-segmentation-eb8c9b50d2d1

