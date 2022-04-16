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
  - [2.2. Training operationalization](#22-training-operationalization)
  - [2.3. Continuous training](#23-continuous-training)
  - [2.4. Model Deployment](#24-model-deployment)
  - [2.5. Prediction serving](#25-prediction-serving)
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
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163666296-0aa65ff8-35f4-42dc-8c48-86138c7bc6b0.png" width="800" />
  <br>The ML development process
</p>

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

## 2.2. Training operationalization
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163669216-5b4f86e6-5866-4de6-bc2e-23091c3675b7.png" width="800" />
  <br>The training operationalization process
</p>

- **Training operationalization** is the process of building and testing a repeatable ML training pipeline and then deploying it to a target execution environment. 
  - For MLOps, ML engineers should be able to use *configurations to deploy the ML pipelines*. 
- **The configurations**: specify variables like the target deployment environment (development, test, staging, and so on), the data sources to access during execution in each environment, and the service account to use for running compute workloads. 
- A *pipeline* typically goes through a *series of testing and staging environments* before it is released to production. 
  - The number of testing and staging environments varies depending on standards that are established in a given organization. 
  - Most organizations have at least one testing environment before production; some have more.
- The above diagram shows a **standard CI/CD workflow**, which consists of
these stages:
  - In the CI stage, the source code is unit-tested, and the training pipeline is built and integration-tested. Any artifacts that are created by the build are stored in an artifact repository.
  - In the CD stage, the tested training pipeline artifacts are deployed to a target environment, where the pipeline goes through end-to-end testing before being released to the production environment. Typically, pipelines are tested in non-production environments on a subset of production data, while the full-scale training is performed only in production environments.
  - The newly deployed training pipeline is smoke-tested. If the new pipeline fails to produce a deployable model, the model serving system can fall back to the model that was produced by the current training pipeline.

## 2.3. Continuous training
- The continuous training process is about orchestrating and automating the execution of training pipelines.
- How frequently you retrain your model depends on your use case and on the business value and cost of doing so.
  - For example: if you run a shopping site that has a recommendation system, user behavior changes continually, and retraining frequently on new data captures new trends and patterns. This investment in retraining can lead to higher click-through rates and therefore potential additional purchases.
- Each run of the **pipeline can be triggered** in several ways, including the following:
  - Scheduled runs based on jobs that you configure.
  - Event-driven runs, such as when new data becomes available above a certain threshold, or when model decay is detected by the continuous monitoring process.
  - Ad hoc runs based on manual invocation.
- Typical **ML training pipelines** have workflows that include to the following:
1. **Data ingestion**: Training data is extracted from the source dataset and feature repository using filtering criteria such as the date and time of the most recent update.
2. **Data validation**: The extracted training data is validated to make sure that the model is not trained using skewed or corrupted data.
3. **Data transformation**: The data is split, typically into training, evaluation, and testing splits. The data is then transformed, and the features are engineered as expected by the model.
4. **Model training and tuning**: The ML model is trained and the hyperparameters are tuned using the training and evaluation data splits to produce the best possible model.
5. **Model evaluation** The model is evaluated against the test data split to assess the performance of the model using various evaluation metrics on different partitions of the data.
6. **Model validation**: The results of model evaluations are validated to make sure that the model meets the expected performance criteria.
7. **Model registration**: The validated model is stored in a model registry along with its metadata.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163670475-c9e9f3be-eb7e-40f7-8966-c8011b96abf8.png" width="800" />
  <br>The continuous training process
</p>

- As the diagram shows, the continuous training pipeline runs based on a **retraining trigger**. When the pipeline starts, it extracts a fresh training dataset from the `dataset and feature repository`, executes the steps in the `ML workflow`, and submits a trained model to the `model registry`. All the run information and the artifacts that are produced throughout the pipeline run are tracked in the `metadata and artifact repository`.
- An orchestrated and **automated** `training pipeline` mirrors the steps of the typical data science process that runs in the **ML development** phase. 
  - However, *the automated pipeline has some differences*. 
  - In an automated pipeline, **data validation and model validation** play a critical role in a way that they don’t during experimentation; these steps are gatekeepers for the overall ML training process. Runs of an automated pipeline are unattended. Therefore, as the runs are executed, the training and evaluation data can evolve to a point where the data processing and training procedures that are implemented by the pipeline are no longer optimal, and possibly are no longer valid.
    - The **data validation step** can detect when data anomalies start occuring. These anomalies can include new features, new feature domains, features that have disappeared, and drastic changes in feature distributions. The data validation step works by comparing the new training data to the expected data schema and reference statistics. For details about how data validation works, see [Analyzing and validating data at scale for machine learning with TensorFlow Data Validation](https://cloud.google.com/architecture/analyzing-and-validating-data-at-scale-for-ml-using-tfx). 
    - The **model validation phase** detects anomalies when a lack of improvement or even a degradation in performance of new model candidates is
observed. The pipeline can apply complex validation logic in this step, including several evaluation metrics, sensitivity analysis based on specific inputs, calibration, and fairness indicators.
- **An important aspect of continuous training**, therefore, is **tracking**. Pipeline runs must track generated metadata and artifacts in a way that enables debugging, reproducibility, and lineage analysis. 
  - `Lineage` analysis means being able to track a trained model back to the dataset (snapshot) that was used to train that model, and to link all the intermediate artifacts and metadata. Lineage analysis supports the following:
    - Retrieve the hyperparameters that are used during training.
    - Retrieve all evaluations that are performed by the pipeline.
    - Retrieve processed data snapshots after transformation steps, if feasible.
    - Retrieve data summaries such as descriptive statistics, schemas, and feature distributions

## 2.4. Model Deployment
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163670734-a2b8b69c-fdc2-4d1f-a27f-653d6f88091b.png" width="800" />
  <br>A complex CI/CD system for the model deployment process
</p>
- In the CI stage of model deployment, tests might include testing your model interface to see if it accepts the expected input format and if it produces the expected output. You might also validate the compatibility of the model with the target infrastructure, such as checking for required packages and accelerators. During this stage, you might also check that the model’s latency is acceptable.
- In the CD stage of model deployment, the model undergoes progressive delivery. Canary deployments, blue-green deployments, and shadow deployments are often used to perform smoke testing, which usually focuses on model service efficiency like latency and throughput, as well as on service errors. After you verify that the model works technically, you test the model’s effectiveness in production by gradually serving it alongside the existing model and running online experiments, which refers to testing new functionality in production with live traffic.
- In the **progressive delivery approach**, a new model candidate does not immediately replace the previous version. 
  - Instead, after the new model is deployed to production, it runs in parallel to the previous version. A subset of users is redirected to the new model in stages, according to the online experiment in place. The outcome of the experiments is the final criterion that decides whether the model can be fully released and can replace the previous version. 
  - [A/B testing](https://en.wikipedia.org/wiki/A/B_testing) and [multi-armed bandit (MAB)](https://en.wikipedia.org/wiki/Multi-armed_bandit) testing are common online experimentation techniques that you can use to quantify
the impact of the new model on application-level objectives. 
  - Canary and shadow deployment methods can facilitate such online experiments.

## 2.5. Prediction serving
- In the **prediction serving process**, after the model is deployed to its target environment, the model service starts to accept prediction requests (serving data) and to serve responses with predictions.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163670884-310b704d-2c20-4000-8bae-39d40faabf0e.png" width="600" />
  <br> Elements of the prediction serving process
</p>

- The serving engine can serve predictions to consumers in the following forms:
  - **Online inference** in near real time for high-frequency singleton
requests (or mini batches of requests), using interfaces like REST or gRPC.
  - **Streaming inference** in near real time, such as through an event-processing pipeline.
  - **Offline batch inference** for bulk data scoring, usually integrated with extract, transform, load (ETL) processes.
  - **Embedded inference** as part of embedded systems or edge devices.
- The inference logs and other serving metrics are stored for continuous monitoring and analysis.

# Resources
- [Practitioners guide to MLOps: A framework for continuous delivery and automation of machine learning](https://services.google.com/fh/files/misc/practitioners_guide_to_mlops_whitepaper.pdf)
[(Back to top)](#table-of-contents)

