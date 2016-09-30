# Network data ingestion process into DLP


# **Introduction about ingestion of network data in real-time using Kafka in Hadoop platform**

Computer network is a telecommunication process which allows computers or devices to exchange data between each other using data pipeline and those devices are controlled by wired or wireless medium. Those devices are keep alive by exchanging data between each other in a continuous way. 
</br>
These network data provides the inside details detail about health and communication performance between of two devices which are communicating. We can extract lots of valuable information from those data set if we can capture those data in real time way. 
</br>
Below example will provide a way to learn the process of ingesting network data into Hadoop environment and perform transformation and extract and display values from there in a analytical tool called Tableau.
# **Lab Overview**

A data collection server, shown in the diagram below, is collecting data in real time from the local network. The data collected by the Server is working with a Client residing in DLP to transfer the network data collected through Kafka. Using Kafka socket code, we are making a connection to the client and capture the network data and send it to a Kafka topic. From this topic, data will be moved to HDFS by a Consumer program. With the data present in HDFS. The diagram shows how exactly network data flows from a local network through Kafka in HDFS. 

![alt tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/flow1.png?raw=true)

In this lab, the network stream data is generated from network traffic simulator. From DLP platform, user can access it directly. The steps for creating a network stream is described below. 

<font color='red'>Request access to the Data Learning Platform by sending a message to:</font> [datalearningplatform@cisco.com](mailto:datalearningplatform@cisco.com)

# Lab Objectives
* How to configure ingest network streaming data.
*	Learn the process of configuring Kafka and network traffic simulator.
* Visualise network data from DLP's platform.

# Prerequisites

*	Knowledge on Hadoop to store data.
*	Basic knowledge of Kafka.
*	Chrome Browser.

# Lab Settings

<b>"Data Repository"</b> section is allowing you to create network real-time data stream. Kafka's producer will push the Network traffic generated data to Kafka cluster and Consumer will consume that data and save that into HDFS in real-time.

<b>N.B.</b>DLP platform provide a default Kafka's Producer, Consumer and Network traffic generator using network traffic simulator. User can select there own network data and use DLP provided Kafka's component to process the network data. User can define and deploy their own service also. 
</br>
# Step 1: Configuring KAFKA for live Stream. </br>
For live stream data ingestion into DLP platform, we need to configure KAFKA. For doing this follow the below steps. </br>
</br>
1. Click on <b>Import New Data</b> button from <b>Data Repository</b> tab.
![network-data](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData.PNG?raw=true)
2. It will open a entry form where user need to set the KAFKA and NTSERVER. 
![network-data](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData2.PNG?raw=true)
*Follow below instructions for entering details in above import data entry form.*
<b> 
name</b>-> Any text as a name </br>
<b>Type </b>-> It is a drop-down list box. Select <b>network</b> from the list. </br>
<b>Select Streaming Data Processing Service</b> -> Select default value from the list. </br>
<b>TOPIC</b> -> Change the topic name as <b>DDP_user_2</b>. If your login id is <b>user_2</b>. If your login id if <b>user_3</b>, then the value of this field would be <b>DDP_user_3</b>. </br>
<b>Description </b> -> Put some details about your live stream. </br>
**Keep the default value of KAFKA and NTSERVER. Don't change the text against these two fields.**

# Step 2: Create Stack for Configuring Consumer in DLP Platform. </br>
Consumer will consume network data and help to preserve into DLP. Please follow the below steps for creating Stack and configuring Consumer.</br>
1. Click on <b>Create Stack</b> button from <b>App Stack Hub</b>. </br>
![network-data](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData4.PNG?raw=true)
2. Create Stack Entry form will open. Enter the details as below. </br>
<b>Stack name</b>-> Enter any text as a Stack name.</br>
<b>Rack Host</b>-> Select <b>sh_rack_1</b> </br>
<b>Running Platform</b>->Select <b>Mesos</b> from the radio button. </br>
<b>Stack Icon</b>-> Select <b>Common</b> from the list box. </br>
<b>Description</b>->Enter description data as a description of this Stack. </br>
![network-data](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData5.PNG?raw=true)
3. Drag and drop <b>network-stream</b> and <b>ntconsumer</b> into the Canvas from <b>DataSource List</b> and <b>Service List</b> section. </br>
![network-data](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData6.PNG?raw=true)
4. Click on <b>network-stream</b> and then click on <b>Config</b> button. <b>Config</b> button is on right side of the screen. This will open an application Configuration window where we need to set below values. </br>
a. <b>Memory(MB)</b> -> Set <b>256</b> as a memory space. </br>
b. <b>TOPIC</b> -> Change the Topic name as <b>DDP_user_2</b>. Here <b>user_2</b> is the user id which is used for login. If user login as <b>user_3</b> then this value would be <b>DDP_user_3</b> </br>
c. Click on <b>Submit</b> button.  </br>
*No edit is required for other fields for this learning lab.*
![network-data](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData13.PNG?raw=true)
5. Click on <b>ntconsumer</b> and click on <b>Config</b> button. This will open an application configuration window. User need to set the below mentioned values there. </br>
a. <b>Memory(MB)</b>-> Set <b>256</b> as a memory space. </br>
b. <b>hdfs_address</b> -> Set the Value as hdfs://172.16.10.16:8020/ddp/[user id]/[any text]. If user's login id is <b>user_2</b> and the output file name is <b>livedata</b> then the value of <b>hdfs_address</b> would be hdfs://172.16.10.16:8020/ddp/user_2/livedata.</br>
c. <b>topic_name</b> -> Set the value as <b>DDP_user_2</b>. </br> Here <b>user_2</b> is the user id which is used for login. If user login as <b>user_3</b> then this value would be <b>DDP_user_3</b> </br>
d. <b>user_name</b> -> Set the login id in this field. Here user login as <b>user_2</b>. </br>
e. Click on <b>Submit</b> button. </br>

6. Starting two services from <b>App Stack Hub-> Stack Library</b> </br>
In this step, we will start the services from <b>Stack Library</b>. Follow the below steps.
a. From <b>Stack Library</b>, click on the Stack name which was created in <b>Step2-4</b>. </br>
It will show the two services where <b>Health</b> must be in <b>Stop</b> state. Find the below screen for the reference.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData8.PNG?raw=true)
b. Click the <b>Green Start</b> button to start both services. The status of <b>Health</b> would be in <b>Running</b> stage.</br> Find below image for reference. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData14.png?raw=true)
*This will start ingesting live stream data into DLP platform. User can view the live stream data from* <b>Data Repository</b>.
</br>
c. Click <b>Data Repository</b> and select the file to view the network stream data. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData10.PNG?raw=true).
Click on <b>eye</b> shaped view button to display the network data.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData15.PNG?raw=true)
</br>
7. After viewing the network data from <b>Data Repository</b>, stop the services from <b>App Stack Hub -> Stack Library</b> by clicking on <b>Stop</b> button. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/net-data-ingest-trans/assets/images/importNetworkData12.PNG?raw=true)
