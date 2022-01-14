# Sqoop-Export-Staging
This repository gives an idea about Sqoop export staging  through a project.

# Export can optionally use staging area.

  ^After populating the staging table, data goes to the target table in Relational DB.

  %It is a good practice in prevention of Sqoop job in case of job failure.

  !It acts as a insuation to prevent the target from data loss in job failure.

  $It is a optional technique, where map tasks populate staging table and each map write is broken down into many transactions.


======Sqoop Staging ======


=======
Edge Node
=======
Login to Edge Node

=========
vi or nano exdata

1,Arun,2015-09-20

2,zeyo,2015-09-21

3,zeyovas,2015-09-22

4,mohamed,2015-09-23

5,arun,2015-09-24

6,61,2015-09-24

=============
hadoop fs -put exdata /user/cloudera/


=======
Mysql
=======

create database stg;
use stg;
CREATE TABLE customermoda(custid INT,firstname VARCHAR(20),lastname VARCHAR(20));
CREATE TABLE customermoda_stg(custid INT,firstname VARCHAR(20),lastname VARCHAR(20));


=======
Edge Node
=======

sqoop export \
--connect jdbc:mysql://localhost/stg \
--username root --password <> \
-m 1 \
--staging-table customermoda_stg \
--clear-staging-table \
--table customermoda \
--export-dir /user/cloudera/exdata

=======
mysql
=======


select * from customermoda_stg;

select * from customermode;
