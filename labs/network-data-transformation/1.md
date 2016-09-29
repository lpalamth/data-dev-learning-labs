# Network data ingestion process into DLP and Transformation

# **Introduction about Network data and ingestion of network data in real-time**

The Computer network is a telecommunication process which allows computers or devices to exchange data between each other using data pipeline and those devices are controlled by the wired or wireless medium. Those devices are kept alive by exchanging data between each other in a continuous way. 
</br>
These network data provide the inside details about communication performance between of two devices which are communicating. We can extract lots of valuable information from those data set if we can capture those data in real time way. 
</br>
Below example will provide a way to learn the process of ingesting network data into Hadoop environment and perform transformation and extract and display values from there in an analytical tool called Tableau.
# **Lab Overview**

A data collection server, shown in the diagram below, is collecting data in real time from the local network. The data collected by the Server is working with a Client residing in DLP to transfer the network data collected through Kafka. Using Kafka socket code, we are making a connection to the client and capture the network data and send it to a Kafka topic. From this topic, data will be moved to HDFS by a Consumer program. With the data present in HDFS, we can then further transform it using our program and visualise the data before and after the transformation in different chart format such as pie chart, bar chart etc. using Tableau tool. The diagram shows how exactly network data flows from a local network through Kafka in HDFS and gets transformed. 

![alt tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/flow1.png?raw=true)

In this lab, the network stream data is already pre-created. From DLP platform, the user can access it directly. The steps for creating a network stream is described below. 

<font color='red'>Request access to the Data Learning Platform by sending a message to:</font> [datalearningplatform@cisco.com](mailto:datalearningplatform@cisco.com)

# Lab Objectives

*	How to get network data from the HDFS. 
*	Learn the process of transform network data by creating a transform function using DLP's IDE.
* Learn how to save a file to HDFS and visualise data.

# Prerequisites

*	Knowledge on Hadoop to store the network data.
*	Basic knowledge of how spark works.
*	Chrome Browser.

# Lab Settings

<b>"Data Repository"</b> section is allowing you to create network real-time data stream. Kafka's producer will push the Network traffic generated data to Kafka cluster and Consumer will consume that data and save that into HDFS in real-time.
From HDFS, we can visualise the data using visualisation tool. This application will allow you to use the existing Kafka's Producer & Consumer function to ingest your real-time network data into HDFS environment.

<b>N.B.</b> DLP platform provide a default Kafka's Producer, Consumer and Network traffic generator. The user can select their own network data and use DLP provided Kafka's component to process the network data. User can define and deploy their own service also. 

# Step 1: Explore Data Learning Platform (DLP)

Workspace is a working zone for the developer. For each programming practice, developer has to create a different workspace from where a user can start practising the programming languages which can work on top of Hadoop platform using Cloud based IDE. 

For network data transformation task, select below-mentioned workspace with sample code.

1. From "Development Hub", select pre-defined workspace called <b>"wksp-transform"</b>
2. Click on  <b>"launch"</b> button. It will open the cloud IDE on another tab.
![alk-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/WorkSpaceSelection.PNG?raw=true)
