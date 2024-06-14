[Notes] Import multiple File Formats
Import as Sequence File :
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1 --table order
 --target-dir /user/cloudera/sequence_dir --as-sequencefile 
 
Import as AVRO File:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1 --table order
 --target-dir /user/cloudera/avro_dir 
 --as-avrodatafile
 
Import as Parquet File:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1 --table order
 --target-dir /user/cloudera/parquet_dir 
--as-parquetfile
 
Import as ORC :  

There is no equivalent of –as-avrodatafile or –as-sequence or –as-parquetfile for ORC. In order to import as ORC file, we need to leverage the sqoop’s Hcatalog integration feature. HCatalog is a table storage management tool for Hadoop that exposes the tabular data of Hive metastore to other Hadoop applications. 
It enables users with different data processing tools (Pig, MapReduce) to easily write data onto a grid.

You can think of Hcatalog as an API to access Hive metastore.
 
To import as ORC, it involves the below two steps:
1) Create Hive Database with your desired HDFS warehouse location
2) Run Sqoop import command to import from RDBMS table to Hcatalog table
Let’s sqoop import the table : customermod3 as ORC. We basically import the data into some hive database. We can ask the sqoop to create a hive table. So basically a hive table will be created and the directory for that hive table will be in ORC format.
 
Here is the sqoop import command :

create database first in HIve 

sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1 --table orders --m 1 --hcatalog-database test --hcatalog-table orders --create-hcatalog-table --hcatalog-storage-stanza "stored as orcfile";

Additional options here are the –hcatalog options where we are giving the database name, hive table to be created and how the storage needs to happen. So hive table will be created under a database test.