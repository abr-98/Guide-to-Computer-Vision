### Faster RCNN

The Fast RCNN worked fine, but in real time environments, we needed a faster algorithm, which can detect objects very quickly. The speed of the Fast RCNN was capped due to selective search algorithm which served as the botteleneck. The Faster RCNN was proposed by Shaoqing Ren and Ross Girshick, where the authors replaced the Selective Search algorithm with a network called RPN or Region Proposal Network. They let the network learn to find out the best target regions which may contain the objects in the image.

#### Architecture

![Arch](https://miro.medium.com/max/770/1*pSnVmJCyQIRKHDPt3cfnXA.png)

The algorithm introduces the Region Proposal Network which is discussed earlier. The RPN selects the target regions which are passed on to the ROI pooling layers, where the classifiers and the bounding box regressors predict the class of the images and the bounding boxes.

#### Algorithm

The image is passed through the convolutional pre-trained backbone and the feature maps are obtained. The image dimensions and the backbone network is same as Fast RCNN. The RPN gives the proposals as previously discussed which are sent to the RoI pooling layer. The operations, loss and training further are similar to that of Fast RCNN. 

#### Full Structure

![Struct](https://miro.medium.com/max/770/1*tTqg3W165itg-LVRFxHJfA.jpeg)

References:

1. https://arxiv.org/pdf/1506.01497.pdf
2. https://towardsdatascience.com/faster-r-cnn-for-object-detection-a-technical-summary-474c5b857b46

