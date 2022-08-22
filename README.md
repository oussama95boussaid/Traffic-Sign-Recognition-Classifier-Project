# Traffic-Sign-Recognition-Classifier-Project


The goals / steps of this project are the following:

- Load the data set (see below for links to the project data set)
- Explore, summarize and visualize the data set
- Design, train and test a model architecture
- Use the model to make predictions on new images
- Analyze the softmax probabilities of the new images
- Summarize the results with a written report

# *Rubric Points*

Here I will consider the rubric points individually and describe how I addressed each point in my implementation. 
This is a summary. Continue further to read each in depth.

- As per project requirements, Traffic Sign Classifier project Notebook, HTML file and write up Files submitted.
- Dataset summary & image visualization with image type distribution plot created.
- Design & test model: which includes preprocessing, model architecture, hyperparameter tunning, training, and solution.
- Test model on new images, Trained model tested on new image downloaded from web, and plotted its softmax probability.
- Featuremap visualisation, Featuremap for all convolution layaer and pooling layer plotted.

# *code*
Here is an explanation of how I approached this project. If you want to dive in the code

# *Data Set Summary & Exploration*

1.Dataset presentation

The data is provided in pickle files. It is already split in a training set, a validation set and a test set.

- There are 34799 images in the training set.
- There are 4410 images in the validation set.
- There are 12630 images in the test set.
- Each image is 32 by 32 pixels, each having a R,G and B component. Their shape is therefore (32, 32, 3).
- The dataset contains 43 different traffic signs. They are called classes.

2.*Visualization of the dataset.*

Here is an exploratory visualization of the data set. It is a bar chart showing how the data is ditributed across the different labels. 

§§

The average number of training examples per class is 809, the minimum is 180 and the maximum 2010, hence some labels are one order of magnitude more abundant than others.

Most common signs:

- Speed limit (50km/h) train samples: 2010
- Speed limit (30km/h) train samples: 1980
- Yield train samples: 1920
- Priority road train samples: 1890
- Keep right train samples: 1860

Most rare signs:

- Speed limit (20km/h) train samples: 180
- Dangerous curve to the left train samples: 180
- Go straight or left train samples: 180
- Pedestrians train samples: 210
- End of all speed and passing limits train samples: 210
-
Here is an visualization of some 5 randomly picked training examples for each class. As we can see, within each class there is a high variability in appearance due to different weather conditions, time of the day and image angle.
§§§
#Design and Test a Model Architecture

# 1. Image preprocessing

Question 1:

Describe how you preprocessed the data. Why did you choose that technique?

Answer

Following a published baseline model on this problem I applied similar normalization and image enhancements . Images were transformed in the YUV space and adjusted by histogram sketching and by increasing sharpness. Finally only the Y channel was selected as in some preliminary experiments full color images seem to confuse the classifier (as also reported in the published baseline), the latter effect however may depend on the network architecture, as in the long term we would intuitively expect to have networks trained with full color images to perform better.

*ROI Cropping*

For each image of each dataset, a region of interest is provided. It gives a precise location to where the sign actually is. In order to maximize my chances that the model is going to learn features from the sign I crop the background to remove the noise as much as possible.

§§§

*Normalization*

What is recommended to do is to center the data so it has 0 mean. Instead, I remove 180 to each RGB channels. It is very similar and would perform well for my model. I normalized the scale of each image to range between -1 and 1. This allows a better convergence of the model because the computation of the gradient is facilitated.

$$$

It is important to note that the normalization needs to be applied to every set (training, validation et test sets) in order to train a working model.

Due to the disparity between classes and the total numbers of images in the training data, I decided to augment the dataset.

To augment the dataset means to add new training data. Copy identically data from the training set is not a good idea because it increases the risk of overfitting. The goal is to take images from the training set and modify them a little bit so that it presents new features but still belonging to the same class.

In order to do so, I created 2 functions.

*Rotation*

The first idea is to rotate the image a little bit. The angle is determined randomly and bounded between -15° and +15°. It wouldn't make sense to rotate them more than that since the car would never see traffic sign that are upside down. It is worth noticing that it could be interesting to do so for another dataset like classify galaxies! for example.

$$$

# 2. Model architecture.

My final model consisted of the following layers:

# 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

Adam Optimizer

Adam offers several advantages over the simple tf.train.GradientDescentOptimizer. Foremost is that it uses moving averages of the parameters. The concept behind this is called "momentum". The provided learning rate is the maximum coefficient applied to the gradient during backpropagation. The Adam optimizer determines when to lower that learning rate for each parameter. This brings some computation overhead as this is performed for each training step (maintain the moving averages and variance, and calculate the scaled gradient). A simple tf.train.GradientDescentOptimizer could equally be used in your MLP, but would require more hyperparameter tuning before it would converge as quickly.

# *Test of my model on New Images*

# 1. Presentation of the images

Theses images have the same meaning that the ones of the German dataset but some might have some small differences like of example the presence of km/h on the 30 km/h speed limit sign or the width of some arrows. Other that that, these images do not present major problems of visibility that might trick the model but in order to perform well on these images, it comes down to how good were the images of the training data. I want to highlight here that I believe that these images were not very clear. I had a hard time determining the class of many of the images in the dataset myself.

$$$ 

# 2. Predictions labels of these images and their top 5 softmax probabilities

$$$



