# Data Warehouse vs Data Lake

Data warehouses, data lakes, and data lakehouses are distinct data management solutions

<img src="Docs/datalakehouse_diagram.png">

## Database
Any collection of data stored in tables. In business, databases are used for online transaction processing (OLTP), which captures and records detailed information in real-time, such as sales transactions. Database Management Systems (DBMS) store data in the database and enable users and applications to interact with the data.

Types:
- Relational databases: Oracle, MySQL, Microsoft SQL Server,  PostgreSQL
- Document databases: MongoDB and CouchDB
- Key-value databases: Redis and DynamoDB
- Wide-column stores: Cassandra and HBase
- Graph databases: Neo4j and Amazon Neptune

Both data warehouses and data lakes are meant to support Online Analytical Processing (OLAP). OLAP systems are typically used to collect data from a variety of sources. The data is used for analytical use cases ranging from business intelligence and reporting (e.g., quarterly sales reports by store) to forecasting (e.g., predicting home sales for the next six months based on historical trends).

## Schema on Write vs Schema on Read
Schema on write:
- data is structured and organised according to a specific schema before it is written to the database or data storage
- Schema defines the structure including data types, columns, and relationships between data elements
- data must conform to schema or it is rejected / requires transformation
- Enforces data consistency and integrity
- Faster query performance
- Associated with relational databases and data warehouses

Schema on read:
- Data ingested without enforcing pre-defined schema
- data stored in its raw format (unstructured or semi-structured)
- Flexibility as data can be ingested without strict structure requirements making it easier to handle data types and formats
- Suitable for unstructured and semi-structured data such as JSON, XML, log files
- Users can apply schemas, data transformations, and structures at the time of data retrieval, making it more adaptable to changing data needs and data exploration
- Associated with NoSQL databases and data lakes


## Data Warehouse

A centralized repository and information system that is used to develop insights and guide decision-making through business intelligence. A data warehouse stores summarised data from multiple sources, such as databases, and employs online analytical processing (OLAP) to analyse data.

- Stores structured or semi-structured data from various sources
- Stores current and historical data to perform in-depth analysis of data, generating business intelligence
- Pre-defined and fixed schema definition for ingest (schema on write and read)
- Data is cleaned, transformed, and aggregated before storage, meaning improved data quality
- Supports OLAP for complex query Processing
- Subject oriented for specific business units
- ETL process moves data from its original source to the data warehouse. ETL process move data at a regular schedule so data may not be in up-to-date state
- Used by business analysts and data scientists
- Pros:
  - The fixed schema makes working with the data easy for business analysts
- Cons:
  - More inefficient and costly as data sources and data volume grows over time
  - Difficult to design and evolve schema since adding tables can be complex and may involve data migration, Evolving the schema for new data sources can be resource intensive and requires planning to ensure data integrity and compatibility
  - Unsuitable for applications that need real-time data
  - As storage and compute resources are tightly couples, scaling up processing power often means scaling up storage. For example, running complex queries may require more processing units but system will provision storage which is costly. Modern cloud-based data warehouses decouple storage and compute, allowing scaling based on needs, meaning improved efficiency and cost savings.
- Technologies: Amazon Redshift, Google BigQuery, Snowflakes, Microsoft Azure Synapse


## Data Lake
A data lake is a centralised repository that allows the storage of structured, semi-structured and unstructured data at any scale. It uses flat architecture and object storage. Data comes from various sources that is stored in its original, raw format. Data lakes are designed to handle data at scale and provide a cost-effective storage solution for organizations dealing with diverse and rapidly growing data sources. This data can be used for machine learning or AI in its raw state and data analytics, advanced analytics, or databases and data warehouses after being processed.

