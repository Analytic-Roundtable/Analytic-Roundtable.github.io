---
layout: tangerine
title: Installation
---

# Server and Client Demo Installation
This chapter covers both the installation of the server web services and the test client with the demonstration scripts and data (see [Demo]({{ site.baseurl}}{% link tangerine/demo.md  %})
        
# Server Installation

Tangerine is currently designed for a J2EE server exposing a JAX-RS (RESTful Java Services) interace. The storage engine is MongoDB 3.x and in theory could be deployed on other noSQL databases with some thought. As of Model 1.0, the Tangerine team had a Java-based Flora reasoner that worked on MongoDB, so MongoDB was chosen. The installation is built out for a Linux platform, however we have demonstrated all the components working in development environments on Windows and Mac OSX.
        </p>
## Linux Install: Ubuntu
        
Using Centos 7, walk through the following YUM package installs. The critical requirements are:
 - latest OS
 - Java 8.x
 - Python 2.7+ with Pip
 - Archival tools TAR, Zip, Gzip
 - Development tools: Gnu GCC, Python dev libraries, XML/XSLT libraries
 - Build tools: Ant 1.9, Gradle, Maven 3.x
 - Runtime tools: Tomcat 8.x
          
Commands, with commentary:
        
``` 
sudo yum install gcc
sudo yum install zip
sudo yum install unzip
sudo yum install ant #(version 1.9.2, adds Perl libraries)
sudo yum install python-devel
sudo yum install libxml2
sudo yum install libxml2-devel
sudo yum install libxslt-devel
sudo pip install --upgrade lxml

#
# Install Maven, Tomcat, and MongoDB; 
# Refer to vendor documentation
#

# Install Python Pip
#

wget https://bootstrap.pypa.io/get-pip.py
sudo python ./get-pip.py
sudo pip install -U setuptools 
sudo pip install -U wheel



#
# Install Java 8.x 
# Refer to vendor documentation
#


```

## Demo Client Connectivity
From the server, confirm you can run a MongoDB shell locally. However, access to MongoDB is limited to the web services, as clients have no direct interface to the database here:

```
> mongo localhost/tangerine
# The shell should confirm the server and client version of MongoDB
# And then "show dbs" command lists available databases. "tangerine" DB
# is created automatically on connect.
> show dbs
<b><i>admin 0.000GB</i></b>
<b><i>local 0.000GB</i></b>
<b><i>tangerine 0.001GB</i></b>

```

# Demo Installation
## 1. First Build and Configure your setup
Optionally use the > **build** option to build Tangerine from scratch and
prepare the demonstration. The server install above is required prior to
running this. The primary demonstration is located at **./demo/Fraud,Waste,Abuse-Demo**

> ./configure.sh [build]

And now for all subsequent operation, note that some additional Python 2.x libraries are used for demo execution.

```
# TANGERINE is where you have checkout or installed this client code 
export FWA_DEMO=$TANGERINE/demo/Fraud,Waste,Abuse-Demo 
export PYTHONPATH=$FWA_DEMO/piplib:$FWA_DEMO/apps/esri
```
## 2. Data Inputs and Outputs

The project has fabricated data in single CSV master files, **./data/AllClaims.CSV** and **./data/Person.csv**. Additionally, interim data files will be found at:
 1. working
 2. temporary files
 3. config 
 4. various generated configuration files used by Tangerine internals
 5. results - AE results per record of data

## 3. Field Tangerine Server

Please refer to Server Installation above. Follow the installation instructions to deploy Tangerine webapp (tangerine.war) on a Tomcat 8.x server. This server could be on your laptop (aka localhost) or a remote server. Wherever that server is, please note the hostname as *TANGERINE_SERVER*. The default port is 8080 and is not part of the TANGERINE_SERVER value. That server installation also involves setting up a local MongoDB 3.x server, which is not referenced here at all because all databasing work is managed through the Tangerine web service. However, if you are interested look at the data in Mongo after a few runs of this demo pipeline.

## 4. Record Analytic Tool Configuration

 - NetOwl server is required for this demonstration to run. Please note this as the base URL, *NETOWL_URL*> in the form:
 > http://server:port
 - ESRI ArcGIS online services are used. If you run the demo pipeline behind a firewall/proxy, set shell variables: 
 > http_proxy
 > https_proxy 

## 5. Running the Demonstration

The demonstration pipeline makes use of the Tangerine Test Client, a.k.a,
**client.jar**, for interacting with the Tangerine Server. The interaction
with NetOwl is managed by the **netowlapp.jar**. Esri integration occurs solely
through the python script, **apps/esri/esri_travel_calculator.py**.So these JAR
files must be in the local directory as a result of running the
**configure.sh** script before continuing. Running the entire demonstration on
a single Claim data file is helpful to understand the combined data analytics
that occur on a "unit" of data -- a unit being here a **<u>single claim</u>**. You are now ready to review the (see [Demo]({{ site.baseurl}}{% link tangerine/demo.md  %}) section and run some analytics. This essence of that pipeline pulls together the above bits of information:

```
# Run claims data through the demo:
#     provide remote Tangerine server,
#     URL for NetOwl, 
#     And clean output folders prior to run.
#    

python ./uc1.py --clean \ 
       --server TANGERINE_SERVER \  
       --netowl-server NETOWL_URL \  
       --claims ./data/AllClaims.csv --pii ./data/Person.csv 

```

The above invocation generates interim output in **output** folder, with a
final result for this claim in *results*. Configurations used for processing or queries may end up in configurations.
