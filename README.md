<!--
  Title: Deep Learning with PyTorch and Google Cloud Platform, Columbia University BMEN4460
  Description: This tutorial is originally designed for the course BMEN4460 instructed by Dr. Andrew Laine and Dr. Jia Guo starting from the Spring 2020 semester at Columbia University. Since we are a medical imaging group, this repository will mainly focus on applications in medical imaging.
 Author: RnR-2018
  -->

# Deep Learning in Biomedical Applications with PyTorch and Google Cloud Platform
Nanyan "Rosalie" Zhu and Chen "Raphael" Liu, Columbia University

## Overview
This tutorial is designed for the course BMEN4460 Deep Learning in Biomedical Applications instructed by Dr. Andrew Laine and Dr. Jia Guo starting from the Spring 2020 semester at Columbia University. Since we are a medical imaging group, this repository will mainly focus on applications in medical imaging.

This repository is still in progress. We will add one new post per week. Please help us improve this repository by leaving your comments or problems you encountered in the "Issues" section.

![](/Images/issues_button.png)

## GCP setup.
- Step 00: [Set up Google Cloud Platform (GCP)](https://github.com/RnR-2018/Deep-learning-with-PyTorch-and-GCP/tree/master/Step00_set_up_GCP).
- Step 01: [Manage anaconda on GCP](https://github.com/RnR-2018/Deep-learning-with-PyTorch-and-GCP/tree/master/Step01_manage_anaconda_on_GCP).
- Step 02: [Set up Jupyter Lab](https://github.com/RnR-2018/Deep-learning-with-PyTorch-and-GCP/tree/master/Step02_Jupyter_lab).
- Step 03 (optional): [Set up a graphical user interface (GUI) on GCP](https://github.com/RnR-2018/Deep-learning-with-PyTorch-and-GCP/tree/master/Step03_GUI_setup%20(optional)).

## BMEN4460 supplementary notebooks.
1. [Simple cell segmentation with a single layered perceptron](https://github.com/RnR-2018/BMEN4460-NB1-simple_cell_segmentation_with_a_single_layered_perceptron).
2. [Image classification on MNIST data](https://github.com/RnR-2018/BMEN4460-NB2-image_classification_on_MNIST_data).
3. [Brain tumor segmentation](https://github.com/RnR-2018/BMEN4460-NB3-brain_tumor_segmentation).
4. [GAN faking MNIST images](https://github.com/RnR-2018/RnR-2018-BMEN4460-NB3-GAN_faking_MNIST_images)


## Tutorials

(Outline is listed. Whenever a content is complete, it will become clickable.)
- [History and background](https://www.notion.so/rosalieraphael/History-and-background-5e914410df9a4fc68c147bf7d442a738)
- Feedforward and backpropagation
  - [Backpropagation](http://neuralnetworksanddeeplearning.com/chap2.html)
- Loss functions and Regularization
  - [Gradient decent](https://www.youtube.com/watch?v=IHZwWFHWa-w)
  - [Why local minima close to global minima in large Neural Networks](http://proceedings.mlr.press/v70/nguyen17a/nguyen17a-supp.pdf)
  - loss functions
  - [Batch Normalization (BN)](https://machinelearningmastery.com/batch-normalization-for-training-of-deep-neural-networks/)
  - Dropout
  - Max Norm
- Optimization
  - [Optimizers](https://algorithmia.com/blog/introduction-to-optimizers)
  - Vanishing/exploding gradient
    - [Exploding Gradient](https://machinelearningmastery.com/exploding-gradients-in-neural-networks/)
- CNN
  - [Convolution kernel basics](https://medium.com/apache-mxnet/multi-channel-convolutions-explained-with-ms-excel-9bbf8eb77108)
  - [Receptive field](https://syncedreview.com/2017/05/11/a-guide-to-receptive-field-arithmetic-for-convolutional-neural-networks/)
  - [Object detection](https://medium.com/zylapp/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
  - Segmentation
    - [Semantic Segmentation](https://towardsdatascience.com/semantic-segmentation-with-deep-learning-a-guide-and-code-e52fc8958823)
  - Classification
- Visualization
  - TensorBoard
  - hook function and CAM visualization
- Transfer Learning
- RNN
- Autoencoders
- Generative Advsersarial Networks


### Additional resources.
1. [Python Basics](https://www.dropbox.com/s/t4anle32op2qn8k/dlforcv-python.ipynb.zip?dl=0). This material comes from another course called Deep Learning for Computer Vision at Columbia University. **Please note that we strongly recommend not to use the 'pip' install ation mentioned in that tutorial, but instead use the 'anaconda' installation we introduced [here](https://github.com/RnR-2018/Deep-learning-with-PyTorch-and-GCP/tree/master/Step01_manage_anaconda_on_GCP).**
2. [Jupyter Notebook Tricks](https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/). Quite cool. There are a lot of things that we never heard of.
3. [Udacity Online Course](https://www.udacity.com/course/intro-to-machine-learning-nanodegree--nd229). This is not free, and not relevant to the course BMEN4460 at all. It is just a course we looked into personally. We are not paid or anything to advertise this. It's just a very friendly course if you are new to deep learning.

### Useful links (to be organized).
- [Biomedical Image Analysis](https://medium.com/@iradche/biomedical-image-analysis-d06024b8c122).
- (Video)[Neural Network Programming - Deep Learning with PyTorch](https://www.youtube.com/playlist?list=PLZbbT5o_s2xrfNyHZsM6ufI0iZENK9xgG).
- (Video)[Introduction - Deep Learning and Neural Networks with Python and Pytorch](https://www.youtube.com/watch?v=BzcBsTou0C0&feature=youtu.be).

### Free Online Courses
- [IBM course](https://courses.edx.org/courses/course-v1:IBM+DL0110EN+3T2019/course/)
- [Udacity deep learning course](https://classroom.udacity.com/courses/ud188) ([related github](https://github.com/udacity/deep-learning-v2-pytorch)) (This is a part of the expensive Udacity course we mentioned before.)

### Other useful GitHubs
- [Deep learning for medical applications (papers)](https://github.com/albarqouni/Deep-Learning-for-Medical-Applications)
- [Medical imaging related project tutorials](https://github.com/mdai/ml-lessons)
- [The incredible pytorch](https://github.com/ritchieng/the-incredible-pytorch)
- [Awesome-pytorch-list](https://github.com/bharathgs/Awesome-pytorch-list)
- [pytorch examples](https://github.com/pytorch/examples)

### Papers.
- [A Review on Generative Adversarial Networks: Algorithms, Theory, and Applications](https://arxiv.org/abs/2001.06937).
- [Imbalance Problems in Object Detection: A Review](https://arxiv.org/abs/1909.00169)
- [A Review of Visual Trackers and Analysis of its Application to Mobile Robot](https://arxiv.org/abs/1910.09761)
- [Deep Semantic Segmentation of Natural and Medical Images: A Review](https://arxiv.org/abs/1910.07655)
- [A Deep Journey into Super-resolution: A Survey](https://arxiv.org/pdf/1904.07523.pdf)

