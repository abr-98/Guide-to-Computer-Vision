### Path Aggregation Network (PANet)

PANet was first proposed by The Chinese University of Hong Kong, Peking University, SenseTime Research, and YouTu Lab, Tencent through the paper "Path Aggregation Network for Instance Segmentation". PANet has been used in several areas like in YOLO v4 for object detection. The authors introduced three chief ideas:

1. Bottom-up path augmentation for shortening the information path between the lower and higher feature map layers.
2. Adaptive feature pooling to obtain the best features after pooling from any feature level
3. Fully connected fusion layer to train the model parameters and get the spatial information in a better way at the same time to improve the mask prediction.

The authors extended their work on the basic principals of Feature Pyramid Network or FPN proposed initially by Facebook AI Research (FAIR).

#### Architecture

![arch](https://miro.medium.com/max/2778/1*dyFC1OPnAZGTxnaQzNrCrw.png)

The above image represents the archiecture proposed by the authors. The (a) portion of the above image, shows the Feature Pyramid network. The (b) part of the image shows the augmented bottom-up path which serves as the shortcut connection. The authors used ResNets as the backbone network of the FPN. Now, as we know in FPN, we obtain a several feature maps, of different sizes based on the level in the pyramid network. We apply convolutions on the feature maps P2 to P5 which gives us the learnable features in case of normal FPN. The authors argue that as there can be more than 100 layers in the backbone network and so the complexity of the path makes it impossible for the lower level features to maintain the finer details as we move to the layers of the top down path, which is depicted by the red dotted line. The authors propose a augmented bottom-up path with clean lateral connection so that the inital low level finer features are not faded. As we can see and the authors pointed out, there will hardly be 10 layers between the shortcut P2 and the high level feature map N5, which is depicted by the green arrow. 

{N2, N3, N4, N5} denote the newly generated feature maps corresponding to {P2, P3, P4, P5}. N2 is simply P2 without any processing. Each building block takes a higher resolution feature map Ni and a coarser map Pi+1 through lateral connection and generates the new feature map Ni+1. Each feature map Ni first goes through a 3×3 convolutional layer with stride 2 to reduce the spatial size.Then each element of feature map Pi+1 and the down-sampled map are added through lateral connection. The fused feature map is then processed by another 3×3 convolutional layer to generate Ni+1 for following sub-networks, as mentioned by the paper.

![connect](https://miro.medium.com/max/946/1*5_6lv-DjlBREha7ZSXsQPw.png)

#### Adaptive Feature Pooling

Normally, for pyramidal feature extraction, where we extract different features from different levels, we mostly consider that the smaller object and finer local details come from the lower level feature maps, and the larger objects are mostly detected from the upper layers or the smaller feature maps. The authors proved this theory may not be correct. The correlations between the feature size and the feature map level may penalize the performance. So, the authors wanted to let the model choose the best fit feature level for a particular object, using an element wise sum or max fusion operations. This part is represented in (c) portion.

First, for each proposal, we map them to different feature levels, as denoted by dark grey regions in the first figure (b). ROIAlign is used to pool feature grids from each level. Then a fusion operation (element-wise max or sum) is utilized to fuse feature grids from different levels.

#### Fully connected fusion

![fusion](https://miro.medium.com/max/1482/1*ofrdo6nQNC74OiAHW03_jw.png)

It was observed by the authors that using fully connected layers helped to learn the features in a much better way compared to FCN with sigmoid or softmax activations, as they are location sensetive since there are differrnt parameters corresponding to different locations in the input, while FCN preserves the spatial structure. PANet uses information from both of these layers to provide a more diverse view for the network while making decision as shown in the above diagram.

References:

1. https://arxiv.org/pdf/1803.01534.pdf
2. https://becominghuman.ai/reading-panet-path-aggregation-network-1st-place-in-coco-2017-challenge-instance-segmentation-fe4c985cad1b
3. https://medium.com/analytics-vidhya/improving-instance-segmentation-using-path-aggregation-network-a89588f3d630






