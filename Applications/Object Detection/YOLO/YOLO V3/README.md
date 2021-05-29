### YOLO V3

Yolo V3 was published with some improvements and some tuning of old ideas from YOLO v2 by Joseph Redmon and Ali Farhadi. 

It brought some changes to the idea of how YOLO v2 detected objects, the architecture and the loss functions used. 

It was noticed that, YOLOv2 considers all the labels mutually exclusive, i.e, it can predict only one label for an object detected. But, if there is a child walking on the street, it can be classified as both "pedestrian" and "child" and the labels are not mutually exclusive. This multilabel classification is not possible in YOLO v2 as it uses, Softmax function in the last layer. For softmax all probabilities sum up to 1 and it outputs the class with maximum probabiity. So, in order to create a multilabel detection, YOLO v3 replaces the final softmax layer with independent logistic regression for individual labels to predict the likeliness of the specific label. So, instead of using a mean square error as loss function, the authors use classification loss. As, we are using individual logistc regression, for each object, so, the model 
