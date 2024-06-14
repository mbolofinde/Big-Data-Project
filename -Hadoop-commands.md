[Notes] Hadoop Commands
1. To list the files in HDFS:

   hdfs dfs -ls

   hdfs dfs -ls /user/cloudera/



2. create directory in HDFS:

    hdfs dfs -mkdir /user/cloudera/dir1

    hdfs dfs -mkdir /user/cloudera/dir2



3.  listing files in hadoop :

    hdfs dfs -ls /user/cloudera/    #list files

    hdfs dfs -ls /user/cloudera/emp #list files in emp directory



4.  copy from local file system to HDFS :

    hdfs dfs -copyFromLocal /home/cloudera/test.csv  /user/cloudera/



5.  put: Copies files from the local file system to the destination file system. This command can also read input from stdin and write to the  destination   file system.

    hdfs dfs -put localfile1 localfile2 /user/cloudera/hadoopdir;



6. moveFromLocal: Works similarly to the put command, except that the source is deleted after it is copied.

   hdfs dfs -moveFromLocal localfile1 localfile2 /user/cloudera/hadoopdir



7. cp: Copies one or more files from a specified source to a specified destination. If you specify multiple sources, the specified destination must be a   directory.

   hdfs dfs -cp /user/cloudera/file1 /user/cloudera/file2 /user/cloudera/dir



8.  Copy from HDFS to Local

    hdfs dfs -copyToLocal   /user/cloudera/test.csv /home/cloudera/test.csv

 

9.  get: Copies files to the local file system

    hdfs dfs -get /user/cloudera/file3 localfile



10. To view the contents of a file :

     hdfs dfs -cat /user/cloudera/student.txt



11. text: Outputs a specified source file in text format. Valid input file formats are zip and TextRecordInputStream.

    hdfs dfs -text /user/cloudera/file8.zip