- Stores structured, semi-structured, and unstructured data in its original, raw format
- Stores current and historical data
- Stores data in a variety of formats JSON, BSON, CSV, Parquet
- No schema definition required for ingest (schema on read)
- Schema or structure is applied when data is accessed or queried instead of when stored. This flexibility allows users to apply different schemas and interpretations of same data for analytics
- Data may not be up-to-date based on frequency of ETL processes
- Raw data and high volume of data allows solving of new problems
- Data in data lakes can be processed with a variety of OLAP systems and visualized with BI tools.
- Highly scalable in terms of storage and compute (suitable for big data applications), Horizontal scaling, Modern data lakes decoupled for independent compute scalability based on performance requirements, Elasticity of dynamically adjusting resources based on demand including resource allocation / optimisation, Parallel processing across multiple nodes/clusters allowing high performance analytics and faster query response times for big data sets
- Advanced analytics including data mining, ML, and predictive analysis due to raw and granular data
- Cost effective cloud based data lakes means organisations can pay for storage usage on demand
- Used by: Business analysts, application developers, and data scientists
- Pros:
  - Easy data storage simplifies ingesting raw data
  - A schema is applied afterwards to make working with the data easy for business analysts
  - Separate storage and compute
  - Low cost storage vs data warehouse
  - Highly scalable and highly agile

- Cons:
  - Requires effort to organize and prepare data for use and a specialised data team
  - Governance implemented downstream means more data silos (data collection help by one group that is not fully accessible by other groups of the organisation, leading to data duplication, multiple security policies, difficult collaborating)
  - Risk of data swamp if not configured to be scalable and agile, if duplicate, inaccurate, or incomplete data is stored that is no longer valuable for insights
  - As no structure, data that looks similar may have different meanings
  - Can design a system to check data for correct JSON format before storing but the checks are not made by data lake technologies, therefore doesn't make sense to use at enterprise level where some business lines may not have data engineering skills
- Technologies: AWS S3, Google Cloud Storage
- For organising and querying data lakes: MongoDB Atlas Data Lake, AWS Athena, DataBricks SQL Analytics




  ## Data Warehouse vs Data Lake Summary

  | Characteristics     | Data Warehouse                                             | Data Lake                                                  |
  |---------------------|------------------------------------------------------------|-----------------------------------------------------------|
  | Data                | Relational from transactional systems, operational databases, and line of business applications | Non-relational and relational from IoT devices, web sites, mobile apps, social media, and corporate applications |
  | Schema              | Designed prior to the DW implementation (schema-on-write) | Written at the time of analysis (schema-on-read)         |
  | Price/Performance   | Fastest query results using higher cost storage            | Query results getting faster using low-cost storage      |
  | Data Quality        | Highly curated data that serves as the central version of the truth | Any data that may or may not be curated (i.e., raw data) |
  | Users               | Business analysts                                          | Data scientists, Data developers, and Business analysts (using curated data) |
  | Analytics           | Batch reporting, BI and visualizations                    | Machine Learning, Predictive analytics, data discovery and profiling |


  A data warehouse is a database optimized to analyse relational data coming from transactional systems and line of business applications. The data structure, and schema are defined in advance to optimize for fast SQL queries, where the results are typically used for operational reporting and analysis. Data is cleaned, enriched, and transformed so it can act as the “single source of truth” that users can trust.

  A data lake is different, because it stores relational data from line of business applications, and non-relational data from mobile apps, IoT devices, and social media. The structure of the data or schema is not defined when data is captured. This means you can store all of your data without careful design or the need to know what questions you might need answers for in the future. Different types of analytics on your data like SQL queries, big data analytics, full text search, real-time analytics, and machine learning can be used to uncover insights.


## Data Lakehouse

A data lakehouse is a data platform, which merges the best aspects of data warehouses and data lakes into one data management solution

Data warehouse provides high performance and scalable analytics with ACID transactions whereas Data Lake consolidates raw data in a single central location without the need for a schema. Data lakes are open format which is essential for modern data architectures, and are durable and low cost due to scalability and object storage. Data lakes have reliability issues such as difficulty combining batch and streaming data, duplicates, corruption, slow performance because of bottlenecks (metadata, data partitions) meaning slow queries, and lack of security and governance.


Technologies enabling data warehouse:
- metadata layers for data lakes
- new query engine designs providing high-performance SQL execution on data lakes
- Optimised access for data science and ML tools


