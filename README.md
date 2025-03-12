Introduction to RESSEL
RESSEL (Reliable Semi-Supervised Ensemble Learning) is a learning method that combines semi-supervised learning with ensemble learning. The method was originally published in an article linked below. 🔬 
Sjoerd de Vries et al in Knowledge-Based Systems vol. 215 p. 106738 (2021) 
DOI: 10.1016/j.knosys.2021.106738 (https://doi.org/10.1016/j.knosys.2021.106738)

In this approach, both labeled and unlabeled data are used to train the model. The goal is to leverage unlabeled data to improve supervised learning. The key idea behind RESSEL is that by utilizing a set of unlabeled samples, the classification process can be enhanced, leading to better prediction accuracy.

Main Objective of RESSEL
The primary objective of this method is to train a model using a small labeled dataset and a large unlabeled dataset.

RESSEL employs self-training, meaning that after an initial round of training, the model identifies the most confidently classified unlabeled samples and adds them to the training set as labeled data.

The goal of this process is to improve classification accuracy and achieve better predictions in real-world scenarios.

Key Parameters Considered
In the Python implementation of RESSEL, several important parameters are defined to control the learning process:

ensemble_size:

Defines the number of classifiers (ensemble members) used in the algorithm.
A larger number of classifiers increases diversity and improves overall accuracy.
Iterations:

Specifies the number of self-training iterations during which unlabeled data is added to the training set.
batch_size:

Defines the number of unlabeled samples selected in each iteration.
Only samples classified with high confidence are labeled and added to the dataset.
unlabeled_fraction:

Determines the fraction of unlabeled data used in each iteration for self-training.
oob_threshold (Out-of-Bag Error Threshold):

Used for early stopping based on the OOB error (out-of-bag error).
If the OOB error falls below this threshold, the model stops training to prevent overfitting.
Steps for Python Implementation
Loading Data:

The dataset used is Spambase, which contains email features.
The dataset is split into labeled data (for initial training) and unlabeled data (for self-training).
Preprocessing the Data:

Feature scaling is applied using MinMaxScaler.
Feature selection is performed using SelectFromModel with a Random Forest model (RandomForest).
Defining the Base Model:

A Decision Tree Classifier (DecisionTreeClassifier) is used as the base model.
This serves as the fundamental unit for the ensemble learning approach.
Creating the Ensemble Model:

Bagging Classifier (BaggingClassifier) is used to create an ensemble of classifiers.
Multiple decision trees are trained using bootstrap sampling.
Out-of-bag (OOB) samples are used for evaluation.
Self-Training Process:

After initial training on labeled data, the model classifies unlabeled samples.
The most confidently classified unlabeled samples are added to the training set with their predicted labels.
OOB Error Calculation:

After each iteration, the OOB error is computed to evaluate model performance.
Early Stopping:

If the OOB error falls below a predefined threshold, the self-training process stops.
Final Model Evaluation
At the end of the process, the trained model is applied to the Spambase dataset to classify email data.

By leveraging ensemble learning and self-training, the model improves classification accuracy by effectively utilizing unlabeled data.

Finally, the model’s performance is evaluated on the test dataset to assess its overall accuracy.
