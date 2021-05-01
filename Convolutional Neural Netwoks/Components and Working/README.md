There are some basic components which are very essential to build a convolutional network. We are going to talk about them.

![Schematic](https://www.researchgate.net/publication/336805909/figure/fig1/AS:817888827023360@1572011300751/Schematic-diagram-of-a-basic-convolutional-neural-network-CNN-architecture-26.ppm)

The above image gives a schematic representation of the parts and functioning of Convolutional Neural Networks. A CNN model consists of mainly two portions: 

1. A Convolution part to extract the features. 
2. A Fully Connected part to learn the features and deliver the final predictions.

The Fully connected layer units are different from the Convoluional layer units as they are dense artificial neurons to learn from 1-dimensional flattened features. 

For several problems like segmentation problems, we remove the Fully connected classification layers from the CNN architecture and replace it using 1x1 convolutional layer to coupled with a sigmoid or a softmax activation to provide the output on a pixel wise basis.

