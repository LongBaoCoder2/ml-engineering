# Chapter 1: Machine Learning Design Patterns
Design patterns are a way to codify the knowledge and experience of experts into advice that all practitioners can follow, which captures best practices and solutions to commonly occurring problems in designing, building, and deploying machine learning systems. 


# Table of contents
- [Table of contents](#table-of-contents)
- [1. Machine Learning Terminology](#1-machine-learning-terminology)
  - [1.1. Data and Feature Engineering](#11-data-and-feature-engineering) 
  - [1.2. Machine Learning Lifecycle](#12-machine-learning-lifecycle)
  - [1.3. Data and Model Tooling](#13-data-and-model-tooling)
  - [1.4. Roles](#14-roles)
- [2. Common Challenges in Machine Learning](#2-common-challenges-in-machine-learning)
  - [2.1. Data Quality](#21-data-quality) 
  - [2.2. ML Experiment Tracking](#22-ml-experiment-tracking)
  - [2.3. Data Drift](#23-data-drift)
  - [2.4. Reproducibility](#24-reproducibility)
  - [2.5. Scale](#24-scale)
  - [2.6. Multiple Objectives](#26-multiple-objectives)
  - [2.7. Software Engineering Concerns](#27-software-engineering-concerns)
- [3. Machine Learning System](#3-machine-learning-system)
  - [3.1. Production ML System](#31-production-ml-system)
    - [3.1.1. Requirements for Production ML System](#311-requirements-for-production-ml-system)  
  - [3.2. ML Pipeline and ML Steps](#32-ml-pipeline-and-ml-steps)
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

## 1.2. Machine Learning Lifecycle
A typical machine learning workflow/lifecycle includes:
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
### Summary ML Life Cycle
- **ML Life Cycle:** Build ML systm is an iterative process
  - Developing an ML system is an iterative and, in most cases, never ending process
  - The speed of going through an iteration of ML lifecycle determines the speed of realizing the value of ML
  - ML system should support developer with process and tools for fast experiment and iteration
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163008848-9a650509-e4be-4248-8630-761399c3b8a9.png" width="600" />
</p>

- Example of R&D ML Workflow (**NOT SCALABLE**):
  - Manual Process: Data Preparation, Model Training, and Model Evaluation to Trained Model, which is saved in Binary format like `pickle`
  - There is a cut-off between Data Science & IT world
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163084820-7a48f77e-6dd1-4ca2-a809-2c605f1e8681.png" width="600" />
</p>

- **ML Pipelines**: multistep solutions for performing feature engineering, training, evaluation, and predictions to handle streaming data

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

[(Back to top)](#table-of-contents)

# 2. Common Challenges in Machine Learning
## 2.1. Data Quality
- Machine learning models are only as reliable as the data used to train them. 
  - If you train a machine learning model on an incomplete dataset, on data with poorly selected features, or on data that doesn’t accurately represent the population using the model, your model’s predictions will be a direct reflection of that data.
  - As a result, machine learning models are often referred to as **"garbage in, garbage out."**
- **Data accuracy** refers to both your training data’s features and the ground truth labels corresponding with those features
  - It’s important to do a thorough analysis to screen for 
    - Typos
    - Duplicate entries
      - Duplicates in your training dataset, for example, can cause your model to incorrectly assign more weight to these data points. 
    - Measurement inconsistencies in tabular data
    - Missing features
    - Other errors that may affect data quality. 
    - Accurate data labels are just as important as feature accuracy. 
- **Data completeness**: ensuring your training data contains a varied representation of each label. 
  - For example: you are building a model to predict the price of real estate in a specific city but only include training examples of houses larger than 2,000 square feet, your resulting model will perform poorly on smaller houses.
- **Data consistency**: for large datasets, it’s common to divide the work of data collection and labeling among a group of people. 
  - Developing a set of standards for this process can help ensure consistency across your dataset, since each person involved in this will inevitably bring their own biases to the process. 

## 2.2. ML Experiment Tracking
- Performing ongoing experimentation of new data sources, ML algorithms, hyperparameters, and then tracking these experiments.
- [Reference](https://neptune.ai/blog/ml-experiment-tracking)
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163127304-0fe5881c-f8b0-4006-a7ad-ffad85b4bd46.png" width="600" />
</p>

## 2.3. Data Drift
### 2.3.1. Data Drift Definition
- While machine learning models typically represent a static relationship between inputs and outputs, data can change significantly over time. 
- **Data drift** (a.k.a `Training-Serving skew`) refers to the challenge of ensuring your machine learning models stay relevant, and that model predictions are an accurate reflection of the environment in which they’re being used.
  - *Example 1*: let’s say you’re training a model to classify news article headlines into categories like “politics,” “business,” and “technology.” If you train and evaluate your model on historical news articles from the 20th century, it likely won’t perform as well on current data. Today, we know that an article with the word “smartphone” in the headline is probably about technology. However, a model trained on historical data would have no knowledge of this word. 
  - *Example 2*: an invoice classification model is trained on a limited set of crowdsourced images. It does well on the test set. But once put in production, it is surprised by the diversity of how people fill in the invoice data. Or the low quality of scanned images compared to model training.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163122854-385c54c7-7e7d-4184-843c-e228c8fed9ed.png" width="600" />
</p>

### 2.3.2. Solution for Data Drift
- ML system should be able to detect the **data drift** (`training-serving skew`) and alert as soon as possible
- To solve for drift, it’s important to continually update your training dataset, retrain your model on the fresh data, and modify the weight your model assigns to particular groups of input data.
  - Exploratory Data Analysis (EDA) can help identify this type of drift and can inform the correct window of data to use for training. 

## 2.4. Reproducibility
- Machine learning models have an inherent element of randomness. 
  - When training, ML model weights are initialized with random values. 
  - These weights then converge during training as the model iterates and learns from the data. Because of this, the same model code given the same training data will produce slightly different results across training runs. 
- In order to address this problem of repeatability, it’s common to set the random seed value used by your model to ensure that the same randomness will be applied each time you run training
  - In TensorFlow, you can do this by running `tf.random.set_seed(value)` at the beginning of your program
- Reproducibility can refer to a model’s training environment. Often, due to large datasets and complexity, many models take a significant amount of time to train. 
  - This can be accelerated by employing distribution strategies like data or model parallelism (see [Chapter 5](#link)). 
  - With this acceleration, however, comes an added challenge of repeatability when you rerun code that makes use of distributed training.


## 2.5. Scale
- The challenge of scaling is present throughout many stages of a typical machine learning workflow: data collection and preprocessing, training, and serving.
- For model training, ML engineers are responsible for determining the necessary infrastructure for a specific training job. Depending on the type and size of the dataset, model training can be time consuming and computationally expensive, requiring infrastructure (like GPUs) designed specifically for ML workloads.

## 2.6. Multiple Objectives
- There is often a single team responsible for building a machine learning model and many teams across an organization will make use of the model in some way. 
  - For example: you’re building a model to identify defective products from images. As a data scientist, your goal may be to minimize your model’s cross-entropy loss. The product manager, on the other hand, may want to reduce the number of defective products that are misclassified and sent to customers. Finally, the executive team’s goal might be to increase revenue by 30%. Each of these goals vary in what they are optimizing for, and balancing these differing needs within an organization can present a challenge.

## 2.7. Software Engineering Concerns
- Realtime or Batch
- Compute resources (CPU/GPU/Memory)
- Latency, throughput (QPS)
- Logging
- Monitoring
- Compliance
- Security and privacy

# 3. Machine Learning System
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163128341-3ae2a6cf-cc93-47b6-b418-7ea7ec8bcd8f.png" width="600" />
</p>

## 3.1. Production ML System
### 3.1.1. Requirements for Production ML System
#### Reliability
- **"Correctness"** might be difficult for ML systems. ML system can run, but the model performs bad or gives wrong predictions.
- **Data Validation**: a very import in ML pipeline 
  - Data comes in must be in the same distribution with the previous data 
- **Model Validation**: to ensure good models before deployment
- **Model Monitoring**

#### Scalability
- There are multiple ways that an ML system can grow
  - **Model Complexity**: a single LR v.s. 100M-parameter neural network
  - **Traffic Volume**: 1000 prediction/day v.s. 1M prediction/day
  - **Model Counts**: 1 model v.s. 1000 models (ensembles of thousand models)
- Autoscaling: automatically scaling up and down the number of machines depending on usage
  - This is an indispensable feature in many cloud services
- Handling growth isn’t just resource scaling, but also **artifact/metadata** management

#### Maintainability
- ML-enabled system is a complex undertaking that combines data engineering, ML engineering, and application engineering tasks
- Many people who will work on an ML system: ML engineers, DevOps engineers, Data analyst, Data scientist
- Different contributors should be able to work together

#### Adaptability
- Machine learning problem is dynamic or constantly changing (Behavior of ML system is defined by Data vs Behavior of IT legacy system is defined by Code)
  - Business requirements
  - External environment
- Data distributions may shift accordingly
- Because ML systems are part code, part data, and data can change quickly, ML systems need to be able to evolve quickly.

#### Iterative Process
- Developing an ML system is an iterative and, in most cases, never ending process
- The speed of going through an iteration of ML lifecycle determines the speed of realizing the value of ML
- ML system should support developer with process and tools for fast experiment and iteration
- Continuous training, continuous integration and continuous deployment

## 3.2. ML Pipeline and ML Steps
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163131008-8e660cef-d4be-487b-bad6-ac1f4d776070.png" width="600" />
</p>

- Automation of the model life cycle steps
- Prevention of bugs
- Useful paper trail
- Standardization
- Free up development time for data scientists
# Resources

[(Back to top)](#table-of-contents)
