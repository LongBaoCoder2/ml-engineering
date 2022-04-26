# Chapter 5: Data Annotation, Cleaning and Verification
- Least Enjoyable Part of Data Science is: Cleaning & Organizing Data

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Data Annotation](#1-data-anotation)
  - [1.1. Examples of Label Design](#11-examples-of-label-design) 
  - [1.2. General principles of label design](#12-general-principles-of-label-design)  

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
 
[(Back to top)](#table-of-contents)
