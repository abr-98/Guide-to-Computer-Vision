### Transfer Learning

1. In most cases, in image processing and detection algorithms need to be super well trained to perform on complex datasets inorder to accomplish certain tasks.
2. Sometimes datasets are very small and we do not have enough to train large and deep models

For the above circumstances, we just do not randomly initialize a network and train it to perform, we use already pretrained networks for the tasks. 

There are several challenges, for example, the ImageNet and MS-COCO challenges, where deep network models are put forward and proposed, and their performances are compared on standard benchmark datasets. The best performing model is stored as a standard state of the art performing pretrained model for further use.

The above concept is called Transfer Learning. Transfer learning allows us to deal with these scenarios by leveraging the already existing labeled data of some related task or domain. We can use the standard models in a number of ways. 

1. We can use only the structure of the networks, and iniialize them with random weights, and train them.
2. We can modify the layer structure, add some of our own layers at the top. 
3. We can use both the weights and structure of the networks. 
4. We may or may not modify, the weights of the pretrained networks. We can only train the weights of our addad layers leaving the rest of the networks unchanged during training.

The above summarizes transfer learning. Next we go to explanation.


### The terminologies and variants

The formal defination states, in case of transfer learning, we have a *Xs*, a source feature set, *P(Xs)* probability distribution, *D(Xs, P(Xs))* a source domain and a *Ts*, which is a source task with *Ys* labels. Similarly, we have *Xt*,a target distribution, *D(Xt,P(Xt))* a target domain,  and so on.

So, our goal is to use the knowledge gained from the source domain to achieve a source task in order to accomplish a target task in the target domain. Depening on the above circumstances, several condition may arise:

1. Xt!=Xs: The feature spaces are different
2. P(Xt)!=P(Xs): The feature spaces are same, but distributions are different
3. Ys!=Yt: The labels of source and targe are different
4. P(Ys|Xs)!=P(Yt|Xt): The conditional probabilities are different.

Based on the above, several methods of transfer learning strategies have been adopted to solve the problems in this field.

### Transfer learning in Deep learning:

In deep learning, we use **inductive based transfer learning**. The deep transfer learning, we have two different strategies:

1. Off-the-shelf Pre-trained model as Feature extractors: Here the pre-trained models, are modified as feature extractors, just by removing the top classification layers, The layered architecture is leveraged into obtaining features from the images. We do not tune the filters in this case.

2. Fine Tuning Off-the-shelf Pre-trained Models: In this case, we replace the final layers with new layers based on the task at hand. We also train the last few layers of the network, in order to obtain finer work. It is due to the fact that the initial layers extract the more generic features, while the deeper layers are more task specific.

The available models for transfer learning in computer vision.
![types](https://www.educative.io/api/edpresso/shot/4574405643468800/image/4521173214822400)

References:

1. https://towardsdatascience.com/a-comprehensive-hands-on-guide-to-transfer-learning-with-real-world-applications-in-deep-learning-212bf3b2f27a
2. https://ruder.io/transfer-learning/
3. https://www.cse.ust.hk/~qyang/Docs/2009/tkde_transfer_learning.pdf
4. https://www.analyticsvidhya.com/blog/2017/06/transfer-learning-the-art-of-fine-tuning-a-pre-trained-model/

Examples: solved on cats-vs-dogs dataset.

**One important point to remember about training model using transfer learning is:**

When the models were initially trained for the imagenet datasets, the authors made some preprocessing to the data, that rescaled the images and shifted the pixel values to a certain amount to obtain the best results. So, when we load the "imagenet" weights, the filter weights are tuned to work, after the image is passsed through the same preprocessing units. 

So, often passing the raw image data using custom preprocessing won't yield better results, and as the models are bulky, it takes huge time and data to train the model parameters with respect to the new custom preprocessing. To deal with these problems, Tensorflow provides the preprocess_input functions, for every transfer learning model, as shown in v3 of the shown examples above.

For example, we can find the preprocess unit of the resnet at https://www.tensorflow.org/api_docs/python/tf/keras/applications/resnet/preprocess_input.

We can use the preprocessing function seperately, manually as 

~~~from keras.applications.resnet50 import ResNet50
from keras.preprocessing import image
from keras.applications.resnet50 import preprocess_input
import numpy as np

model = ResNet50(weights='imagenet')

img_path = 'elephant.jpg'
img = image.load_img(img_path, target_size=(224, 224))
x = image.img_to_array(img)
x = preprocess_input(x)
~~~

Or we can deploy it using the ImageDataGenerator:

~~~from tensorflow.keras.preprocessing.image import ImageDataGenerator
from keras.applications.resnet_v2 import preprocess_input
train_set=ImageDataGenerator(
    rotation_range=20,
    zoom_range=0.1,
    shear_range=0.2,
    preprocessing_function=preprocess_input
)
val_set=ImageDataGenerator(preprocessing_function=preprocess_input)
~~~


*For GPU, its better to keep the batch_size bigger*