Data Lakehouse:
- Combines data warehousing and data lake capabilities
- Single low-cost data store for structured, semi-structured and unstructured database
- Data management features for schema, data governance, ETL processes, data cleaning
- ACID (atomicity, consistency, isolation, and durability) properties to ensure data consistency when multiple users concurrently read and write data
- End-to-end streaming to support real-time ingestion of data and insight generation
- Separate compute and storage resources to ensure scalability for a diverse set of workloads

A data lakehouse uses the same low-cost cloud object storage of data lakes to provide on-demand storage for easy provisioning and scaling. Like a data lake, it can capture and store large volumes of all data types in raw form. The lakehouse integrates metadata layers over this store to provide warehouse-like capabilities, such as structured schemas, support for ACID transactions, data governance, and other data management and optimization features.

Pros:
- Data lakehouse removes silos of two separate systems meaning single data repository maintenance, and tools connected to source data
- Enforce schema means better data quality and consistency, with reduced time for new data availability
- Low storage costs and Data lakehouses help reduce costs from ETL processes and de-duplication
- Reliable due to reduced ETL data transfer between multiple systems, reducing data quality problems or technical issues
- Data governance as data is consolidated in one place allowing robust security controls, schema requirements can be enforced as data is ingested and uploaded, reducing downstream data quality issues
- Reduced data duplication and redundant data in disparate systems, simplified observability as less data moving through pipelines into multiple systems
- Connect multiple tools to the lakehouse for analytics, SQL, ML
- Scalability as low cost cloud object storage allows for decoupling compute from Storage
- Streaming support for real-time ingestion from devices

Cons:
- Complexity in implementing and maintaining data lakehouse as it requires technical expertise to integrate systems efficiently (initial cost higher)
- For decoupled architecture models, data movement between data lake and data warehouse requires complex ETL processes, which can be resources intensive and lead to latency in data availability, which makes data governance difficult (but decoupled and hybrid models exist)
- Schema-on-read may result in latency when processing data, affecting real-time or near-real-time analytics
- New technology

## Architecture of Data Lakehouse

A data lakehouse typically consists of five layers: ingestion layer, storage layer, metadata layer, API layer, and consumption layer.

- **Ingestion layer**: gathers data from different sources and transforms it into format for storage and analysis in the lakehouse. Uses protocols to connect with internal/external sources such as DBMS, NoSQL database, social media
- **Storage Layer**: structured, unstructured, and semi-structured data is stored in open-source file formats, such as such as Parquet or Optimized Row Columnar (ORC)
- **Metadata Layer**: Unified catalogue that delivers metadata for every object in the lake storage for organisation and information about the data in the system. Utilise ACID transactions, file caching, indexing for faster query. Use predefined schemas for governance
- **API layer**: lakehouse uses API to increase task processing and for more advanced analytics, including use of TensorFlow
- **Data consumption layer**: layer for hosting client apps and tools enabling access to all metadata and data stored in the lake. Users across an organisation can carry out analytics such as BI dashboard, visualisation, ML


## Delta Lake
It is an Open source storage layer that provides reliability to the data lakes. Delta Lakes provides ACID properties, scalable metadata handling, and unifies streaming and batch data processing. It runs on the top of data lakes and it is fully compatible with Spark APIs.
- Acid transactions
- Scalable handling of Metadata
  - Does not face small file problem like HDFS
  - HDFS is designed for storing and managing large files as its optimised for high throughput and fault tolerance
  - Small files (less than the HDFS block size) are stored in one block causing excessive memory requirement, access time and processing time
  - Also causes excessive load on the name node which translates file system operations into block operations on the data node meaning increased metadata operations
  - Similarly MapReduce is used in Hadoop for parallel processing of large datasets where small files create many map tasks causing overhead and inefficiency
  - Solution is to combine small files, store data in formates like SequenceFile, or use data warehousing tool like Hive / NoSQL database like HBase for small data
- Unified batch and streaming allowing concurrent streaming or batch writes to tables
- Can specify and enforce schema using metadata, enabling schema to evolve over time without affecting pipelines
- Time travel (data versioning) allows querying and data exploration of past data for historical analysis
- Delta allows upserts and merges:  DML language operations including merge, update, delete, and also complex streaming upserts
- Companies have existing data lakes in place, so use delta lake to run on top of an existing data lake and improve its reliability, security, and performance
