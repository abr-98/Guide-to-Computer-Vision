### SPP-Net (Spatial Pyramidal Pooling)

SPP-Net was proposed by Kaiming He in the year 2014 from Microsoft. It mainly focused on two ideas. The first one is that, it was seen that, in order to obtain predictions, we need to fix the size of the input image, so the authors came up with a way to make the model independent of the input size. So, the model could predict on any size of the input image. The second one is that the authors wanted to deploy the idea of image or feature pyramids using pooling layers, which will allow creation of a multi-scale featture map, and thus help to obtain more robust features. 

The authors proposed at the transisition level between the convolutional layers and the fully connected layers, mutiple pooling layers must be used with completely varying scales. 

#### SPP Layer

![SPP module](https://miro.medium.com/max/1176/1*Af0rCJ67rVYdfIfhwnwi3A.png)

The SPP module is represented in the above image. As we can see the feature maps are obtained after going through the backbone network. The feature maps are of arbitrary dimension of say MxN and has 256 channels. Now, a set of pooling layers are applied with different scales, to obtain different feature maps. As we can see the 1st feature map is pooled to have one value for each channel. So, for 256 channels, there are 256 such values, which are flattened to obain a 1d vector of 1 x 256 values. The 2nd feature map is pooled such that the resultant feature map can contain 4 values for a channel, so it is flattened to create a 4 x 256d vector. Similarly, for the third scale we obtain a 16 x 256d vector.
