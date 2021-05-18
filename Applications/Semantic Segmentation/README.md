### Semantic Segmentation

Semantic segmentation is said to be a dense prediction method, as in this method, we make pixel wise predictions, that is we predict each pixel to be a back ground or belonging to a fore ground object. 

![example](https://www.jeremyjordan.me/content/images/2018/05/Screen-Shot-2018-05-17-at-7.42.16-PM.png)

As shown in the above, we classify the pixels in three classes: Background, Person and Bicycle. One thing to notice is, we marked all the instance of the person and the bicycle same, where as, in instance segmentation, we colour each of the instances of an object differently.

![Segmentation](https://www.jeremyjordan.me/content/images/2018/05/Screen-Shot-2018-05-17-at-9.02.15-PM.png)

The segmentation labelling process is something like as shown above, we assign labels to each pixel. So, we basically create a mask of labels of the same size as the image size and over lap them, to find the pixel wise labels.

Now, to do this we can simply use stacked convolutional layers without dimensional change, but we it would be too computationally expensive to preserve the full resolutional image all through. So, several models have been proposed to solve this problem. Most significant of them are:

1. Fully Convolutional Network
2. U-net and its variants
3. Mask-RCNN
4. Pyramid Scene Parsing Network(PSPNet)
5. Fully Convolutional DenseNets
6. Deeplab family
7. FastFCN —Fast Fully-connected network

### Popular Metrics

Apart from normal classification problem metrics, like Precision, Recall, F1 score and accuracy, we have some other metrics. They are:

**Specificity:**  Specificity is the measure of the accuracy of learning the background.

Given by: True negative/(True Negative+False Positive) 

**Sensitivity:** Sensitivity is the measure of the True Positive or how good the target class has been learned.

Given by: True positive/(True Positive+False Negative)

**Dice Coefficient** = 2* True positive / (2* True positive + False Positive + False Negative)

**Jaccard Index** = True positive / (True positive + False Negative + False Positive )

In most segmentation problems, there is a huge imbalance between the foreground and the background classes. As foreground is very small with respect to background, the model learns the back ground better and predicts fore grounds as backgrounds which increases the False Negatives. So, the above metrics are used to keep a tab on how the model is learning both the foreground and the back ground classes. Dice coefficient and Jaccard Index are very common as they focus on the foreground only. 








