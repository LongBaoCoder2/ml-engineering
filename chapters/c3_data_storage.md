# Data Storage
- 90% of the time spends on Data. If the company spends 50% of the time on machine learning model, the company will fail.

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Basics of Git](#1-basics-of-git)
- [2. Storage for Complex ML Data](#2-storage-for-complex-ml-data)
- [Resources](#resources)


# 1. Basics of Git
## 1.1. Centralized version control
- Limitations:
  - If the main server goes down, developers can’t save versioned changes
  - Remote commits are slow
  - Unsolicited changes might ruin development
  - If the central database is corrupted, the entire history could be lost (security issues)
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163991997-a63f4f8a-0f39-4b0f-8fab-ff6f2dd5623d.png" width="350" />
</p>


## 1.2. Decentralized version control
- Local repos host all versions
  - `pull`: get the updates from central server
  - `push`: send the updated repos to the central server
- Advantage:
  - Full history is always available
  - No need to access a remote server (faster access)
  - Abibility to push your changes continously 
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163991479-16f40c48-1d3d-4383-9253-51dec9b2e10f.png" width="350" />
</p>

## 1.3. Branches and commits
### 1.3.1. Conflicts in Version Control
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163992391-c1c7f0be-8349-4f29-a8a5-6c4a48abac40.png" width="450" />
</p>

- `git remote add origin <link_to_remote_server>`: to link the local repo to the remote repo
- `git init`: create a local repo
- `git add <name_of_file>`: 
- `git commit -m "message"`: to push the commit to the local repo
- `git push -u origin master`: to push the updated files from local repo to remote repo
  - `-u`: to set the upstream as `origin master` 
- `git pull origin <branch_name>`: to pull the latest update from the current branch in the remote server.

### 1.3.2. Merge a branch to the master
- When merging the branch to the master, we need to run a lot of tests. This is very costly.
- Best Practise: Try to minimize number of branches, and try to merge the branches to the master as soon as possible.

## 1.4. Pull Request
- Pull RequestL: alert to the owner someone wants a change
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163994210-70f8cf62-2190-440b-bf34-66533c448cdf.png" width="550" />
</p>

## 1.5. Fork 
- Once you fork a repo
  - A new repo appears in your account
  - You have complete control over it
  - You can clone the project for local edits
  - Raise a pull request to merge into original repo

<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163994488-b02a1d08-1436-4ba8-b7e1-1f4bc79eb49b.png" width="350" />
</p>

# 2. Storage for Complex ML Data
## 2.1. Why Storage matters to ML
- *Data Type* complex and high diversified
  - Different data types (images, video, audio, text)
  - Label complexity: not only 1, 2, 3 but like bounding boxes
- *High Performance* requirement:
  - Need to pack data in a efficient way 
  - Select & de-select data, based on the training results

- Nature of Data: 
  - Semi-structured objects
  - Key-value objects (Redis)
  - Object store (Amazon S3). 
  - Document Store (Mongo DB): formal text like medical report
  - Elastic Search: text logs from the systems

## 2.2. Amazon S3 - Simple Storage Service
- It’s originally proposed by AWS, but not almost every cloud provides a copycat
- Simple Idea: every **object** (binary string) is indexed with 2 strings
  - A bucket name
  - A key name 
<img width="1035" alt="Screenshot 2022-04-19 at 19 48 41" src="https://user-images.githubusercontent.com/64508435/163996879-b3013dad-2833-411e-b7d0-6e794ce0c2a6.png">
This image is stored in S3.
Hireachy: Amazon S3 > Buckets > neuron-server (bucket_name)
<img width="1035" alt="Screenshot 2022-04-19 at 19 51 31" src="https://user-images.githubusercontent.com/64508435/163997320-1d40da2f-be81-48a4-822e-cbb64a43bc4b.png">

- Access to S3 is very easy
  - `boto3`: is the python library for S3 access
  - `s3.object(bucket_name, object_name)`
- Problem: very hard to filter the object as the data is not organized. Only good for massive data storage
- Solution: MongBD: Managing a collection of documents

## 2.3. MongoDB
- `JSON format`: to organize data in the plain text, so that any machine can understand the data format
- MongoDB: to manage the collection of these `json` documents and you can query the data. 
  - In practice: MongoDB is used as the data warehouse.   
  - **No Schema**: it can accept any json format, **need to be very careful**.
  - GUI: Robo3T
- MongoDB client with Python: `pymongo`
  - Query, Aggregrateion pipeline (Group By similar to SQL), Sort 
<img width="908" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/163997774-d13ca302-257e-46b9-b253-f2ca1f7926fd.png">

- Comparison between RDBMS vs MongoDB
<img width="938" alt="Screenshot 2022-04-19 at 19 57 32" src="https://user-images.githubusercontent.com/64508435/163998225-e37a6367-aad8-428b-8d4c-3a2978b23624.png">

- Command Line Tutorial:
- EmployeeDB: name of the database
- Employee: name of the colletion
- WriteResult: one document inserted in a collection
<img width="474" alt="Screenshot 2022-04-19 at 19 58 59" src="https://user-images.githubusercontent.com/64508435/163998441-211f445c-0cfa-4436-a154-125141ce0045.png">

### 2.3.1. Storing Complex Objects
- Convert binary file into a Base64 string
  - Split the binary string into a sequence of 8-bit number
  - Convert every 8-bit number to a character according to the Base64 Encoding Table
- Reverse conversion
  - Convert a character to 8 binary bits
  - Concatenate the bits into a long binary string


<img width="413" alt="Screenshot 2022-04-19 at 20 16 20" src="https://user-images.githubusercontent.com/64508435/164001482-5bac836f-9103-4626-9fca-8f95afc056c2.png">


<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164001532-a25ac14b-d5f3-4a46-82d1-5b0b8a59495b.png" width="550" />
  <br>Base64 encoding in Python for storing an image in MongoDB
</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164001761-c531c951-65b9-4f64-9e49-1a2b450604d9.png" width="550" />
  <br>Base64 decoding in Python 
</p>

## 2.4. ElasticSearch
- ElasticSearch behaves like a search engine
  - The adoption of RESTful interface
  - Its very unique score function over **text search queries**
  - Powerful query language over text data
  - Strong consistency guarantee
- The demand of text search is more complicated
<img width="1126" alt="Screenshot 2022-04-19 at 20 43 11" src="https://user-images.githubusercontent.com/64508435/164006572-c6ac4bfd-8c35-4dd9-9cc3-5fbe13fcc82c.png">

- ElasticSearch organizes documents in a **hierarchy** and provide search functions

<img width="618" alt="Screenshot 2022-04-19 at 20 43 49" src="https://user-images.githubusercontent.com/64508435/164006882-59da250c-fd2e-4ef9-8bfc-503a2cf2d486.png">

- No need the command-line, but via Browser, you can connect to ElasticSearch database
- For example: create `hardwarezone` database on ElasticSearch
  <img width="986" alt="Screenshot 2022-04-19 at 20 44 42" src="https://user-images.githubusercontent.com/64508435/164007027-77a70c7b-9e6b-4157-9645-be57b85aad5c.png">
  
- Use RESTFUL API to insert data into the database via POST method.
  - `201`: operation is successsfully applied. 
<img width="1052" alt="Screenshot 2022-04-19 at 20 45 36" src="https://user-images.githubusercontent.com/64508435/164007166-4e681580-b860-49e6-912c-d1e7e0489bc0.png">


# Resources




[(Back to top)](#table-of-contents)
