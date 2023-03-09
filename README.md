# csbl

Week March 5th - March 12th

This week I have worked on improving my previous documentation. After feedback from my professors, the final documentation for the LSTM analysis is the following:

The following code aims to classify incline and speed as a function of grf through a 3,6,18-class classification task using time series data and a Recurrent Neural Network (RNNN). The code is written in Python.

image

Data: the preprocessed data is stored in a MATLAB file, which is loaded into a Python dictionary using the mat4py library.

image

The data consists of time series measurements of three features (Forefoot, Midfoot, and Heel) collected from multiple subjects walking on a treadmill at different inclines and speeds. The goal is to classify each time series based on the incline and speed combination.

image

Preprocessing: the code extracts time series data from the dictionary and constructs time series of 85 time steps and 3 features. The time series data is then appended to a 2D list along with its corresponding label, which is an integer between 0 and 17, representing the incline and speed combination. The label_list and timeseries_list are constructed and converted to numpy arrays. More specifically, the first loop loops through each subject. Within this loop, a label is set to 0 to keep track of the speed. The next two for loops loop through each incline and each speed, respectively (the try and except statements are used to handle cases where there is no data available for the current incline and speed for the current subject. If this is the case, the contain statement is executed, and the loop moves on to the next incline and speed).

image

Note: This part of the code varies depending on how many classes we aim to predict.
Then the code loops through each key-value pair in the subject data. For each key-value pair, the forefoot, midfoot, and heel data are flattened into lists using the list (chain.from_iterable()) method. The first 85 values of each list are taken, and the three lists are combined into one list of length 255. If the length of the combined list is not equal to 255 (i.e., there is missing data), the continue statement is executed, and the loop moves on to the next key-value pair. If there is no missing data, the combined list is appended to the timeseries_list along with the corresponding label. The label is incremented by 1 for each speed. This process is repeated for each subject, incline, and speed.

image

The timeseries_list and label_list are then converted to numpy arrays using np.array() and assigned to timeseries_ matrix and label_array, respectively. The shape of timeseries_matrix is then printed to confirm that the resulting 2D numpy array has the expected shape.

image

Finally, the two-dimensional timeseries_matrix array is transformed into a three-dimensional tensor with 85 time steps and three features per step. The reshape() function is applied to timeseries_matrix with three arguments: -1, 85, and 3. The first argument (-1) instructs NumPy to calculate the size of the first dimension based on the original array and the other two dimensions. The second argument (85) specifies the number of time steps, while the third argument (3) denotes the number of features per step.

image

RNN Modeling: The RNN is defined using the Keras API from TensorFlow. The model consists of an LSTM layer with 64 units, followed by two fully connected layers with 32 and 18 units, respectively. The LSTM layer takes in the reshaped time series data as input. The output of the final dense layer is a probability distribution over the 3/6/18 possible labels. The sparse_categorial_crossentropy loss function is used, along with the Adam optimizer. The sparse_categorical_accuracy metric is used to evaluate the performance of the model during training.

image

Training and Evaluation: The data is split into training and testing sets using the train_test_split function for the sklearn.model_seletion library.

image

The model is trained using the fit method, with the training and testing sets as inputs. The training is run for 200 epochs with a batch size of 32. The validation data is passed as a tuple to the validation_data argument of the fit method.

image

After training, the performance model is visualized using matplotlib. Two plots are created, one for training accuracy and one for validation accuracy. These plots show the accuracy of the model on the training and validation sets as a function of the number of epochs. The accuracy of the model can be interpreted as the fraction of correctly classified time series in the dataset.

image

Conclusion: This code provides an example of how to preprocess time series data, train an RNN for classification tasks (3,6,18-class classification), and evaluate its performance. The code can be adapted to other datasets and classification tasks by modifying the data extraction and preprocessing steps and changing the RNN architecture and hyperparameters.

https://github.com/lvancells/csbl.git (3,6,18-class classification)
