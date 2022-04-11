# Machine Learning Engineering

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Machine Learning Terminology](#1-machine-learning-terminology)
  - [1.1. Data and Feature Engineering]() 
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
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/159864817-bd10b5c0-1537-4ee9-bff9-9bb52ae792dc.png" width="400" />
</p>

[(Back to top)](#table-of-contents)

# Resources
- Tools: Bigquery, Vertex AI Pipeline, Airflow
- Coursera 
  - [Google Cloud Fundamentals: Core Infrastructure](https://www.coursera.org/learn/gcp-fundamentals)
  - [Machine Learning Engineering for Production (MLOps) Specialization](https://www.coursera.org/specializations/machine-learning-engineering-for-production-mlops)
- Qwiklab
  - [Build and Deploy Machine Learning Solutions on Vertex AI](https://www.qwiklabs.com/quests/183)
  - [MLOps with Vertex AI](https://www.qwiklabs.com/focuses/3389?parent=catalog)
- Google Cloud
  - [Google Cloud Technical Guides for Startups](https://www.youtube.com/playlist?list=PLIivdWyY5sqJOQJCXW_aYEqwfyi6bu1gC) 

[(Back to top)](#table-of-contents)
