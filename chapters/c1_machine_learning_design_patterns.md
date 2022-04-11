# Chapter 1: Machine Learning Design Patterns


# Table of contents
- [Table of contents](#table-of-contents)
- [1. Machine Learning Terminology](#1-machine-learning-terminology)
  - [1.1. Data and Feature Engineering](#11-data-and-feature-engineering) 
  - [1.2. Machine Learning Process](#12-machine-learning-process)
  - [1.3. Data and Model Tooling](#13-data-and-model-tooling)
  - [1.4. Roles](#14-roles)
- [2. Common Challenges in Machine Learning](#2-common-challenges-in-machine-learning)
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
[(Back to top)](#table-of-contents)

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

[(Back to top)](#table-of-contents)

## 1.3. Data and Model Tooling
- There are various Google Cloud products that provide tooling for solving data and machine learning problems. 
  - All of the products in Google Cloud are serverless, allowing us to focus more on implementing machine learning design patterns instead of the infrastructure behind them. 
- [**BigQuery**](https://cloud.google.com/bigquery) is an enterprise data warehouse designed for analyzing large datasets quickly with SQL. 
  - Data in BigQuery is organized by Datasets, and a Dataset can have multiple Tables. 
- [**BigQuery ML**](https://cloud.google.com/bigquery-ml/docs/introduction) is a tool for building models from data stored in BigQuery. 
  - With BigQuery ML, we can train, evaluate, and generate predictions on our models using SQL. 
  - It supports classification and regression models, along with unsupervised clustering models. 
  - It’s also possible to import previously trained TensorFlow models to BigQuery ML for prediction.
- [**Cloud AI Platform** (Vertex AI)](https://cloud.google.com/vertex-ai) includes a variety of products such as *AI Platform Training* and *AI Platform Prediction* for training and serving custom machine learning models on Google Cloud.
  - **AI Platform Training** provides infrastructure for training machine learning models on Google Cloud. 
  - **AI Platform Prediction** you can deploy your trained models and generate predictions on them using an API. Both services support TensorFlow, scikit-Learn, and XGBoost models, along with custom containers for models built with other frameworks. 
  - [**Explainable AI**](https://cloud.google.com/explainable-ai): a tool for interpreting the results of your model’s predictions, available for models deployed to AI Platform
 
## 1.4. Roles
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/162789242-3ada4b9d-362b-4b1f-b161-0cf979cf71c7.png" width="600" />
</p>

### 1.4.1. Data Scientist, Data Engineer and Machine Learning Engineer
- **Data scientist** is someone focused on collecting, interpreting, and processing datasets. They run statistical and exploratory analysis on data. As it relates to machine learning, a data scientist may work on data collection, feature engineering, model building, and more. Data scientists often work in Python or R in a notebook environment, and are usually the first to build out an organization’s machine learning models.
- **Data engineer** is focused on the infrastructure and workflows powering an organization’s data. They might help manage how a company ingests data, data pipelines, and how data is stored and transferred. Data engineers implement infrastructure and pipelines around data.
- **Machine learning engineer** do similar tasks to data engineers, but for ML models. They take models developed by data scientists, and manage the infrastructure and operations around training and deploying those models. ML engineers help build production systems to handle updating models, model versioning, and serving predictions to end users.

- *Note*: The smaller the data science team at a company and the more agile the team is, the more likely it is that the same person plays multiple roles. If you are in such a situation, it is very likely that you read the above three descriptions and saw yourself partially in all three categories. You might commonly start out a machine learning project as a data engineer and build data pipelines to operationalize the ingest of data. Then, you transition to the data scientist role and build the ML model(s). Finally, you put on the ML engineer hat and move the model to production. In larger organizations, machine learning projects may move through the same phases, but different teams might be involved in each phase.
### 1.4.2. Research scientists, Data analysts, and Developers
-  **Research scientists** focus primarily on finding and developing new algorithms to advance the discipline of ML. This could include a variety of subfields within machine learning, like model architectures, natural language processing, computer vision, hyperparameter tuning, model interpretability, and more. Unlike the other roles discussed here, research scientists spend most of their time prototyping and evaluating new approaches to ML, rather than building out production ML systems.
- **Data analysts** evaluate and gather insights from data, then summarize these insights for other teams within their organization. They tend to work in SQL and spreadsheets, and use business intelligence tools to create data visualizations to share their findings. Data analysts work closely with product teams to understand how their insights can help address business problems and create value. While data analysts focus on identifying trends in existing data and deriving insights from it, data scientists are concerned with using that data to generate future predictions and in automating or scaling out the generation of insights. With the increasing democratization of machine learning, data analysts can upskill themselves to become data scientists.
- **Developers** are in charge of building production systems that enable end users to access ML models. They are often involved in designing the APIs that query models and return predictions in a user-friendly format via a web or mobile application. This could involve models hosted in the cloud, or models served on-device. Developers utilize the model serving infrastructure implemented by ML Engineers to build applications and user interfaces for surfacing predictions to model users.

# 2. Common Challenges in Machine Learning


[(Back to top)](#table-of-contents)

# Resources

[(Back to top)](#table-of-contents)
