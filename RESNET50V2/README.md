# Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic

## Explaining the Dataset:
The Dataset Images are glomerulus identified from kidney biopsy images (Whole Slide Imaging). The dataset consists of a 'public.csv' file and images classified into two folders, namely 'globally_sclerotic_glomeruli' and 'non_globally_sclerotic_glomeruli'. The 'public.csv' file has two columns 'name',i.e, image file_name and 'ground truth',i.e, binary label for the image (0 - non-globally sclerotic; 1 - globally sclerotic).

## Approach to create model: 
Training a pretrained ResNet50V2 model by unfreezing top few layers.

### Observations made from the dataset:
1. Globally Sclerotic Glomeruli are homogeneously pink while Non-Globally Sclerotic Glomeruli have lot of details at the center.

Based on the observations, Preprocessing is employed to create a set of training, validation and testing datasets. The preprocessing involves enhancing the color for training. Also, Data Augumentation is implemented to create more variation in the dataset. In Augumentaion, Horizontal flip, Vertical flip and Rotation were implemented.

### Techniques employed for preprocessing to enhance Colors:
1. Equalized Histogram
2. Saturation Adjustments
3. Hue Adjustments

#### Color Enhanced and Augumented Images:
![download](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/6b2d2c78-b523-4066-8f64-3de026f3efa6)

## Binary Classification using ResNet50V2:
### Base Learner 1: ResNet50V2 trained on color enhanced images:
#### link to access the Base Learner model-1: [link]()
-> The standard input size for ResNet50V2 with ImageNet weights is (224,224,3) and the input dataset should be preprocessed with 'tf.keras.applications.resnet.preprocess_input'.\
-> ResNet50V2 is pretrained on ImageNet Dataset which consists of 1000 classes, to suit this CNN to our Binary Classification requirements, three more layers were added on top, one is Global Average Pooling 2D Layer, A Dropout layer with Regularization parameter set to 0.3, A prediction layer with sigmoid activation that gives a binary output.\
-> Since the dataset is only 5757 images and the entire 190 layers in the ResNet50V2 cannot be trained with such small dataset, the lower 140 layers are set not to train and the rest top layers are trained.\
-> Learning Rate: 0.001.\
-> Optimizer: Stochastic Gradient Descent.\
-> Loss Function: Binary Cross Entropy.\
-> Metrics: Binary Accuracy with threshold set to 0.5.

![model_1](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/b1348704-7e2a-441a-9a45-c49e034a1ee7)

#### Plot for Training and Validation Accuracy:
![download_1](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/a67fbc8e-945b-4aed-99f9-96f214a29b68)

#### Plot for Training and Validation Loss:
![download_2](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/assets/124871182/7095fc53-3576-4ab9-a599-6a91a286f924)
