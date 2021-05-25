### Fast R-CNN

R-CNN algorithms had a number of issues:
1. It had to propose 2000 candidates using selective search and train the neural network seperately on the regions. and then generate feature maps seperately, so it was very time consuming
2. The R-CNN algorithm needed to train three different algorithms CNN for obtaining the feature maps, SVM for the classification and a Regression model for finding the bounding boxes.

The author of R-CNN, Ross Girshick propoposed, a new and modified network in order to solve the above problems with the R-CNN network.

#### Architecture:

![arch](https://lilianweng.github.io/lil-log/assets/images/fast-RCNN.png)

The above image shows the architecture of the Fast R-CNN algorithm. This algorithm also uses selective search algorithms alike R-CNN (discussed earlier). The Fast R-CNN consists of a CNN (usually pre-trained on the ImageNet classification task) with its final pooling layer replaced by an “ROI pooling” layer and its final FC layer is replaced by two branches — a (K + 1) category softmax layer branch and a category-specific bounding box regression branch.

#### Algorithm:

1. In the initial step, the image is passed through a basic pre-trained backbone network like VGG with a stride of 16 just like the R-CNN network. The initial size of the image is 1000 x 600 as was in the case of R-CNN also. The last layer of the backbone is 512. So, the size of the feature map is 1000/16 x 600/16 x 512 = 60 x 40 x 512.
2. Similar to the RCNN, the projection of the Region of Interests from the actual image to the feature maps is done by projecting the centre of the actual image to a pixel on the feature map.
3. Next, similar to RCNN, we use a Selective Search algorithm to find the target region of interest, but this time on the feature maps. The selective search algorithms generate about 2000 ROI or target regions.
4. Now, to feed the Connected layers, the ROI feature maps must be equal in size. To solve this problem, we use a specially designed max pooling layer called the ROI pooling layer. This layer was introduced as a modification from the SPP-Net. It works by dividing the whole image into a N number of sub-division or parts, and we use max-pooling in each of the parts, so, we get N values, one from each part. The size of the output is therefore equal to the number of parts we want to make, irrespective of our original input size. If we want to obtain a final image of dimension H x W, we just create H x W divisions. If our input image is of dimension h x w, and we need to convert it to H x W, each of the parts need to be of size (h/H x w/W), and we apply Max pooling on each part, finally obtaining a HxW image. In this H and W equals to 7. So, as output of ROI pooling layer we obtain an output of dimension of 7x7x512. 

![ROI](https://miro.medium.com/max/362/1*qhN4EKjJO1hxKfpADOkcaw.png)

5. We pass the feature map from the ROI pooling layer into a set of fully connected layers, after flattening. Each of the FC has 4096 nodes.
6. Then finally the output from the FC layers are fed to a classification softmax layer with N+1 nodes, the extra node is for background class and a Regression branch for the bounding boxes output.

![Final](https://miro.medium.com/max/770/1*jYDMaYeH-TrcoofDqCdxug.jpeg)

#### Training

For training mini batch is used. The batch consists of 2 images having 64 regions each. 25% of the ROIs are object proposals that have at least 0.5 IoU with a ground-truth bounding box of a foreground class. These would be positive for that particular class and would be labelled with the appropriate u = 1 to K. The remaining ROIs are sampled from proposals that have an IoU with groundtruth bounding boxes between \[0.1, 0.5). These ROIs are labelled as belonging to the class u = 0 (background class).  


#### Loss Function

The loss function used here is a multitask loss given by:

![loss](https://miro.medium.com/max/481/1*R9hDmwuDDnP_LVIUWsuhsQ.png)

The loss is very similar to RCNN. The first part Lcls is the classification Log Loss for each class and the Second part is a Smooth L1 regression loss as given by the equaltion. The second part is only applicable for the object classes, i.e, from u>0, as u=0 is the background class, the loss is not applicable.

References:

1. https://arxiv.org/pdf/1504.08083.pdf
2. https://towardsdatascience.com/fast-r-cnn-for-object-detection-a-technical-summary-a0ff94faa022
3. https://medium.datadriveninvestor.com/review-on-fast-rcnn-202c9eadd23b




