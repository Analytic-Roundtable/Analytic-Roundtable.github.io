---
layout: tangerine
title: Demonstration
---


# Use Case Demonstration: Fraud, Waste and Abuse

The Fraud, Waste and Abuse use case was designed to illustrate
multiple analytics working together on data enrichment and then
on interpretation to flag potential fraud. This portion of
the demonstration is focused on the data enrichment,
specifically:
 1. raw claims data ingestion and adaptation
 2. data joins to re-associate relational data
 3. extraction and coding of names, addresses, and monetary
values from semi-structured data
 4. calculation of approximate travel distances and times

The enrichment activity happens in roughly that order and
results in a single row of data with the pertinent dollar
amounts, names, identities, and claimed travel time and
distance. The final step for this exercise to export the
enrichment to a single combined CSV to be used to share with
other use case developers.

The data set is 190 travel voucher claims for reimbursable
travel. The demonstration pipeline walks through the
Analysis Exchange (AE) mechanics step by step for a single claim
at a time. This surely could be optimized in various ways,
but we devised this scripted approach to illustrate the key
tasks leveraging the AE web services via Tangerine. The AE
Knowledge Store component is referred to several times, because
it is the central place where all the given and derived
assertions aka "knowledge" are stored, linked, queried, etc.

# Demo Realities
The demonstration is aimed at a data scientist, a data
modeler, a system integrator, or some other type of
information technologist. It consists of a Tangerine
Server as prescribed in our installation section. The
components facing the user here are the Python pipeline code
and the Java Test Client code. While it does seem
obscure to have the Python code call the Java program to call
the RESTful Tangerine Server, it is for now a working
solution. For scripting client side capabilities, something
like Groovy would make life even simpler capturing the best of
Python's scriptability with Java's formality.

And so the number of hops between interfaces -- data files
in, REST calls out, saving REST responses as temporary data
files, and back and forth, etc -- is somewhat unavoidable. No
matter what one does, this will be a complicated chaining of
tasks. In time this will all become easier, especially
if we are going beyond the context of pure demonstration.


# Demo Setup
Refer to the [Installation]{{site.baseurl }}{% link tangerine/install.md  %}) Section.


# Demo Pipeline Logic
The logic for the automating this use case is in the script 
 <tt>./demo/Fraud,Waste,Abuse-Demo/pipeline.py</tt>.

In all command invocations of the Tangerine Test Client, the
arguments <tt>-host localhost -port 8080</tt> are assumed as
they are the default. Let's assume we are processing the
claims data = <tt>data/AllClaims.csv </tt>and the companion
identifying data,<tt> ./data/Person.csv</tt>

The demonstration starts with a list of claims; the
description of the analytic exchanges in steps 1 through 8
below operates on a single claim, e.g., the pipeline(file)
function consumes a file with one record. For the
sake of development, the ingest and processing of a single
claim is captured in a Tangerine database <b><i>collection</i></b>
dedicated to that claim.

The primary unit of data dealt with inside Tangerine is an <b>
<i>assertion</i></b>: a subject-predicate-object tuple that
describes a relationship between data elements using the AE
Ontology. Each step below is noted with the relevant
phase of AE services is addressed.


# 1. INGEST AND ADAPT CLAIM VOUCHER DATA

The ingest phase demonstrates how single records are parsed and
adapted as they are submitted to the Transfer Services.

<b>PHASE</b>: INGEST  
<b>COMMAND</b>: java -jar client.jar insert  
./one-record.csv org.mitre.tangerine.analytic.VoucherAdapter  
<b>RESULT</b>: Raw claim is parsed and inserted into
collection with a generated ID, <tt>VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840</tt>  
  
<b>JSON REPRESENTATION OF ADAPTED VOUCHER</b>:
```
{
 "dataType": "",
 "numberOfAssertions": 46,
 "errorMessage": "",
 "collection":
"VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840",
 "assertions": [ 
 {
 "A": {
 "P": "a",
 "S":
"VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_2",
 "O": "sumo#Human"
 }
 },
 {
 "A": {
 "P": "a",
 "S":
"VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_3",
 "O":
"AE#PostalAddress"
 }
 },
..... /* Followed by 44 more assertions */

``` 

