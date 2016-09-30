# <center>Develop a Stream Handler for Cisco CSA</center>

<b>Introduction about Cisco® Connected Streaming Analytics (CSA) </b><br>

Cisco® Connected Streaming Analytics (CSA) is an analytics platform that delivers predictive, actionable insights from high-velocity streams of live data.

* Streaming query processing supports active, continuous monitoring of live data. This provides instantaneous, real-time analysis and action, as well as efficient use of computing resources. 
* CSA’s framework and interfaces are ideal for use case development across a wide variety of business and network management functions and industries. 
* CSA provides real-time insights into big data views to support actionable events and dynamic dashboards to help you get more value out of your data. 

<font color='red'>Request access to the Data Learning Platform by sending a message to:</font> [datalearningplatform@cisco.com](mailto:datalearningplatform@cisco.com)

## Lab Overview

In this Learning Lab, you will learn how to develop CSA custom handlers for using CSA in our DLP platform.<br>
Our platform has Kafka messaging framework working from the backend. This utility will take the IP, Port and the Topic details of Kafka messaging system. The application will listen to a local socket continuously and will push the stream from this socket to the Kafka. Our sample Java code for handling the log data stream. This java file needs to mention in the XML configuration file.

![Figure](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/csa.jpg?raw=true)

## Lab Objective

* Building custom handler for CSA in DLP and analyze the data at real time. 

## Prerequisites

* knowledge on Java 1.6 or above.
* knowledge on SQL query.
* knowledge using GitHub.
* Basic knowledge of XML.
* Chrome Browser.


### Now we are going to demo for a web server log Analysis step by step.

In this Web Server Log Analysis demo, we are going to use a Log Simulator, CSA Engine and the customised handler. First, we need to create the environment. We need to start the Log simulator and CSA engine. This can be done through the configuration file which will build the handler.
Basically the full process we can split into 3 major sections.

</br>
* Section A: Setup The CSA Engine and Log Simulator.
* Section B: Coding and configure the customised CSA Handler.
* Section C: The Visualisation section with Zeppelin.

### Section A: Setup The CSA Engine and Log Simulator

<b>Step 1:</b> Explore Data Learning Platform(DLP)

<font color='red'>Request access to the Data Learning Platform by sending a message to:</font> [datalearningplatform@cisco.com](mailto:datalearningplatform@cisco.com) 
</br>

<b>Step 2:</b> After login into DLP platform go to the <b>App Stack Hub</b> and click on Stack library tab then click on <b>CSA_user</b> stack.
</br>
Two micro-services are under this stack. These are </br>
a) logsimulator </br>
b) trucq </br>

Now we need to start both of this micro service..<br>
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/StartService.PNG?raw=true)

Click on the Green arrow button for starting both the micro services.

![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/runMicroservices.png?raw=true)

Running state of two micro services:
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/CSA_6.png?raw=true)

<b>Step 3:</b> After running Trucq, we will get IP and port. The First IP and port for SQL query to CSA Engine those will vary in every startup.</br>
For example:</br>

```
     10.10.10.92:11841	    // 11841 is the SQL query Listener Port
```
N.B : This IP and Port will be required in <b>Step 8 and Step 13</b>
</br></br>
### Section B: Writing the customized CSA Handler and configurations

<b>Step 4:</b> <b>Select CSA customize handler "wksp-csa-handler"</b> and click on <b>"Launch"</b>
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/CSAWorkSpaceSelection.PNG?raw=true)

On clicking on <b>Launch</b> button, the IDE will be launched based on workspace.
![Figure](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/csa-IDE.PNG?raw=true)

<b>Step 5:</b> All the basic configurations are written in “include-handler.xml” file. Find this file in below location: <b>CsaCustomHandler-->build-->tmp-->include-handler.xml.</b> Double click on it and open it in right panel.<br>

![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/csaHandlerPNG.png?raw=true)

<b>Step 6:</b> In the “include-handler.xml” file set the kafka Topic and Kafka Zookeeper IP and Port and change the name of the custom class which we are going to develop. Here handler java class name is ETLHandler.java.

```
	<topic>CiscoDDP</topic>     // Change the Kafka Topic here.
	<arguments>
 		<arg name="zookeeper.connect">172.16.10.8:2181/kafka</arg>  //Configure IP & Port
	</arguments>
	<custom class="custom.handlers.ETLHandler” </custom>        
	//Set the Handler Java Class which we are going to code next step
```

<b>Step 7 :</b> Sample Java class for CSA handler is placed in below path. Here we named it as ETLHandler.<br>
<b>CsaCustomHandler --> customizations --> src --> ETLHandler.java </b>

![alt-tag](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/ETLHandlerClass.PNG?raw=true)

<b><u>Sample Coding Exercise</u></b><br>

```
package custom.handlers;

import org.apache.commons.configuration.SubnodeConfiguration;
import com.cisco.pa.handlers.model.DataRecord;
import com.truviso.system.handlers.AbstractEntryHanlder;
import com.truviso.system.handlers.HandlerException;

public class ETLHandler extends AbstractEntryHanlder<DataRecord, DataRecord> {
	String string;
	public ETLHandler(SubnodeConfiguration c) {
		super(c);
	}
	@Override
	public void init() throws HandlerException {
		super.init();
        try {
        	string = config.getString("string", "POST");
               } catch (IllegalArgumentException e) {}
	}
	@Override
	public void handle(DataRecord record) throws HandlerException {

		try {
			if (null != record) {
				if (record.toString().contains(string))
					resultListener.handle(record);
			}

		      } catch (Exception ex) {throw new HandlerException(ex);}}}
```



<b>Step 8:</b> Above Truecq IP and Port number details are required to set the handler. We need to update the configuration file.<br> Open the IDE and double click on the below file

<b>CsaCustomHandler-->customizations-->instances-->local-runtime.properties</b></br>
We will get the Trucq port number from <b>Step 3</b>

![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/aaaaa.png?raw=true)

<b>Step 9:</b>In this step we need to stop the handler first. In the top of the IDE we can select stop from the combo. 
![Figure](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/step13.jpg?raw=true)

<b>Step 10:</b>In this step we need to build our handler. In the top of the IDE we can select build from the combo.
![Figure](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/step14.jpg?raw=true)

<b>Step 11:</b>In this step we need to Start our handler to select Run. In the top of the IDE we can select run from the combo.
![Figure](https://raw.githubusercontent.com/prakdutt/data-dev-learning-labs/master/labs/develop-stream-handler-cisco-csa/assets/images/step15.jpg)

Here We finished all the configurations and coding lession.In the next section we will see the visualization.
</br></br>
**The Visualising of the data using Zeppelin is described in next section. Please visit next section for details.**

