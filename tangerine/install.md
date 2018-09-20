---
layout: tangerine
title: Installation
---

# Server and Client Demo Installation
This chapter covers both the installation of the server web services and the test client with the demonstration scripts and data (see [Demo]({{ site.baseurl}}{% link tangerine/demo.md  %})
        
# Server Installation

Tangerine is currently designed for a web server exposing a RESTful interace.
The web server uses MongoDB as the backend; however, it is possible to extend
the prototype to use a different database.

The Tangerine team used a Java-based Flora reasoner that worked on MongoDB, so
MongoDB was chosen. The installation is built out for a Linux platform.
However, it should be possible to deploy the prototype on any operating system.

## Linux Install: Ubuntu
        
Using Ubuntu 16.04, walk through the following APT package installs. The
critical software dependencies include: 
 - Java 8.x
 - Maven
 - Tomcat 8 
 - MongoDB

Note that the script below:
 - Does not take into consideration network proxy settings
 - Installs the prototype to the home directory

```
#add mongodb repository https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/

sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update

sudo apt-get install -y git openjdk-8-jdk maven tomcat8 mongodb-org

cd ~
git clone https://github.com/Analytic-Roundtable/tangerine.git
cd tangerine/Tangerine
mvn compile install

sudo cp ~/tangerine/Tangerine/server/target/tangerine.war  /var/lib/tomcat8/webapps/
cd ~/tangerine/Tangerine/server/
sudo mkdir -p /usr/share/tomcat8/inbound; for f in `find adapters/analytics | grep jar`; do sudo cp $f /usr/share/tomcat8/outbound ; done
sudo mkdir -p /usr/share/tomcat8/outbound; for f in `find adapters/analytics | grep jar`; do sudo cp $f /usr/share/tomcat8/inbound ; done


sudo chown tomcat8:tomcat8 /usr/share/tomcat8/inbound/
sudo chown tomcat8:tomcat8 /usr/share/tomcat8/outbound/

systemctl start mongod
systemctl enable mongod
systemctl start tomcat
systemctl enable tomcat
```

The client folder contains the client side interface to the webserver. To
invoke the client the following command should be used. 

```

java -cp
~/tangerine/Tangerine/client/lib/*:~/tangerine/Tangerine/client/target/client.jar
org.mitre.tangerine.client.TangerineTester --help

Usage:
  client.jar (analytics | collections | outputs)  [--host <hostname> --port <port> --count]
  client.jar collection <id> [--host <hostname> --port <port> --count ]
  client.jar analytic <name> [--host <hostname> --port <port> --count ]
  client.jar insert <file> <analyticName> [--uuid <uniqueIdentifier> --entity <entityName>  --key <key>  --host <hostname> --port <port>]
  client.jar drop <collectionId> [--host <hostname> --port <port>]
  client.jar reason <configuration> <ontology> <queries> [--outputFormat <type> --host <hostname> --port <port>]
  client.jar (-h | --help)
  client.jar --version

Arguments:
  analytics  List supported analytics on the Tangerine Server.
  analytic  Retrieve datamap for the analytic.
  collection  Get the elements in a specific collection.
  collections  List data collections on Tangerine server.
  outputs  List output formats supported by the Tangerine server for returning reasoner responses.
  reasoner  Leverage the reasoner to query the data using a specified ontology.
  insert  Insert data into a specific collection using a specific analytic; optionally, create connections.
Options:
  --key <key>, -f <key>  Key to use when resolving entity [default: ].
  --uuid <uniqueIdentifier>, -u <uniqueIdentifier>  Unique identifier of entity [default: ].
  --entity <entity>, -e <entity>  Entity to resolve [default: ].
  --outputFormat <type>, -o <type>  Output format of reasoner response [default: org.mitre.tangerine.adapter.outbound.JsonAdapter].
  --count  Only return the number of items.
  --host <hostname>  Tangerine host server name or ip. [default: localhost]
  --port <port>  Port number Tangerine Server is running on. [default: 8080]
  --version  Show version.
  -h, --help  Show this screen.

```
