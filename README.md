# FaceMaskDetection

1.	Exploratory Data Analysis
a.	The Dataset consists of roughly 18,000 train images and 6,000 test images of people faces, some of which are wearing different forms of face masks and covers.
All images containing a person with a covered face are labeled "1" meaning the person in the image is wearing a mask, it's important to note that mask is not the only form of "face cover" which is recognized as a positively labeled image.
Examples of training data images (original size):
![image](https://user-images.githubusercontent.com/26842519/94170473-cc0b5400-fe98-11ea-90a2-3d1c9209ff62.png)
![image](https://user-images.githubusercontent.com/26842519/94170490-d1689e80-fe98-11ea-962d-a10b9f55cdd8.png)


Examples of test data images (original size):
![image](https://user-images.githubusercontent.com/26842519/94170515-d9284300-fe98-11ea-93d1-56ed5fb485f1.png)
![image](https://user-images.githubusercontent.com/26842519/94170523-db8a9d00-fe98-11ea-85ad-2a12587017d4.png)

b.	Key insights from the data:
-	The images are of different size, meaning we will have to resize them before handing them over to our network.
-	Unlike basic open source data sets for deep learning such as Fashion-Mnist, our images are taken in different orientations, angles and directions meaning we don’t have to add any form of random rotation and crop for them to improve our network.
2.	Network Experiments – Net #1

a.	Data Loading and Preprocess:
To use the Pytorch package to build our network we had to build a custom data loader for our dataset, the resulting loader output is 32X32 size images.
As mentioned above, we chose not to use any form of data augmentation because of the nature of the images in the dataset.

b.	Architecture:
Our network consists of 6 convolution layers, and 1 fully connected layer:

![image](https://user-images.githubusercontent.com/26842519/94170553-e3e2d800-fe98-11ea-8215-54a73a841400.png)

![image](https://user-images.githubusercontent.com/26842519/94170568-e80ef580-fe98-11ea-8040-4a9afc3aec02.png)

c.	Loss Function – We choose the Negative Log Likelihood Loss as we are dealing with a classification task.

d.	Optimizer – We choose the Adam optimizer which is an extension of the classical SGD algorithm as it introduces individual learning rate for each parameter and converges faster.

e.	Regularization – We choose to use weight decay as our regularization technique instead of the classical dropout.
Other Parameters:


![image](https://user-images.githubusercontent.com/26842519/94170592-ee9d6d00-fe98-11ea-94c8-f5a91b190f2e.png)
![image](https://user-images.githubusercontent.com/26842519/94170629-f9f09880-fe98-11ea-929d-728b321472cf.png)
![image](https://user-images.githubusercontent.com/26842519/94170652-feb54c80-fe98-11ea-982e-232fdad89c6b.png)

i.	Key Insights:
-	Increasing the number of training epochs is necessary to achieve high performance. 
-	Increasing the size of the first convolution filter to 5X5 proved very useful to our model.
-	Our model barley used a tenth of the total number of available parameters (400K from 5 Mil) and might be too simple.
-	We might want to use dropout in our next attempt as another form of regularization while we are building more complex networks.

3.	Network Experiments – Net #2

a.	Data Loading and preprocess:
After examining the data closely, we noticed that most images are bigger than 32X32 pixels and compressing them to that size might harm our model performance, hence, we decided that our second networks should use 64X64 Images (we did not choose 128X128 because half of the images on the training set are smaller than that size and extensive stretching might distort the images).
As mentioned above, in this attempt we also chose not to use any form of data augmentation.

b.	Architecture:

Apart from adding another convolution layer and increasing the size of filters from 3 to 5, we will use similar architecture as our first attempt:

![image](https://user-images.githubusercontent.com/26842519/94170672-04ab2d80-fe99-11ea-8834-1c86a99397dc.png)
![image](https://user-images.githubusercontent.com/26842519/94170690-08d74b00-fe99-11ea-8b74-cab74332b388.png)
![image](https://user-images.githubusercontent.com/26842519/94170706-0ecd2c00-fe99-11ea-9eb8-2d0b293816c5.png)
![image](https://user-images.githubusercontent.com/26842519/94170733-18569400-fe99-11ea-93c6-fd11c878a414.png)
![image](https://user-images.githubusercontent.com/26842519/94170775-24daec80-fe99-11ea-8e14-68547c8c80db.png)
