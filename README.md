# MobileFaceNet-Keras
A Keras implementation of MobileFaceNet from https://arxiv.org/abs/1804.07573. It is the 1st time I uploaded my own work. If the license or citation is wrong, please inform me and I will change it ASAP. The Keras model for inference is ~14 Mb, as well as the TensorFlow model in optimized protobuf format, so I might not follow all the details in the original work (should be around 5 Mb). 
  
## 1. Data Preprocessing Strategy  
(1) Use the celebrity & msra datasets from the Trillion Pairs dataset: http://trillionpairs.deepglint.com/data.  
(2) For each identity folder:  
a. n > 350  
Randomly pick 350 pics from the origin data set  
b. 200 < n <= 350  
Keep all the pics  
c. 90 < n <= 200  
Keep all the pics & Apply Opening to them (Double the data)  
d. 30 < n <= 90  
Keep all the pics, Apply Opening to them, Add Gaussian noise to them & Add Salt & Pepper noise to them (Four times the data)  
e. n <= 30  
Drop the folder  
(3) Crop & resize:  
a. Use MTCNN to locate the face (which has already been aligned) & Crop it out  
b. Resize the image to 112 x 112  
(4) PS: The OpenCV ops in Python run really slow and all the operations above have a quite similar code implementation in C++. Thus it is recommended to use C++ for prerocessing the image dataset. 

## 2. Training Strategy  
The GPU memory is not enough for mini-batch size 512 for training on a Nvidia 2080 Ti, thus I have to downsize it to 256.  
  
## 3. Improvement for training step in progress.  

## Reference  
(1) Original paper: https://arxiv.org/abs/1804.07573  
(2) The idea of the implementation of model structure is from MobileNet v2: https://github.com/xiaochus/MobileNetV2  
(3) The implementation of ArcFace loss (InsightFace loss) is from: https://github.com/ewrfcas/Machine-Learning-Toolbox/blob/127d6e5d336614d1efb21e78865501435cdb7b8b/loss_function/ArcFace_loss.py  
