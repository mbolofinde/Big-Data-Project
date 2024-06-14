[Notes] Using Last Modified

If there is an update in database , say some column value changed, then it should reflect in hdfs. This is like scd type 1. Updating the hdfs to be in sync with db. Sqoop will run 2 map reduce jobs here. One Map reduce job to bring the data(here only mappers run) and the second map reduce job to compare the data(here reducers also run because it would compare from different nodes and consolidate).

If you run only import, there is only mappers involved. No reducers because there is no shuffling.

eg: sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1 --table orders  --target-dir /user/cloudera/data_import



--mysql database
select * from orders where order_id in (68871,68809,68817,68827);



Now lets update/insert  values in the table :

update orders set order_status='test1' where custid=68809; --2014-03-12
update orders set order_status='test2' where custid=68817; -- 2014-03-27
update orders set order_status='test3' where custid=68827; -- 2014-04-16
update orders set order_status='test4' where custid=68871;  -- 2014-06-28



Below is the query for last modified:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1 --table order
  --target-dir  /user/cloudera/cust_mod --incremental lastmodified --check-column order_date --last-value 2014-04-15 --merge-key order_id



Here, --check-colum createdt : mention the column where it should pick data for comparison

--last-value : Give the value for createdt . From this value, it would pick the data

--merge-key : Column used for comparison