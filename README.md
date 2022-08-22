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
# code
Here is an explanation of how I approached this project. If you want to dive in the code

# Data Set Summary & Exploration

1.Dataset presentation

The data is provided in pickle files. It is already split in a training set, a validation set and a test set.

- There are 34799 images in the training set.
- There are 4410 images in the validation set.
- There are 12630 images in the test set.
- Each image is 32 by 32 pixels, each having a R,G and B component. Their shape is therefore (32, 32, 3).
- The dataset contains 43 different traffic signs. They are called classes.

2.Visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data is ditributed across the different labels. 

§§

The average number of training examples per class is 809, the minimum is 180 and the maximum 2010, hence some labels are one order of magnitude more abundant than others.

Most common signs:

- Speed limit (50km/h) train samples: 2010
- Speed limit (30km/h) train samples: 1980
- Yield train samples: 1920
- Priority road train samples: 1890
- Keep right train samples: 1860
-
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

1. Image preprocessing

Question 1:

Describe how you preprocessed the data. Why did you choose that technique?

Answer

Following a published baseline model on this problem I applied similar normalization and image enhancements . Images were transformed in the YUV space and adjusted by histogram sketching and by increasing sharpness. Finally only the Y channel was selected as in some preliminary experiments full color images seem to confuse the classifier (as also reported in the published baseline), the latter effect however may depend on the network architecture, as in the long term we would intuitively expect to have networks trained with full color images to perform better.

ROI Cropping

For each image of each dataset, a region of interest is provided. It gives a precise location to where the sign actually is. In order to maximize my chances that the model is going to learn features from the sign I crop the background to remove the noise as much as possible.

§§§
