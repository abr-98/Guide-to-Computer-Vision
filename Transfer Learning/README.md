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

References:

1. https://towardsdatascience.com/a-comprehensive-hands-on-guide-to-transfer-learning-with-real-world-applications-in-deep-learning-212bf3b2f27a
2. https://ruder.io/transfer-learning/
3. https://www.cse.ust.hk/~qyang/Docs/2009/tkde_transfer_learning.pdf
4. https://www.analyticsvidhya.com/blog/2017/06/transfer-learning-the-art-of-fine-tuning-a-pre-trained-model/
