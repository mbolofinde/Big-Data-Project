[Notes] Sqoop eval and change the file delimiter
Sqoop Eval:

Sometimes we may want to evaluate the data before importing into Hadoop. Sqoop eval will help us doing this. Sqoop Eval basically is connecting to database from sqoop command. All the sql commands that you can fire on database, we can execute them using the sqoop eval. When you put a sql query in sqoop eval, it will connect to the database, fire the command and display the results on the edge node. We use eval instead of import and place the query in --query.

Eg :sqoop eval --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --query "Select * from customers limit 10";



Changing Import delimiter:
When sqoop imports the data into hadoop, by default it stores the data in comma delimeter. We can change this using : fields-terminated-by and lines-terminated-by



Eg: sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password cloudera --m 2 --table customers --split-by customer_id --fields-terminated-by '|' --lines-terminated-by '\n' --delete-target-dir --target-dir /user/cloudera/customer