# 2. QUERY CLAIM VOUCHER DATA TO WORK FROM ADAPTED VOUCHER

Flora is a semantic reasoning language used here to facilitate
data queries against complex ontologies.
A templated query is formed and back-filled with the CLAIM
collection ID aka <font face="Courier New, Courier, monospace">CLAIM_UUID</font>
  
<b>PHASE</b>: QUERY  
<b>INPUT</b>: config/flquery-config-voucher.json  
<b>COMMAND</b>:   


<pre>

java -jar client.jar reason \
 
config/flquery-config-voucher.json \
  config/AE.flr \
  configvoucher.qry</font>

</pre>

<b>RESULT</b>: working/ReasonerNetOwl.json now contains
selected data for CLAIM


# 3. PARSE QUERY RESULT INTO USABLE ASSERTIONS
Next, we retrieve the assertion identifiers for related data --
that is the name(s), address(es) and expense amounts into data
arrays to pass to downstream analytics NetOwl and Esri
travel calculator.

<b>PHASE</b>: ADAPTATION / INTERPRETATION OF QUERY RESULTS

```

# Some Python code to illustrate navigating a <b><i>Flora</i></b> query result, 
# which is a JSON formatted response

names = []
namesUUID = []
addresses = []
addressesUUID = []
expenses = []
expensesUUID = []
for datalist in data["dataList"]:
 if "sumo#Human" in datalist["query"]:
  for resultlist in
datalist["resultList"]:
   for
result in resultlist["result"]:
  
 if "?S" in result["key"]:
  
 
namesUUID.append(result["val"])
  
 if "?o" in result["key"]:
  
 
names.append(result["val"])
 if "AE#PostalAddress" in
datalist["query"]:
  for resultlist in
datalist["resultList"]:
   for
result in resultlist["result"]:
  
 if "?S" in result["key"]:
  
 
addressesUUID.append(result["val"])
  
 if "?o" in result["key"]:
  
 
addresses.append(result["val"])
 if "AE#VATravelVoucher" in
datalist["query"]:
  for resultlist in
datalist["resultList"]:
   for
result in resultlist["result"]:
  
 if "?S" in result["key"]:
  
 
expensesUUID.append(result["val"])
  
 if "?o" in result["key"]:
  
 
expenses.append(result["val"])
```

# 4. FOR EACH NAME, ADDRESS & EXPENSE DETECT/PARSE/NORMALIZE FURTHER YIELDING NEW "VALUE-ADDED" ASSERTIONS

While we have a data field called "ClaimantName" in the original
data, we may have other name fields or the value in those fields
my contain complex names, hyphenation, abbreviation, etc.
NetOwl is a named entity extractor that provides some deeper
analysis of these snippets of text (it provides more value on
longer texts, of course). The fields teased apart here are
names, addresses, and expenses.

<b>PHASE</b>: ADAPTATION OF ENTITY EXTRACTION

<b>COMMAND(S)</b>:

<pre>
 java -jar netowlapp.jar -server
NETOWL_URL -text <i>ClaimaintName</i>
 java -jar netowlapp.jar -server
NETOWL_URL -text <i>Address</i>
 java -jar netowlapp.jar -server
NETOWL_URL -text <i>Expense</i>
</pre> 
  
<b>INTERMEDIATE RESULT</b>: for each text value found, the
NetOwl output in XML is saved to a file named after the
assertion ID associated with that subject/value pair, e.g.,
>./output/<ClaimaintName_UUID>_netowlapp.xml 

Above NetOwl may uncover new distinct entities, parse fields
better, or normalized the data that was there. The result
is that more data is now available for our analysis of the
claim, but first this output must be linked to the original
claim data. 

