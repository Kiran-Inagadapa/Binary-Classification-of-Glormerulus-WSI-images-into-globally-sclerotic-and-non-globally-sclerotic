# Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic

## Explaining the Dataset:
The Dataset Images are glomerulus identified from kidney biopsy images (Whole Slide Imaging). The dataset consists of a 'public.csv' file and images classified into two folders, namely 'globally_sclerotic_glomeruli' and 'non_globally_sclerotic_glomeruli'. The 'public.csv' file has two columns 'name',i.e, image file_name and 'ground truth',i.e, binary label for the image (0 - non-globally sclerotic; 1 - globally sclerotic).

## Approach to create model: "Stack Ensemble Modeling"
Stack Ensemble Modeling is an advanced technique designed to enhance predictive accuracy by integrating multiple models, known as base learners. In this approach, the predictions generated by these base learners are utilized to train a higher-level model, called a meta learner. The meta learner's objective is to effectively learn the optimal way to combine the predictions from the various base models. This method leverages the strengths and mitigates the weaknesses of individual models, resulting in a more robust and accurate final prediction.

### Observations made from the dataset:
1. Globally Sclerotic Glomeruli are homogeneously pink while Non-Globally Sclerotic Glomeruli have lot of details at the center.
2. Globally Sclerotic Glomeruli have a thin wall around compared to the thick wall observed in Non Globally Sclerotic Glomeruli.

Based on the observations, Preprocessing is employed to create two different sets of training, validation and testing datasets. The first preprocessing involves enhancing the color for training. The second preprocessing involves extracting the structure and patterns in the images. Also, Data Augumentation is implemented to create more variation in the dataset. In Augumentaion, Horizontal flip, Vertical flip and Rotation were implemented.

### Techniques employed for preprocessing to enhance Colors:
1. Equalized Histogram
2. Saturation Adjustments
3. Hue Adjustments

![download](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/6b2d2c78-b523-4066-8f64-3de026f3efa6)

### Techniques employed for preprocessing to extract structure and patterns:
1. Dilation and Erosion
2. Gaussian bluring
3. Edge Detections using Canny

![download](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/a96f410d-b758-42f2-a6a1-2842ef71e398)

The created two preprocessed datasets of training, validation and testing, are then used to train two different Base Learner models. The Base Learner models are ResNet50V2 adn InceptionV3, both these Image Classification CNNs are pretrained on ImageNet Dataset and have shown very promising results with minimal computational resource requirements.

## Binary Classification using Stack Ensemble Technique with two Base Learners and a Meta Learner:
### Base Learner 1: ResNet50V2 trained on color enhanced images:
-> The standard input size for ResNet50V2 with ImageNet weights is (224,224,3) and the input dataset should be preprocessed with 'tf.keras.applications.resnet.preprocess_input'.\
-> ResNet50V2 is pretrained on ImageNet Dataset which consists of 1000 classes, to suit this CNN to our Binary Classification requirements, three more layers were added on top, one is Global Average Pooling 2D Layer, A Dropout layer with Regularization parameter set to 0.3, A prediction layer with sigmoid activation that gives a binary output.\
-> Since the dataset is only 5757 images and the entire 190 layers in the ResNet50V2 cannot be trained with such small dataset, the lower 140 layers are set not to train and the rest top layers are trained.\
-> Learning Rate: 0.001.\
-> Optimizer: Stochastic Gradient Descent.\
-> Loss Function: Binary Cross Entropy.\
-> Metrics: Binary Accuracy with threshold set to 0.5.

![model_1](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/b1348704-7e2a-441a-9a45-c49e034a1ee7)

#### link to access the Base Learner model-1:

#### Plot for Training and Validation Accuracy:
![download_1](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/a67fbc8e-945b-4aed-99f9-96f214a29b68)

#### Plot for Training and Validation Loss:
![download_2](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/7095fc53-3576-4ab9-a599-6a91a286f924)

### Base Learner 2: InceptionV3 trained on images preprocessed with edge detection:
-> The standard input size for InceptionV3 with ImageNet weights is (299,299,3) and the input dataset should be preprocessed with 'tf.keras.applications.inception_v3.preprocess_input'.\
-> Similar to ResNet50V2, three additional layers were added with same settings.\
-> Similar to ResNet50V2, the entire 311 layers in the InceptionV3 cannot be trained with such small dataset, the lower 230 layers are set not to train and the rest top layers are trained.\
-> Learning Rate: 0.001.\
-> Optimizer: Stochastic Gradient Descent.\
-> Loss Function: Binary Cross Entropy.\
-> Metrics: Binary Accuracy with threshold set to 0.5.

![model](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/94570019-45a6-4376-ae69-10e69f5fa425)

#### link to access the Base Learner model-2:

#### Plot for Training and Validation Accuracy:

#### Plot for Training and Validation Loss:

To store the best two learned models out of the each 7 epochs run on each Base Learner model, "tf.keras.callbacks.ModelCheckpoint" have been used.

### Meta Learner: Binary Logistic Regression trained on the predictions of the Base Learners:

##### link to access the Meta Learner:
