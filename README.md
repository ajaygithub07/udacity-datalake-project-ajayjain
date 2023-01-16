# Project: Data Lake with Spark###
## Introduction##
A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

Sparkify want to build an ETL pipeline that extracts their data from S3, processes them using Spark, and loads the data back into S3 as a set of dimensional tables. This will allow their analytics team to continue finding insights in what songs their users are listening to.

So in brief, We will <br>
1) Create EMR scluster, and then  SFTP project files using Winscp (dl.cfg and etl.py) to cluster master node home directory. <br>
3) Run the etl.py that will Use Spark to read data from S3 and then transform the files. <br>
3) Store Spark parquet files in S3  <br>
4) We will create artist, song, user, time dimension tables and a songplay fact table stored as Spark parquet files.<br>



# How to run on Spark 

## Prerequisite Steps:
I could not to it on my office compure due to security, so I have to do it in my personal computer.<br>

1) Create an EC2 Pair and save the private key (.ppk) in your desktop <br>
2) Download Putty <br>
3) Download Winscp <br>


## Start Up EMR Cluster:

1. Log into the AWS console  and navigate to EMR<br>

2. Click "Create Cluster"<br>

3. Select "Go to advanced options"<br>

4. Under "Software Configuration", select Hadoop, Hive, and Spark<br>

* Optional: Select Hue (to view HDFS) and Livy (for running a notebook)<br>

5. Under "Edit software settings", enter the following configuration:<br>
[{"classification":"spark", "properties":{"maximizeResourceAllocation":"true"}, "configurations":[]}]<br>

6. Click "Next" at the bottom of the page to go to the "Hardware" page<br>

7. Click "Next" at the bottom of the page to go to the "General Options" page<br>

10. Give your cluster a name and click "Next" at the bottom of the page<br>

11. select your EC2 key pair. This is required to ssh into master node and run the etl.py<br>

12. Click "Create Cluster"<br>

13. Open putty an provide host name <br>
    e.g.; hadoop@ec2-99-99-999-999.us-west-2.compute.amazonaws.com and <br>
    click on under ssh/auth and then browse to folder where private key is stored and select the privatye key
    that was selected while creating the cluster   <br>

14. Open Winscp and copy etl.py and dlcfg  in the hadoop home directory<br>

15.  Append the following line to the /etc/spark/conf/spark-env.sh file:<br>
    export PYSPARK_PYTHON=/usr/bin/python3<br>

## Run your job

1. In your home directory on the EMR master node (/home/hadoop), run the following command:

   <strong>spark-submit etl.py<strong>

2. After a couple of minutes your job should show up in the Spark History Server page in your browser

* You should see the real-time logging output in your EMR AWS console


## Project Files
In addition to the data files, the project workspace includes following files:

1. aws/dl.cfg stores AWS keys 

2. etl.py - Get the song and log data from S3 to Spark, process the data into dimensional tables, finally saves the data back to S3

4. etl.ipynb - design and creating buckets

5. README.md Provides project info

## Configuration
AWS key and secret are in ./aws/dl.cfg, Please set them before running  etl.py<br>
Note: no need to put the quotes or double quotes around the key and secret value

[AWS]
key =<br>
secret =<br>

## Build ETL Pipeline
etl.py will process the entire datasets.

## Instruction
Provide the key and secrect access key in aws/dl.cfg file 

for run on your Local computer or project workspace - Open the terminal and the run below command at workspace directory<BR>
<strong>python etl.py<strong>

## Author
<strong>Ajay Jain<strong>