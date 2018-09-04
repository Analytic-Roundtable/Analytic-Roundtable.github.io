---
layout: tangerine
title: Test Client
---

# Test Client and Scenarios

Usage: 

<pre>
java -jar client.jar
   command args [options]
</pre> 

The CLASSPATH must include "./lib/`*" which represents all the client.jar dependencies.

```
# Inventory operations  
client.jar (analytics | collections | outputs) \
   [SERVER_OPTIONS --count]  

# Record count for a collection  
client.jar collection <id> [SERVER_OPTIONS  --count ]  

# Record for an analytic  
client.jar analytic <name> [SERVER_OPTIONS  --count ]  

# Insert data  
client.jar insert <file> <analyticName> \
    [--uuid <uniqueIdentifier> 
     --entity <entityName>  
     --key <key>  
     SERVER_OPTIONS]  
  
# Drop a collection  
client.jar drop <collectionId> [SERVER_OPTIONS]  
  
# Invoke a Flora Reasoner query  
client.jar reason <configuration> <ontology> <queries> \
    [--outputFormat <type> SERVER_OPTIONS ]  
  
#Where SERVER_OPTIONS are the optional arguments 
# [--host <hostname> --port <port>].  

```

All arguments and options are:  

```
Command:      
  analytics    List supported analytics on the 
                  Tangerine Server.      
  analytic     Retrieve datamap for the analytic.      
  collections  List data collections on 
                  Tangerine server.      
  outputs      List output formats supported by 
                  the Tangerine server for returning 
                  reasoner responses.      
  reasoner     Leverage the reasoner to query the data 
                  using a specified ontology.      
  insert       Insert data into a specific collection 
                  using a specific analytic  

Command Arguments:      
  --key <key>, -f <key>  
           Key to use when resolving entity.     
  --uuid <uniqueIdentifier>, -u <uniqueIdentifier>  
           Unique identifier of entity.      
  --entity <entity>, -e <entity>  
           Entity to resolve.      
  --outputFormat <type>, -o <type>  
           Output format of reasoner response 
  --count  
           Only return the number of items.  

Options:      
  --host <hostname>  
       Tangerine host server name or IP address. 
  --port <port>  
       Port number Tangerine Server is running on. 
  --version  
       Show version.      
  -h, --help  
       Show this screen.
```
## Use Case #1 Test Scenario

This quick summary of uses of the test client only show command line invocation
for discrete operations.&nbsp; To make more sense of how to apply this in a
particular use case, consult [Use Case #1 Demonstration]({{ site.baseurl }}{%
link tangerine/demo.md  %}) 

<pre style="font-size: 11px">

// Insert data.  Capture the reported "collection" ID 
// as <i><b>P1</b></i>. We may use this variable to refer 
// to the collection rather than a literal string
 
 java -jar client.jar insert ./one-claim.csv \ 
   org.mitre.tangerine.analytic.VoucherAdapter

<i><b>>> P1</b></i>

// Confirm collection, by counting records
  
  java -jar client.jar collection P1 -count
  
// Try extracting postal addresses or other entities 
// using the means you have available (e.g., NetOwl 
// in our case), then insert the results against that 
// collection ID the UUID <i><b>X</b></i> in this 
// case is the identity of the row of data being processed.

  java -jar client.jar insert results/P1_entities.xml \
       org.mitre.tangerine.analytic.NetOwlAdapter \   
       --entity entity:address:mail --uuid <i><b>X</b></i>

</pre>
