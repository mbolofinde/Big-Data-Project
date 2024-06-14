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