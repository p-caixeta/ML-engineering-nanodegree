# Plagiarism Detector Project

## Project Overview
In this project, I was tasked with building a plagiarism detector that examines a text file and performs binary classification; labeling that file as either **plagiarized** or not, depending on how similar that text file is to a provided source text. Detecting plagiarism is an active area of research; the task is non-trivial and the differences between paraphrased answers and original work are often not so obvious.


## Contents
Inside this folder, there are 3 python notebooks:

1. Data Exploration:
* loaded in the data;
* explored the existing features and distribution
2. Feature Engineering:
  * cleaned and pre-processed the text data;
  * defined features for comparing the similarity of an answer text and a source text, and extracted similarity features;
  * selected "good" features (analyzing the correlations between different features);
  * created the train and test .csv files holding the relevant features and class labels for train/test data points.
3. Trained and deployed the model in SageMaker:
* Uploaded the train/test feature data to S3;
* defined a binary classification model and a training script;
* trained and deployed the model using SageMaker;
* evaluated the deployed classifier.

#### Obs: this projects uses AWS' Sagemaker as well as other python files (which are not included here), so it will no be able to run from here.
For the complete description and original files, please refer to https://github.com/udacity/ML_SageMaker_Studies
