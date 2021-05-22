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

#### Precision and Recall 

Precision depicts how many of the objects detected by the model are actually present in the ground truth.

Given by: TP / (TP + FP)

Recall depicts how many of the objects  actually present in the ground truth are detected by the model. 

Given by: TP / (TP + FN)

#### Precision-Recall Curve

Precision and Recall always has a tradeoff among themselves. The predictive model during a binary classification actually predicts confidence percentages for the object belonging to respective classes. For example, say for an object, a model predicts, 0.55 confidence that the object belongs to class 1 and 0.45 that it belongs to class 0. Here, we consider a threshold *alpha*, normally 0.5. If the confidence score is above threshold, considered as 1 else 0. So, if we lower the value of the threshold, more objects will be predicted as class 1 and False Negative will decrease but, the model will start classifying objects as class 1 with lower confidence, so False Positive will increase and vice versa.

So, if we roll the value of alpha we will generate a Precision-Recall curve, which is often a very good estimator for a model performance, as we need our model to have good presicion, even when we increase the recall. 

#### Average Precision

Average Precision is given by the area under the Precision-Recall curve. We just consider the total area under the curve using an integration. Given by:

![Formula](https://miro.medium.com/max/672/1*bs56Iu0mzjAP-QAM4XAAhw.png)


Now, often, the precsion-recall curve is zig-zag and is not monotonically decreasing, due to the stochastic nature of black-box models, but in order to evaluate the area under the curve, we want to make the curve monotonically decreasing as shown in the image. For this, we can use two methods.

![zz](https://miro.medium.com/max/443/1*7oGMy1fbcWw_jQttX0MNdw.png)

1. All points interpolation
2. 11 point interpolation.

Normally, we use the 11 point interpolation, In this point, we pick 11 equally spaced recall values, namely, 0.0, 0.1,.....1.0. We consider the precision against these points. If suddenly precision drops, we consider the maximum of the values on the right hand, to keep the curve monotonically non-increasing. We just take the Average of the precision of the 11 corresponding recall values.

![11](https://miro.medium.com/max/463/1*4lx2r2HUx0wRbQOjWMcAZA.png)

#### Mean Average Precision

Often, we do not detect only one type of object using one model. We detect multiple objects. For every object we get an Average Precision, the Mean Average Precision (mAP) is the mean of AP for all the objects. For models, which detect only one object, mAP=AP.

#### Variations of mAP:

Several Papers used several version of mAP. Some use 0.5 mAP with 0.5 as threshold for IOU. Similarly, some use 0.75 mAP, others 0.95 mAP. Others have also used Large mAP, i.e, the performance is measured based only on larger objects. Similarly, we have samll mAP.

References:

1. https://github.com/rafaelpadilla/Object-Detection-Metrics
2. https://blog.zenggyu.com/en/post/2018-12-16/an-introduction-to-evaluation-metrics-for-object-detection/










