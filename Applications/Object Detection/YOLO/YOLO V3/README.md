### YOLO V3

Yolo V3 was published with some improvements and some tuning of old ideas from YOLO v2 by Joseph Redmon and Ali Farhadi. 

It brought some changes to the idea of how YOLO v2 detected objects, the architecture and the loss functions used. 

It was noticed that, YOLOv2 considers all the labels mutually exclusive, i.e, it can predict only one label for an object detected. But, if there is a child walking on the street, it can be classified as both "pedestrian" and "child" and the labels are not mutually exclusive. This multilabel classification is not possible in YOLO v2 as it uses, Softmax function in the last layer. For softmax all probabilities sum up to 1 and it outputs the class with maximum probabiity. So, in order to create a multilabel detection, YOLO v3 replaces the final softmax layer with independent logistic regression for individual labels to predict the likeliness of the specific label. So, instead of using a mean square error as loss function, the authors use classification loss. As, we are using individual logistic regression, for each object, so, the model can either predict 0 or 1, so a binary cross-entropy as the loss function. This also reduces computation complexity.

YOLOv3 also uses logistic regression for the confidence score. There is one bounding box for each object. If the bounding box overlaps with the ground truth more than any other bounding boxes the objectness score is 1. If other predicted bounding box overlaps with the ground truths more than the threshold (0.5), no classification loss and localization loss is incurred. Other bounding boxes are ignored.

The network predicts 4 coordinates for each bounding box, tx, ty, tw, th. If the cell is offset from the top left corner of the image by (cx,cy) and the bounding box prior has width and height Pw, Ph, then the predictions correspond to:

![bounding](https://miro.medium.com/max/235/1*L2mpfhg2tixnWJqMSyoEEQ.png)

where,

![box](https://miro.medium.com/max/402/1*K5_cJ0wy_7uOxXvrm-4rQw.png)

#### Change in modelling

YOLO struggles to detect small objects as due to the downsampled feature maps, the finer details are missed. YOLO v3 improves the small object detections using short cut connections, which helps to allow obtain finer features. YOLO v3 predicts at three levels instead of YOLO V2's single level prediction. So, YOLO v3 adapts and functions like a feature pyramid network, and uses different sized feature maps for prediction. 

YOLO v3 predicts from the last feature maps. Then, it goes back 2 layers back and upsamples it by 2. YOLOv3 then takes a feature map with higher resolution and merge it with the upsampled feature map using element-wise addition. YOLOv3 apply convolutional filters on the merged map to make the second set of predictions. Agein it repeats the same above process to obtain the third set of predictions.

#### DarkNet-53:

The YOLO-v3 introduces  DarkNet-53 replacing Darknet-19 as the feature extractor. It consists of 3x3 convolutions followed by 1x1 filters for dimensionality reductions. Skip connections like the residual networks has been introduced in Darknet-53 as an additional change.

![Model](https://miro.medium.com/max/334/1*biRYJyCSv-UTbTQTa4Afqg.png)


The above image gives the model.

Apart from all these changes, authors applied a K-means clustering and chose 9 anchor boxes with pre-decided dimensions based on the size and dimension of the input image. The 9 anchor boxes are of the size:  (10×13),(16×30),(33×23),(30×61),(62×45),(59× 119),(116 × 90),(156 × 198),(373 × 326) respectively. Now, these 9 boxes are divided in groups of 3 based on their dimensions. Each group is assigned one of the 3 set of predictions that the model produces, as discussed above. The assignment is done based on the dimension of the feature maps at each level of prediction and the size of the anchor boxes.

At each level of prediction, 3 anchor boxes are assigned for each grid cell, so, for each predicted output, the size of the output is N x N x \[3 x (4 + 1 +80)], where N is the number of grids the feature map is divided into, 3 is the number of anchor boxes, 4 are boundary box predictions, 1 is the objectness score, and 80 are the total number of classes to be predicted.

References:

1. https://arxiv.org/pdf/1804.02767v1.pdf
2. https://medium.datadriveninvestor.com/review-on-yolov3-faae0dd59425
3. https://towardsdatascience.com/yolo-v3-object-detection-53fb7d3bfe6b

