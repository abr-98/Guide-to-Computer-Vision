### Region Proposal Network

In the RCNN and fast RCNN networks, Selective Search algorithm was used to obtain region proposals. But, the algorithms were very slow as it implemented a segmentation underneath. So, in the faster RCNN networks, the authors replaced the Selective Search algorithm with a much faster RPN network.

The RPN itself is a neural network based architecture which is responsible for obtaining the target portions of the image which may contain object. These portions of the images are sent to the classifier in order to classify the objects in the image. The algorithm is much more effective and fast than the sliding window and Selective Search algorithms.

#### Architecture and Working

![Arch](https://miro.medium.com/max/770/1*S_-8lv4zP3W8IVfGP6_MHw.jpeg)

The diagram above shows the given architure of the RPN network. 

It initially passes the input image through a basic backbone block like VGG networks, which identify the basic features of the image. The backbone network generates a feature map of the image for the RPN network to identify the targets. The bakbone network stride is kept equal to 16, i.e, if two pixels are 16 pixels apart in the main image, the whole 18 pixels will be represented by 2 corresponding pixels on the feature map.

After the backbone layer, we obtain a M x N sized feature maps. The center of each area of the original image is represented by the coordinates of a pixel on this feature map. Now, one element of concern is the objects in the image can be of any size and shape. To solve this the idea of anchor boxes were introduced. 

![Anchor](https://miro.medium.com/max/401/1*muU7TGhE7ke1nqnHQbbdKg.jpeg)

In order to detect the objects of different sizes and shapes we use bounding boxes (called anchor boxes, which actually gives the area of interest) of different sizes and aspect ratio. The authors used total of 3 different sizes, and for each different size, a total of 3 different aspect ratios have been used, which gives a total of 9 anchor boxes. Normally, we have an input image of 10000 x 6000 size which is reduced to 10000/16 x 6000/16 after passing through backbone. We pass anchor boxes of sizes 128 x 128, 256 x 256 and 512 x 512.

Initially, we use a sliding window protocol to generate the anchor boxes, so we obtain a large number of anchor boxes. Primarily we remove all the cross boundary anchor boxes. 

For each anchor box left after primary removal, a classification score is obtained from the network. The RPN uses a two class classification. It predicts whether an anchor box contains an object or not. It doesnot specify which type of object. The classification provides us with a confidence score. If multiple anchor boxes indicate a particular set of pixels, we keep only the anchor wiith maximum confidence score, rejecting the others. This is called **Non-max suppression**.

The model also predicts bounding box coordinates (tx,ty,th,tw), which gives the position of the area of interest. (tx,ty) is the center of the area and (tw,th) represents hieght and width of the box. These values are predicted using regression. 

So, finally, we get a number of bounding boxes with their confidence scores and the coordinates. 

#### Training

We consider the predicted bounding boxes with IOU > 0.7 with the actual bounding boxes as Positive samples and the bounding boxes with IOU < 0.3 are considered as negative samples. This is done to balance the number of positive and negative samples. 128 positive and 128 negative samples are randomly selected to form the batch, and training of the model is done. The butraining of the RPN consists of a multi-task loss fucntion, as it is a combination of classification and a regression losses. It is gven by:

![Loss](https://miro.medium.com/max/678/1*mq0jKvp4I1o1ecHBTzQLHA.png)

Here i is the index of the anchor in the mini-batch. The classification loss L𝒸ₗₛ(pᵢ, pᵢ*) is the log loss over two classes (object vs not object). pᵢ is the output score from the classification branch for anchor i, and pᵢ* is the groundtruth label (1 or 0). 
The regression loss Lᵣₑ(tᵢ, tᵢ*) is activated only if the anchor actually contains an object i.e., the groundtruth pᵢ* is 1. The term tᵢ is the output prediction of the regression layer and consists of 4 variables \[tₓ, tᵧ, tw, tₕ] It is given by:

![reg](https://miro.medium.com/max/769/1*s6uMkokhzyGoMLSXLMm9Ug.png)

Here x, y, w, and h correspond to the (x, y) coordinates of the box centre and the height h and width w of the box. xₐ, x* stand for the coordinates of the anchor box and its corresponding groundtruth bounding box.

The *lambda* parameter is used to stabilize the balance of the two losses. Normally the value is kept equal to 10.

![out](https://miro.medium.com/max/375/1*JDQw0RwmnIKeRABw3ZDI7Q.png)

So, finally we flatten the anchor boxes as a 256-d 1D vector and send to the dense layers from where we get an output of 2 x k confidence scores from the classification layer and a 4 x k coordinates from the regression layers, for k chosen anchor boxes.

##### Hard Negative Mining

It is a strategy which are used in most of such algorithms, in order to balance the number of positive and negative samples. When initially we obtain a lot of anchor boxes, its very easy to get the Positive samples, using the overlap with the original bounding boxes. But, for the negative samples, we have a huge number of anchor boxes, which if all are considered will cause a huge imbalance. To solve this we do not consider the boxes, which cover absolutely dark backgrounds or have 0 overlap with the actual boxes. We consider such boxes, which cover interesting points with some variations in the feature maps but actually are not object, to make our model more robust.

References:

1. https://www.geeksforgeeks.org/faster-r-cnn-ml/
2. https://medium.com/@nabil.madali/demystifying-region-proposal-network-rpn-faa5a8fb8fce
3. https://towardsdatascience.com/faster-r-cnn-for-object-detection-a-technical-summary-474c5b857b46










