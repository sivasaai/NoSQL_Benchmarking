# NoSQL_Benchmarking
This project contains the steps and required files to perform bench marking MongoDB and Cassandra using Yahoo! cloud serving benchmark(YCSB) done for the Term Paper for Advanced Computer Networks.

# Environment Used
- RockyLinux 8.5 Operating System. (Rocky Linux is an open-source enterprise operating system designed to be 100% bug-for-bug compatible with Red Hat Enterprise Linux®. It is under intensive development by the community.)
- 4GB RAM
- 100 GB Disk
- 4 CPUS of model 64 bit  Intel(R) Xeon(R) CPU E5-2620 0 @ 2.00GHz

# Steps to setup MongoDB for Benchmarking
- Install MongoDB using the steps specified here in the url - https://www.golinuxcloud.com/install-mongodb-rocky-linux/#:~:text=Install%20MongoDB%20on%20Rocky%20Linux%208.4%20%28Step-by-Step%29%201,SELinux%20...%208%20Step%208%3A%20Uninstall%20MongoDB%20

- connect to the mongodb prompt using the command `mongo` in the terminal.
- switch to admin using following command.


![image](https://user-images.githubusercontent.com/44334277/209716154-eea2ac67-8491-4741-b255-74df1774e9c9.png)

- create a user using following command as shown in image
![image](https://user-images.githubusercontent.com/44334277/209716297-88ef7f75-76cc-4ff8-9142-04b6a0ea3d06.png)

# Steps to setup Cassandra for Benchmarking
-  Install openjdk using command.
`sudo yum install java-1.8.0-openjdk-devel`
- Setup cassandra repo for installing casandra, Add cassandra.repo file with following content to /etc/yum.repos.d/


`[cassandra]`

`name=Apache Cassandra`

`baseurl=https://www.apache.org/dist/cassandra/redhat/311x/`

`gpgcheck=1`

`repo_gpgcheck=1`

`gpgkey=https://www.apache.org/dist/cassandra/KEYS`


- Install cassandra package

`yum install -y cassandra`

- Start cassandra service using command `systemctl start cassandra`

- connect to Cassandra client prompt using command `cqlsh`

- Create a keyspace with name `ycsb` using the following command.
`create keyspace ycsb WITH REPLICATION = {'class': 'SimpleStrategy', 'replication_factor':3};`

-  Create usertable using following command.

![image](https://user-images.githubusercontent.com/44334277/209742738-f69f947d-a5cf-4424-bf80-812ff3dc08e1.png)


# Installation of YCSB tool.
-  Download tar archive of the YCSB tool using following command 

`curl -O -location https://github.com/brainfrankcooper/YCSB/releases/download/0.15.0/ycsb-0.15.0.tar.gz`

- untar the downloaded archive using the following command

`tar -xvfz ycsb-0.15.0.tar.gz`

- change current directory to `ycsb-0.15.0`
 using the following command.

`cd ycsb-0.15.0`

- All the predefined workload files can be found in `../ycsb-0.15.0/workloads/*`

# Important parameters updated or changed in workload files for different tests for this term paper.

- `recordcount:` This decides number of records to be loaded when ran ycsb with load option.
- `operationcount:` This decides number of operations to be run for the test run.
- `readpropotion`: This parameter decides how much percent of operations of operationcount will be read operations.
- `insertpropotion`: This parameter decides how much percent of operations of operationcount will be insert operations.
- `updatepropotion`: This parameter decides how much percent of operations of operationcount will be update operations.


# Custom work loads.

- For the purpose of testing the Update Heavy workloads and Update only workload , the following two custom workloads were added.
- workloadg(This is upload heavy workload which has 5% of read operations and 95 % of update operations)
for this `readproportion` is set to 0.05 and `updateproportion`  is set to 0.95.
- workloadf(This is upload only workload which is 100% of update of operations)
for this `readproportion` is set to 0 and `updateproportion`  is set to 1.00.
- `workloadg` and `workloadf` files are added in the repostiory for the use.

# How to run and collect the execution time of workload on cassandra.


# How to run and collect the execution time of workload on MongoDB.





