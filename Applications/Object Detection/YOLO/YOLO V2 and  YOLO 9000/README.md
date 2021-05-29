### YOLO V2 and YOLO 9000

The problem with YOLOv1 was that it can only detect 1 object per cell, so if there were multiple objects in 1 grid, it could not be detected plus it was impossible to detect the smaller objects. 

To overcome these problems, the authors Joseph Redmon and Ali Farhadi proposed YOLOv2. The speed and accuracy improved along with the capacity to detect more objects from an image in YOLO v2 compared to YOLO. YOLOv2 also improved on the recall and the localization errors. 

#### Modifications:

1. YOLOv2 introduced Batch-Normalizaion, which increased the mAP by 2%.

2. The YOLOv2 introduced a new neural network model with 19 convolutional layers and 5 maxpooling layers as the backbone CNN. It uses 3x3 filters for feature extraction, followed by 1x1 filter to reduce the number of output channels. It also uses a global average pooling layer. It is given as:

![model](https://miro.medium.com/max/464/1*8FiQUakp9i4MneU4VXk4Ww.png)

The model gave an accuracy of 91.2% on the imagenet classification dataset which is better than VGG and YOLO networks.

3. The YOLO v2 model was trained on 224 x 224 size data for classification and fine-tuned. Then the resolution of the input images were increased to 448 x 448, and the model was trained and retuned with much fewer epochs, for detection. This makes the model robust and makes detector training easier and moved up the mAP by 4%.

4. The YOLO v2 removed one of the pooling layers to give better resolution. It was found that the performance is better if the feature maps are of odd spatial size. So, for that reason the input size was shifted from 448 x 448 to 416 x 416. The authors removed 1 pooling layer, so we got a higher resolution feature map of size 13 x 13 instead of 7 x 7. The feature map was down-sampled by a factor of 32.

5. The authors removed the last 2 fully connected layers as was present in the YOLOv1 architecture. This made the network capable of training on any size of the image. Only the size needed to be a multiple of 32, as the image is downsampled by a factor of 32. So, during training the authors used a variety of size from \[320,352,608].  So, for training, after 10 batches the size of the images are resized randomly using one of the given sizes. This give a sense of data augmentation while training and also helps the model to train on multi-scale or resolution of data. 





 
