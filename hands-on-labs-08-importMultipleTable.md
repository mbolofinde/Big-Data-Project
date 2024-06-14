[Notes] Import multiple Tables

sqoop import-all-tables --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1 --warehouse-dir /user/cloudera/tables;

Below query imports all except for few tables:
sqoop import-all-tables --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1
--exclude-tables categories,customers,orders --warehouse-dir /user/cloudera/tables;



import-all-tables will import all the tables. But since I want to import only 2 tables, I have to skip the remaining tables. This we can do using –exclude-tables.

--warehouse-dir is same as –target-dir except that in –target-dir a folder is created by the table name and then we have part files in it. In warehouse-dir, an extra folder is created and inside that we have folder for each table. Since we are using multiple tables here, we are using –warehouse-dir instead of –target-dir.