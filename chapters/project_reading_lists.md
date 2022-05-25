- [How to implement CI/CD for your Vertex AI Machine Learning Pipeline](https://medium.com/google-cloud/how-to-implement-ci-cd-for-your-vertex-ai-pipeline-27963bead8bd)
- [Deploy an end-to-end Tensorflow Pipeline on Kubeflow](https://blog.searce.com/deploy-an-end-to-end-tensorflow-pipeline-on-kubeflow-688f769a4698)


### Tensorflow Extended (TFX)
- TFX is an end to end platform for deploying production ML pipelines. It provides a configuration framework and shared libraries to integrate common components needed to define, launch and monitor an ML system.
- It becomes easy to preprocess the data using the functionalities of TFX components and TFX libraries:
  - `Tensorflow Data Validation(TFDV)` automatically identifies anomalies, such as missing features, out-of-range values, or wrong feature types so that one doesn’t have to manually look for anomalies and make changes which make the task time efficient.
  - `Tensorflow Model Analysis (TFMA)` allows users to evaluate their models on large amounts of data in a distributed manner.
  - Also, Once the pipeline is ready, It is easy to deploy the model on any serving architecture using the ‘Pusher’ component.

### Kubeflow 
- Kubeflow is an open-source Kubernetes-native platform for developing, orchestrating, deploying, and running scalable and portable machine learning workloads.

![image](https://user-images.githubusercontent.com/64508435/170211933-0aed5280-c677-41e2-9139-86b44fc13492.png)
