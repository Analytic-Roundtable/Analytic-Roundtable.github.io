<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN">
<html>
  <head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7">
    <link href="./css/manual.css" rel="stylesheet" type="text/css"
      media="screen">
    <title>Tangerine Installation</title>
  </head>
  <body>
    <script type="text/javascript" src="./manual.js"></script>
    <script type="text/javascript">
        write_user_sidebar()
    </script>
    <div id="wrapper-content">
      <div id="content">
        <h1>Server and Client Demo Installation</h1>
        <p>This chapter covers both the installation of the server web
          services and the test client with the demonstration scripts
          and data (<a href="#demo">Demo Installation</a>)<br>
        </p>
        <h1>Server Installation</h1>
        <p>Tangerine is currently designed for a J2EE server exposing a
          JAX-RS (RESTful Java Services) interace. The storage engine is
          MongoDB 3.x and in theory could be deployed on other noSQL
          databases with some thought.&nbsp; As of Model 1.0, the
          Tangerine team had a Java-based Flora reasoner that worked on
          MongoDB, so MongoDB was chosen.&nbsp; The installation is
          built out for a Linux platform, however we have demonstrated
          all the components working in development environments on
          Windows and Mac OSX.<br>
        </p>
        <h2>Linux Install: Ubuntu<br>
        </h2>
        <p>Using Ubuntu 16_04, walk through the following YUM package
          installs.&nbsp; The critical requirements are:<br>
        </p>
        <ul>
          <li>latest OS</li>
          <li>Java 8.x</li>
          <li>Python 2.7+ with Pip<br>
          </li>
          <li>Archival tools TAR, Zip, Gzip</li>
          <li>Development tools: Gnu GCC, Python dev libraries, XML/XSLT
            libraries</li>
          <li>Build tools: Ant 1.9, Gradle, Maven 3.x<br>
          </li>
          <li>Runtime tools: Tomcat 8.x<br>
          </li>
        </ul>
        <p><br>
          Commands, with commentary:<br>
        </p>
        <br>
        <font face="Courier New, Courier, monospace">sudo apt-get update<br>
          <br>
          sudo yum install gcc<br>
          sudo yum install zip<br>
          sudo yum install unzip<br>
          sudo yum install
          ant&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
          (version 1.9.2, adds Perl libraries)<br>
          sudo yum install python-devel<br>
          sudo yum install libxml2<br>
          sudo yum install libxml2-devel<br>
          sudo yum install libxslt-devel<br>
          sudo pip install --upgrade lxml<br>
          <br>
          #<br>
          # Install Maven, Tomcat, and MongoDB;&nbsp; <br>
          # Refer to vendor documentation if you wish to further
          automate<br>
          #<br>
          (mkdir /data/build;&nbsp; cd /data/build/)<br>
          <br>
          Verify links here, if they fail.<br>
          <br>
          export http_proxy=http://myproxy:80<br>
          export https_proxy=https://myproxy:80<br>
          <br>
          # Maven<br>
          wget
http://www.gtlib.gatech.edu/pub/apache/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.zip<br>
          <br>
          # Tomcat<br>
          wget
http://apache.mirrors.hoobly.com/tomcat/tomcat-8/v8.5.15/bin/apache-tomcat-8.5.15.zip<br>
          <br>
          cd /opt/<br>
          unzip apache-tomcat-8.5.15.zip<br>
          <br>
          # Tomcat tuning<br>
          #<br>
          sudo apt-get install libapr1-dev libssl-dev<br>
          <br>
          # Download MongoDB for your OS and follow instructions here,
          which <br>
          # may involve configuring your OS to point to a vendor pacakge
          repository online.<br>
          #<br>
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/<br>
          #<br>
          # MongoDB Tuning<br>
