## vertex AI - Workbench - Notebook
- Go to vertex AI > Workbench > New Notebook > Tensorflow Enterprise > Tensorflow Enterprise 2.8 (LTS) without GPU (to save cost)
![image](https://user-images.githubusercontent.com/64508435/170166496-daecb52f-12be-41a9-aa52-e87e0c55605a.png)

## Cloud Storage: Bucket
- Create the bucket S3 for the cloud storage
  - Note: The bucket must be in the same region as the notebook
![image](https://user-images.githubusercontent.com/64508435/170169284-b461fe25-e688-450d-ab98-48cc94118c71.png)

![image](https://user-images.githubusercontent.com/64508435/170169656-7d9abcef-17ff-477e-a1b3-e7c2bcddf07d.png)
- Save the model to S3, before we build a new instance hosting the service.
![image](https://user-images.githubusercontent.com/64508435/170169797-7d83b924-4492-4680-901c-de1a8a53050d.png)
- Model file is pushed to S3 storage
![image](https://user-images.githubusercontent.com/64508435/170169847-03b0ceaa-e2e2-4415-84d1-40789658da0e.png)
- Upload the sample_image.png to Cloud Storage as well
![image](https://user-images.githubusercontent.com/64508435/170174006-b65ded4a-0dc3-4db3-8bd1-5763d5786c64.png)

# AI Platform
- to deploy the model
![image](https://user-images.githubusercontent.com/64508435/170170655-88e11ff5-135b-42e1-b6a0-a56a5b187058.png)
- clikc Models > Create Model > choose the same region as the notebook, in this case is Us-East-1
![image](https://user-images.githubusercontent.com/64508435/170170873-65cc8911-9edd-4d70-b3d8-49a25de4fcd7.png)
- Once model is created, selected the deployment region & you will see the model is just created
![image](https://user-images.githubusercontent.com/64508435/170171130-4f2632cc-0b36-4ee2-9955-bf4620c2243b.png)
- Click on the new version of the model

![image](https://user-images.githubusercontent.com/64508435/170171243-cda1ea44-a7e7-4f0b-98c9-20236c3c06d9.png)
- Currently there is no custom container on GCP

![image](https://user-images.githubusercontent.com/64508435/170171414-a923473d-2b21-4fad-995e-80ce50130967.png)
![image](https://user-images.githubusercontent.com/64508435/170171448-594ab2ba-23bd-4c89-9f49-e388ce425919.png)
![image](https://user-images.githubusercontent.com/64508435/170171485-952de8dd-8974-4405-8ae8-b4b1edf2a465.png)

- Once model version is created > Click the model name > Test the model version via 'TEST & USE`

![image](https://user-images.githubusercontent.com/64508435/170174278-25c39a09-7fc3-42b9-ad68-ca6b4e944c93.png)
![image](https://user-images.githubusercontent.com/64508435/170174443-89eaac80-1043-47c9-9d0d-92aa3a3c0bd2.png)

