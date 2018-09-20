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
        
Using Ubuntu 16.04, walk through the following APT package installs. The critical software dependencies include: 
 - Java 8.x
 - Maven
 - Tomcat 8 
 - MongoDB

See [tangerine/install-deb] (https://github.com/Analytic-Roundtable/tangerine/blob/master/install-deb)
