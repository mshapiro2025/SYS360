# AWS Database Services

## Lecture Notes: AWS Database Services

### Cloud Databases

* advantages of cloud databases:
  * fully managed
    * services relieve many of the setup, management, and monitoring responsibilities off of the business's shoulders
  * scalable
    * databases that can be highly scalable when compared to on-premise systems
  * highly available
    * global infrastructure setup and fault tolerance mechanisms
  * security
    * implementation of multi-level security systems like network isolation and end-to-end encryption

### Amazon Relational Database Services (RDS)

* managed relational database service with a choice of six popular database engines
  * Amazon Aurora
  * MySQL
  * PostgreSQL
  * MariaDB
  * Microsoft SQL Server
  * Oracle
* easy to administer
  * no need for infrastructure provisioning, installing, and maintaining DB software
* available and durable
  * automatic Multi-AZ data replication; automated backup, snapshots, failover
* highly scalable
  * scale database compute and store with a few clicks with no app downtime
* fast and secure
  * SSD storage and guaranteed provisioned I/O; data encryption at rest and in transit

### Amazon Aurora

* MySQL and PostgreSQL-compatible relational database built for the cloud
* Amazon's own optimized database engine that works in EC2
  * why it works much faster and has better availability
* performance and availability of commercial-grade databases at 1/10th the cost
* performance and scalability
  * 5x throughput of standard MySQL and 3x of standard PostgreSQL; scale-out to 15 read replicas
* availability and durability
  * fault-tolerant, self-healing storage; six copies of data across three availability zones; continuous backup to Amazon S3
* highly secure
  * network isolation, encryption at rest and in transit
* fully managed
  * managed by RDS; no hardware provisioning, software patching, setup, configuration, or backups
* new features:
  * Amazon Global Database
    * designed for globally distributed applications, allowing a single database to span multiple AWS regions
  * Aurora Serverless
    * on-demand, auto-scaling configuration; the database automatically starts up, shuts down, and scales capacity up or down on your application's needs
  * Aurora Parallel Query
    * faster analytical queries over your current data
    * can speed up queries by up to 2 orders of magnitude, while maintaining high throughput for your core transactional workload

### Aurora vs. RDS

* Aurora is a proprietary database engine developed by AWS and is compatible with MySQL and PostgreSQL
* performance:
  * RDS offers good performance for standard database workloads
  * Aurora provides significantly better performance
* architecture:
  * RDS is a single-instance architecture where one instance serves the application's read and write requests
  * Aurora has Aurora Storage, which is distributed and replicated across multiple Availability Zones
* replication:
  * RDS has traditional read replicas that can be used to offload read traffic from the primary database instance
  * Aurora has distributed storage architecture that replicates data across multiple replicas in different availability zones
* failover:
  * RDS offers Multi-AZ deployments, where a standby replica is maintained in a different availability zone to provide automatic failover in case of a primary instance failure
  * Aurora provides automatic failover with faster recovery times compared to Multi-AZ deployments; Aurora replicas are used for read scaling as well as for failover purposes
* storage and scalability:
  * RDS has storage based on the selected database engine's characteristics and limits
  * Aurora has a storage capacity that can grow dynamically up to 128 TB
* price:
  * RDS is generally lower cost
  * Aurora is generally higher cost due to better performance

### Amazon DynamoDB

* fast and flexible key value database for any scale
* performance at scale:
  * consistent, single-digit millisecond response times at any scale; build applications with virtually unlimited throughput
* serverless:
  * no server provisioning, software patching, or upgrades; scales up or down automatically; continuously backs up your data
* comprehensive security
  * encrypts all data by default and fully integrates with AWS IAM for robust security
* global database for global users and apps:
  * build global applications with fast access to local data by easily replicating tables across multiple regions

### Amazon DocumentDB

* fast, scalable, and fully managed MongoDB-compatible database service
* fast
  * millions of requests per second with millisecond latency; twice the throughput of MongoDB
* scalable
  * separation of compute and storage enables both layers to scale independently; scale otu to 15 read replicas in minutes
* fully managed
  * managed by AWS; no hardware provisioning; auto patching, quick setup, secure, and automatic backups
* MongoDB compatible
  * compatible with MongoDB 3.6; use the same SDKs, tools, and applications with Amazon DocumentDB

### Amazon ElastiCache

* Redis and Memcached compatible, in-memory data store and cache
* extreme performance:
  * in-memory data store and cache for microsecond response times
