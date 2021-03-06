#**Traffic Sign Recognition** 


**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:

* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

###Data Set Summary & Exploration

####1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410  
* The size of test set is 12630
* The shape of a traffic sign image is (32,32,3)
* The number of unique classes/labels in the data set is 43

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing the frequency of each traffic signs in the dataset. Distribution of traffic sign types is not uniform. Certain signs have significantly more representations (1 and 2 for example).

![text](/Users/hyu/SideProjects/SelfDriving/ProjectSubmissions/Project2/freq_dist.png) 




###Design and Test a Model Architecture

####1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale to reduce the influence of shadows and color variations.
Here is an example of a traffic sign image before and after grayscaling.

![normal](/Users/hyu/SideProjects/SelfDriving/ProjectSubmissions/Project2/normal.png)![grayscale](/Users/hyu/SideProjects/SelfDriving/ProjectSubmissions/Project2/grayscale.png)


As a last step, I normalized the image data because it reduced the range of pixelvalues, alowing the network to converge easier.


####2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description | 
|:---------------------:|:---------------------------------------------:| 
|Input	|32x32x3 RGB image|
|Convolution 5x5|	1x1 stride, same padding, outputs 32x32x6
|RELU	
|Max pooling	|2x2 stride, outputs 14x14x16
|Convolution 5x5|	1x1 stride, outputs 10x10x16
|RELU	
|Max pooling	|2x2 stride, outputs 5x5x16
|Flatten	|outputs 1x400
|Fully connected	|outputs 1x120
|RELU	
|Fully connected	|outputs 1x84
|RELU	
|Fully connected	|outputs 1x43



####3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an Adam optimizer and set the batch size to 128. I used a number of epochs of 30 and set my learning rate to 0.001. 

####4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.997
* validation set accuracy of 0.927
* test set accuracy of 0.921

If a well known architecture was chosen:
* The LeNet architecture is used. 
* From the course lectures, LeNet has been applied to MNIST dataset to recognize hand-written numbers. The German Traffic Sign dataset has the same dimensions as MNIST dataset, leaving LeNet a promissing candidate.
* The model's accuracy on training and validation is not bad (>92%) with even minor modification of parameters in LeNet indicates that LeNet is working well for this problem. 


###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![](new_images/p_1.png)

![](new_images/p_2.png)

![](new_images/p_3.png)

![](new_images/p_4.png)

![](new_images/p_5.png)

The images are of different sizes and resolutions. The first image might be difficult to classify because the traffic sign only occupies a small portion of the whole image.

####2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 30 km/h |30 km/h|
|Construction | Construction|
|Stop	|Stop |
|Right-of-way at the next intersection |Right-of-way at the next intersection|
| No passing    		| End of no passing|  			


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. 

####3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 20th cell of the Ipython notebook.
For the first image, the model predicts "30 km/h" with 0.96 probability, and the image does contain a "30 km/h" speed limit sign. The top five soft max probabilities are

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 9.58636463e-01       			| **30 km/h** | 
| 4.08801958e-02  				| 60 km/h										|
| 4.57877060e-04				| Wild animals crossing											|
| 2.46378568e-05      			| 50 km/h					 				|
| 5.00919668e-07				    |Road narrows on the right      							|
For image 2 ~ image 4, the model is pretty sure about the prediction, with probability of almost 1.0.
For the last image (no passing), the model gives a wrong prediction (end of no passing). The top five soft max probabilities are
          
| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 9.99611557e-01       			| end of no passing| 
| 3.88456974e-04  				| **no passing**|
| 8.25234082e-23				| Priority road|
| 2.63337722e-28      			| Priority road|
| 1.92636711e-31			    |Go straight or right      |




