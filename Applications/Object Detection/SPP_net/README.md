### SPP-Net (Spatial Pyramidal Pooling)

SPP-Net was proposed by Kaiming He in the year 2014 from Microsoft. It mainly focused on two ideas. The first one is that, it was seen that, in order to obtain predictions, we need to fix the size of the input image, so the authors came up with a way to make the model independent of the input size. So, the model could predict on any size of the input image. The second one is that the authors wanted to deploy the idea of image or feature pyramids using pooling layers, which will allow creation of a multi-scale featture map, and thus help to obtain more robust features. 

The authors proposed at the transisition level between the convolutional layers and the fully connected layers, mutiple pooling layers must be used with completely varying scales. 

#### SPP Layer

![SPP module](https://miro.medium.com/max/1176/1*Af0rCJ67rVYdfIfhwnwi3A.png)

The SPP module is represented in the above image. As we can see the feature maps are obtained after going through the backbone network. The feature maps are of arbitrary dimension of say MxN and has 256 channels. Now, a set of pooling layers are applied with different scales, to obtain different feature maps. As we can see the 1st feature map is pooled to have one value for each channel. So, for 256 channels, there are 256 such values, which are flattened to obain a 1d vector of 1 x 256 values. The 2nd feature map is pooled such that the resultant feature map can contain 4 values for a channel, so it is flattened to create a 4 x 256d vector. Similarly, for the third scale we obtain a 16 x 256d vector.

All the vectors are concatenated to form a 1-d vector. Now, this vector is sent to the predicting layer, but it has all multiscale information. And as we create fix length 1d vectors, we donot need to worry about the size of the input image size. 

So, how is this achieved? It has been shown by the authors by global pooling and proper selection of the window of the pooling layers and stride we can create output features as we want. The authors have shown, if we want an output feature map of \[n x n]  and we have an input of size \[a x a]. We must select a window size of cieling(a/n) and stride of size floor(a/n). 

#### Multiview Training and Testing

The authors used a pre-trained ZFNet, AlexNet and Overfeat networks with SPP layer and found improvement in performance. To train for multi view or prediction on different size of images, authors trained the networks initially on 224 x 224 size data and changed to 180 x 180 size input images randomly after some epochs. The trainings shared same parameters. During testing 6 scales were used {224, 256, 300, 360, 448, 560}.

The authors also used a 4-level SPPnet pyramid with {6×6, 3×3, 2×2, 1×1} pooled feature maps. These showed improved performance. 

#### SPPNet in Object Detection

![Arch](https://miro.medium.com/max/1374/1*EMhHR_g4UWEYpxsVWdpKdA.png)

For object detection, SPPNet works very similar to RCNN networks. It uses a Selective search algorithm to obtain the region proposals. The only difference is in SPPNet the backbone layer is applied on the input image and feature maps are obtained. On these feature maps we use selective search algorithms, get the region proposals, which are sent to the spp layers to obtain a fixed size vector. For each vector, we have a SVM for the prediction and a bounding box regressor.

References:

1. https://arxiv.org/pdf/1406.4729.pdf
2. https://medium.com/coinmonks/review-sppnet-1st-runner-up-object-detection-2nd-runner-up-image-classification-in-ilsvrc-906da3753679

Deeper understanding:

https://towardsdatascience.com/understanding-sppnet-for-object-detection-and-classification-682d6d2bdfb


