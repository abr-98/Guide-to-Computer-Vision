### MASK-RCNN

Mask-RCNN is a extended version of Faster-RCNN designed in order to achieve instance segmentation. It was proposed by Kaiming He from Facebook AI Research in the paper "Mask R-CNN". The authors added a third mask prediction branch to the pre-existing Class and bounding box predictors in faster RCNN. The authors have used a FCN or fully convolutional networks on the obtained feature maps after the ROI pooling layers, in order to learn the mask predictions. 

![Arch](https://miro.medium.com/proxy/1*IWWOPIYLqqF9i_gXPmBk3g.png)

The above image shows the official architecture of Mask RCNN. Similar to Faster RCNN, Mask RCNN also uses Region Proposal Network (RPN) in order to propose the region of Interests that may contain objects. After obtaining the ROI proposals, in faster RCNN, the region proposals are sent through ROI-Pooling layers, in order to transform the varying sized region proposal into fixed sized feature maps, for predictions. The Mask-RCNN authors replaced the ROI pooling layers into ROI-Align layers. The results of the ROIAlign layer are sent to the heads for detection.

#### Back-bone and Head Structure details:

![Back_Head](https://miro.medium.com/max/2286/1*IV6q-xtvxdLTg1h9Jk5lGg.png)

Faster RCNN uses ResNet as a the back-bone, while the Mask RCNN uses a total of 3 back-bones and compare their corresponding performances. The head structures also changes with the architectural back bone. The above image shows the backbones and their head structure. The proposed backbones are ResNet, ResNeXt, and ResNet with FPN. If we do not use FPN the authors have used two layers of convolutions before splitting else if FPN is used, the network is directly split into two heads. One head for classification and bounding box and the second head for the mask.

![Over all architecture](https://miro.medium.com/max/533/1*Tm5ia-bzsVq3lw8TJt08YA.png)

The overall architecture of Mask-RCNN.

#### ROI-Align layer

As we have seen in case of Faster R-CNN, we use ROI-pooling to represent the varying sized ROIs in a fixed size. The ROI pooling layer divides the ROIs into fixed number of divisions, and it picks the max value from each division, so we obtain a fixed size resultant feature maps. Now, for this conversion from a h x w image to H x W image, we take h/H x w/W to be a division. But, h/H and w/W may not be integers, so we need to floor the value down, as the index can't be float values. So, every time we do this we lose some data. This process is called Quantization. In Faster RCNN, this happens twice, once when the ROIs are mapped on the actual images, and secondly in the ROI pooling layers. This does not cause much trouble in object detection, but in case of instance segmentation, this causes a significant misalignment, due to the pixelwise predictions and loss of information. To prevent the loss of information, the Mask-RCNN introduced ROI-Align. The authors used bilinear interpolations to create 4 points with interpolated values for each divisions and avoid quantizations. The max of these 4 values is taken as the representing value for the division. 

#### Loss

The Loss function used is again an extension of the loss function used in faster-RCNN. The Faster RCNN contains two components in its loss function, while the Mask RCNN adds the third component for the Mask predictions.

![loss](https://images1.programmersought.com/60/12/12c7259bbd34305df9f55905957b7174.png)

The Loss Lcls and Lbox is same as faster-RCNN. Lmask is responsible for training the masks. For K classes, M\*M size feature map is taken. Sigmoid activation function is used in the last layer of the network, for predictions, and an average binary cross-entropy is used as loss function. The binary cross-entropy is calculated for all the K classes seperately and then their average is taken. If the class label is the i-th class during training, then only the loss of the i-th mask output is calculated as Lmask, and the other K-1 mask outputs contribute 0 to Lmask.

References:

1. https://arxiv.org/pdf/1703.06870.pdf
2. https://medium.com/analytics-vidhya/review-mask-r-cnn-instance-segmentation-human-pose-estimation-61080a93bf4#:~:text=Mask%20R%2DCNN%20is%20one,based%20on%20Mask%20R%2DCNN.
3. https://www.programmersought.com/article/61614366875/

ROI Align:
1. https://towardsdatascience.com/understanding-region-of-interest-part-2-roi-align-and-roi-warp-f795196fc193
2. https://towardsdatascience.com/understanding-region-of-interest-part-1-roi-pooling-e4f5dd65bb44
3. 










