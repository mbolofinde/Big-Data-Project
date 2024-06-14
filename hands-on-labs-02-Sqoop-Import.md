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