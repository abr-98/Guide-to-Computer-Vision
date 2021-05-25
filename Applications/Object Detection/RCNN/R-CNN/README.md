### Regional Convolutional Neural Networks (R-CNN)

R-CNN was one of the first major approaches to solve the problem of object detecttion. The approach was first proposed by Ross Girshick of UC Berkeley in the paper titled "Rich feature hierarchies for accurate object detection and semantic segmentation". We previouly had image classification algorithms which can handle only one object at a time, but as we have already seen in case of object detection, we need to detect multiple objects in an image, we needed something which can give us the regions where objects may be found and then pass these regions to get the object classifications. 

To solve the above mentioned problem Girshick proposed R-CNN. 

#### Architecture

![arch](https://lilianweng.github.io/lil-log/assets/images/RCNN.png)

The above image depicts the proposed architecture. The architecture proposes the use of a selective search algorithm for the proposal of the target regions that may contain objects in the image. 

#### Algorithm:

1. Initially, A selective search algorithm is applied on the input image. Selective search algorithm has been previously discussed. 
2. The Selective search algorithm provides 2000 region proposals for every image.  
3. Then we use a pre-trained Convolutional Neural Network on these 2000 regions to obtain the feature maps for the classifying Network.
4. The pre-trained nework is "AlexNet". The pre-trained network is fine tuned further to best fit the domain of the dataset. 
5. A final classification softmax layer with (N+1) classification nodes, N for each target class and 1 for the background. 
6. As we know CNN needs a fixed shape, so the 2000 extracted regions are warped in a fixed size and sent as input to the network for training.
7. For the target labels, every region, which has an IOU overlap of 0.5 with the actual ground truth is taken as positive sample, else taken as negative sample. 
8. For more robust training strategies like **Non-Max Suppression** and **Hard Negative Mining** have been used along with the use of a low learning rate and mini batches.
9. After training the model, the classification softmax layers are removed, in order to generate just the feature maps.
10. After generating the feature maps, the feature maps are flattened to generate 4096-d vectors, which are sent to N seperate binary SVMs, one for each class. 
11. For training the SVMs, the proposed regions with IOU >=0.3 are taken as positive samples.
12. To reduce the localization errors, a regression model is trained to correct the predicted detection window on bounding box correction offset using CNN features.

![Model](https://miro.medium.com/max/612/1*NX5yYTi-eQjP0pMWs3UbUg.png)

The bounding box coordinates are predicted by an regression model. So, its training is done using some custom multitask loss function given by:

![Loss](https://miro.medium.com/max/2142/1*PUJocoWsZIHZltbQeXsqaw.png)

The first equation shows how the predicted and the ground truth box are predicted. (px,py) give the coordinates to the center of the box and (pw,ph) give width and hieght. The equation 2 and 3 show the transformations between the Ground truth to prediction and vice versa transformations.

Fourth equation is the actual regression loss functtion, which is a MSE or least square error, with a regularization term (L1) to prevent the weights w from attaining very large velue and overfit. The importance factor *lambda* is selected using cross-validation. For the ground truth, in case of regression, we consider boxes with IOU overlap >= 0.6.


References:

1. https://arxiv.org/pdf/1311.2524.pdf
2. https://towardsdatascience.com/r-cnn-for-object-detection-a-technical-summary-9e7bfa8a557c


