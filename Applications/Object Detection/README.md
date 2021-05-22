### Object Detection

It is one of the major tasks in the computer vision domain. Till now we have done image classification, that is we have answered the question, **"what is the image?"**. Then we started looking at the question **"Where is the object in the image?"**, through image localization concepts. Object detection problem attempts to answer both the questions **where** and **what** together, i.e, both localization and classification. Now, in classification, we can have only one object in the image. There can be multiple objects in the image in case of object detection algorithms. For every object present in the image, we need to find where the object is present and what the object is. 

![Ex](https://miro.medium.com/max/1600/1*u3SAkFbIQHBC8hSifHUMeA.jpeg)

### Algorithms

To accomplish this task, we have uncovered several algorithms over the time. Major algorithms are:

1. R-CNN: Regional-Convolutional Network
2. Histogram of Oriented Gradients(HOG)
3. R-FCN: Regional-Fully Convolutional Network
4. Fast R-CNN
5. Faster R-CNN
6. Mask R-CNN
7. Spatial Pyramid Pooling (SPP-net)
8. Single Shot Detector (SSD)
9. You Only Look Once (YOLO)
10. MobileNet (For embedded and mobile devices)

HOG is one the traditional descripter based method. Others are majorly divided into two classes based on the methodology of the algorithms:

**1. Classification based methods:** Methods like RCNN, Fast RCNN, Faster RCNN amd SPP-Net models the Object Detection problem as classification problem . So, in this case, we take windows of fixed side from input images, from locations that may contain objects, and feed the patches to the image classifiers. so, we know the location through the windows and the classifier replies the "what" question. So, these are two step detectors. On first stage, the algorithm selects the proposed regions where objects are present and on the second stage it deploys the classifier on the regions proposed.

**2. Regression based methods:** Methods like YOLO and SSD formulate the object detection problem differently. These classifiers detects and classifies the objects on an image on a single shot. Instead of selecting regions or patches, these algorithms detects images and places bounding boxes all over the image.

