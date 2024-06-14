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