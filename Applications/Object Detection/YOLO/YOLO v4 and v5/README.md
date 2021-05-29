### YOLO V4

YOLO v4 was introduced by Alexey Bochkovskiy in the paper titled **YOLOv4: Optimal Speed and Accuracy of Object Detection**. The paper made major modifications from the YOLO v3 architecture. The changes were mostly made in the architecture of the backbone model. 

#### Architecture:

![Arch](https://miro.medium.com/max/3660/1*Z5GOPYFgh7_NTr7drt45mw.png)

The image above shows the architecture of the YOLO v4 network. It has 3 seperate portion as a one stage detector. The input is first passed through a Backbone network, which can be pretrained networks like VGG, ResNet, DenseNet or Darknet53 as used in YOLOv3. The paper mentions the backbone to be CSPDarknet53, which stands for Cross-Stage-Partial-Darknet, which means that the input feature maps are divided into two parts, one of them is sent through the module,while other is directly added with the results, and the resultant is sent forward, as shown in the figure below for DenseNet. The main function of this part is to extract features from to 

![CSP](https://miro.medium.com/max/2400/0*6wqDSouRXeJIgAYj.jpeg)

The Next layer is called the Neck. This is the part connects the backbone with the head, which is the main prediction layer. YOLO v4 tries to extract predictions at different levels to get coverage of both large and smaller units. The larger feature maps help to obtain the finer features and hence the smaller objects. These finer features get omitted when we move further in the dense layers, due to the downsampling. At the deeper levels the larger objects are more robustly detected. 

The Neck portion mostly contains of layers like, Path Aggregated Networks (PaNets), Spatial Pyramidal Pooling Network (SPP_Nets) or Spatial Attention Modules (SAM). These networks are used to draw, multi scale and dimensional features to generate more robust set of features.

Then comes the Head or the Detector portion. It detects the bounding boxes and the predicts the classes, just like YOLOv3.

The YOLOv4 also introduces two types of techniques to boost up the performance of the models.

The two methods are:

1. **Bag of Freebies**: It is a set of techniques that help during training without adding much inference time. Some popular techniques include data augmentation, random cropping, shadowing, dropout, etc.

2. **Bag of Specials**: Unlike BoF, they change the architecture of the network and thus might augment the inference cost a bit. SAM, PAN, and SPP, all belong to this family.

These techniques were used in the Backbone, the neck and the head detector regions of the networks as suggested by the authors.

Reference:

1. https://arxiv.org/pdf/2004.10934.pdf
2. https://becominghuman.ai/explaining-yolov4-a-one-stage-detector-cdac0826cbd7
3. https://towardsdatascience.com/yolo-v4-optimal-speed-accuracy-for-object-detection-79896ed47b50
4. https://blog.roboflow.com/a-thorough-breakdown-of-yolov4/

### YOLO v5

YOLO-v5 was soon introduced after YOLO-v4 was introduced. It was first introduced in a github repo by Glenn Jocher the founder and CEO of Ultralytics. It's architecture is pretty similar to YOLO-v4. The details can be found in the references.

Reference:

1. https://github.com/ultralytics/yolov5
2. https://blog.roboflow.com/yolov5-is-here/
3. https://blog.roboflow.com/yolov4-versus-yolov5/








