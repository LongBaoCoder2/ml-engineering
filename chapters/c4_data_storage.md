# Data Storage
- 90% of the time spends on Data. If the company spends 50% of the time on machine learning model, the company will fail.

# Table of contents
- [Table of contents](#table-of-contents)
- [1. Storage for Complex ML Data](#1-storage-for-complex-ml-data)
  - [1.1. Why Storage matters to ML](#11-why-storage-matters-to-ml)
- [2. Object Store: originated from Amazon S3](#2-object-storage)
  - [2.1. Access S3 with Python](#21-access-s3-with-python) 
  - [2.2. Object Storage on Google Cloud](#22-object-storage-on-google-cloud)
- [3. Document Store: Mongo DB](#3-mongodb)
  - [3.1. Access MongoDB with Python](#31-access-mongodb-with-python)
  - [3.2. Comparison between RDBMS vs MongoDB](#32-comparison-between-rdbms-vs-mongodb) 
  - [3.3. Complex Object Storage in MongoDB](#33-complex-object-storage-in-mongodb)
  - [3.4. Command Line Access for MongoDB](#34-command-line-access-for-mongodb)
- [4. Document Store: ElasticSearch](#4-elasticsearch)
  - [4.1. Index Operation](#41-index-operation) 
  - [4.2. Domain-Specific Language (DSL)](#42-domain-specific-language)
  - [4.3. What makes ElasticSearch different](#43-what-makes-elasticsearch-different)
  - [4.4. When ElasticSearch ? When MongoDB ?](#44-when-to-use-elasticsearch-or-mongodb)
- [Resources](#resources)


# 1. Storage for Complex ML Data
## 1.1. Why Storage matters to ML
- *Data Type* complex and high diversified
  - Different data types (images, video, audio, text)
  - Label complexity: not only 1, 2, 3 but like bounding boxes
- *High Performance* requirement:
  - Need to pack data in a efficient way 
  - Select & de-select data, based on the training results
- *Different Nature of Data*: :rocket:
  - Semi-structured objects
  - Key-value objects (Redis)
  - Object store (Amazon S3). 
  - Document Store 
    - Mongo DB: Plain text, without fuzzy search
      - For ex: medical report
    - Elastic Search: Plain text, search index needed
      - For ex: text logs (plain text) from the systems

# 2. Object Storage
- It’s originally proposed by AWS, but not almost every cloud provides a copycat
- Simple Idea: every **object** (binary string) is indexed with 2 strings
  - A bucket name
  - A key name 
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163996879-b3013dad-2833-411e-b7d0-6e794ce0c2a6.png" width="550" />
</p>

- This `.JPG` image is stored in S3.
  - Hireachy: Amazon S3 &#8594; Buckets &#8594; neuron-server (bucket_name)

## 2.1. Access S3 with Python
<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/163997320-1d40da2f-be81-48a4-822e-cbb64a43bc4b.png" width="550" />
</p>

- Access to S3 is very easy
  - `boto3`: is the python library for S3 access
  - `s3.object(bucket_name, object_name)`
- *Problem*: very hard to filter the object as the data is not organized. Only good for massive data storage
- *Solution*: MongDB - managing a collection of documents

## 2.2. Object Storage on Google Cloud
- Create a new bucket for Object Storage
<img width="1154" alt="Screenshot 2022-04-25 at 00 55 28" src="https://user-images.githubusercontent.com/64508435/164987514-90814957-9b2d-4c72-a1df-5ec68f71b947.png">

- Choose Bucket Name which is unique.
<img width="1164" alt="Screenshot 2022-04-25 at 00 56 05" src="https://user-images.githubusercontent.com/64508435/164987534-f50b1066-e293-492c-ba06-466ccbd14e9c.png">

- Choose Location, Region 
<img width="1083" alt="Screenshot 2022-04-25 at 00 58 20" src="https://user-images.githubusercontent.com/64508435/164987617-f9009963-d13c-4df9-8ee2-5f423c386dd3.png">

- Access Control: 
  - Uniform: same permission control over every object
  - Fine-grained: define the rules who can control which objects 
<img width="1083" alt="Screenshot 2022-04-25 at 00 59 13" src="https://user-images.githubusercontent.com/64508435/164987642-b16aa0bf-1b85-4c7b-9168-5fc8aa24c132.png">

- Data Recovery:
<img width="1083" alt="Screenshot 2022-04-25 at 01 01 07" src="https://user-images.githubusercontent.com/64508435/164987728-ad54bdb9-36ee-4b52-8532-be14dc8b6e4d.png">


# 3. MongoDB
- `JSON format`: to organize data in the plain text, so that any machine can understand the data format
- **MongoDB**: to manage the collection of these `json` documents and you can query the data. 
  - In practice: MongoDB is used as the data warehouse.   
  - **No Schema**: it can accept any json format, **need to be very careful**.
  - GUI: Robo3T
<p align="center">
<img width="500" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/163997774-d13ca302-257e-46b9-b253-f2ca1f7926fd.png">
</p>

## 3.1. Access MongoDB with Python
<p align="center">
<img width="700" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/164891126-ddf5b0d0-52a3-407b-a3de-4bfd662e9e81.png">
</p>

  - Query, Aggregrateion pipeline (similar to SQL - Group By), Sort 
<p align="center">
<img width="700" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/164891197-5e515492-9507-450d-8be7-4f24b7a3aeba.png"><br>
<img width="700" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/164891245-11850898-6d09-4fdb-ac77-5a962e3ac04f.png">
</p>

## 3.2. Comparison between RDBMS vs MongoDB
<p align="center">
<img width="600" alt="Screenshot 2022-04-19 at 19 54 32" src="https://user-images.githubusercontent.com/64508435/163998225-e37a6367-aad8-428b-8d4c-3a2978b23624.png">
</p>

## 3.3. Complex Object Storage in MongoDB
- Convert binary file into a Base64 string
  - Split the binary string into a sequence of 8-bit number
  - Convert every 8-bit number to a character according to the Base64 Encoding Table
- Reverse conversion
  - Convert a character to 8 binary bits
  - Concatenate the bits into a long binary string

<p align="center">
  <img width="413" alt="Screenshot 2022-04-19 at 20 16 20" src="https://user-images.githubusercontent.com/64508435/164001482-5bac836f-9103-4626-9fca-8f95afc056c2.png">
  <img src="https://user-images.githubusercontent.com/64508435/164001532-a25ac14b-d5f3-4a46-82d1-5b0b8a59495b.png" width="550" />
  <br>Base64 encoding in Python for storing an image in MongoDB
</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/64508435/164001761-c531c951-65b9-4f64-9e49-1a2b450604d9.png" width="550" />
  <br>Base64 decoding in Python 
</p>

## 3.4. Command Line Access for MongoDB:
- Start MongoDB Service: `brew services start mongodb-community@5.0`
- Stop MongoDB Service: `brew services stop mongodb-community@5.0`
  - Further Reading: [Install MongoDB Community Edition on macOS](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/)
- Open Mongo Shell: `mongo`
<p align="center"><img width="570" alt="Screenshot 2022-04-25 at 00 39 58" src="https://user-images.githubusercontent.com/64508435/164986873-63167ba7-0572-4a08-895d-5bce90eae536.png"></p>

- `EmployeeDB`: name of the database
- `Employee`: name of the colletion
- `WriteResult`: one document inserted in a collection
<p align="center">
<img width="474" alt="Screenshot 2022-04-19 at 19 58 59" src="https://user-images.githubusercontent.com/64508435/163998441-211f445c-0cfa-4436-a154-125141ce0045.png">
</p>
  
[(Back to top)](#table-of-contents)


# 4. ElasticSearch
- ElasticSearch behaves like a search engine
  - The adoption of RESTful interface
  - Its very unique score function over **text search queries**
  - Powerful query language over text data
  - Strong consistency guarantee
- The demand of text search is more complicated
<p align="center">
<img width="500" alt="Screenshot 2022-04-19 at 20 43 11" src="https://user-images.githubusercontent.com/64508435/164006572-c6ac4bfd-8c35-4dd9-9cc3-5fbe13fcc82c.png">
</p>

- ElasticSearch organizes documents in a **hierarchy** and provide search functions
<p align="center">
<img width="450" alt="Screenshot 2022-04-19 at 20 43 49" src="https://user-images.githubusercontent.com/64508435/164006882-59da250c-fd2e-4ef9-8bfc-503a2cf2d486.png">
</p>

## 4.1. Index Operation
- No need the command-line, but via Browser, you can connect to ElasticSearch database
  - For example: create `hardwarezone` database on ElasticSearch
<p align="center">
<img width="500" alt="Screenshot 2022-04-19 at 20 44 42" src="https://user-images.githubusercontent.com/64508435/164007027-77a70c7b-9e6b-4157-9645-be57b85aad5c.png">
</p>

- **Insert & Retrieve**: Use RESTFUL API to insert data into the database via POST method.
  - `201`: operation is successsfully applied. 
<p align="center">
<img width="600" alt="Screenshot 2022-04-19 at 20 45 36" src="https://user-images.githubusercontent.com/64508435/164007166-4e681580-b860-49e6-912c-d1e7e0489bc0.png"><br>Insert a document with-out an ID<br>
<img width="600" alt="Screenshot 2022-04-19 at 20 48 02" src="https://user-images.githubusercontent.com/64508435/164007533-2f332ad8-a0a8-4edb-9f5e-89dbd252f344.png"><br>Insert & Delete a document with an ID<br>
<img width="600" alt="Screenshot 2022-04-19 at 20 51 29" src="https://user-images.githubusercontent.com/64508435/164008122-9b311e61-e45d-4be7-a544-39fbaf4eaff9.png"><br> Retrieve a document based on ID<br>
</p>

- **Search operations**: Simple Lucene-style search
<p align="center"><img width="400" alt="Screenshot 2022-04-19 at 20 52 35" src="https://user-images.githubusercontent.com/64508435/164008338-81a8550b-b0c7-4e92-99a2-22ad1f364844.png"><br>
<img width="400" alt="Screenshot 2022-04-19 at 20 55 10" src="https://user-images.githubusercontent.com/64508435/164008775-95009fdd-79f7-4895-bdb8-58d6729f023b.png">
</p>


## 4.2. Domain-Specific Language 
-  Query in a tree structure
- *First part*: **query context** is involved in the score function (`must` condition: must have)
- *Second part*: **filter context** includes filtering conditions (`filter` condition: add some scores, if a good match, the score will be high)
<p align="center"><img width="600" alt="Screenshot 2022-04-19 at 20 52 35" src="https://user-images.githubusercontent.com/64508435/164980899-b9d76849-1c33-4722-915a-bf7a56c8c281.png">
</p>

- Boolean query combines 
  - `must` query
  - `filter` query
  - `must_not` query
  - `should` query
<p align="center">
<img width="450" alt="Screenshot 2022-04-19 at 20 57 35" src="https://user-images.githubusercontent.com/64508435/164009180-26a5bf97-e383-4481-9491-7fa3ea8e63a1.png">
</p>

- Boosting query combines 
  - `positive` query
  - `negative` query
<p align="center">
<img width="450" alt="Screenshot 2022-04-19 at 20 57 35" src="https://user-images.githubusercontent.com/64508435/164981279-762ee500-3897-4ef7-9a80-023d31905491.png">
</p>

## 4.3. What makes ElasticSearch different
<p align="center">
<img width="500" alt="Screenshot 2022-04-19 at 21 00 14" src="https://user-images.githubusercontent.com/64508435/164009708-a6f6ec9a-5b16-4b97-a5dd-0a8bb0c75744.png"></p>

- **Chracter Filter in Analyzer**:
  - Replacement over character level
    - Convert Hindu-Arabic numbers to Arabic-Latin letters
    - Strip HTML elements
      - For example: `html_strip` a character filter to remove any HTML character texts.
  - Every analyzer can have zero or more character filters
<p align="center">
<img width="548" alt="Screenshot 2022-04-19 at 21 01 18" src="https://user-images.githubusercontent.com/64508435/164009906-aae86f34-701e-4808-bb43-ff4e7a705a86.png"></p>

- **Tokenizer in Analyzer**:
  - Break sentence into tokens
  - Every analyzer has exactly one `tokenizer`
  - Transformation over the tokens 
    - Convert to lower-case
    - Stemming
    - Synonyms
  - Every analyzer can have zero or more `token filters`
<p align="center">
<img width="600" alt="Screenshot 2022-04-19 at 21 02 51" src="https://user-images.githubusercontent.com/64508435/164010157-99bfed91-d77b-4c41-aaf1-e5bded61ae90.png"><br>Customize an analyzer in ElasticSearch
</p>

## 4.4. When to use ElasticSearch or MongoDB
- **Use Elastic Search**: search over the documents, log analysis from IoT system.
  - An internal search engine over massive documents
  - Advanced text search involving complex text pre-processing
- **Use MongoDB**: dump all the data
  - A general-purpose database for all sorts of data
  - An engine with data retrieval based data id or batches 
  - **High performance** as *object* store in compare with Elastic Search. 

- Example of E-scooter business using `ELK` (three open source projects: Elasticsearch, Logstash, and Kibana):
  - Multiple sources of logs 
    - Scooter IoT
    - Rider app
    - Operation team
  - Many analysis involves different logs
  - Does the operation team move the scooters timely?
  - *Solution*: ELK (three open source projects: Elasticsearch, Logstash, and Kibana) for log analysis
<p align="center">
<img width="600" alt="Screenshot 2022-04-19 at 21 02 51" src="https://user-images.githubusercontent.com/64508435/164983550-49c8aaaf-47e2-47cd-a102-ebd1c1b70a64.png">
</p> 

- Concern: hardly control the format of the logs
  - Many are developed by third-party
  - Different time/data format
- `Logstash` helps to quickly digest massive logs from multiple sources 
  - Define filters and transformation over the original logs
- `Elastic` provides the search engine over the logs 
- `Kibana` visualizes the data based on user’s query

# Resources




[(Back to top)](#table-of-contents)
