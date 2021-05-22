### Metrics

In order to evaluate object detection algorithm, we use a different set of metrics. Normal, metrics of Accuracy, Precision and Recall won't work in this scenaerios as we basically need to evaluate both the classification and the localization capacity of the model.

#### IOU

The primary concept we want to know, is the idea of **IOU** or **Intersection Over Union**. It denotes the overlap between the predicted bounding box and the actual bounding box around the object in the image. So, it deals with how correctly our model has localized the image

It is given by:

IOU = (Intersection of the predicted and actual bounding boxes) / (Union of the predicted and actual bounding boxes)
 
![IOU](https://miro.medium.com/max/683/1*6B58Ohs9t7sRjYISbYZs-Q.png)

The above image depicts the IOU in three cases.

#### Confidence Score

For every bounding box predicted by the object detection model, the model provides a confidence score. The confidence score depicts the confidence of the model on the fact that an object is present in the corresponding bounding box. This confidence score is used in **Non-Max Suppression** i.e, when an object is predicted by multiple bounding boxes, the box with the highest confidence score is kept and other bounding boxes are removed.

#### False Positive, True Positive and False Negative

True Positive is where the IOU between the predicted bounding box and the actual bounding box is above a given threshold T. So, if the threshold is 0.5 and IOU is 6, we consider it True Positive.

False Positive is where the IOU between the predicted bounding box and the actual bounding box is below a given threshold T. So, if the threshold is 0.5 and IOU is 4, we consider it False Positive.

False Negative is the condiion, if there is an object and a bounding box but the model fails to detect it. 

True Negative is all the other pixels which doesnot have an object and our model did not predict also, So, it is insignificant in this scenerio.

#### 