Consider <b><font face="Courier New, Courier, monospace">"$13"</font></b>
appears in given data. The original expense data has an
assertion UUID
NetOwl detects something like <b><font face="Courier New,
Courier, monospace">MONEY = ( quantity="13.00",
currency="USD" )</font></b>.
This new normalized data is then linked to the original expense
assertion using the <font face="Courier New, Courier,
monospace">-insert </font>operation below. 

Example data: 
<font face="Courier New, Courier, monospace">
 "Expense" = "$13",
 "Expense_UUID" =
VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_0</font>

Finally, since we have the analytic output in XML files (mainly
for ease of inspection), but the values have to be excised from
the analytic output and linked with our original subject through
the new assertions.

<b>COMMAND</b>: 

```
java -jar client.jar insert
./output/<ClaimaintName_UUID>_netowlapp.xml \
 
org.mitre.tangerine.analytic.NetOwlAdapter \
  --entity "entity:person"
--uuid <ClaimaintName_UUID>

 java -jar client.jar insert
./output/<Address_UUID>_netowlapp.xml \
 
org.mitre.tangerine.analytic.NetOwlAdapter \
  --entity
"entity:address:mail" --uuid <Address_UUID>

 java -jar client.jar insert
./output/<Expense_UUID>_netowlapp.xml \
 
org.mitre.tangerine.analytic.NetOwlAdapter \
  --entity
"entity:currency:money" --uuid <Expense_UUID>

```
  
<b>RESULT</b>: New value-added assertions are added to the
AE Knowledge Store  

  
# 5. IDENTIFY ITEMIZED EXPENSES
Next Flora is used again to compose a query to retrieve
currency/monetary data from the particular claim. The
resulting instances of currency are trivially associated with
the claim as being "itemized expenses". The data specifics
for the query are in the JSON file.

<b>COMMAND</b>: 
```
java -jar client.jar reason \
 
config/flquery-config-voucher.json \
  config/AE.flr \
  config/currency.qry
```
  
<b>RESULT</b>: working/ReasonerCurrency.json

The result is parsed and new assertion with the Boolean flag
"hasItemizedExpense" is asserted.
This assertion is staged in <b>./working/currency.txt</b>, then
loaded with the test client. The following assertion is an
example of what this data linking looks like.
```
{"A" : 
 { 
 "S" :
"VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840_0", 
 "P" : "AE#hasItemizedExpense", 
 "O" :
"NO_2937adad_0685_4a2e_b3e4_b5ea4d9471d4_1506546051047_id1"}
}
```
  
<b>COMMAND</b>: 

```
java -jar client.jar insert working/currency.txt \
 
    org.mitre.tangerine.analytic.GeneralAdapter</font>
```
  
<b>RESULT</b>: final boolean assertion is made and saved to
Knowledge Store.


# 6. ASSOCIATE PII TO CLAIM
  
<b>PHASE</b>: INGEST
  
<b>COMMAND</b>: 
  
```
java -jar client.jar reason \
 
config/flquery-config-voucher.json \
  config/AE.flr \
  config/pii.qry
```

<b>INTERMEDIATE RESULT</b>: The query results in PII data in the
claim, in particularly social security numbers (SSN). 
  
Next only SSN in the claim data are retrieved from the fake PII
data files. For each SSN found, the more complete person data is
loaded and asserted in the Knowledge Store. Detected SSN have
additional information in CSV files PiiDataset/<SSN>.csv
  
<b>COMMAND</b>: 
```
java -jar client.jar insert working/temp.csv \
 
org.mitre.tangerine.analytic.PiiAdapter --uuid
<PERSON_UUID> \
  --entity SSN --key
<SSN> 
```
  
<b>RESULT</b>: PII data is ingested, amplifying the claimaint's
profile
  
# 7. CALCULATE TRAVEL TIME AND DISTANCE
Given the address information in the claim we will use Esri
Network Analysis route calculations to measure the distance
traveled by car from a residence to a point of service, e.g.,
hospital or health benefits center. Additionally, an estimate of
trip duration is provided. Units are meters for distance
and minutes for drive times.

