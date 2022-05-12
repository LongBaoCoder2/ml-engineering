# Kedro

- Standarisation 
![image](https://user-images.githubusercontent.com/64508435/168012204-651d9d8d-45bc-48b4-86b8-428cb9361c82.png)
- Guided Example: Housing Price Classifier
  - There are 2 pipelines:
    - Data Processing
    - Data Science 
![image](https://user-images.githubusercontent.com/64508435/168012333-b8f44c27-58c0-4b09-857e-7fd27aff90e9.png)

![image](https://user-images.githubusercontent.com/64508435/168012581-1e1fca46-cd68-4fb8-9327-e3896255ea9a.png)

- Step 1: File Management
  - Supported Data Files 
![image](https://user-images.githubusercontent.com/64508435/168012703-9edbb770-89a1-4c61-863b-8a4a9a807e0f.png)
  - If not, you can write your own data class
![image](https://user-images.githubusercontent.com/64508435/168012826-d2876289-1ba0-4f23-a5ae-0fef00be6961.png)
  - `catalog.yml`: once data put into the folder, need to registered in `catalog` file

- Step 2: Pre-process data set: "Processing pipeline"
  - can perform unit test for the pipeline

![image](https://user-images.githubusercontent.com/64508435/168013231-9822f234-8213-4fbe-b907-605e77dc3d88.png)

- Step 3: Traing & Validate Classifier: "Data Science pipeline"
  - Can ask everyone body developement multiple models at the same time and put into the pipeline
![image](https://user-images.githubusercontent.com/64508435/168013370-0ab1b6a4-6a4e-4dbf-9892-7ab924d2d670.png)

- No need to hard-code parameter
![image](https://user-images.githubusercontent.com/64508435/168013508-cec578b4-2d01-4dac-861c-3b6ee0520ef9.png)

- Store/Register the models and error metrics
- Put the classifier node into the "data science" pipeline
  
![image](https://user-images.githubusercontent.com/64508435/168013735-bd5c0710-09a8-4152-8172-93e7e7403376.png)
- Run different pipelines via command `kedro run --pipeline=dt`
![image](https://user-images.githubusercontent.com/64508435/168013834-86e5b4a7-7fef-445f-8c69-d54908100fb0.png)

- Visualize the pipeline
![image](https://user-images.githubusercontent.com/64508435/168013966-22e27e2c-2073-4b67-a596-209a4036fa70.png)

- Step 4: Predict Prices
  - XGBoost is the best, so we create a new pipeline called inference to serve it.
![image](https://user-images.githubusercontent.com/64508435/168016159-1c924a50-ef82-4da7-a434-9b7228152e72.png)

- Step 5: Store & Register Output
- ![image](https://user-images.githubusercontent.com/64508435/168016360-c67c68a1-985f-4911-9c79-d78f02bf29ba.png)

![image](https://user-images.githubusercontent.com/64508435/168015917-8c8fd16b-28a4-4f99-a12a-c5a89947b2ad.png)

- Step 6: versioning & Monitor
  - Versioning based on timestamp
  - Also can use the inference run for versioning
![image](https://user-images.githubusercontent.com/64508435/168016499-146cdac2-1831-49ac-b8e4-c3c19a84adcb.png)
  - Can roll back by `run_id` or `model_uid`
![image](https://user-images.githubusercontent.com/64508435/168016735-eb5f4eca-c3d1-4070-be86-1189938d4e9a.png)
![image](https://user-images.githubusercontent.com/64508435/168016789-a250bd86-2e0e-4d45-920b-442820e43af0.png)

## Conclusion
![image](https://user-images.githubusercontent.com/64508435/168016893-60e8efa6-3618-475e-878b-d186fadfad41.png)
