# Chapter 1: Machine Learning Design Patterns


# Table of contents
- [Table of contents](#table-of-contents)
- [1. Machine Learning Terminology](#1-machine-learning-terminology)
  - [1.1. Data and Feature Engineering](#11-data-and-feature-engineering) 
  - [1.2. Machine Learning Process](#12-machine-learning-process)
  - [1.3. Data and Model Tooling](#13-data-and-model-tooling)
- [Resources](#resources)

# 1. Machine Learning Terminology
## 1.1. Data and Feature Engineering
- **Training data**: the data fed to your model during the training process. 
- **Validation data**: the data that is held out from your training set and used to evaluate how the model is performing after each training epoch (or pass through the training data). 
  - The performance of the model on the validation data is used to decide when to *stop the training run*, and to choose `hyperparameters`
- **Test data**: the data that is not used in the training process at all and is used to evaluate how the trained model performs. 
  - Performance reports of the machine learning model must be computed on the independent test data, rather than the training or validation tests.
- **Data validation**: is the process of computing statistics on your data, understanding your schema, and evaluating the dataset to identify problems like *drift* and *training-serving skew*. 
  - Evaluating various statistics on your data can help you ensure the dataset contains a balanced representation of each feature.
  - Data validation can identify inconsistencies that may affect the quality of your training and test sets
  - For example, maybe the majority of your training dataset contains weekday examples while your test set contains primarily weekend examples.
## 1.2. Machine Learning Process
A typical machine learning workflow includes:
- **Training**: the process of passing training data to a model so that it can learn to identify patterns. 
- **Model evaluation**: After training, the next step in the process is testing how your model performs on data outside of your training set. 
  - You might run training and evaluation multiple times
  - Performing **additional feature engineering**  
  - Tweaking your model architecture. 
  - Once you are happy with your model’s performance during evaluation, you’ll likely want to serve your model so that others can access it to make predictions.
- **Serving**: refer to accepting incoming requests and sending back predictions by deploying the model as a microservice. 
  - The serving infrastructure could be in 
    - Cloud
    - On-premises: on the premises of the person or organization using the software, rather than at a remote facility such as a server farm or cloud.
    - On-device
- **Prediction**: This can refer both to generating predictions from local models that have not yet been deployed as well as getting predictions from deployed models. 
  - For *deployed* models: `Online` and `Batch` prediction. 
- **Online prediction**: is used when you want to get predictions on a few examples in near real time. 
  - With online prediction, the emphasis is on *low latency*. 
- **Batch prediction**: refers to generating predictions on a large set of data offline. 
  - Batch prediction jobs take longer than online prediction and are useful for precomputing predictions (such as in recommendation systems) and in analyzing your model’s predictions across a large sample of new data.
- **Streaming**: New data being ingested continuously and need to process this data immediately before sending it to your model for training or prediction
- **ML pipelines**: multistep solutions for performing feature engineering, training, evaluation, and predictions to handle streaming data

## 1.3. Data and Model Tooling

<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/159864817-bd10b5c0-1537-4ee9-bff9-9bb52ae792dc.png" width="400" />
</p>

[(Back to top)](#table-of-contents)

# Resources

[(Back to top)](#table-of-contents)
