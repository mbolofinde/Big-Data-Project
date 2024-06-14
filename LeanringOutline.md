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

[Notes] sqoop import
sqoop import:

sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 1 --table customers  --target-dir /user/cloudera/data_import



Try executing the command again. It fails. So use append:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 1 --table customers --append  --target-dir /user/cloudera/data_import



What if we want to overwrite:

sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 1 --table customers --delete-target-dir  --target-dir /user/cloudera/data_import



[Notes] Sqoop Multiple Mappers
Multiple Threading in sqoop:
Multiple mappers will be working on importing the file. i.e multiple threads will work on importing the file . This is basically like parallelism. We mention the mappers using -m. So -m 1 is one mapper i.e one thread only. So you will see only one part file in output directory.

Add 2 mappers here. Add split-by column as well:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2  --split-by customer_id --table customers --delete-target-dir  --target-dir /user/cloudera/data_import



Now what happens if you dont specify number of mappers? If you dont specify number of mappers, it will by default take 4

If you dont specify split-by when the number of mappers are more than 1, it will fail. However if the table has a primary column, then sqoop will take that primary column as the split-by column


[Notes] import portion of data
using where:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2 --table customers --split-by customer_id
--where 'customer_state="TX"'  --delete-target-dir --target-dir /user/cloudera/where_eg



using select columns:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2 --table customers --split-by customer_id
--where 'customer_state="TX"'  --columns 'customer_fname,customer_lname,customer_state,customer_city' --delete-target-dir --target-dir /user/cloudera/where_eg



query:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2 --table customers --split-by customer_id
--query 'customer_fname,customer_lname,customer_state,customer_city from customers where  $CONDITIONS' --delete-target-dir --target-dir /user/cloudera/query_eg



$CONDITIONS: When you are executing sqoop in parallel, each sqoop process will replace this $CONDITIONS with a unique condition expression. Here one mapper may execute your query with custid<5 and another mapper with cust_id>5



What if we also have a where clause condition in our query. We will still need to use $CONDITIonS as below :
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2 --table customers --split-by customer_id
--query 'customer_fname,customer_lname,customer_state,customer_city from customers where customer_state="TX" AND  $CONDITIONS' --delete-target-dir --target-dir /user/cloudera/query_eg



[Notes] Sqoop eval and change the file delimiter
Sqoop Eval:

Sometimes we may want to evaluate the data before importing into Hadoop. Sqoop eval will help us doing this. Sqoop Eval basically is connecting to database from sqoop command. All the sql commands that you can fire on database, we can execute them using the sqoop eval. When you put a sql query in sqoop eval, it will connect to the database, fire the command and display the results on the edge node. We use eval instead of import and place the query in --query.

Eg :sqoop eval --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --query "Select * from customers limit 10";



Changing Import delimiter:
When sqoop imports the data into hadoop, by default it stores the data in comma delimeter. We can change this using : fields-terminated-by and lines-terminated-by



Eg: sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2 --table customers --split-by customer_id --fields-terminated-by '|' --lines-terminated-by '\n' --delete-target-dir --target-dir /user/cloudera/customer



[Notes] incremental import

Sqoop Incremental Import:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2 --table customers --split-by customer_id
--target-dir /user/cloudera/customer1 --incremental append --check-column customer_id --last-value 0

--incremental append : to tell that it is incremental load
--check-column : Which colum you want to use to do the incremental load. Here it is custid
--last-value : sqoop will import data that is greater than this last-value. Here it will import where custid>0. This last value an be an integer, date or timestamp but not string as it will search for data greater than that last value

Next time, you need to change the last-value to import from the value greater than the last imported.So, everytime you need to import any records, you must remember the last-value from previous import and use it in the sqoop command. This is very manual. What if sqoop does this job for us ? What if sqoop remembers the last-value and imports from that last-value in next sqoop ? This is possible by creating a sqoop job.



We create a sqoop job with an import statement. We give it a name. We then execute the job which will internally execute the sqoop import and the last-value is then saved by the sqoop. When there are additional rows to the table, you just execute the sqoop job.

sqoop job --create myJob -- import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2 --table customers
--split-by customer_id
--target-dir /user/cloudera/customer2  --incremental append
--check-column custid --last-value 0



Note : myJob is the name of the sqoop job
-- import : There must be a space between -- and import.



Now to execute this job :
sqoop job --exec myJob

