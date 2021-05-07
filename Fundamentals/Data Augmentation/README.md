### Data Augmentation

Often in Computer vision problems, we need huge datasets to train deep learning models. But in some cases, mostly in medical imaging fields, the datasets are very hard to obtain owing to the amount of manual labour required to obtain the datasets. But on the other hand, we can not train our networks again and again based on the same data, as it would highly overfit the model. So, we need **data augmentation** to deal with the above problems.

Data Augmentation is a method that let's us transform the already provided images in our dataset and create new image sets. The processes makes several changes randomly, to an image to create a new image that the model has not seen before.

The common transformations used in case of Data Augmentation are:

1. **Mirroring:** We can just invert the whole image based on one given axis to obtain the new image. The inversion can be horizontal inversion or may be it can be vertical inversion. 
2. **Random Cropping:** It crops portions of the image randmly, to create the new image. This is not a very good method, as it can omit important portion of the image which can cause loss in information. 
3. **Rotation:** This transfomation rotates the image by a random amount within a certain range specified by the designer.
4. **Shearing:** This type of transformation provide shear to the image by a random amount within a certain limit.
5. **Colour Shifting:** We add some values to the values of the RGB channels to change the hue. It changes the colour distribution of the image.

We use a combination of these operations to create a new image for training of the models.

Resources:
1. https://www.analyticsvidhya.com/blog/2020/08/image-augmentation-on-the-fly-using-keras-imagedatagenerator/
2. https://www.pyimagesearch.com/2019/07/08/keras-imagedatagenerator-and-data-augmentation/

Library and documentation:

https://www.tensorflow.org/api_docs/python/tf/keras/preprocessing/image/ImageDataGenerator
