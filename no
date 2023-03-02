# csbl

################################################################################################################################################
#
# Written by: Laia Vancells Lopez
# 03/02/2023
#
#################################################################################################################################################


The following code aims to classify incline and speed as a function of grf through a 18-class classification task using time series data and a Recurrent Neural Network (RNN). The code is written in Python and utilizes various libraries including mat4py, pandas, numpy, itertools, os, and matplotlib.

**Data**
The preprocessed data is stored in a MATLAB file, which is loaded into a Python dictionary using the mat4py library. The data consists of time series measurements of three features (Forefoot, Midfoot, and Heel) collected from multiple subjects walking on a treadmill at different inclines and speeds. The goal is to classify each time series based on the incline and speed combination.

**Preprocessing**
The code extracts time series data from the dictionary and constructs time series of 85 time steps and 3 features. The time series data is then appended to a 2D list along with its corresponding label, which is an integer between 0 and 17, representing the incline and speed combination. The label_list and timeseries_list are constructed and converted to numpy arrays.

**RNN Modeling**
The RNN is defined using the Keras API from TensorFlow. The model consists of an LSTM layer with 64 units, followed by two fully connected layers with 32 and 18 units, respectively. The LSTM layer takes in the reshaped time series data as input. The output of the final dense layer is a probability distribution over the 18 possible labels. The sparse_categorical_crossentropy loss function is used, along with the Adam optimizer. The sparse_categorical_accuracy metric is used to evaluate the performance of the model during training.

**Training and Evaluation**
The data is split into training and testing sets using the train_test_split function from the sklearn.model_selection library. The model is trained using the fit method, with the training and testing sets as inputs. The training is run for 200 epochs, with a batch size of 32. The validation data is passed as a tuple to the validation_data argument of the fit method.
After training, the performance of the model is visualized using matplotlib. Two plots are created, one for training accuracy and one for validation accuracy. These plots show the accuracy of the model on the training and validation sets as a function of the number of epochs. The accuracy of the model can be interpreted as the fraction of correctly classified time series in the dataset.

**Conclusion**
This code provides an example of how to preprocess time series data, train an RNN for classification tasks, and evaluate its performance. The code can be adapted to other datasets and classification tasks by modifying the data extraction and preprocessing steps and changing the RNN architecture and hyperparameters.
![image](https://user-images.githubusercontent.com/126813118/222515907-a5cd8b94-030c-4177-9d30-37f4e903e704.png)
