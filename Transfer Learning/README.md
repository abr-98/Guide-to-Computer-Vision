### Transfer Learning

1. In most cases, in image processing and detection algorithms need to be super well trained to perform on complex datasets inorder to accomplish certain tasks.
2. Sometimes datasets are very small and we do not have enough to train large and deep models

For the above circumstances, we just do not randomly initialize a network and train it to perform, we use already pretrained networks for the tasks. 

There are several challenges, for example, the ImageNet and MS-COCO challenges, where deep network models are put forward and proposed, and their performances are compared on standard benchmark datasets. The best performing model is stored as a standard state of the art performing pretrained model for further use.

The above concept is called Transfer Learning. We can use the standard models in a number of ways. 

1. We can use only the structure of the networks, and iniialize them with random weights, and train them.
2. We can modify the layer structure, add some of our own layers at the top. 
3. We can use both the weights and structure of the networks. 
4. We may or may not modify, the weights of the pretrained networks. We can only train the weights of our addad layers leaving the rest of the networks unchanged during training.
