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
  <img src="https://user-images.githubusercontent.com/64508435/163659032-f37a8ede-220b-4d20-a368-0d8fec3e4dae.png" width="600" />
</p>

- **ML development**: developing a robust and reproducible model training procedure (training *pipeline* code).
- **Training operationalization**: automating the process of packaging, testing, and deploying repeatable and reliable training pipelines.
- **Continuous training**: repeatedly executing the training pipeline in response to new data or to code changes.
- **Model deployment**: packaging, testing, and deploying a model to a serving environment for online experimentation and production serving.
- **Prediction serving**: about serving the model that is deployed in production for inference.
- **Continuous monitoring**: about monitoring the effectiveness and efficiency of a deployed model.
- **Data and model management**: a central, cross-cutting function for governing ML artifacts to support *auditability*, *traceability*, and *compliance*.

# Resources

[(Back to top)](#table-of-contents)

