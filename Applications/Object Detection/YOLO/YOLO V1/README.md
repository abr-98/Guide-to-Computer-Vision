### YOLO Version 1 or YOLO

The YOLO algorithm is known to be one of the first one shot detectors use to detect multiple objects in an image in real time. The paper was proposed by Facebook AI research in 2016 in the paper titled: "You Only Look Once:
Unified, Real-Time Object Detection".

#### Idea
The basic idea behind the YOLO algorithm is to divide the original input image is S x S subgrids and predict the object in each grid seperately and simultaneosly and thus speeding up the process. In the original paper, the value of S=7. So, the authors divided the entire image into 7x7=49 total grids. 

![Divisions](https://miro.medium.com/max/770/1*9nikM2b0u-m67SJpQXftKA.png)

For each grid cell, if the centre of an object falls in a grid cell, that grid cell is responsible for detecting the object. But one grid can have detect only one object. So, all over the 49 grids only 49 objects can be detected.

![Center](https://miro.medium.com/max/667/1*4Y1PaY3ZgxKt5w84_0pNxw.jpeg)

For example, in the above figure, the cell marked by yellow is reponsible for detecting the person because the center of the person falls in that paeticular cell or grid. Now, in order to localize or get the idea of the location of the object detected, each grid can predict a fixed number of bounding boxes (shown in blue). In the original paper the number of bounding boxes that can be used is B=2, as shown in the image.  

The issue with the algorithm is it can only detect fixed number of objects and one grid can only detect one object. This prevents the algorithm from detecting smaller and multiple elements. 

For every cell grid, the YOLO predicts:

1. B boundary boxes using 4 values (bx, by, bh, bw) giving the center and the hieght and weight of the bounding boxes respectively, The values are normalized, so, the values fall between 0 and 1. 
2. A confidence score for each bounding box. It shows the how likely is tha fact that, there are objects in the bounding boxes. It is also termed as objectness. 
3. C conditional class probabilities, for each class that need to be detected in the image. 

So, the output shape of YOLOv1 algorithm is: S x S x (B x 5 + C). where S is the number of Grids, B is the number od bounding boxes and C is the number of classes to be classified. For the original network, it creates an output of dimension of 7 x 7 x (2 x 5 + 20)  = 7 x 7 x 30 which is reshaped as (7,7,30) output dimensions. It creates and predicts the values for two boundary boxes.

#### Architecture

![Arch](https://miro.medium.com/max/3840/1*9ER4GVUtQGVA2Y0skC9OQQ.png)

The YOLO v1 architecture has 24 convolutional layered architecture: 20 layers of pretrained network followed by 4 more convolutional layers, further followed by 2 fully connected layers. One with 4096 nodes and the last one with 7x7x30 nodes which gives an output of (7, 7, 30) as we want. The architecure is inspired by GoogleNet's architecture and has 1x1 reduction layers to reduce dimensions along with 3x3 convolutions.  The last layer predicts the outputs as linear Regression, as we do not use a softmax or sigmoid function. The CNN networks outputs the feature maps of dimension 7 x 7 x 1024. which is falttened and sent to fully connected layers.

#### Loss function

Similar to the RCNN family, the YOLO algorithm also uses a multipart multitask loss. It uses sum of squared errors SSE for each part and scale them using scaling or weightage variables to maintain the importance of the term in the loss function.

![loss](https://miro.medium.com/max/2400/1*aW6htqx4Q7APLrSQg2eWDw.png)

Now, as we can see our loss function actually has total 5 parts which actually derived from three main losses:

1. The localization loss: It is the loss obtained as the sum of squared differences between the predicted bounding box and the actual bounding box.

Given by:

![loc_loss](https://miro.medium.com/max/700/1*BwhGMvffFfqtND9413oiwA.png)

The *lambda coord* controls the weight of localization error in the loss function. Now, as YOLO predicts bounding boxes for small as well as large objects the error is taken as the squared difference between the square root of the width and hieght instead of the actual values of width and hieght of the bounding boxes. The first part of the error gives the SSE between the center points of the bounding boxes. The *lambda coord* is kept at a default value of 5.

2. Confidence loss: It focuses on the confidence of the model about the objectness of the bounding box, or what is the probability of the box really containing an object. We consider an weighted sum of errors for the boxes containing the objects and the boxes not containing the objects.

For the box containing the objects, the error is given by:

![contain](https://miro.medium.com/max/700/1*QT7mwEbyLJYIxTYtOWClFQ.png)

If the box does not really contain the objects, the error is given by:

![not_contain](https://miro.medium.com/max/700/1*Yc_OJIXOoV2WaGQ6PqhTXA.png)

A weight parameter is used the boxes, that does not have the objects, and kept a value of 0.5. This is kept as most of the boxes do not have any objects, it creates a huge imbalance, in classes. So, we use a weighted to loass function to give lower importance to the over represeneted class. 

3. Classification loss: If an object is detected, the classification loss at each cell is the squared error of the class conditional probabilities for each class.

![class](https://miro.medium.com/max/700/1*lF6SCAVj5jMwLxs39SCogw.png)

#### Training and Evaluation

For training the, confidence value c for each bounding box is taken as the IoU value of the actual bounding box and the predicted bounding box. So, we obtain a score of 0 for bounding box which has no object, and a score of 1 for the boxes, which completely overlap with the actual boxes.

The Evaluation is done using a metrics called the **class confidence score** given by: 

class confidence score = box confidence score x conditional class probability.

It measures both the classification and the localization of the object.

Defn:

![defn](https://miro.medium.com/max/700/1*0IPktA65WxOBfP_ULQWcmw.png)

The algo also uses a concept of Non-Max Supression to obtain the best bounding box for an object, if it is detected by multiple bounding boxes. It selects the bounding box with the highest confidence value, rejecting the others. If other bounding boxes has a IOU >0.5 with the best selected box, the boxes are removed.

Reference:

1. https://arxiv.org/pdf/1506.02640.pdf
2. https://towardsdatascience.com/yolov1-you-only-look-once-object-detection-e1f3ffec8a89










