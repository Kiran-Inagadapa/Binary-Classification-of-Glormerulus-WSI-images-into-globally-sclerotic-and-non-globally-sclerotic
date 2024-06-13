# Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic

## Explaining the Dataset:
The Dataset Images are glomerulus identified from kidney biopsy images (Whole Slide Imaging). The dataset consists of a 'public.csv' file and images classified into two folders, namely 'globally_sclerotic_glomeruli' and 'non_globally_sclerotic_glomeruli'. The 'public.csv' file has two columns 'name',i.e, image file_name and 'ground truth',i.e, binary label for the image (0 - non-globally sclerotic; 1 - globally sclerotic).

### Observations made from the dataset:
1. Globally Sclerotic Glomeruli are homogeneously pink while Non-Globally Sclerotic Glomeruli have lot of details at the center
2. Globally Sclerotic Glomeruli have a thin wall around compared to the thick wall observed in Non Globally Sclerotic Glomeruli

## Binary Classification using Stack Ensemble Technique with two Base Learners and a Meta Learner:
### Base Learner 1: ResNet50V2 trained on color enhanced images
### Base Learner 2: InceptionV3 trained on images preprocessed with edge detection
### Meta Learner: Binary Logistic Regression trained on the predictions of the Base Learners
