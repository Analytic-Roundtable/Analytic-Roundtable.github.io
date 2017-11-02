<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN">
<html>
  <head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7">
    <link href="./css/manual.css" rel="stylesheet" type="text/css"
      media="screen">
    <title>Analysis Exchange / Use Case #1: Fraud, Waste and Abuse</title>
    <meta name="author" content="MITRE">
    <meta name="description" content="look at claims data processing in
      search of potential wrong doing">
  </head>
  <body>
    <script type="text/javascript" src="./manual.js"></script>
    <script type="text/javascript">
        write_user_sidebar()
    </script>
    <div id="wrapper-content">
      <div id="content">
        <h1>Use Case Demonstration: Fraud, Waste and Abuse</h1>
        The Fraud, Waste and Abuse use case was designed to illustrate
        multiple analytics working together on data enrichment and then
        on interpretation to flag potential fraud.&nbsp; This portion of
        the demonstration is focused on the data enrichment,
        specifically:<br>
        <ol>
          <li>raw claims data ingestion and adaptation</li>
          <li>data joins to re-associate relational data</li>
          <li>extraction and coding of names, addresses, and monetary
            values from semi-structured data</li>
          <li>calculation of approximate travel distances and times</li>
        </ol>
        The enrichment activity happens in roughly that order and
        results in a single row of data with the pertinent dollar
        amounts, names, identities, and claimed travel time and
        distance. The final step for this exercise to export the
        enrichment to a single combined CSV to be used to share with
        other use case developers.<br>
        <br>
        The data set is 190 travel voucher claims for reimbursable
        travel.&nbsp; The demonstration pipeline walks through the
        Analysis Exchange (AE) mechanics step by step for a single claim
        at a time.&nbsp; This surely could be optimized in various ways,
        but we devised this scripted approach to illustrate the key
        tasks leveraging the AE web services via Tangerine.&nbsp; The AE
        Knowledge Store component is referred to several times, because
        it is the central place where all the given and derived
        assertions aka "knowledge" are stored, linked, queried, etc.<br>
        <h1>Demo Realities</h1>
        <p>The demonstration is aimed at a data scientist, a data
          modeler, a system integrator, or some other type of
          information technologist.&nbsp; It consists of a Tangerine
          Server as prescribed in our installation section. The
          components facing the user here are the Python pipeline code
          and the Java Test Client code.&nbsp; While it does seem
          obscure to have the Python code call the Java program to call
          the RESTful Tangerine Server, it is for now a working
          solution. For scripting client side capabilities, something
          like Groovy would make life even simpler capturing the best of
          Python's scriptability with Java's formality.<br>
        </p>
        <p>And so the number of hops between interfaces -- data files
          in, REST calls out, saving REST responses as temporary data
          files, and back and forth, etc -- is somewhat unavoidable. No
          matter what one does, this will be a complicated chaining of
          tasks.&nbsp; In time this will all become easier, especially
          if we are going beyond the context of pure demonstration.<br>
        </p>
        <h1>Demo Setup</h1>
        <p>Refer to the <a href="install.htm">Installation</a> Section.<br>
        </p>
        <h1>Demo Pipeline Logic</h1>
        <p>The logic for the automating this use case is in the script <br>
          &nbsp;&nbsp;&nbsp; <tt>./demo/Fraud,Waste,Abuse-Demo/pipeline.py</tt>.&nbsp;
          <br>
          In all command invocations of the Tangerine Test Client, the
          arguments <tt>-host localhost -port 8080</tt> are assumed as
          they are the default.&nbsp; Let's assume we are processing the
          claims data = <tt>data/AllClaims.csv </tt>and the companion
          identifying data,<tt> ./data/Person.csv</tt><br>
          <br>
          The demonstration starts with a list of claims;&nbsp; the
          description of the analytic exchanges in steps 1 through 8
          below operates on a single claim, e.g., the pipeline(file)
          function consumes a file with one record.&nbsp;&nbsp; For the
          sake of development, the ingest and processing of a single
          claim is captured in a Tangerine database <b><i>collection</i></b>
          dedicated to that claim.<br>
          <br>
          The primary unit of data dealt with inside Tangerine is an <b>
            <i>assertion</i></b>: a subject-predicate-object tuple that
          describes a relationship between data elements using the AE
          Ontology.&nbsp; Each step below is noted with the relevant
          phase of AE services is addressed.<br>
        </p>
        <h2>1. INGEST AND ADAPT CLAIM VOUCHER DATA<br>
        </h2>
        The ingest phase demonstrates how single records are parsed and
        adapted as they are submitted to the Transfer Services.<br>
        <br>
        <b>PHASE</b>: INGEST<br>
        <b>COMMAND</b>:&nbsp; java -jar client.jar insert
        ./one-record.csv org.mitre.tangerine.analytic.VoucherAdapter<br>
        <b>RESULT</b>:&nbsp; Raw claim is parsed and inserted into
        collection with a generated ID, <tt>VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840</tt><br>
        <br>
        <b>JSON REPRESENTATION OF ADAPTED VOUCHER</b>:<br>
        <br>
        <font face="Courier New, Courier, monospace">{<br>
          &nbsp; "dataType": "",<br>
          &nbsp; "numberOfAssertions": 46,<br>
          &nbsp; "errorMessage": "",<br>
          &nbsp; "collection":
          "VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840",<br>
          &nbsp; "assertions": [&nbsp; <br>
          &nbsp;&nbsp;&nbsp; {<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "A": {<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "P": "a",<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "S":
          "VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_2",<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "O": "sumo#Human"<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }<br>
          &nbsp;&nbsp;&nbsp; },<br>
          &nbsp;&nbsp;&nbsp; {<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "A": {<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "P": "a",<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "S":
          "VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_3",<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "O":
          "AE#PostalAddress"<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }<br>
          &nbsp;&nbsp;&nbsp; },<br>
          ..... /*&nbsp; Followed by 44 more assertions&nbsp; */<br>
          <br>
        </font>
        <h2>2. QUERY CLAIM VOUCHER DATA TO WORK FROM ADAPTED VOUCHER</h2>
        <br>
        Flora is a semantic reasoning language used here to facilitate
        data queries against complex ontologies.<br>
        A templated query is formed and back-filled with the CLAIM
        collection ID aka <font face="Courier New, Courier, monospace">CLAIM_UUID</font><br>
        <br>
        <b>PHASE</b>: QUERY<br>
        <b>INPUT</b>: config/flquery-config-voucher.json<br>
        <b>COMMAND</b>: <br>
        <br>
        <font face="Courier New, Courier, monospace">&nbsp;&nbsp;&nbsp;&nbsp;



          java -jar client.jar reason \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          config/flquery-config-voucher.json \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/AE.flr \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; configvoucher.qry</font><br>
        <b><br>
          RESULT</b>:&nbsp; working/ReasonerNetOwl.json now contains
        selected data for CLAIM<br>
        <br>
        <h2>3. PARSE QUERY RESULT INTO USABLE ASSERTIONS</h2>
        Next, we retrieve the assertion identifiers for related data --
        that is the name(s), address(es) and expense amounts into data
        arrays&nbsp; to pass to downstream analytics NetOwl and Esri
        travel calculator.<br>
        <br>
        <b>PHASE</b>: ADAPTATION / INTERPRETATION OF QUERY RESULTS<br>
        <br>
        <blockquote><font face="Courier New, Courier, monospace"># Some
            Python code to illustrate navigating a <b><i>Flora</i></b>
            query result, <br>
            # which is a JSON formatted response<br>
            names = []<br>
            namesUUID = []<br>
            addresses = []<br>
            addressesUUID = []<br>
            expenses = []<br>
            expensesUUID = []<br>
            for datalist in data["dataList"]:<br>
            &nbsp;&nbsp;&nbsp; if "sumo#Human" in datalist["query"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; for resultlist in
            datalist["resultList"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; for
            result in resultlist["result"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; if "?S" in result["key"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            namesUUID.append(result["val"])<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; if "?o" in result["key"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            names.append(result["val"])<br>
            &nbsp;&nbsp;&nbsp; if "AE#PostalAddress" in
            datalist["query"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; for resultlist in
            datalist["resultList"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; for
            result in resultlist["result"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; if "?S" in result["key"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            addressesUUID.append(result["val"])<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; if "?o" in result["key"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            addresses.append(result["val"])<br>
            &nbsp;&nbsp;&nbsp; if "AE#VATravelVoucher" in
            datalist["query"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; for resultlist in
            datalist["resultList"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; for
            result in resultlist["result"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; if "?S" in result["key"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            expensesUUID.append(result["val"])<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; if "?o" in result["key"]:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
            expenses.append(result["val"])</font><br>
        </blockquote>
        <br>
        <h2>4. FOR EACH NAME, ADDRESS &amp; EXPENSE
          DETECT/PARSE/NORMALIZE FURTHER YIELDING NEW "VALUE-ADDED"
          ASSERTIONS<br>
        </h2>
        While we have a data field called "ClaimantName" in the original
        data, we may have other name fields or the value in those fields
        my contain complex names, hyphenation, abbreviation, etc.&nbsp;
        NetOwl is a named entity extractor that provides some deeper
        analysis of these snippets of text (it provides more value on
        longer texts, of course).&nbsp; The fields teased apart here are
        names, addresses, and expenses.<br>
        <br>
        <b>PHASE</b>: ADAPTATION OF ENTITY EXTRACTION<br>
        <br>
        <b>COMMAND(S)</b>:<br>
        <font face="Courier New, Courier, monospace"><br>
          &nbsp;&nbsp;&nbsp;&nbsp; java -jar netowlapp.jar -server
          NETOWL_URL -text &lt;ClaimaintName&gt;<br>
          &nbsp;&nbsp;&nbsp;&nbsp; java -jar netowlapp.jar -server
          NETOWL_URL -text &lt;Address&gt;<br>
          &nbsp;&nbsp;&nbsp;&nbsp; java -jar netowlapp.jar -server
          NETOWL_URL -text &lt;Expense&gt;</font><br>
        <br>
        <b>INTERMEDIATE RESULT</b>:&nbsp; for each text value found, the
        NetOwl output in XML is saved to a file named after the
        assertion ID associated with that subject/value pair, e.g.,<font
          face="Courier New, Courier, monospace">
          ./output/&lt;ClaimaintName_UUID&gt;_netowlapp.xml </font><br>
        <br>
        Above NetOwl may uncover new distinct entities, parse fields
        better, or normalized the data that was there.&nbsp; The result
        is that more data is now available for our analysis of the
        claim, but first this output must be linked to the original
        claim data. <br>
        <br>
        Consider <b><font face="Courier New, Courier, monospace">"$13"</font></b>
        appears in given data. The original expense data has an
        assertion UUID<br>
        NetOwl detects something like <b><font face="Courier New,
            Courier, monospace">MONEY = ( quantity="13.00",
            currency="USD" )</font></b>.<br>
        This new normalized data is then linked to the original expense
        assertion using the <font face="Courier New, Courier,
          monospace">-insert </font>operation below.&nbsp; <br>
        <br>
        Example data: <br>
        <font face="Courier New, Courier, monospace"><br>
          &nbsp;&nbsp;&nbsp; "Expense" = "$13",<br>
          &nbsp;&nbsp;&nbsp; "Expense_UUID" =
          VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_0</font><br>
        <br>
        Finally, since we have the analytic output in XML files (mainly
        for ease of inspection), but the values have to be excised from
        the analytic output and linked with our original subject through
        the new assertions.<br>
        <br>
        <b>COMMAND</b>: <br>
        <br>
        <font face="Courier New, Courier, monospace">&nbsp;&nbsp;&nbsp;
          java -jar client.jar insert
          ./output/&lt;ClaimaintName_UUID&gt;_netowlapp.xml \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          org.mitre.tangerine.analytic.NetOwlAdapter \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; --entity "entity:person"
          --uuid &lt;ClaimaintName_UUID&gt;<br>
          <br>
          &nbsp;&nbsp;&nbsp; java -jar client.jar insert
          ./output/&lt;Address_UUID&gt;_netowlapp.xml \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          org.mitre.tangerine.analytic.NetOwlAdapter \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; --entity
          "entity:address:mail" --uuid &lt;Address_UUID&gt;<br>
          <br>
          &nbsp;&nbsp;&nbsp; java -jar client.jar insert
          ./output/&lt;Expense_UUID&gt;_netowlapp.xml \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          org.mitre.tangerine.analytic.NetOwlAdapter \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; --entity
          "entity:currency:money" --uuid &lt;Expense_UUID&gt;</font><br>
        <br>
        <b>RESULT</b>:&nbsp; New value-added assertions are added to the
        AE Knowledge Store &nbsp; <br>
        <br>
        <br>
        <h2>5. IDENTIFY ITEMIZED EXPENSES</h2>
        Next Flora is used again to compose a query to retrieve
        currency/monetary data from the particular claim.&nbsp; The
        resulting instances of currency are trivially associated with
        the claim as being "itemized expenses".&nbsp; The data specifics
        for the query are in the JSON file.<br>
        <br>
        <b>COMMAND</b>:&nbsp; <br>
        <font face="Courier New, Courier, monospace">&nbsp;&nbsp;&nbsp;
          java -jar client.jar reason \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          config/flquery-config-voucher.json \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/AE.flr \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/currency.qry<br>
        </font><br>
        <b>RESULT</b>:&nbsp; working/ReasonerCurrency.json<br>
        <br>
        The result is parsed and new assertion with the Boolean flag
        "hasItemizedExpense" is asserted.<br>
        This assertion is staged in <b>./working/currency.txt</b>, then
        loaded with the test client. The following assertion is an
        example of what this data linking looks like.<br>
        <font face="Courier New, Courier, monospace"><br>
          {"A" : <br>
          &nbsp; { <br>
          &nbsp;&nbsp;&nbsp; "S" :
          "VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_0", <br>
          &nbsp;&nbsp;&nbsp; "P" : "AE#hasItemizedExpense", <br>
          &nbsp;&nbsp;&nbsp; "O" :
          "NO_2937adad_0685_4a2e_b3e4_b5ea4d9471d4_1506546051047_id1"}<br>
          }</font><br>
        <br>
        <b>COMMAND</b>: <br>
        <br>
        &nbsp;&nbsp;&nbsp;<font face="Courier New, Courier, monospace">
          java -jar client.jar insert working/currency.txt \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          org.mitre.tangerine.analytic.GeneralAdapter</font><br>
        <br>
        <b>RESULT</b>: final boolean assertion is made and saved to
        Knowledge Store.<br>
        <br>
        <h2>6. ASSOCIATE PII TO CLAIM<br>
        </h2>
        <b>PHASE</b>: INGEST<br>
        <br>
        <b>COMMAND</b>:&nbsp; <br>
        <br>
        <font face="Courier New, Courier, monospace">&nbsp;&nbsp;&nbsp;
          java -jar client.jar reason \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          config/flquery-config-voucher.json \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/AE.flr \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/pii.qry</font><br>
        <br>
        <b>INTERMEDIATE RESULT</b>: The query results in PII data in the
        claim, in particularly social security numbers (SSN). <br>
        <br>
        Next only SSN in the claim data are retrieved from the fake PII
        data files. For each SSN found, the more complete person data is
        loaded and asserted in the Knowledge Store. Detected SSN have
        additional information in CSV files PiiDataset/&lt;SSN&gt;.csv<br>
        <br>
        <b>COMMAND</b>: <br>
        <font face="Courier New, Courier, monospace">&nbsp;&nbsp;&nbsp;
          java -jar client.jar insert working/temp.csv \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          org.mitre.tangerine.analytic.PiiAdapter --uuid
          &lt;PERSON_UUID&gt; \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; --entity SSN --key
          &lt;SSN&gt; </font><br>
        <br>
        <b>RESULT</b>: PII data is ingested, amplifying the claimaint's
        profile<br>
        <br>
        <h2>7. CALCULATE TRAVEL TIME AND DISTANCE</h2>
        Given the address information in the claim we will use Esri
        Network Analysis route calculations to measure the distance
        traveled by car from a residence to a point of service, e.g.,
        hospital or health benefits center. Additionally, an estimate of
        trip duration is provided.&nbsp; Units are meters for distance
        and minutes for drive times.<br>
        <br>
        The relevant fields are queried using Flora, the relevant values
        are parsed and fed to an analytic.&nbsp; The result of the
        analytic is deciphered and asserted back into the Knowledge
        Store.<br>
        <br>
        <b>PHASE</b>: ADAPTATION OF GEODETIC CALCULATIONS<br>
        <br>
        <b>COMMAND</b>:<br>
        <br>
        <font face="Courier New, Courier, monospace">&nbsp;&nbsp;&nbsp;
          java -jar client.jar reason \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          config/flquery-config-voucher.json \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/AE.flr \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/esri.qry</font><br>
        <br>
        <b>RESULT</b>: The query result contains UUID for claim data
        that have a non-null origin and destination.&nbsp; <br>
        <br>
        The Python script <tt><b>esri_travel_calculator.py</b></tt> can
        either be run from the command line or as a library call.&nbsp;
        This routine is used to return the following. The Python library
        call is used here, as the pipeline script is already
        Python.&nbsp; Responses are temporarily parked in <b><font
            face="Courier New, Courier, monospace">output/<i>TRAVEL_UUID</i>_esri.csv<br>
          </font></b><br>
        <blockquote> <font face="Courier New, Courier, monospace">#
            Library that calls Esri's ArcGIS Online route analysis
            service<br>
            from <b>esri_travel_calculator</b> import
            drive_time_and_distance, write_result<br>
            for travel,origin,destination in
            zip(travelling,origins,destinations):<br>
            &nbsp;&nbsp;&nbsp; travel_csv =
            os.path.join('output',travel+'_esri.csv')<br>
            &nbsp;&nbsp;&nbsp; travel_calc = None<br>
            &nbsp;&nbsp;&nbsp; with open(travel_csv, 'wb') as fh:<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp; travel_calc = <b>drive_time_and_distance</b>(
            origin, destination )<br>
            &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp; <b>write_result</b>(fh,




            travel_calc)</font><br>
        </blockquote>
        <b>COMMAND</b>: <br>
        <br>
        <font face="Courier New, Courier, monospace">&nbsp;&nbsp;&nbsp;
          java -jar client.jar insert output/<i>TRAVEL_UUID</i>_esri.csv
          \&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; <br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          org.mitre.tangerine.analytic.EsriAdapter \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; --uuid
          TRAVEL_UUID --entity "AE#Travelling" </font><br>
        <br>
        <br>
        <h2>8. FINAL ASSEMBLED OUTPUT</h2>
        The demonstration is not yet done -- just this portion of data
        enrichment. The intermediate work done here is primarily
        enrichment with mostly factual or objective assertions. <br>
        Assessing potential fraudulent claims is far more subjective and
        will involve additional analytics provided by <b>IBM</b> and <b>SAS</b>
        analysis suites.<br>
        <br>
        <b>PHASE</b>: QUERY, EXPORT<br>
        <br>
        <b>COMMAND</b>:<br>
        <br>
        <font face="Courier New, Courier, monospace">&nbsp;&nbsp;&nbsp;
          java -jar client.jar reason \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
          results/&lt;CLAIM_UUID&gt;.json \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/AE.flr \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; config/final.qry \<br>
          &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; -o
          org.mitre.tangerine.adapter.outbound.CsvAdapter</font><br>
        <br>
        <b>RESULT</b>:&nbsp; The response is saved locally to a file <tt>
          ./results/CLAIM_UUID_final.csv</tt>, for example <tt>results/VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840.csv</tt><br>
        <br>
        The contents may resemble something like (a sampling of about 40
        fields from the actual output):<br>
        <br>
        <table width="644" height="577" cellspacing="2" cellpadding="2"
          border="1">
          <tbody>
            <tr>
              <th valign="top" bgcolor="#ff9900"><font size="+1"><b>FIELD</b><b><br>
                  </b></font></th>
              <th valign="top" bgcolor="#ff9900"><font size="+1"><b>VALUE</b><b><br>
                  </b></font></th>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">beneficiaryHasArrestRecordBoolean</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">false<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">beneficiaryHasLiensBoolean</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">true<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">beneficiaryHasDeclaredBankruptcyBoolean</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">false<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">itemizedExpense<br>
                </font> </td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">$11.10<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">originState</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">CA<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">originFullAddress</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace"> 714 Riverside Rd. San Diego, CA
                  92117</font></td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">originCity<br>
                </font> </td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">San Diego<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">destinationFullAddress<br>
                </font> </td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace"> 2790 Truxton Road, Suite 130, San
                  Diego, CA 92106 </font></td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">distanceUnitOfMeasure</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">meters<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">timeUnitOfMeasure</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">minutes<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">expectedDistanceValue</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">8771.6<br>
                </font> </td>
            </tr>
            <tr>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">expectedTimeValue</font></td>
              <td valign="top"><font size="+1" face="Courier New,
                  Courier, monospace">9.22<br>
                </font> </td>
            </tr>
          </tbody>
        </table>
        <br>
        <br>
      </div>
    </div>
  </body>
</html>
