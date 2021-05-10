### Densenet

Densenet was first proposed in 2017 by a joint team of Tsinghua university, Cornell University and Facebook AI Research. 

The idea of densenet is driven as a modified idea of Pre-activated Resnet with much more stronger gradient flow. Densenet modified the resnet module completely. In the basic version, the authors ensured, that while extracting, each layer has the additional inputs from all the previous layers and passes on the feature maps. The feature maps are concatenated in Densenets instead of adding the gradients as in Resnets.

![Densenet](https://miro.medium.com/max/770/1*rmHdoPjGUjRek6ozH7altw.png)

The above image represents the structure of Densenets. Each layer recieves "collective Knowledge" of all previous layers. Now this arrangements lets us use a controlled number of channels, given by growth rate k. K is the number of channels added for each layer and the concatenated feature maps move forward.

![Concat](https://miro.medium.com/max/660/1*9ysRPSExk0KvXR0AhNnlAA.gif)

The module was then modified in a format of the preactivated Resnet having, batch normalization, ReLU, a 3x3 convolution layer and to reduce rhe complexity and size was additionally convoluted with a 1x1 filter for each block in a layer.

![final](https://miro.medium.com/max/770/1*dniz8zK2ClBY96ol7YGnJw.png)

#### Architecture

![Arch](https://miro.medium.com/max/770/1*BJM5Ht9D5HcP5CFpu8bn7g.png)

Three blocks of Densenet module is used in the final architecture, with a transition block, containing a 1x1 convolution and an average pooling layer. At the end of the last dense block, a global average pooling is performed and then a softmax classifier is attached.

Reference:

1.https://towardsdatascience.com/review-densenet-image-classification-b6631a8ef803
2.https://arxiv.org/pdf/1608.06993.pdf

More at:
https://towardsdatascience.com/densenet-2810936aeebb
