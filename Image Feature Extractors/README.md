### Feature Extraction

Feature extraction the idea of extraction of some important useful features to define the characteristic of a data. The extracted features are fed to the machine learning algorithms to make a classification or prediction. Selecting a good set of features help to increase the predictive power of the model.

In image data, the measurable features are distinct colour or specific shape like, corner, line, edge or an image segment. Good set of features extracted from images can help machine learning algorithms to accomplish image comparison and object detection tasks. [WIKI](https://en.wikipedia.org/wiki/Feature_(computer_vision)#Extraction)

Machine Learning models like SVM, draw important conclusions from these features which help them to make decision,so, to use these hand-crafted feature importancenis necessary.

![ML](https://miro.medium.com/max/700/0*SVNmDa8IGVle0ue9.png)

Deep learning algorithms on the other hand, are built-in feature extractors + decision makers. They do not need hand crafted feature extraction filters. They automatically extract features and learn their importance bt applying weights to the connection, using backpropagation in Neural Networks.

![DL](https://miro.medium.com/max/700/0*LYa9apx25QSsRgj5.png)

In order to use state of the art ML algorithms to make predictions on image data, we have several traditional feature extractors. These extractors are present in the OpenCV libraries of python. Apart from Traditional extractors, we can also use the pretrained models as feature extractors using transfer learning, by removing the top softmax layer. The pre-trained models outputs the feature maps in the shape 7 x 7 x N where N is the number of channels, for a given image, in most cases. We need to use a flatten to obtain the training data for the predictive ML model for an image.

Reference Example:
1. https://www.pyimagesearch.com/2019/05/27/keras-feature-extraction-on-large-datasets-with-deep-learning/
2. https://liu.diva-portal.org/smash/get/diva2:1151145/FULLTEXT01.pdf

In case of traditional feature extractors, we need to apply the available filters on the image to extract the feature maps from the image. We need to flatten the feature maps to create dataset in order to train the traditional ML models. The filters used in traditional extractors are designed with fixed weight kernels to highlight specific features like, edges, corners and lines. Some of the most used traditional extraction methods are: 

**1. Histogram of Oriented Gradients (HOG):** It is one of the most important feature descriptors, which is very useful for training algorithms like SVM. It calculates the pixel gradients, i.e, the rate of change in pixel values along the x and y axis, and the direction of the gradient. The magnitude of gradient helps to detect the edges and corner and the direction gives information about the shape. The HOG descriptor is used in patches in multiple scales cropped from the original image in the aspect ratio of 1:2.

Reference Links: 
1. https://stackoverflow.com/questions/6090399/get-hog-image-features-from-opencv-python
2. https://learnopencv.com/histogram-of-oriented-gradients/
3. https://www.analyticsvidhya.com/blog/2019/09/feature-engineering-images-introduction-hog-feature-descriptor/

**2.Haar Cascades:** Object Detection using Haar feature-based cascade classifiers is an effective object detection method proposed by Paul Viola and Michael Jones in their paper, “Rapid Object Detection using a Boosted Cascade of Simple Features” in 2001. Haar cascades are presented as a cascade of classifiers. The final classifier is a weighted sum of weak classifiers. These weak classifiers can’t alone classify an image, but together form a strong classifier. We know that, in the case of convolutions, the kernels are devised during training but here they have a set of Haar features or filters that are fixed which are applied on the training images to extract features from them. These filters or kernels of different sizes are passed over the images and extract a huge number of features from images that are used to classify the target objects. OpenCV has a trainer and a detector that can use Haar Cascades. 

![Filters](https://miro.medium.com/max/489/1*AeAYGJkO_tNhjhI0ajFwTQ.png)

There are several filters to detect different features. They are majorly used for face detection.

References:

1.https://github.com/opencv/opencv/tree/master/data/haarcascades  /n
2.https://docs.opencv.org/3.4/db/d28/tutorial_cascade_classifier.html  /n
3.https://www.pyimagesearch.com/2021/04/12/opencv-haar-cascades/   /n

**3.SIFT: Scale Invariant Feature Transform:** In this method, we locate features called "keypoints" on the image, which are invariant to rotation, noise, scaling. Using the gradient magnitude and direction, at the keypoints we create unique footprints for the objects in the image. These footprints are used in case of object identification, matching and detection. In order to find the "keypoints", we use a guassian blur to remove noise, a scale space inorder to obtain the scale invariant points. Next, we use a Differnece of Gaussian (DOG) method to extract the points of interest. We then proceed to an orientation assignment operation, in order to check if the points are rotation invariant. Lastly, using the combination of values, we develop an unique fingerprint for every keypoint called the feature descriptor.

References: 
1. https://www.analyticsvidhya.com/blog/2019/10/detailed-guide-powerful-sift-technique-image-matching-python/
2. https://docs.opencv.org/3.4/da/df5/tutorial_py_sift_intro.html \
3. https://link.springer.com/article/10.1023/B:VISI.0000029664.99615.94 \


**4. SURF: Speeded-Up Robust Feature:** It is a faster version of SIFT.

References: \
1.https://docs.opencv.org/3.4/df/dd2/tutorial_py_surf_intro.html \
2.https://medium.com/data-breach/introduction-to-surf-speeded-up-robust-features-c7396d6e7c4e \
3.https://link.springer.com/chapter/10.1007/11744023_32 \

Other most used Feature exractors are: \
BRIEF: https://docs.opencv.org/3.4/dc/d7d/tutorial_py_brief.html \
ORB: https://docs.opencv.org/3.4/d1/d89/tutorial_py_orb.html \
FAST: https://docs.opencv.org/3.4/df/d0c/tutorial_py_fast.html 

More Resources:

1. https://arxiv.org/pdf/1710.02726.pdf
2. https://ieeexplore.ieee.org/document/8346440
3. https://towardsdatascience.com/image-feature-extraction-traditional-and-deep-learning-techniques-ccc059195d04
4. https://medium.com/machine-learning-world/feature-extraction-and-similar-image-search-with-opencv-for-newbies-3c59796bf774
5. https://medium.com/data-breach/introduction-to-surf-speeded-up-robust-features-c7396d6e7c4e









