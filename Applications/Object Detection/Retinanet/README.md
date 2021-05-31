#### RetinaNet

RetinaNet was proposed by Tsung-Yi Lin at Facebook AI Research in the year 2018. RetinaNet was proposed as a one stage detector like SSD and YOLO. The RetinaNet introduced a Focal loss inorder to deal with the imbalance in the data samples while training object detection networks.

There are two types of negatives in detection problems, "easy negatives" (the plain background classes, without any type of noise) which are detected very easily by the detectors, and the "hard negetives" (having noise in the background) which are not detected easily. We need to train the model harder on the hard negtives rather than the easy ones. Other than that there is a huge class imbalance between the foreground and the background detections in the object detections. Several methods like SSD use methods like "hard negative mining" but when a large number of bounding boxes are predicted, it is impossible to handle the imbalance using plain bootstrapping. 

To handle this RetinaNet, introduced the concept of **focal loss**.

#### Focal loss

RetinaNet was able to detect about 100k boxes by resolving the class imbalance problem using focal loss.

For the normal Cross-Entropy we use, 

**C.E = - ylog(p) - (1-y)log(1-p).**

so for y=1 we get the first part and if y=0 we go for the 2nd part. But in this case, we focus on both the classes equally plus the loss contributions from the easy negatives are much much bigger than the hard negative ones, due to the imbalance between the foreground and background. The hard negatives are mostly obtained from places which are foreground but are not detectable objects. This imbalance leads to overshadowing of the "hard-negative classes". 

One of the methods to deal with the problem was the alpha-balanced loss equation given by:

**alpha weighted C.E= alpha\*y\*log(p) - (1-alpha)\*(1-y)\*log(1-p).**

Now the alpha parameter is the ratio between the frequency of the over-represented class and the under represented class. So, larger the value of alpha more weighted the error is for the under-represented class, and less weighted is the higher represented background class. In real sceneraio, alpha is found using cross validation.

The idea of focal loss went on to penalize and train, focussed more on the hard negatives training. They replaced the loss functions as:

**Focal loss= (1-p)^gamma\*y\*log(p) - p^gamma\*(1-y)\*log(1-p).**

So, if the examples are easy negatives, there probability of prediction is close to zaro, so log(1-p) tends to be 0, but for hard negatives, the model tends to predict them, as 1 so, the value of log(1-p) tends to be a higher negtive number, and more the value of the predicted probability more is the weightage due to the p^gamma term. How much we want to penalize is controlled by the gamma parameter. It has values from \[0,5]. Similarly, for the easy ones the value of predicted probability is less, and thus so is the weightage.

The variant used in RetinaNet is the alpha-variant of the Focal loss, which made it extremely customized due to the alpha and gamma control variables. It is given by:

**alpha variant Focal loss= alpha\*(1-p)^gamma\*y\*log(p) - (1-alpha)\*p^gamma\*(1-y)\*log(1-p).**\

This lets the loss function focus on the imbalance and the hard negatives at the same time.

#### RetinaNet Training

The RetinaNet used the alpha-trained Focal loss for the classification loss, and L1-smooth loss for the bounding box regression, just like SSD and fast-RCNN. So, these two combined make up, the multi-task loss function for the RetinaNet.

Total loss is given by:

Loss= lambda\*localization loss + classification loss.

where lambda is the weight control parameter. 

#### Matching

In case of RetinaNet, we use the predicted boxes, that have IOU>=0.5 with the grund truth as positive and the ones with IOU<=0.4 as negative and ignore from 0.4 to 0.5. For the range IOU>=0.5 the classification loss is considered. 

#### Architecture of RetinaNet

RetinaNet uses a combination of Feature Pyramid Network and ResNet as backbone network for prediction.

![Arch](https://blog.zenggyu.com/post/2018-12-05/fig_1.jpg)

The above network gives the architectural details of the RetinaNet. FPN is built on top of a ResNet, which serves as the deep feature extractor and the bottom up pathway of the FPN network. The top down pathway is used to predict and detect the object at different resolutions, which help the model detect different size of objects. 

![Arch_FPN](https://lilianweng.github.io/lil-log/assets/images/featurized-image-pyramid.png)

The above architecture was proposed for FPN. The architecture of RetinaNet remains similar, but in case of ResNet there are 5 layers in both the bottom up and top down paths. So, we get C5 also, on which we apply 3x3 convolutions to obtain P5 and, then we apply a 3x3 conv with stride 2 on C5 again to obtain P6. We further apply 3x3 conv,with stride 2 and ReLU on P6 to get P7. P3 to P7 are used for predictions to give multi-scale detections,

The upper layers are smaller in dimansion and robust to detect large objects and vice versa. All the feature maps are sent to the classification  and regression box subnets for further detection. The classification subnet gives an output of W x H x KA and the regression subnet gives an output of W x H x 4A, where W and H are width and hieght of the feature maps on which the predictions are done, A is the number of anchor boxes and K is the number of classes we want to predict.

The authors have considered 9 anchor boxes per level. The size ratios used are 2^0, 2^(1/3), 2^(2/3) and each size has three aspect ratios 1/2,1 and 2.

References:

1. https://arxiv.org/pdf/1708.02002.pdf
2. https://arxiv.org/pdf/1612.03144.pdf
3. https://towardsdatascience.com/review-retinanet-focal-loss-object-detection-38fba6afabe4
4. https://blog.zenggyu.com/en/post/2018-12-05/retinanet-explained-and-demystified/
5. https://medium.com/@14prakash/the-intuition-behind-retinanet-eb636755607d