* secure and reliable:
  * network isolation, encryption at rest and in transit, HIPAA, PCI, FedRAMP, Multi-AZ, and automatic failover
* easily scalable
  * scale writes and reads with sharding and replicas

### Common Data Categories and Use Cases

* relational
  * relational data:
    * divide data among tables
      * highly structured
        * each row has the same number of columns and each column has data in the same format
    * relationships established via keys enforced by the system
      * ex. values that are common across tables to link the tables together
    * data accuracy and consistency
  * referential integrity, ACID transactions, schema-on-write
  * common use cases: lift and shift, ERP, CRM, finance
  * AWS services: Aurora, RDS
* key-value
  * high throughput, low-latency reads and writes, endless scale
  * common use cases: real-time bidding, shopping cart, social, product catalog, customer preferences
  * AWS services: DynamoDB
* document
  * document databases:
    * data is stored in JSON-like documents
      * first-class objects of the database
    * documents map naturally to how humans model data
    * flexible schema and indexing
    * expressive query language built for documents (ad hoc queries and aggregations)
  * store documents and quickly access querying on any attribute
  * common use cases: content management, user profiles, mobile
  * AWS services: DocumentDB
* in-memory
  * query by key with microsecond latency
  * common use cases: leaderboards, real-time analytics, caching
  * AWS services: ElastiCache

### Additional Notes

* structured vs. unstructured databases
  * ex. relational vs. key-value and document
  * structured databases are tables- rows and columns of data
  * unstructured databases are like JSON files
* Amazon Redshift: data warehousing relational database that serves as an alternative to Oracle

## Lecture Notes: AWS DynamoDB

### NoSQL

* NoSQL databases are non-tabular and store data differently than relational tables
* a common misconception is that NoSQL databases or non-relational databases don't store relationship data well
* NoSQL databases can store relationship data- they just store it differently than relational databases
* NoSQL data models allow related data to be nested within a single data structure and not in separate "tables" like traditional relational databases
* SQL vs. NoSQL
  * in traditional relational databases like SQL, data is stored in tables with keys that correlate each table to each other
    * fixed and structured attributes
  * with NoSQL, the same data can be stored in an unstructured format
    * information from all tables combined into a single JSON document
    * each column attribute becomes a field and the information in the rows become data values associated with the field
    * can be indexed and searched with field/value pairs
* storage costs have drastically decreased, so data models like SQL built for reducing data duplication aren't necessary
  * devs became the primary cost, so NoSQL databases were optimized for dev productivity
* as storage costs decreased, the amount of data applications need to store and query increased and that data came in all forms, so defining the schema in advance became nearly impossible

### DynamoDB

* tables, items, and attributes are the core components that you work with
  * a table is a collection of items
  * each item (a record in a database) is a collection of attributes
* uses primary keys to uniquely identify each item in a table and secondary indexes to provide more querying flexibility
* can use DynamoDB Streams to capture data modification events in DynamoDB tables
* on-demand pricing
  * write operations cost more than read operations
  * also charged by data stored

#### Tables

* similar to other database systems, DynamoDB stores data in tables
* a table is a collection of data
* ex. a table called People stores personal contact information

#### Items

* an item is a group of attributes that is uniquely identifiable among all of the other items
* ex. in the Peoples table, each item represents a person
* items in DynamoDB are similar to rows, records, or tuples in other database systems
* no limit to the number of items you can store in a table

#### Attributes

* each item is composed of one or more attributes
  * a fundamental data element, something that does not need to be broken down any further
* an item in the People table contains attributes called PersonID, FirstName, LastName, etc.
* attributes in DynamoDB are similar in many ways to fields or columns in other database systems

#### Secondary Indexes

* can create one or more secondary indexes on a table
  * a secondary index lets you query the data in the table using an alternate key, in addition to queries against the primary key
* DynamoDB doesn't require that you use indexes, but indexes give your applications more flexibility when querying your data
* after you create a secondary index on a table, you can read data from the index in much the same way as you can do from the table

## Lab Notes: DynamoDB

* AWS Management Console -> DyanmoDB -> Dashboard -> Create Table -> enter table details, leave default settings -> Create
* Tables -> choose table -> Explore Table Items -> Items returned -> Create item
  * can add values
  * can add new attributes with Add new attributes -> select data type -> input name and value
* Query -> select table, attributes, add Artist value, SongTitle, can add filters
  * only required value is Artist
* Tables -> select table -> Indexes -> Create index
* Imports from S3 -> Import from S3 -> Browse S3 -> format DynamoDB JSON and compression NONE
