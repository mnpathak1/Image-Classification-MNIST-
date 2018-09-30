# Image classification in MNIST dataset
## Dataset
This datsaet is taken from Kaggle:  
https://www.kaggle.com/c/digit-recognizer/data  
The data files train.csv and test.csv contain gray-scale images of hand-drawn digits, from zero through nine.  
Each image is 28 pixels in height and 28 pixels in width, for a total of 784 pixels in total. Each pixel has a single pixel-value associated with it, indicating the lightness or darkness of that pixel, with higher numbers meaning darker. This pixel-value is an integer between 0 and 255, inclusive.

The training data set, (train.csv), has 785 columns. The first column, called "label", is the digit that was drawn by the user. The rest of the columns contain the pixel-values of the associated image.

Purpose of this analysis is to build a model to predict the the digits in test dataset.
A Convolutional Neural Network (CNN)  model is applied using Keras for this analysis.

## Image classification model building and results

Datasetcolumns are normalized to (0...1) from (0...255) and reshaped into 28 x 28 x 1 matrices (1 channel  for grey scale).  
Digits (Y labels) are encoded to one-hot-vectors.  
Following CNN is used for model  building:  
Conv2D->relu -> Conv2D->relu -> MaxPool2D -> Dropout -> Conv2D->relu -> Conv2D->relu -> MaxPool2D -> Dropout -> Flatten -> Dense -> Dropout -> Dense -> Dropout -> Output  
First layer uses 32 filters, same padding for to keep same input and output lengths, maxpull 2 x 2 and dropout of 0.25, categorical_crossentropy loss, Adam optimizer, learning rate is dynalically adjusted with half the value if the accuracy is not improved after 3 epochs.  
It was observed that data augmentation improves accuracy and therefore certain data augmentations in the training dataset were implemented.  
Based on comparison of optimization algorithms (SGD, RMSProp, Adam etc.), although other methods showed slightly higher accuracies, Adam was used for final model.   
With 25 epochs and batch size of 86, training and validation losses and accuracies were observed to be saturating. 
Accuracies obtained in the test dataset is about 99.5% or higher (not shown), comparable to training and validation accuracies.  
Error analysis showed that the model was not able to identify mostly incomprehensible handwritten images.  
