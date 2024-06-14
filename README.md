# Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic

## Explaining the Dataset:
The Dataset Images are glomerulus identified from kidney biopsy images (Whole Slide Imaging). The dataset consists of a 'public.csv' file and images classified into two folders, namely 'globally_sclerotic_glomeruli' and 'non_globally_sclerotic_glomeruli'. The 'public.csv' file has two columns 'name',i.e, image file_name and 'ground truth',i.e, binary label for the image (0 - non-globally sclerotic; 1 - globally sclerotic).

## Approach to create model: "Stack Ensemble Modeling"
Stack Ensemble Modeling is a technique used to improve predictive performance by combining multiple models (Base Learners), whose predictions are used train a Meta Learner to learn how to best combine the predictions of several base models.

### Observations made from the dataset:
1. Globally Sclerotic Glomeruli are homogeneously pink while Non-Globally Sclerotic Glomeruli have lot of details at the center
2. Globally Sclerotic Glomeruli have a thin wall around compared to the thick wall observed in Non Globally Sclerotic Glomeruli

Based on the observations, Preprocessing is employed to create two different sets of training, validation and testing datasets. The first preprocessing involves enhancing the color for training. The second preprocessing involves extracting the structure and patterns in the images.

###Techniques employed for preprocessing to enhance Colors:
1. Equalized Histogram
2. Saturation Adjustments
3. Hue Adjustments

###Techniques employed for preprocessing to extract structure and patterns:
1. Dilation and Erosion
2. Gaussian bluring
3. Edge Detections using Canny


The created two preprocessed datasets of training, validation and testing, are then used to train two different Base Learner models.

## Binary Classification using Stack Ensemble Technique with two Base Learners and a Meta Learner:
### Base Learner 1: ResNet50V2 trained on color enhanced images
### Base Learner 2: InceptionV3 trained on images preprocessed with edge detection
### Meta Learner: Binary Logistic Regression trained on the predictions of the Base Learners
