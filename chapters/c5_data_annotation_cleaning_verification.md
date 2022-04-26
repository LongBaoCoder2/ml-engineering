# Chapter 5: Data Annotation, Cleaning and Verification
- Least Enjoyable Part of Data Science is: Cleaning & Organizing Data

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Data Annotation](#1-data-annotation)
  - [1.1. Examples of Label Design](#11-examples-of-label-design) 
  - [1.2. General principles of label design](#12-general-principles-of-label-design)  
  - [1.3. Data Annotation Tool](#13-data-annotation-tool)
  - [1.4. Data Annotation Evaluation](#14-data-annotation-evaluation)
  - [1.5. Quality control over the annotations](#15-quality-control-over-the-annotations)
- [2. Data Cleaning](#2-data-cleaning)

# 1. Data Annotation
## 1.1. Examples of Label Design
- Example 1: if we check images of *chairs* in ImageNet dataset, you may find chair images like these
  - Solution: manually design some sub-classes by asking annotation team, instead of the original "chair" labels. 
    - This helps the machine learning models work better.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/165287611-2b27b5fe-5d4a-4c41-b223-3554b9cfc5b6.png" width="600" />
</p>

- Example 2: Warehouse Fire Detection 
  - Fire in the warehouse is a very rare event & we’d like to design a CV algorithm for fire detection.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/165288394-8351c291-7dd7-4820-9981-7a904d646af8.png" width="600" />
</p>

- Example 3: Text annotation for speech synthesis
  - Without *emotion labels*, the synthesis algorithm may inject emphasis wrongly into the speech synthesis.
  - Solution:
    - Collect more data and let the model learns itself. 
    - Ask annotation team to mark if audio is strongly emotional or not.
## 1.2. General principles of label design
- General principles of label design/review
  - The sample with the **identical** labels are similar to each
  - The **semantic meaning** of the label is easy to understand 
  - The **number of samples for each label** is sufficiently large
    - If there’s a label with very few samples: Give it up!
- The process of label design:
  - Design the label structure
  - Annotate by yourself
  - Review and revise the label structure
  - Pass the instructions to annotation teams to start the real work of annotation on training and test sets.

### 1.2.1. Example of Label Design
- Context: Scooter parking audit
- The task is to recognize if the scooter is parking appropriately
- The business value
  - Educate riders on good parking
  - Reduce operational cost
- Initial version with three labels: 
  - Good parking
  - Bad parking
  - Toppled: if the scooter is toppled, the team will send the operation team to remove that. 
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/165290438-2f8cd1c9-d562-4278-b726-33ea9fd5d8e7.png" width="600" />
</p>

- After labelling 500 images, I came up with the second version
  - Invalid photo
  - Good parking
  - Bad parking
  - ~~Toppled~~
- Re-labelling 500 images, we had the third version 
  - Invalid photo
  - Good parking
  - Against the wall
  - Blocking access

## 1.3. Data Annotation Tool
- **Data sets**: objects for data annotation
- **Label sets**: labels/dictionary for annotation
- **Instructions**: connection between dataset and label sets examples on how to do the annotation
<p align="center">
<img width="600" alt="Screenshot 2022-04-26 at 19 44 58" src="https://user-images.githubusercontent.com/64508435/165292909-e88bac03-69ff-4d21-bf6e-2ba3ab00d487.png"></p>

- Step 1: Create a data set
  - Dump the objects for annotation into a bucket
  - Build a CSV file (resp. json file) containing links to the objects on Google Cloud (resp. AWS)
<p align="center">
<img width="300" alt="Screenshot 2022-04-26 at 19 44 58" src="https://user-images.githubusercontent.com/64508435/165293087-d880a2db-aecf-4701-82ab-d3b5173917f2.png"></p>
                                                                                                                               
- Step 2: Config the data set: image, audio
- Step 3: Create a labelling task
- Step 4: Manage the team 
  - Inivte annotator into the team   
  - Annotation team management is a big challenge 
    - `Quality`: The accuracy of the labels decide the accuracy of the model
    - `Efficiency`: The annotation speed decides how much training is available after a period of time                                                                                                            
 ## 1.4. Data Annotation Evaluation
- **Consistency Rate**: Percentage of identical labels from at least two annotators
  - Consistency rate drops when the same annotators run on the same job for a few weeks
- For training data, we will use the data that being labeled and agreed by at least 2 annotators.
<p align="center">
<img width="800" alt="Screenshot 2022-04-26 at 19 44 58" src="https://user-images.githubusercontent.com/64508435/165294384-49fa995a-c364-4aee-93a3-bcb496f35fc6.png"></p>

- The problem of **concept understanding drift**
  - New annotators are not familiar with the rules
  - After a weekend, annotators forget the rules
  - The distribution of the data affects the priori (prior knowledge) of the annotators.
    - For example: the training samples come from batches everyday, and there will be a different between the weekday, weekend and public holidays.
 
## 1.5. Quality control over the annotations
- Write your instructions in a better way
  - Clear descriptions and samples over all possible cases
  - You need to go through them by yourself
  - Don’t expect your annotators help you find the corner/boundary cases
- Methods for **daily quality control**
  - Sample and check the labels every day by yourself (**Consistency Rate**)
  - Run an exam for your annotators every day before they start their daily work

# 2. Data Cleaning


[(Back to top)](#table-of-contents)
