# Chapter 2: Machine Learning Ops (MLOPs)
- MLOps is a methodology for ML engineering that unifies 
  - ML system Development (ML element)
  - ML system Operations (Ops element)

# Table of contents
- [Table of contents](#table-of-contents)
- [1. MLOps Introduction](#1-mlops-introduction)
  - [1.1. Software Engineering vs Machine Learning Engineering](#11-software-engineering-vs-machine-learning-engineering) 
  - [1.2. MLOps vs DevOps](#12-mlops-vs-devops)
  - [1.3. Benefits of MLOps practices](#13-benefits-of-mlops-practices)
- [2. MLOps Lifecycle and Workflow](#2-mlops-lifecycle-and-workflow)
  - [2.0. MLOps capabilities](#20-mlops-capabilities) 
  - [2.1. ML Development](#21-ml-development) 
- [Resources](#resources)


# 1. MLOps Introduction
- MLOps provides a set of standardized processes and technology capabilities: for building, deploying, and operationalizing ML systems rapidly and reliably.
- MLOps supports ML *development* and *deployment* in the way that DevOps and DataOps support application engineering and data engineering (analytics).

## 1.1. Software Engineering vs Machine Learning Engineering
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163658747-433e2477-b8cb-4fe3-ae62-6326b5d81d65.png" width="500" />
</p>

## 1.2. MLOps vs DevOps
- DevOps: When you deploy a web service, you care about resilience, queries per second, load balancing, and so on.
- MLOps : When you deploy an ML model, you also need to worry about changes in the data, changes in the model, users trying to game the system, and so on

## 1.3. Benefits of MLOps practices
- Shorter development cycles, and as a result, shorter time to market.
- Better collaboration between teams.
- Increased reliability, performance, scalability, and security of ML systems.
- Streamlined operational and governance processes.
- Increased return on investment of ML projects.

# 2. MLOps Lifecycle and Workflow
- MLOps Lifecycle is more about *ML System* Life Cycle rather than *ML Solving Problem* Lifecycle
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163659925-3b029f87-e12d-4b4e-ae84-377638092418.png" width="600" />
  <br>MLOps Lifecyle
</p>

- **ML development**: developing a robust and reproducible model training procedure (training *pipeline* code).
- **Training operationalization**: automating the process of packaging, testing, and deploying repeatable and reliable training pipelines.
- **Continuous training**: repeatedly executing the training pipeline in response to new data or to code changes.
- **Model deployment**: packaging, testing, and deploying a model to a serving environment for online experimentation and production serving.
- **Prediction serving**: about serving the model that is deployed in production for inference.
- **Continuous monitoring**: about monitoring the effectiveness and efficiency of a deployed model.
- **Data and model management**: a central, cross-cutting function for governing ML artifacts to support *auditability*, *traceability*, and *compliance*.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163659900-05058897-8897-458d-b877-9f63508b2a43.png" width="600" />
  <br>MLOps Workflow
</p>

## 2.0. MLOps capabilities
- To effectively implement the key MLOps processes outlined in the previous section, organizations need to establish a set of core technical capabilities.
  -  IT workload, such as a reliable, scalable, and secure compute infrastructure.
  -  Standardized configuration management and CI/CD capabilities to build, test, release, and operate software systems rapidly and reliably, including ML systems.
  -  A set of core MLOps capabilities. These include experimentation, data-processing, model training, model evaluation, model serving, online experimentation, model monitoring, ML pipeline, and model registry
  -  ML metadata and artifact repository
  -  ML dataset and feature repository
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163660041-a7a2ecbc-a8c9-436b-9639-98d7536802cf.png" width="500" />
  <br>Core MLOps technical capabilities
</p>


## 2.1. ML Development
- **Experimentation** is the core activity in ML development.
  - The following questions have been answered
    - What is the task?
    - How can we measure business impact?
    - What is the evaluation metric?
    - What is the relevant data?
    - What are the training and serving requirements?
  - Experimentation aims to arrive at an effective prototype model for the ML use case
  - During experimentation, data scientists typically perform the following steps:
    - Data discovery, selection, and exploration.
    - Data preparation and feature engineering, using interactive data processing tools.
    - Model prototyping and validation.
- **Training Formalization**:  to formalize their ML training procedures by implementing an end-to-end pipeline, so that the procedures can be operationalized and run in production.
- **The primary source of development data**: the dataset and feature repository. This repository contains curated data
assets that are managed on either the entity-features level or the full dataset level.
- **The key success aspects for this process**: experiment tracking, reproducibility, and collaboration. 
  - To be able to reproduce an experiment, your data science team needs to track configurations for each experiment, including the following:
    - A pointer to the version of the training code in the version control system.
    - The model architecture and pretrained modules that were used.
    - Hyperparameters, including trials of automated hyperparameter tuning and model selection.
    - Information about training, validation, and testing data splits that were used.
    - Model evaluation metrics and the validation procedure that was used.
- **The output of ML development process**: the *implementation of the continuous training pipeline* (not the model to be deployed in
production) to be deployed to the target environment. 
- **Typical assets produced in ML development process** include the following:
  - Notebooks for experimentation and visualization
  - Metadata and artifacts of the experiments
  - Data schemas
  - Query scripts for the training data
  - Source code and configurations for data validation and transformation
  - Source code and configurations for creating, training, and evaluating models
  - Source code and configurations for the training-pipeline workflow
  - Source code for unit tests and integration tests
# Resources
- [Practitioners guide to MLOps: A framework for continuous delivery and automation of machine learning](https://services.google.com/fh/files/misc/practitioners_guide_to_mlops_whitepaper.pdf)
[(Back to top)](#table-of-contents)

