# Wine Quality Prediction in Spark over AWS
 
> build a wine quality prediction ML model in Spark over AWS
  
## 🚩 Table of Contents  
* [Description](#-Description)  
* [Preparing development environment](#-Preparing-development-environment)  
* [Running programs in AWS](#-Running-programs-in-AWS)  
* [Credits](#-Credits)  
* [License](#-License)  
  
## 🚩 Description  
     
Develop machine learning applications in Amazon AWS cloud platform. Use Apache Spark to train an ML model on EC2 instances. Use Spark's MLlib to develop and use an ML model in the cloud.
## 🚩 Preparing development environment  
  
1. Sign up for an AWS account if you haven't.  
2. Launch instance 
> Note1: choose Ubuntu Server 18.04 LTS (HVM), SSD Volume Type - ami-085925f297f89fce1 (64-bit x86). 
> Note2: add Rule under Configure Security Group, set 'port range = 8888' and 'source = 0.0.0.0/0'.
> Note3: save .pem file to local, e.g. /path/your.pem  

## 🚩 Running programs in AWS   
  
1. Connecting to instance using SSH  
```bash  
chmod 400 your.pem  
```  
  
```bash  
ssh -i /path/your.pem ubuntu@[instance public DNS]  
```  
 
2. Copy data files from local to instance  
```bash  
scp -i /path/your.pem /path/trainingDataset.csv ubuntu@[instance public DNS]:~  
```  
```bash  
scp -i /path/your.pem /path/ValidationDataset.csv ubuntu@[instance public DNS]:~
```  
   
3. Install Java
```bash  
sudo apt install openjdk-8-jre-headless
```

4. Install Hadoop / Spark
```bash  
wget http://archive.apache.org/dist/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz
sudo tar -zxvf spark-2.4.4-bin-hadoop2.7.tgz
```

````bash
$ export SPARK_HOME='/home/ubuntu/spark-2.4.4-bin-hadoop2.7'
$ export PATH=$SPARK_HOME:$PATH
$ export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
````
````bash
cp spark-env.sh.template spark-env.sh
sudo vim spark-env.sh
````
> add "export PYSPARK_PYTHON=/usr/bin/python3"
       "export PYSPARK_DRIVER_PYTHON=/usr/bin/python3" in spark-env.sh

5. Install Anaconda
````bash
wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh
bash Anaconda3-2020.02-Linux-x86_64.sh
source .bashrc
jupyter notebook --generate-config
$ mkdir certs
$ cd certs
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem
$ cd ~/.jupyter/
$ vi jupyter_notebook_config.py
````
> add the following in jupyter_notebook_config.py
````
       c = get_config()
       # Notebook config this is where you saved your pem cert
       c.NotebookApp.certfile = u'/home/ubuntu/certs/mycert.pem' 
       # Run on all IP addresses of your instance
       c.NotebookApp.ip = '*'
       # Don't open browser by default
       c.NotebookApp.open_browser = False  
       # Fix port to 8888
       c.NotebookApp.port = 8888
````
6. Run Jupyter Notebook
```
$ jupyter notebook
```
In browswer, go to https://[instance public DNS]:8888
> tokens can be found in terminal

## 🚩 Credits  
Developer: Yupeng Lei  
  
Thanks to Cristian Borcea@NJIT, Hessam Mohammadi@NJIT  
  
  
## 🚩 License  
The MIT License
