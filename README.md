# Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic

To solve the problem, two approaches were followed:

## 1. Stack Ensemble Method with two Base Learners and a Meta Learner:
#### link to folder: [STACK ENSEMBLE](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/tree/main/STACK%20ENSEMBLE)
A [README.md](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/blob/main/STACK%20ENSEMBLE/README.md) file is included in the Folder, that explains the implementation of this solution.
### Evaluation procedure:
-> evaluation.py is renamed as ['evaluation_stackedensemble.py'](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/blob/main/STACK%20ENSEMBLE/evaluation_stackedensemble.py)\
-> Download the models from the links provided in the README.md.\
-> Save the models and the dataset in the local directory of the script.\
-> Run the script.\
-> Script will prompt for the dataset folder filename, base model 1 filename, base model 2 filename and meta learner filename.\
-> Script will create other directories with names 'processed_test_data_1' and 'processed_test_data_2' to store preprocessed images.\
-> The predicted values will be stored as 'evaluation.csv'

## 2. ResNet50V2:
#### link to folder: [RESNET50V2](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/tree/main/RESNET50V2)
A [README.md](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/blob/main/RESNET50V2/README.md) file is included in the Folder, that explains the implementation of this solution.
### Evaluation procedure:
-> evaluation.py is renamed as ['evaluation_resnet50v2'](https://github.com/Kiran-Inagadapa/Binary-Classification-of-Glormerulus-WSI-images-into-globally-sclerotic-and-non-globally-sclerotic/blob/main/RESNET50V2/evaluation_resnet50v2.py)
-> Download the models from the links provided in the README.md.\
-> Save the models and the dataset in the local directory of the script.\
-> Run the script.\
-> Script will prompt for the dataset folder filename and model filename.\
-> Script will create a directory named 'processed_test_data' to store preprocessed images.\
-> The predicted values will be stored as 'evaluation.csv'
