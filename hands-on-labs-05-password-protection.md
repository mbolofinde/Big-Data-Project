[Notes] Password Protection
Saving the password to a file and using that file for password:
sqoop import --connect jdbc:mysql://localhost:3306/retail_db --username root --password-file file:///home/cloudera/passfile --m 1 --table customers  --target-dir /user/cloudera/data_import

Instead of storing the password in text format, we can encrypt the passoword and store the encrypted password and then refer to this encrypted password in our sqoop command. As of Sqoop version 1.4.5, Sqoop supports the use of JKS to store passwords which would be encrypted,so that you do not need to store passwords in clear text in a file.This can be achieved using Java KeyStore.A Java KeyStore (JKS) is a repository of security certificates – either authorization certificates or public key certificates – plus corresponding private keys, used for instance in TLS encryption.



Below is the command to store the encrypted password:
hadoop credential create encrytpassword -provider jceks://hdfs/tmp/mypassword



It will ask you for password Give your password and it will encrypt the password and store in hdfs path :jceks://hdfs/tmp/mypassword. You can provide the alias : encryptpassword instead of the orginal password or the password file.



Now, we will use this encrypted password. We will pass the alias : encryptedpassword we created above. Here is the command for this :



sqoop import -Dhadoop.security.credential.provider.path=jceks://hdfs/tmp/mypassword --connect jdbc:mysql://localhost:3306/retail_db --username root --password-alias encrytpassword --table customers -m 1 --target-dir /user/cloudera/data_import_encrypted
