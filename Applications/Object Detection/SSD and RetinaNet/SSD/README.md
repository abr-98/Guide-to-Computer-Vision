### Single Shot Detector

It is one of the earliest attempts in order to build an one stage object detector, i.e, without the region proposal part as in the two stage detectors in the RCNN family. The concept was put forward by Wei Liu in the paper titled "SSD: Single Shot MultiBox Detector". The algorithm was fast and meant for real time object detection.

Instead of using a region proposal algorithm to propose a region and using classification algorithms on the proposed regions, Single Shot detectors the sent the image through a backbone network and generated a feature map, divided it into grids and applied detection and classification on each of the grids simultaneously in a single stage.

#### Architecture

![Arch](https://miro.medium.com/max/2464/1*hdSE1UCV7gA7jzfQ03EnWw.png)

The architecture of the single shot detector is given in the above image. It has a base network which can be any pretrained network, that functions like a backbone, and extracts a feature map from the image. In the paper, the used backbone in VGG-16 network. The VGG-16 network provides the feature map of size 38 x 38 x 1024 after the Conv_5_3 or the final layer of the network. The authors have added 6 convolutional layers after the backbone network in order to downsample the feature map and extract more robust features.

SSD make predictions from 6 levels of the feature maps. This form a image pyramid type structure. The base feature obtained from the Conv_4_3 layer of the  backbone network, of size 38 x 38 gives the first set of detections. Then the map obtained from the backbone is downsampled using 6 more convolutional layers. The first obtained feature map is of dimension 19x19, which gives the second set of detections. We further apply convolutions on it to obtain another feature map of dimension 10x10, which gives the third set, and then we get 5x5,3x3 and 1x1 size feature maps correspondingly.

![Pyramid](https://miro.medium.com/max/700/1*sZUWR2XgCAJ6AXM5NXYjNg.png)

The larger feature maps are responsible for the detection of the finer features and thus the samller objects, while the downsampled feature maps having more globally robust features are responsible for the detection of the larger objects in the image. 


#### Localization:

The SSD algorithm, like YOLO also divides the feature maps into grids, the first feature map in 38x38, the second one in 19x19 and so on. The SSD algorithm uses anchors (called default box here) just as YOLO and Faster RCNN. The anchors are responsible for detecting the position of the objects. The authors have used a k-means clustering method to determine the number of anchor boxes to be used for a particular grid. The authors decided to use 4 anchor boxes for few level of predictions out of the 6 and 6 anchor boxes for other levels. The number of anchor boxes for each level were chosen based on the results of the k-means clustering.

![anchor](https://miro.medium.com/max/2400/1*vNaiiFUVwCfzx1znKiFYYw.jpeg)

So, for the 38x38 feature map we have 4 anchor boxes for each grid. For the 19x19 feature map size level we have 6 boxes for each grid each, then again  per grid for 10x10 feature map level, 6 for 5x5 level, and 4 for 3x3 and 1x1. So, total we the SSD outputs predictions for 8732 anchor boxes. The anchor boxes vary in scales and aspect ratios, with respect to the size of the feature maps used on the level. The aspect ratio is fixed to some values which help the anchor boxes initiate with a size that can detect objects easily, and helps the network to obtain stability. The 5 aspect ratios and there corresponding hieght and widths are:  

![ar](https://miro.medium.com/max/558/1*vI4qQt5MRNTtOA1ODyKbEA.png)

1:1 is used as the 6th aspect ratio. So, we obtain 6 anchor boxes and  for the levels with 4 anchor boxes the 1/3 and 1 aspect ratios are dropped. And sk is the scaling factor for the anchor boxes, given by:

![scale](https://miro.medium.com/max/868/1*bX2dGa3mgbO5Fdwv8biQUg.png)

Where k denotes the level of the feature map. Smin is the minimum scale 0.2 and Smax is the maximum scale 0.9 and the total number of levels m=6.

#### Prediction

For each anchor box, we obtain the 4 details values for the bounding boxes (∆cx,∆cy,w,h), 21 class probability values, 20 for the specific classes and 1 for the background class. Bounding box with shape offset. ∆cx, ∆cy, h and w, representing the offsets from the center of the anchor box and its height and width So,each of the anchor boxes predicts 25 values. So, in the first level, we get 38 x 38 x 4 x (21 + 4) predictions. We obtain the feature maps of NxNxM directions, where M is the number of channels and used 3x3 convolutions to obtain the results.   

SSD predictions are classified as positive matches or negative matches. SSD only uses positive matches in calculating the localization cost. If the corresponding anchor box has an IoU greater than 0.5 with the ground truth, the match is positive. Otherwise, it is negative. It also uses a Non-max supression method to obtain the predicted box. The box with the maximum overlap with the ground truth is chosen.

#### Loss Function: 

Like other object detection network and mostly like fast and faster RCNN the SSD uses a multi task loss function. Its loss function consists of two terms. One term serves as the loss function for the localization portion and the second term serves for the class prediction confidence score. 

Localization loss is given by a smooth L1 loss as in case of Fast RCNN. It is given by:

![loc_loss](https://miro.medium.com/max/590/1*yOU4TCmYwLgS06kvcfSWxA.png)

Lloc is the localization loss which is the smooth L1 loss between the predicted box (l) and the ground-truth box (g) parameters. These parameters include the offsets for the center point (cx, cy), width (w) and height (h) of the bounding box.

The Confidence loss for the class prediction is given by:

![Conf](https://miro.medium.com/max/770/1*flNOlxfJj0Pyt1lNZmQaLA.png)

Lconf is the confidence loss which is the softmax loss over multiple classes confidences (c).

The combined loss is given by:

![Total](https://miro.medium.com/max/900/1*vfpARz-ozzpb0jHM8yJ0zA.png)


The alpha value is a weight variable and set to 1.

References:

1. https://arxiv.org/pdf/1512.02325.pdf
2. https://towardsdatascience.com/review-ssd-single-shot-detector-object-detection-851a94607d11
3. https://jonathan-hui.medium.com/ssd-object-detection-single-shot-multibox-detector-for-real-time-processing-9bd8deac0e06










