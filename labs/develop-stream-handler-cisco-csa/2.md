### Section C: The Visualization section with Zeppelin.

<b>Step 12:</b> Now we can start Zeppelin for visualization. In the Data Repository we will get the  </>Drill button.</br>
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/ZepplineSelection.PNG?raw=true)

1. In the popup frame with Zeppelin and Jupyter as options, click Zeppelin.
2. Follow the pop-out chrome page to begin the interactive analysis and visualization using Zeppelin

![alt-tag](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/selectZappline.PNG?raw=true)

Browser may block Zeppline. In this case, allow browser to open Zeppelin by selecting the <b>Always allow pop-up from http://xxx.xxx.xxx.xxx</b> and click on <b>Done</b> button.
<b>IP address may differ based on server</b>
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/popUpBlockerAllowed.PNG?raw=true)
3. On allowing popup blocker, Zeppelin notebook will open in another tab.
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/welcome-to-zeppelin.png?raw=true)


Note: You can use the top-right tool buttons to do corresponding configurations (e.g., set paragraph width, copy visual report link, etc.) when necessary.

<b>Step 13:</b> We need to configure Zeppelin. When the Trucq micro service is running, we need to collect the IP and Port from the End Point for SQL query listener.</br>
We will get the Trucq port number from <b>Step 7</b>
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/CSA_4.png?raw=true)

Now we need to create a new Zeppelin Notebook for CSA and edit the PSQL configuration with below mentioned parameters.<br>

Click <b>Interpreter</b> from Zepplin and reach <b>psql</b> section. After clicking on <b>Edit</b> button, edit the respective details given in below and click on <b>Save</b> button. 
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/ZapplineConfigurationRestartImage.png?raw=true) </br>

```
postgresql.driver.name    :  org.postgresql.Driver
postgresql.max.result     :  1000
postgresql.password	  : 
postgresql.url		  :  jdbc:postgresql://10.10.10.92:11841/cqdb
postgresql.user	          :  trucq

```

After clicking on <b>Save</b> button, click the <b>OK</b> button for final updation. </br>
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/ZapplineConfigurationUpdate.PNG?raw=true)

After setting the above value, click on the <b>Restart</b> button.
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/ZapplineConfigurationRe.PNG?raw=true) </br>
<b>Above settings in Zeppelin, helps to configure it with Postgresql database. We can apply SQL queries on Zeppelin for interacting with Postgresql database and display output in graphical format. We need to configure a Zeppelin notbook editor where we can insert SQL queries. Below steps describe the process of configuring Zeppelin notebook.</b> 
</br></br>
<b> Develop in Zeppelin notebook. </b>

1. On the Zeppelin homepage, create your own notebook by click on &quot;Create new note&quot;.
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/welcome-to-zeppelin-notebook.png?raw=true)

2. Create and name your new notebook in the pop up dialog.
![Figure](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/create-note.png?raw=true)

3. In your newly created notebook, a typical Zeppelin interactive development and visualization working environment.

![alt-tag](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/ZapplineIntf.PNG?raw=true)


<b>Step 14:</b> After restarting the configuration we can execute the SQL queries to the CSA engine and plot the graph according to data stream. 
Till now, we have configured the process of reading log data from multiple Web servers located in different location. In below, we will do the query to view the log data using sql query on web server's log data which are stored in postgresql database(configured in above steps). User can learn the process of log status from log data using sql query and display the data in different format(table/graph) as per their choice. 

```
%psql
select * from apachelog.sapachelog_archive order by access_time DESC limit 300
```
Input above sql query in te Zeppelin and execute the query by clicking on the Execute button(marked with Red color box).
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/sqlinZeppelin.PNG?raw=true)

This query will show the output as below. It is showing the web server's log server data from CSA engine. These log data are stored in the postgresql database which is mentioned in above step. 
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/ZepplinePreview.png?raw=true)

On clicking on the Settings icon(marked in above image), we can drag and drop the fields as mentioned in below screen and display the output as graph format. User can change the graph based on their choice. 
![Figure](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/develop-stream-handler-cisco-csa/assets/images/zeppelinSqlQurery.png?raw=true)


### Things to Try

Developers can build their own application for the Run Time Visualization, CSA engine or Trucq support Restful web services and also support SQL queries to fetch the data from the Engine.

### Reference:
1.	 [http://www.cisco.com/c/dam/en/us/products/collateral/analytics-automation-software/streaming-analytics/connected-streaming-analytics-aag.pdf](http://www.cisco.com/c/dam/en/us/products/collateral/analytics-automation-software/streaming-analytics/connected-streaming-analytics-aag.pdf)

2.	[http://www.cisco.com/c/dam/en/us/products/collateral/analytics-automation-software/streaming-analytics/connected-streaming-analytics.pdf](http://www.cisco.com/c/dam/en/us/products/collateral/analytics-automation-software/streaming-analytics/connected-streaming-analytics.pdf)
 


## <center>Thank You</center>
