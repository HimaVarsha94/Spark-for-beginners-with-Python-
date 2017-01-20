I used *virtualenv* since it is my first time installing and I didn't want to mess up my working space. I am installing on virtualenv because I just want to play with Spark as of now. But it is optional and completely based on your personal preference. I do know many who are adverse to using virtualenv, so I leave this to you.

*Optional:*

    pip install virtualenv
    virtualenv spark_workspace
    source spark_workspace/bin/activate

There is another wrapper for this which makes it really use it easily, have a look at [this](http://exponential.io/blog/2015/02/10/install-virtualenv-and-virtualenvwrapper-on-mac-os-x/).

<div id='requirements'/></div>
## 1. Install requirements:

### 1.1 Installing Java:
I am assuming that java is already installed in your system else please follow a detailed instructions booklet to do so.

### 1.2 Installing Scala:
```
brew install scala
```
### 1.3 Install py4j:
```
sudo pip install py4j
```
## 2.1 Install Apache Spark:
Download the recent version of Spark from [Apache Spark](http://spark.apache.org/downloads.html). As of this article's written date, the recent version was spark-2.1.0 with Hadoop 2.7. There is no need of doing ```sbt/sbt assembly``` as the downloaded version already takes care of it for this version.

You can check the working of spark by
```
./bin/run-example SparkPi 10
```
It will return all the log files along with
```
Pi is roughly 3.14042
```
So all is good! Now in order to remove excessive logging, let us go into  
```
cp conf/log4j.properties.template conf/log4j.properties
nano conf/log4j.properties
```
and replace the line:
```
log4j.rootCategory=INFO, console
```
by
```
log4j.rootCategory=ERROR, console
```
This will log only when there is an error which is very convenient.

### 2.2. Setup
```
sudo mv ~/Downloads/spark-2.1.0-bin-hadoop2.7 /opt/
sudo ln -s /opt/spark-2.1.0-bin-hadoop2.7 /opt/spark

```
Add this to bashrc file by first opening the file:
```
nano ~/.bashrc
```
Add these lines at the bottom of the file:
```
export SPARK_HOME=/opt/spark
export PYTHONPATH=$SPARK_HOME/python
```
Restart bash to make use of these changes by running:
```
. ~/.bashrc
```
## 3. Example:
Let us check the working of apache spark. For this, open python console.
If you are using a virtualenv, source that else
```
from pyspark import SparkContext
sc = SparkContext()
```
If this works without throwing an import error, you are good to go.
