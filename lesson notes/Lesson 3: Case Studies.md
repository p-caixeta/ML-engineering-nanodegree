# Case Studies
Case studies are in-depth examinations of specific, real-world tasks (with focus on three different problems and look at how they can be solved using various machine learning strategies). The case studies are as follows:

### Case Study 1 - Population Segmentation using SageMaker

Using portion of US census data and a combination of unsupervised learning methods, meaningful components from that data were extracted, and grouped regions by similar census-recorded characteristics. This case is a deep dive into Principal Components Analysis (PCA) and K-Means clustering methods, and the end result will be groupings that are used to inform things like localized marketing campaigns and voter campaign strategies.

### Case Study 2 - Detecting Credit Card Fraud

This case demonstrates how to use supervised learning techniques, specifically SageMaker’s LinearLearner, for fraud detection. The payment transaction dataset we'll work with is unbalanced, with many more examples of valid transactions vs. fraudulent, so methods for compensating for this imbalance and tuning your model to improve its performance according to a specific product goal were investigates.

#### Custom Models - Non-Linear Classification

Adding on to it, it was shown how to manage cases where classes of data are not separable by a linear line, by training and deploying a custom, PyTorch neural network for classifying data.

### Case Study 3 - Time-Series Forecasting

This case demonstrates how to train SageMaker's DeepAR model for forecasting predictions over time. Time-series forecasting is an active area of research because a good forecasting algorithm often takes in a number of different features and accounts for seasonal or repetitive patterns. 

___________________________________________________________________________________________________________________________________________
# Lesson 1: Population Segmentation

* Ground Truth: Combination of human labeling and active learning model to efficiently label data

## K-Means Clustering

You select k, a predetermined number of clusters that you want to form. Then k points (centroids for k clusters) are selected at random locations in feature space. This algorithm can be applied to any kind of unlabelled data. For each point in your training dataset:

- You find the centroid that the point is closest to;
- And assign that point to that cluster;
- Then, for each cluster centroid, you move that point such that it is in the center of all the points that are were assigned to that cluster in step 2;
- Repeat steps 2 and 3 until you’ve either reached convergence and points no longer change cluster membership _or_ until some specified number of iterations have been reached.


- To print one histogram under the other:

    for column_name in transport_list:
        ax=plt.subplots(figsize=(6,3))
        # get data by column_name and display a histogram
        ax = plt.hist(clean_counties_df[column_name], bins=n_bins)
        title="Histogram of " + column_name
        plt.title(title, fontsize=12)
        plt.show()
    
    
- To normalize the data: https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.MinMaxScaler.html  

    from sklearn.preprocessing import MinMaxScaler ; scaler = MinMaxScaler() ; new_df = scaler.fit_transform(df)
    
## PCA

Principal Component Analysis (PCA) attempts to reduce the number of features within a dataset while retaining the “principal components”, which are defined as weighted combinations of existing features that:

- Are uncorrelated with one another, so you can treat them as independent features, and
- Account for the largest possible variability in the data!
So, depending on how many components we want to produce, the first one will be responsible for the largest variability on our data and the second component for the second-most variability, and so on, which is exactly is needed for clustering purposes. PCA is commonly used when you have data with many many features.

Obs: it is **necessary** to *center* your data around 0; and it is **Optional** to *normalize* the data before applying pca. The pca.fit object already does this for you

To choose how many elements to retain, use pca.explained_variance_ratio

### PCA Model Attributes

Three types of model attributes are contained within the PCA model.

* **mean**: The mean that was subtracted from a component in order to center it.
* **v**: The makeup of the principal components; (same as ‘components_’ in an sklearn PCA model).
* **s**: The singular values of the components for the PCA transformation. This does not exactly give the % variance from the original feature space, but can give the % variance from the projected feature space.
    
We are only interested in v and s. 

From s, we can get an approximation of the data variance that is covered in the first `n` principal components. The approximate explained variance is given by the formula: the sum of squared s values for all top n components over the sum over squared s values for _all_ components:

\begin{equation*}
\frac{\sum_{n}^{ } s_n^2}{\sum s^2}
\end{equation*}

From v, we can learn more about the combinations of original features that make up each principal component.

## Choosing a "Good" K

One method for choosing a "good" k, is to choose based on empirical data. A bad k would be one so *high* that only one or two very close data points are near it, and another bad k would be one so *low* that data points are really far away from the centers.

You want to select a k such that data points in a single cluster are close together but that there are enough clusters to effectively separate the data. You can approximate this separation by measuring how close your data points are to each cluster center; the average centroid distance between cluster points and a centroid. After trying several values for k, the centroid distance typically reaches some "elbow"; it stops decreasing at a sharp rate and this indicates a good value of k.

##### Deploy the trained model to an Amazon SageMaker endpoint and return a sagemaker.Predictor object.
https://sagemaker.readthedocs.io/en/stable/api/inference/predictors.html#sagemaker.predictor.Predictor

# Lesson 2: Detecting Credit Card Fraud

##### WHEN USING LABELED DATA, PASS THE LABEL TO RECORD_SET

### Precision and recall

**Precision** is defined as the number of *true positives* over *all positives*. Which means how many *true* predictions were actually true

**Recall** is defined as the number of *true positives* over *true positives + false negatives*. Which means how many *of the actual true cases* were predicted

![precision-recall.png](precision-recall.png)

### Model Improvement: Accounting for Class Imbalance
Class imbalance may actually bias our model towards predicting that all transactions are valid, resulting in higher false negatives and true negatives. 
If you just train the model to get a higher **recall** (using binary_classifier_model_selection_criteria, and therefore getting *fewer false negatives*), you will endup with a **smaller precision**(i.e., a lot of *false positives* - flagging legitimate transactions as fraudulent)

To account for imbalance, LinearLearner offers the **positive_example_weight_mult**, which is the *weight assigned to positive (fraudulent data) examples when training a binary classifier*. The weight of negative examples (valid data) is fixed at 1:
"If you want the algorithm to choose a weight so that errors in classifying negative vs. positive examples have equal impact on training loss, specify balanced."

# Lesson 3: Time-Series Forecasting

Example of 3-layer MLP
https://github.com/udacity/deep-learning-v2-pytorch/blob/master/convolutional-neural-networks/mnist-mlp/mnist_mlp_solution.ipynb

### Defining a Custom Model
To define a custom model, you need to have the model itself and the following two scripts:

- A training script that defines how the model will accept input data, and train. This script should also save the trained model parameters.
- A predict script that defines how a trained model produces an output and in what format.

##### PyTorch
In PyTorch, you have the option of defining a neural network of your own design. These models do not come with any built-in predict scripts and so you have to write one yourself.

##### SKLearn
The scikit-learn library, on the other hand, has many pre-defined models that come with train and predict functions attached!

You can define custom SKLearn models in a very similar way that you do PyTorch models only you typically only have to define the training script. You can use the default predict function.

### Create and Deploy a Trained Model
Before you can deploy a custom PyTorch model, you have to take one more step: creating a PyTorchModel. In earlier exercises, you could see that a call to .deploy() created both a model and an endpoint, but for PyTorch models, these steps have to be separate. PyTorch models do not automatically come with .predict() functions attached (as many Amazon and Scikit-learn models do, for example) and you may have noticed that you've been given a predict.py file in the source directory. This file is responsible for loading a trained model and applying it to passed in, numpy data.

Now, when we created a PyTorch estimator, we specified where the training script, train.py was located. And we'll have to do something very similar here, but for a PyTorch model and the predict.py file.