https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/<br>
          <br>
          # created and ran&nbsp; disable-transparent-hugepages&nbsp;
          per instructions above.<br>
          sudo ./disable-transparent-hugepages start<br>
          <br>
          #&nbsp; Install Python Pip<br>
          #<br>
          wget https://bootstrap.pypa.io/get-pip.py<br>
          sudo python ./get-pip.py<br>
          sudo pip install -U setuptools <br>
          sudo pip install -U wheel<br>
          <br>
          #&nbsp; Oracle Server JRE 8 ==&gt; /opt/java8<br>
          # <br>
          http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html




          <br>
          - accept agreement<br>
          - Download 64-bit Linux server JRE 8 (8u131)<br>
          <br>
          # copy file to /data/build/<br>
          cd /opt/<br>
          tar xzf /data/build/jdk-8u131-linux-x64.tar.gz <br>
          sudo mv&nbsp; jdk1.8.0_131 java8 </font>
        <p> <br>
        </p>
        <h2>Linux Services</h2>
        <p>First establish some predictable environment for your install</p>
        <p><tt>export JAVA_HOME=/opt/java8</tt><tt><br>
          </tt><tt>export CATALINA_HOME=/opt/tomcat</tt><tt><br>
          </tt><tt>export CATALINA_BASE=/opt/Tangerine/server</tt><tt><br>
          </tt></p>
        <p><tt># Capture these variables in your shell environment <br>
            # wherever you invoke Java<br>
          </tt></p>
        <p>Independently, start the services<br>
        </p>
        <blockquote>
          <p><tt>sudo service mongod start</tt><tt><br>
            </tt></p>
        </blockquote>
        <p>and Tomcat:</p>
        <blockquote>
          <p><tt>/opt/tomcat/bin/startup.sh</tt><tt><br>
            </tt><tt># Or</tt><tt><br>
            </tt><tt>/opt/tomcat/bin/shutdown.sh</tt><tt><br>
            </tt></p>
        </blockquote>
        <p>If you use root user to start/stop the Tomcat server, then
          always use that method.<br>
        </p>
        <h2>Demo Client Connectivity</h2>
        <p>From the server, confirm you can run a MongoDB shell
          locally.&nbsp; However, access to MongoDB is limited to the
          web services, as clients have no direct interface to the
          database here:<br>
        </p>
        <blockquote>
          <p><tt>mongo localhost/tangerine</tt><tt><br>
            </tt> </p>
          <tt><b> </b></tt>
          <p><tt># The shell should confirm the server and client
              version of MongoDB</tt><tt><br>
            </tt><tt> # And then "show dbs" command lists available
              databases. "tangerine" DB</tt><tt><br>
            </tt><tt> # is created automatically on connect.</tt></p>
          <tt><b> </b></tt>
          <p><tt>&gt; show dbs</tt><tt><br>
            </tt><tt> </tt><tt><b><br>
              </b></tt><tt><b> </b></tt><tt><b><i>admin&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

                  0.000GB</i></b></tt><tt><b><i><br>
                </i></b></tt><tt><b><i>local&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

                  0.000GB</i></b></tt><tt><b><i><br>
                </i></b></tt><i><tt><b>tangerine&nbsp; 0.001GB</b></tt><br>
            </i></p>
          <br>
        </blockquote>
        <h1><a name="demo"></a>Demo Installation</h1>
        <h2>1. First Build and Configure your setup</h2>
        <p>Optionally use the <tt><b>build</b></tt> option to build
          Tangerine from scratch and prepare the demonstration. The
          server install above is required prior to running this.&nbsp;
          The primary demonstration is located at <tt><b>./demo/Fraud,Waste,Abuse-Demo</b></tt><br>
        </p>
        <pre><font size="+1">&nbsp;&nbsp;&nbsp; ./configure.sh [build]</font></pre>
        <p> And now for all subsequent operation, note that some
          additional Python 2.x libraries are used<br>
          for demo execution.&nbsp; For convenience all such libraries
          are installed using Pip locally in <b><font face="Courier
              New, Courier, monospace">piplib</font></b>.<br>
          <br>
        </p>
        <pre>&nbsp;&nbsp;<font size="+1">&nbsp; # TANGERINE is where you have checkout or installed this client code<br>&nbsp;&nbsp; FWA_DEMO=$TANGERINE/demo/Fraud,Waste,Abuse-Demo<br>&nbsp;&nbsp; export PYTHONPATH=$FWA_DEMO/piplib:$FWA_DEMO/apps/esri</font></pre><h2>2. Data Inputs and Outputs<br></h2><p>The project has fabricated data in single CSV master files, <tt><b>./data/AllClaims.CSV</b></tt> and ./data/Person.csv.&nbsp;&nbsp; Additionally, interim data files will be found at:</p><ul><li><tt>working</tt> - temporary files<br></li><li><tt>config</tt> - various generated configuration files used by Tangerine internals<br></li><li><tt>results</tt> - AE results per record of data<br></li></ul><h2>3. Field Tangerine Server</h2><p>Please refer to Server Installation above. Follow the installation instructions to deploy Tangerine webapp (tangerine.war) on a Tomcat 8.x server.&nbsp; This server could be on your laptop (aka localhost) or a remote server. Wherever that server is, please note the hostname as <i>TANGERINE_SERVER</i>.&nbsp; The default port is 8080 and is not part of the TANGERINE_SERVER value.&nbsp; That server installation also involves setting up a local MongoDB 3.x server, which is not referenced here at all because all databasing work is managed through the Tangerine web service.&nbsp; However, if you are interested look at the data in Mongo after a few runs of this demo pipeline.<br><br></p><h2>4. Record Analytic Tool Configuration</h2><ul><li>NetOwl server is required for this demonstration to run. Please note this as the base URL, <i>NETOWL_URL</i> in the form <font face="Courier New, Courier, monospace"><b>http://server:port</b></font></li><li>ESRI ArcGIS online services are used.&nbsp; If you run the demo pipeline behind a firewall, set shell variables <font face="Courier New, Courier, monospace"><b>http_proxy</b></font> and&nbsp; <font face="Courier New, Courier, monospace"><b>https_proxy </b></font>as <i><font face="Courier New, Courier, monospace">PROXYHOST:PORT </font></i>or as you see fit</li></ul><h2>5. Running the Demonstration</h2><p>The demonstration pipeline makes use of the Tangerine Test Client, aka <b><font face="Courier New, Courier, monospace">client.jar</font></b><br>for interacting with the Tangerine Server.&nbsp; The interaction with NetOwl is managed<br>by the <b><font face="Courier New, Courier, monospace">netowlapp.jar</font></b>.&nbsp; Esri integration occurs solely through the python script, <b><font face="Courier New, Courier, monospace">apps/esri/esri_travel_calculator.py. </font></b>So these JAR files must be in the local directory as a result of running the <tt>configure.sh</tt> script before continuing.<br><br>Running the entire demonstration on a single Claim data file is helpful to understand the <br>combined data analytics that occur on a "unit" of data -- a unit being here a <b><u>single claim</u></b>.<br></p><p>You are now ready to review the <a href="file:///Users/ubaldino/workspace/Roundtable/Tangerine-Master/doc/demonstration-fwa.htm">Demonstration Pipeline</a> section and run some analytics.&nbsp; This essence of that pipeline pulls together the above bits of information:<br>
</p><tt>&nbsp;&nbsp; # Run claims data through the demo:</tt><tt><br></tt><tt>&nbsp;&nbsp; #&nbsp;&nbsp; provide remote Tangerine server,</tt><tt><br></tt><tt>&nbsp;&nbsp; #&nbsp;&nbsp; URL for NetOwl,</tt><tt><br></tt><tt>&nbsp;&nbsp; #&nbsp;&nbsp; And clean output folders prior to run.</tt><tt><br></tt><tt>&nbsp;&nbsp; #<br>   &nbsp;&nbsp; python ./uc1.py --clean </tt><tt>\<br>&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; --server TANGERINE_SERVER \</tt><tt><br>&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; --netowl-server NETOWL_URL</tt><tt> \<br>&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; --claims ./data/AllClaims.csv --pii ./data/Person.csv </tt><font size="+1">  </font><p>The above invocation generates interim output in <b>output</b> folder, with a final<br>result for this claim in <b>results. </b>Configurations used for processing or queries may end up in configurations.<br></p></div>
    </div>
  

</body></html>