The relevant fields are queried using Flora, the relevant values
are parsed and fed to an analytic. The result of the
analytic is deciphered and asserted back into the Knowledge
Store.

<b>PHASE</b>: ADAPTATION OF GEODETIC CALCULATIONS

<b>COMMAND</b>:

```
java -jar client.jar reason \
 
config/flquery-config-voucher.json \
  config/AE.flr \
  config/esri.qry
```
  
<b>RESULT</b>: The query result contains UUID for claim data
that have a non-null origin and destination. 
  
The Python script <tt><b>esri_travel_calculator.py</b></tt> can
either be run from the command line or as a library call.
This routine is used to return the following. The Python library
call is used here, as the pipeline script is already
Python. Responses are temporarily parked in <b><font
face="Courier New, Courier, monospace">output/<i>TRAVEL_UUID</i>_esri.csv
</font></b>
<pre>
from <b>esri_travel_calculator</b> import
drive_time_and_distance, write_result
for travel,origin,destination in
zip(travelling,origins,destinations):
 travel_csv =
os.path.join('output',travel+'_esri.csv')
 travel_calc = None
 with open(travel_csv, 'wb') as fh:
  travel_calc = <b>drive_time_and_distance</b>(
origin, destination )
  <b>write_result</b>(fh,travel_calc)
</pre> 
  
<b>COMMAND</b>: 

```
java -jar client.jar insert output/<i>TRAVEL_UUID</i>_esri.csv \  
  org.mitre.tangerine.analytic.EsriAdapter \
   --uuid TRAVEL_UUID --entity "AE#Travelling"
```



# 8. FINAL ASSEMBLED OUTPUT
The demonstration is not yet done -- just this portion of data
enrichment. The intermediate work done here is primarily
enrichment with mostly factual or objective assertions. 
Assessing potential fraudulent claims is far more subjective and
will involve additional analytics provided by <b>IBM</b> and <b>SAS</b>
analysis suites.
  
<b>PHASE</b>: QUERY, EXPORT
  
<b>COMMAND</b>:
  
```
java -jar client.jar reason \
 
results/<CLAIM_UUID>.json \
  config/AE.flr \
  config/final.qry \
  -o org.mitre.tangerine.adapter.outbound.CsvAdapter
```
   
<b>RESULT</b>: The response is saved locally to a file <tt>
./results/CLAIM_UUID_final.csv</tt>, for example <tt>results/VO_dd0c519a_7867_48d7_b369_36b2061026d4_1506546040840.csv</tt>

The contents may resemble something like (a sampling of about 40
fields from the actual output):

<table width="644" height="577" cellspacing="2" cellpadding="2"
border="1">
<tbody>
<tr>
<th valign="top" bgcolor="#ff9900"><font size="+1"><b>FIELD</b><b>
</b></font></th>
<th valign="top" bgcolor="#ff9900"><font size="+1"><b>VALUE</b><b>
</b></font></th>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">beneficiaryHasArrestRecordBoolean</font></td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">false
</font> </td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">beneficiaryHasLiensBoolean</font></td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">true
</font> </td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">beneficiaryHasDeclaredBankruptcyBoolean</font></td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">false
</font> </td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">itemizedExpense
</font> </td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">$11.10
</font> </td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">originState</font></td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">CA
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
Courier, monospace">originCity
</font> </td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">San Diego
</font> </td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">destinationFullAddress
</font> </td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace"> 2790 Truxton Road, Suite 130, San
Diego, CA 92106 </font></td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">distanceUnitOfMeasure</font></td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">meters
</font> </td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">timeUnitOfMeasure</font></td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">minutes
</font> </td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">expectedDistanceValue</font></td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">8771.6
</font> </td>
</tr>
<tr>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">expectedTimeValue</font></td>
<td valign="top"><font size="+1" face="Courier New,
Courier, monospace">9.22
</font> </td>
</tr>
</tbody>
</table>


