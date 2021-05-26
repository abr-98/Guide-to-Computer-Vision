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




