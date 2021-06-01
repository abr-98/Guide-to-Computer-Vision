### Path Aggregation Network (PANet)

PANet was first proposed by The Chinese University of Hong Kong, Peking University, SenseTime Research, and YouTu Lab, Tencent through the paper "Path Aggregation Network for Instance Segmentation". PANet has been used in several areas like in YOLO v4 for object detection. The authors introduced three chief ideas:

1. Bottom-up path augmentation for shortening the information path between the lower and higher feature map layers.
2. Adaptive feature pooling to obtain the best features after pooling from any feature level
3. Fully connected fusion layer to train the model parameters and get the spatial information in a better way at the same time to improve the mask prediction.

The authors extended their work on the basic principals of Feature Pyramid Network or FPN proposed initially by Facebook AI Research (FAIR).

#### Architecture

![arch](https://miro.medium.com/max/2778/1*dyFC1OPnAZGTxnaQzNrCrw.png)

The above image represents the archiecture proposed by the authors. The (a) portion of the above image, shows the Feature Pyramid network. The (b) part of the image shows the augmented bottom-up path which serves as the shortcut connection. The authors used ResNets as the backbone network of the FPN. Now, as we know in FPN, we obtain a several feature maps, of different sizes based on the level in the pyramid network. We apply convolutions on the feature maps P2 to P5 which gives us the learnable features in case of normal FPN. The authors argue that as there can be more than 100 layers in the backbone network and so the complexity of the path makes it impossible for the lower level features to maintain the finer details as we move to the layers of the top down path, which is depicted by the red dotted line. 
