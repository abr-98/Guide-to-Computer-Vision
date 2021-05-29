### YOLO V2 

The problem with YOLOv1 was that it can only detect 1 object per cell, so if there were multiple objects in 1 grid, it could not be detected plus it was impossible to detect the smaller objects. 

To overcome these problems, the authors Joseph Redmon and Ali Farhadi proposed YOLOv2. The speed and accuracy improved along with the capacity to detect more objects from an image in YOLO v2 compared to YOLO. YOLOv2 also improved on the recall and the localization errors. 

#### Modifications:

1. YOLOv2 introduced Batch-Normalizaion, which increased the mAP by 2%.

2. The YOLOv2 introduced a new neural network model with 19 convolutional layers and 5 maxpooling layers as the backbone CNN. It uses 3x3 filters for feature extraction, followed by 1x1 filter to reduce the number of output channels. It also uses a global average pooling layer. It is given as:

![model](https://miro.medium.com/max/464/1*8FiQUakp9i4MneU4VXk4Ww.png)

The model gave an accuracy of 91.2% on the imagenet classification dataset which is better than VGG and YOLO networks.

3. The YOLO v2 model was trained on 224 x 224 size data for classification and fine-tuned. Then the resolution of the input images were increased to 448 x 448, and the model was trained and retuned with much fewer epochs, for detection. This makes the model robust and makes detector training easier and moved up the mAP by 4%.

4. The YOLO v2 removed one of the pooling layers to give better resolution. It was found that the performance is better if the feature maps are of odd spatial size. So, for that reason the input size was shifted from 448 x 448 to 416 x 416. The authors removed 1 pooling layer, so we got a higher resolution feature map of size 13 x 13 instead of 7 x 7. The feature map was down-sampled by a factor of 32.

5. The authors removed the last 2 fully connected layers as was present in the YOLOv1 architecture. This made the network capable of training on any size of the image. Only the size needed to be a multiple of 32, as the image is downsampled by a factor of 32. So, during training the authors used a variety of size from \[320,352,608].  So, for training, after 10 batches the size of the images are resized randomly using one of the given sizes. This give a sense of data augmentation while training and also helps the model to train on multi-scale or resolution of data. This forces the model to predict well on different scale and dimension of input images.

The above are some of the modifications made in case of YOLO v2 now, we see two of the most major changes YOLO v2 brought.

In YOLO v1, we could detedct only one object and to detect the location and size of the object we used two bounding boxes per cell. It was observed that the size of the bounding boxes was the factor that the model took more time to learn. And also, it was observed, if we fix the bounding boxes, we can detect several objects easily. Like, if we use a bounding box with aspect ratio of 0.41 we can detect a human easily, and for every car the shape is nearly the same. So, the authors initialized 5 fixed bounding box shapes, for each grid or cell of the SxS cells the image was divided in, and named them **Anchor Boxes** previously _Priors_. So, initially the training is more stable. 

![anchor](https://miro.medium.com/max/504/1*8Q8r9ixjTiKLi1mrF36xCw.jpeg)

Each of the anchor boxes could detect an object. So, we went from detection per cell to detection per anchor box.
The bounding box coordinates were changed. They were now expressed with respect to the anchor boxes. For each anchor box,the model still predicted 5 values, _to_ the box confidence score and the box offsets with respect to the anchor box.

![pred](https://miro.medium.com/max/700/1*38-Tdx-wQA7c3TX5hdnwpw.jpeg)

The below image shows the exact locations.

![pred_anchor](https://miro.medium.com/max/700/1*gyOSRA_FDz4Pf5njoUb4KQ.jpeg)

Consequently, the output dimension also changed. For each anchor box, we had 1 confidence score, 4 bounding box offsets, and the scores of 20 classes, we need to classify the objects in. So, the full prediction, for an anchor box is of size 25. Each grid has 5 anchor boxes, so in total, the dimension for a grid is of size 25x5= 125. Now, as we saw previously, we obtain a feature map of 13x13 after the backbone network. So, we generate an output of size (13,13,125). As we already know, the fully connected layers are removed, the authors have used an 1x1 convolutions to convert the dimension of the 13 x 13 x 1024 (of the feature map) into the output 13 x 13 x 125. 

The number of anchor-boxes is set to 5, using a clustering method. Using the clustering, we identify the top-K boundary boxes that have the best coverage for the training data, we run K-means clustering on the training data to locate the centroids of the top-K clusters.

![Cluster](https://miro.medium.com/max/700/1*l5wvrPjLlFp6Whgy0MqbKQ.png)

YOLOv2 also brought a major change in the structure of the network, in order to obtain fine grain features. The 13x13 feature map can be used to detect large objects but no finer features can be detected, so no smaller objects detected. To solve this, the authors, picked up 26x26x512 feature maps from the previous layers in the backbone, then reshapesd it to (13,13,2048) and contatenated with the final downsampled feature map of (13,13,1024), and obtained a map of (13,13,3072), then predicted on that map.

![fine_graib](https://miro.medium.com/max/700/1*RuW-SCIML8SHc5_PrIE9-g.jpeg)

The training of YOLOv2 is same as v1. The IOU of the actual boxes and the bounding boxes, give the box confidence score.

### YOLO 9000

One particular problem was observed, that the available data was very less, so, the classes categories available for detection is much less than the corresponding classfication problems. To expand the classes that YOLO can detect, YOLO proposes a method to mix images from both detection and classification datasets during training. It trains the end-to-end network with the object detection samples while backpropagates the classification loss from the classification samples to train the classifier path. So, for classiication we train the classification model of YOLO v2. The authors finally made the network to detect 9000 objects by using multiple datasets.

The problems with this was, how to merge labels and if we do so, the labels may not be mutually exclusive. For example, ImageNet dataset has more than a hundred breeds of dogs like “german shepherd” and “Bedlington terrier” where as MS-cOCO has only "dog" Class. To solve this the authors merge these datasets creating a hierarchical model of visual concepts and called it **wordtree**.

![Word Tree](https://miro.medium.com/max/700/1*nskRV4Wt9Dul-6Jv1x09Bw.png)

Say, for the imageNtes 1000 classes, we create a WordTree1k. We create 369 nodes as their parent classes and add them as an intermidiate layer in the tree. Initially YOLO used a single softmax layer to detect all the classes, now, we will be using seperate softmax layers for all child nodes seperately. So, “german shepherd” and “Bedlington terrier” will be identified in the next layer using a seperate softmax after the first layer identiefies its parent class to be dog. It is completely based on a tree structure, we choose the node with highest probabaiity and travel that branch.

In YOLO 9000. the authors trained the network on 9000 class categories with 418 intermidiate nodes.


Refernce:

1. https://arxiv.org/pdf/1612.08242.pdf
2. https://towardsdatascience.com/review-yolov2-yolo9000-you-only-look-once-object-detection-7883d2b02a65
3. https://medium.datadriveninvestor.com/review-on-yolov2-11e93c5ea3f1












 
