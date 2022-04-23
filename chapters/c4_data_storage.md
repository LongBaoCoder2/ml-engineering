# Data Storage
- 90% of the time spends on Data. If the company spends 50% of the time on machine learning model, the company will fail.

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Basics of Git](#1-basics-of-git)
  - [1.1. Centralized Version Control](#11-centralized-version-control) 
  - [1.2. Decentralized Cersion Control](#12-decentralized-version-control)
    - [1.2.1. Basics Git Commands](#121-basics-git-commands)
  - [1.3. Branches and Commits](#13-branches-and-commits)
    - [1.3.1. Conflicts in Version Control](#131-conflicts-in-version-control)
    - [1.3.2. Merge a Branch to the Master]()
- [2. Storage for Complex ML Data](#2-storage-for-complex-ml-data)
- [Resources](#resources)


# 1. Basics of Git
## 1.1. Centralized Version Control
- **Limitations of Centralized Version Control**:
  - If the main server goes down, developers can’t save versioned changes
  - Remote commits are slow
  - Unsolicited changes might ruin development
  - If the central database is corrupted, the entire history could be lost (security issues)
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163991997-a63f4f8a-0f39-4b0f-8fab-ff6f2dd5623d.png" width="350" />
</p>

- **Solution**: Decentralized version control
[(Back to top)](#table-of-contents)

## 1.2. Decentralized Version Control
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

[(Back to top)](#table-of-contents)

### 1.2.1. Basics Git Commands
- `git init`: create a local repo
- `git remote add origin <link_to_remote_server>`: to link the local repo to the remote repo
- `git add <name_of_file>`:  to add a file/files to the stage
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164873696-03b0923b-4f05-488d-9453-899b37647901.png" width="650" />
</p>

- `git commit -m "message"`: to push the commit to the local repo
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164873754-9219d7eb-e292-485b-80d6-f2563d7eb9f8.png" width="450" />
</p>

- `git push -u origin master`: to push the updated files from local repo to remote repo
  - `-u`: to set the upstream as `origin master` 
- `git pull origin <branch_name>`: to pull the latest update from the current branch in the remote server.

[(Back to top)](#table-of-contents)

## 1.3. Branches and Commits
### 1.3.1. Conflicts in Version Control
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163992391-c1c7f0be-8349-4f29-a8a5-6c4a48abac40.png" width="450" />
</p>

### 1.3.2. Merge a branch to the master
- When merging the branch to the master, we need to run a lot of tests. This is very costly.
- **Best Practise**: Try to minimize number of branches, and try to merge the branches to the master as soon as possible.
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164874589-8d5f5ee8-0fd4-4bfb-aba9-edcc1bea64f8.png" width="450" />
</p>

## 1.4. Pull Request
- Pull Request: alert to the owner someone wants a change
<p align="center">
  <img width="450" alt="Screenshot 2022-04-23 at 11 57 58" src="https://user-images.githubusercontent.com/64508435/164874357-0e3e6dd7-97b7-4a00-9271-71b318bbfaf4.png">
  <img src="https://user-images.githubusercontent.com/64508435/163994210-70f8cf62-2190-440b-bf34-66533c448cdf.png" width="550" />
</p>

## 1.5. Fork a repo in GitHub
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
  - Insert a document without an ID 
<img width="1052" alt="Screenshot 2022-04-19 at 20 45 36" src="https://user-images.githubusercontent.com/64508435/164007166-4e681580-b860-49e6-912c-d1e7e0489bc0.png">

  - Insert a document with an ID
<img width="787" alt="Screenshot 2022-04-19 at 20 48 02" src="https://user-images.githubusercontent.com/64508435/164007533-2f332ad8-a0a8-4edb-9f5e-89dbd252f344.png">
  
  - Retrieve a document based on ID
<img width="787" alt="Screenshot 2022-04-19 at 20 51 29" src="https://user-images.githubusercontent.com/64508435/164008122-9b311e61-e45d-4be7-a544-39fbaf4eaff9.png">

- Simple search operations: Simple Lucene-style search
- <img width="679" alt="Screenshot 2022-04-19 at 20 52 35" src="https://user-images.githubusercontent.com/64508435/164008338-81a8550b-b0c7-4e92-99a2-22ad1f364844.png">
<img width="476" alt="Screenshot 2022-04-19 at 20 55 10" src="https://user-images.githubusercontent.com/64508435/164008775-95009fdd-79f7-4895-bdb8-58d6729f023b.png">
#### Domain-Specific Language (DSL)
-  Query in a tree structure
-  The first part query context is involved in the score function
- The second part filter context includes filtering conditions
- "must" condition: must have 
- "filter" condition: add some scores, if a good match, the score will be high.
- Boolean query combines 
  - Must query
  - Filter query
  - Should query
  - Must_not query

<img width="385" alt="Screenshot 2022-04-19 at 20 57 35" src="https://user-images.githubusercontent.com/64508435/164009180-26a5bf97-e383-4481-9491-7fa3ea8e63a1.png">

- Boosting query combines 
  - Positive query
  - Negative query
#### what makes ElasticSearch different

<img width="734" alt="Screenshot 2022-04-19 at 21 00 14" src="https://user-images.githubusercontent.com/64508435/164009708-a6f6ec9a-5b16-4b97-a5dd-0a8bb0c75744.png">
- Chracter Filter in Analyzer: Elastic Search can ignore the 

<img width="548" alt="Screenshot 2022-04-19 at 21 01 18" src="https://user-images.githubusercontent.com/64508435/164009906-aae86f34-701e-4808-bb43-ff4e7a705a86.png">

- Tokenizer in Analyzer
  - Break sentence into tokens
  - Every analyzer has exactly one tokenizer
  - Stem

  - Transformation over the tokens 
    - Convert to lower-case
    - Stemming
    - Synonyms

- html_strip: a character filter to remove any HTML character texts.
<img width="977" alt="Screenshot 2022-04-19 at 21 02 51" src="https://user-images.githubusercontent.com/64508435/164010157-99bfed91-d77b-4c41-aaf1-e5bded61ae90.png">


- When Elastic Search? And When MongoDB?
- Use Elastic Search: search over the documents, log analysis from IoT system.
  - An internal search engine over massive documents
  - Advanced text search involving complex text pre-processing
- Use MongoDB: dump all the data
  - A general-purpose database for all sorts of data
  - An engine with data retrieval based data id or batches 
  - **High performance** as *object* store in compare with Elastic Search. 

# Resources




[(Back to top)](#table-of-contents)
