---
layout: tangerine
title: Tangerine Transfer Services
---

# Transfer Services REST API
The Transfer Services API is depicted in the AE Model 1.0 design document. 
This limited demonstration provides four major functions:
 - **submit** to ingest data
 - **query** to retrieve result sets
 - **fetch** to retrieve full documents
 - **remove** to delete or redact documents and or entire collections
            
The top level web application URL is of the form: 

> http://(server):(port)/tangerine/(***operation***)

The *operations* are listed below in these four functional categories. "@arg" arguments are parameters that tune the operation, where "@path-arg" are part of the URL path and provide context. "@input" or "@output" fields are optional, e.g., a GET operation has no input, whereas POST and PUT do.

## Data Model
        
All persisted data is stored in a Knowledge Store or Knowledge Base (KB). For the purposes of demonstration submitted data sets are funneled into their own KB collection, and any enrichment through processing, attaching assertions, etc. is also contained within that collection. In actual production settings, KB design could be done quite differently. 
        
Here are examples of assertions that are the result of processing a record. A UUID is assigned to records when ingested. From there assertions link together identities representing subjects and objects using the simple model below.

```
{
   "A": {
     "P": "a",
     "S": "VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_2",
     "O": "sumo#Human"
   }
}
```
          
The "Response" from transfer services has the following output schema, which may be XML returned by the REST calls, but is just as easily formatted as JSON. The content is more important than the format. The fields in a Response are:
 - message
 - error
 - errorMessage
 - dataType
 - collection
 - assertions
 - numberOfAssertions
        
For example, the insertion of data reports back a collection ID. Other fields default to empty strings if there is nothing useful to report. 

```
{ 
  "error":false, 
  "message":"",
  "dataType":"",
  "errorMessage":"",
  "collection":"PI_4dcad001_9a11_4429_8f2b_23d9f11d2ba3_1501703988790",
  "numberOfAssertions":4,
  "assertions":[{"A":{}},{"A":{}},{"A":{}},{"A":{}}]
}
```

## Submit

Insert operations has the form:
        
<pre>

HTTP/PUT
/AETServer/host/insert/(collection) 

<b>@arg type</b> one of "general","esri", "netowl", "pii", "voucher" 
<b>@path-arg  collection</b>: ID or name of the collection 
<b>@input</b> data payload is an application/octet-stream 
<b>@output</b> application/json, based on ResponseModel class

Description:  Insert rows of data or assertions into the KB.

</pre>

## Query

Listing collections has the form:
```
HTTP/GET
/AETServer/host/collections

**No arguments or inputs**

Description: List available collections and their identifiers
```

Inventorying a particular collection, e.g., counting rows, is this:
<pre>
HTTP/GET
/AETServer/host/count/(collection)

<b>@path-arg collection</b>: the ID of the collection.

Description: count rows of data in a collection.

</pre>

*Reasoning* against a conditioned data set involves the "reasoner" function. This demonstrates how a complex query can be sent to the transfer service, which assesses the query leveraging the AE Ontology to extract results. Reasoning-style queries are not formally part of the core Analysis Exchange interface, but does demonstrate the powerful routines that can be applied once the common ontology is in play.
<pre>
HTTP/POST
/AETServer/host/reasoner

<b>@input</b> multipart-form-data, containing a Flora JSON query
<b>@output</b> application/json, based on ResponseModel class

Description: given a reasoner-style query, return the matching assertions.

</pre>

## Fetch

Getting rows of data from a collection has the form:

<pre>
HTTP/GET 
/AETServer/host/elements/(collection)/(limit)

<b>@path-arg collection</b>: the ID of the collection.
<b>@path-arg limit</b>: the maximum number of returned rows.
<b>@output</b>: application/xml, as described by class ResponseModel

Description: the actual data.

</pre>

## Remove

Getting rows of data from a collection has the form:

<pre>
HTTP/DELETE 
/AETServer/host/drop/(collection)

<b>@path-arg collection</b>: the ID of the collection.
<b>@output</b> HTTP/2xx status, if collection is dropped successfully

Description: drop the collection

</pre>
