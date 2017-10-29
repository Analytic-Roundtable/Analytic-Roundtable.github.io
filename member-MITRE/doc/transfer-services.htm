<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN">
<html>
  <head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7">
    <link href="./css/manual.css" rel="stylesheet" type="text/css"
      media="screen">
    <title>Tangerine Transfer Services</title>
  </head>
  <body>
    <script type="text/javascript" src="./manual.js"></script>
    <script type="text/javascript">
        write_user_sidebar()
    </script>
    <div id="wrapper-content">
      <div id="content">
        <h1>Transfer Services REST API</h1>
        <p>The Transfer Services API is depicted in the AE Model 1.0
          design document. <br>
          This limited demonstration provides four major functions:<br>
        </p>
        <ul>
          <li><b>submit</b> to ingest data</li>
          <li><b>query</b> to retrieve result sets</li>
          <li><b>fetch</b> to retrieve full documents</li>
          <li><b>remove</b> to delete or redact documents and or entire
            collections</li>
        </ul>
        <p>The top level web application URL is of the form <tt><i>http://(server):(port)/tangerine</i></tt>/(<b><i>operation</i></b>).&nbsp;&nbsp;





          The <i>operations</i> are listed below in these four
          functional categories.&nbsp; "@arg" arguments are parameters
          that tune the operation, where "@path-arg" are part of the URL
          path and provide context.&nbsp; "@input" or "@output" fields
          are optional, e.g., a GET operation has no input, whereas POST
          and PUT do.<br>
        </p>
        <h2>Data Model<br>
        </h2>
        <p>All persisted data is stored in a Knowledge Store or
          Knowledge Base (KB).&nbsp; For the purposes of demonstration
          submitted data sets are funneled into their own KB collection,
          and any enrichment through processing, attaching assertions,
          etc. is also contained within that collection.&nbsp;&nbsp; In
          actual production settings, KB design could be done quite
          differently. <br>
        </p>
        Here are examples of assertions that are the result of
        processing a record. A UUID is assigned to records when
        ingested. From there assertions link together identities
        representing subjects and objects using the simple model below.
        <br>
        <font face="Courier New, Courier, monospace"><br>
          &nbsp;&nbsp;&nbsp; {<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "A": {<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "P": "a",<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "S":
          "VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_2",<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "O": "sumo#Human"<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }<br>
          &nbsp;&nbsp;&nbsp; }<br>
          <br>
          <br>
        </font>The "Response" from transfer services has the following
        output schema, which may be XML returned by the REST calls, but
        is just as easily formatted as JSON.&nbsp; The content is more
        important than the format.&nbsp; The fields in a Response are:<br>
        <ul>
          <li>message</li>
          <li>error</li>
          <li>errorMessage</li>
          <li>dataType</li>
          <li>collection</li>
          <li>assertions</li>
          <li>numberOfAssertions</li>
        </ul>
        <br>
        For example, the insertion of data reports back a collection ID.
        Other fields default to empty strings if there is nothing useful
        to report. <br>
        <font face="Courier New, Courier, monospace"><br>
          { "error":false, "message":"","dataType":"",
          "errorMessage":"",<br>
          &nbsp;
          "collection":"PI_4dcad001_9a11_4429_8f2b_23d9f11d2ba3_1501703988790",<br>
          &nbsp; "numberOfAssertions":4,<br>
          &nbsp; "assertions":[{"A":{}},{"A":{}},{"A":{}},{"A":{}}]}</font>
        <blockquote><tt><font face="Courier New, Courier, monospace"><br>
            </font></tt></blockquote>
        <p> </p>
        <h2>Submit</h2>
        <p>Insert operations has the form:<br>
        </p>
        <blockquote>
          <pre><font size="+1">HTTP/PUT<br>/AETServer/host/insert/(collection) <br><br>@arg <b>type</b>: one of "general", "esri", "netowl", "pii", "voucher" <br>@path-arg  <b>collection</b>: ID or name of the collection <br>@input data payload is an application/octet-stream <br>@output: application/xml, based on RespnoseModel class<br>Description:  Insert rows of data or assertions into the KB<br></font></pre><font size="+1">
</font></blockquote><font size="+1">
</font><h2>Query<br></h2><p>Listing collections has the form:<br></p>
     <blockquote><pre><font size="+1">HTTP/GET<br>/AETServer/host/collections<br>No arguments or inputs.<br><br>Description: List available collections and their identifiers</font><br></pre></blockquote><p>Inventorying a particular collection, e.g., counting rows, is this:<br></p><blockquote><pre><font size="+1">HTTP/GET<br>/AETServer/host/count/(collection)<br>@path-arg collection: the ID of the collection.<br><br>Description: count rows of data in a collection.<br></font><br><br></pre></blockquote><p><i>Reasoning</i> against a conditioned data set involves the "reasoner" function.&nbsp; This demonstrates how a complex query can be sent to the transfer service, which assesses the query leveraging the AE Ontology to extract results.&nbsp;&nbsp; Reasoning-style queries are not formally part of the core Analysis Exchange interface, but does demonstrate the powerful routines that can be applied once the common ontology is in play.<br></p><blockquote><pre><font size="+1">HTTP/POST<br>/AETServer/host/reasoner<br>@input multipart-form-data, containing a Flora JSON query<br>@output: application/xml, based on RespnoseModel class<br><br>Description: given a reasoner-style query, return the matching assertions.<br></font></pre></blockquote><font size="+1">

</font><h2>Fetch<br></h2><p>Getting rows of data from a collection has the form:<br></p>

  <blockquote><pre><font size="+1">HTTP/GET <br>/AETServer/host/elements/(collection)/(limit)<br>@path-arg collection: the ID of the collection.<br>@path-arg limit: the maximum number of returned rows.<br>@output: application/xml, as described by class ResponseModel<br><br>Description: the actual data.</font></pre></blockquote>

<h2>Remove<br></h2><p>Getting rows of data from a collection has the form:<br></p>


  
<blockquote>
  <pre><font size="+1">HTTP/DELETE <br>/AETServer/host/drop/(collection)<br>@path-arg collection: the ID of the collection.<br>@output: HTTP/2xx status, if collection is dropped successfully<br><br>Description: drop the collection</font></pre></blockquote><p><br></p>

<p><br></p>
      </div>
    </div>
  

</body></html>