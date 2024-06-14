Big data comprises structured and unstructured data gathered by organizations to train predictive models, find patterns, and various comprehensive analytic techniques. It is a popular and rapidly growing tool among data engineers around the globe.

1. Hadoop

1.1 Introduction
1.2 Rise of Big Data
1.3 Untitled Masterpiece
1.4 Big Data Defined
1.5 Big Data vs Data Warehouse

Module 1: Introduction to Big Data and Hadoop
1. Introduction to Big Data
Explanation: Big Data refers to the vast volumes of data that cannot be efficiently processed using traditional database systems due to their size, complexity, and rate of growth. In this section, we'll explore how big data is changing the landscape of data analysis and decision-making.

Problems Being Solved: Traditional data processing tools are inadequate for handling the scale, diversity, and complexity of big data. This section explains the need for specialized approaches and technologies to manage, process, and extract value from big data.
Application: This concept is crucial for organizations dealing with large-scale data environments, such as social media platforms, e-commerce sites, and large-scale sensor networks in IoT applications.

2. Rise of Big Data
Explanation: This topic covers the historical evolution of big data, highlighting the technological advancements and organizational demands that have driven its prominence in recent years.
Problems Being Solved: Understanding the rise of big data helps in comprehending the scale of data generated today and the urgency for advanced analytics to leverage this data for competitive advantage.
Application: Relevant for data scientists, business analysts, and IT professionals who work with data-intensive applications across various sectors including healthcare, finance, and retail.

3. Big Data Defined
Explanation: We'll define big data through the 5 Vs: Volume, Velocity, Variety, Veracity, and Value, which collectively characterize the challenges and opportunities of big data.
Problems Being Solved: Provides a framework for understanding the multifaceted aspects of big data and its implications on data handling and processing technologies.
Application: Essential for anyone involved in data management, data engineering, and data analysis, facilitating a structured approach to tackling big data projects.
4. Big Data vs Data Warehouse
Explanation: This segment contrasts big data with traditional data warehouses, focusing on the differences in data types, processing methodologies, scalability, and performance.
Problems Being Solved: Clarifies misconceptions and sets expectations for the capabilities and limitations of big data technologies versus traditional data warehousing solutions.
Application: Useful for database administrators, data architects, and decision-makers planning data strategy and infrastructure.
5. Introduction to Hadoop
Explanation: An introduction to Hadoop as a framework that allows for the distributed processing of large data sets across clusters of computers using simple programming models.
Problems Being Solved: Hadoop addresses issues of scaling up for big data processing and provides fault tolerance and high availability, which are not easily achievable with traditional systems.
Application: Critical for data engineers and developers in environments where large-scale data processing and cost-effective storage solutions are necessary.
6. Hadoop Ecosystem Components: HDFS, Yarn, and MapReduce
Explanation:
HDFS (Hadoop Distributed File System): Designed to store very large data sets reliably and to stream those data sets at high bandwidth to user applications.
Yarn (Yet Another Resource Negotiator): Manages and monitors cluster resources, facilitating job scheduling.
MapReduce: A programming model for processing large data sets with a distributed algorithm on a Hadoop cluster.
Problems Being Solved: Each component is designed to solve specific challenges in big data handling—HDFS for storage, Yarn for resource management, and MapReduce for processing.
Application: Integral for developers building applications that require scalable, efficient, and reliable data processing capabilities across large clusters.

[Notes] Serialized File Formats
Serialization :
Serialization is the process of converting a data structure or an object into a format that can be easily stored or transmitted over a network and can be easily reconstructed later.
For example : If I have the below data :
“This is my Data”
Now this data will be serialized ie converted into stream of bytes(human unreadable format). So serialized data is unreadable. IT is either stored or transmitted over a network. Then this is deserialized ie converted back to its original form which is readable.

Advantages of Serialization :
1) Serialized data are easy and fast to transmit over a network. Read and write are fast
2) Some serialized file formats offer good compression, they can be encrypted
3) Deserialization also does not take much time



Serialized File Formats in Big Data :
1) Sequence file format
2) RC File format
3) ORC File Format
4) AVRO File Format
5) Parquet File Format

For more details on these files, check the Hive document.

1) Sequence File Format : Its pure Java serialization. It helps in easy retrieval of data But since it is java serialization, it works best for map reduce only. Does not work well with Spark or other tech. Since map reduce is extinct, so is sequence

2) RC File Format: Row Columnar File Format : Write takes time. Read would be easy .Columnar file format are easy to read. No compression technique so data size would be huge

3) Parquet : Columnar File Format .Reasonable Compression technique (50 to 55%).
Compression technique supported by Parquet : snappy(default),lzo,gzip
Parquet is used in Target system as querying is fast

4) ORC : Optimized Row Columnar File Format.It is Columnar FIle format
75% compression Ratio. Use when you are dealing with historical data when you are not using it often. Decompression will take time. So ORC is used for historical data storages
ORC has ZLIB compression which provides much more compression. It also has snappy but has less compression to ZLIB

5) AVRO - Row File Format
File size is big. Write is easy. Read is tough bcoz its row file format.AVRO supports Schema Evolution(channginng the structure of the data)

Sequence File Format and RC file format are not used much. Parquet is the most preferred one followed by both ORC and AVRO

Note :
Sqoop supports - Sequence, Parquet, AVRO directly
ORC - Sqoop needs Hive Integration



AVRO vs ORC vs Parquet :

1) AVRO is a row Format while ORC and Parquet are columnar format

2) Because AVRO is row Format, it is write heavy while ORC and Parquet are read heavy.

3) In all these 3 file formats, along with data, the schema will also be there. This means you can take these files from one machine and load it in another machine and it will know what the data is about and will be able to process

4) All these file formats can be split across multiple multiple disks. Therefore scalability and parallel processing is not an issue.

5) ORC provides maximum compression followed by Parquet followed by AVRO

6) If the schema keeps changing then AVRO is preferred as AVRO supports superior schema evolution. ORC also supports to some extent but AVRO is best

7) AVRO is commonly used in streaming apps like Kafka, Parquet is commonly used in Spark and ORC in Hive. Parquet is good in storing nested data. So usually in spark, parquet is used

8) Because compression of ORCFile is more, it is used for space efficiency. Query time will be little more as it has to decompress the data. In case of AVRO, the time efficiency would be good as it takes little less time to decompress. So if you want to save space, use ORC . if you want to save time, use Parquet