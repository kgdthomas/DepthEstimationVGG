# Fine-Tuning Vgg16 For Depth Estimation

### Introduction
This repository contains a set of python scripts to fine-tune a vgg16 model in order to do real-time depth estimation task

### Network Architecture
I've added a 1*1 conv in order to reduce the number of channels of the last conv layer from 512 to 128.This reduces the model size in order to make it fit in my poor GPU [2GB].

![img_1](./Arch.png)

Note: I think implementing a FC-Layers is an improper approach to do this task instead i am currently training a model using a simple Up-Conv technique , I've got that feeling after several failed training sessions and the FC-layers are discriminative by its' nature.

I've added a Scale-Invarient Loss because i think learning relative depth estimation is much easier.
![img_1](./loss.png)

### Dataset
I've used the NYU Depth V2 dataset.

### Training
For the FC Implementation : I am working on it, but currently i am stucked at 0.15 RMSE on training data and 0.45 RMSE on validation data.

For the Up-Conv Implementation : I've reached a 0.109 RMSE on Training data and a 0.165 RMSE on Validation data. 

### Output
![img_1](./output.png)

Note : the provided output samples are predicted by the Up-Conv implementation

### Conclusion

I've used only 1449 image-depthmap pairs during this fine-tuning process, I think getting more data will help me to significantly improve my results.

Some tricks as the 1*1 conv can make life easier and training faster while preserving most of the model's capcity
 
Using Upsampling to upsize the last feature map makes it sparse "Around 75% of the weights are zeros" , I think using this Up-Projection block to Up-Sample the last feature map will help. 

Note : This block was introduced into ["**Depth from a Single Image by Harmonizing Overcomplete Local Network Predictions**," 
](https://arxiv.org/abs/1605.07081) NIPS 2016.

Note : I've already implemented this paper. ["**DeeperDepthEstimation**," 
](https://github.com/MahmoudSelmy/DeeperDepthEstimation)

![img_1](./up_projection.png)

### Future Work

1) I will collect more NYU-Depth V2 data by extracting them from the provided raw data.
2) I will train my model on AWS to get a chance to train on a powerful resources.
3) I will try to predict larger depth map.
4) I will add the gradient at the x and y directions in order to reduce sudden changes in depth , This idea was introduced into     ["*Predicting Depth, Surface Normals and Semantic Labels with a Common Multi-Scale Convolutional Architecture**," 
](https://arxiv.org/abs/1411.4734) NIPS 2015.


