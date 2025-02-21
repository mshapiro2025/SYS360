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
