# Step 2: Developing code in IDE
a) On selecting the Workspace and clicking on the Launch button, IDE will open in your browser. Double click on TransformData.java file which will open in the right panel.</br>
Here the sample code is given for network data ingestion. User can edit the code. Build and execute the program from IDE.

![alt tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/ide1.PNG?raw=true)
Below steps are describing the process of packaging and running the sample program. 

b) Select the <b>package</b> and click on <b>Blue</b> button to build. 
   IDE will perform the build process on the selected file. There should not be any error messages in the console window for a successful build process.

![alt tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/ide2.PNG?raw=true)


# Step 3: Executing the Program
We need to perform below settings before we execute the program and generate the result. Below steps describe the process of generating and saving the output from the above program in the Hadoop platform. 
a)	Select the <b>run.sh</b> file from the left panel and double click on it. The content of this file will open in the right panel.
There are three parameters mentioned in this script file. Change the values as described in below and select <b>run</b> and click the execute button to execute the script. </br>
* USER: your current login user name </br>
<b>N.B</b> Enter your login userid. If you login as user_1 then enter user_1 here as USER. </br>
* INPUT: The file name in “Data Repository” section which you want to transform. </br>
<b>N.B:</b> Sample preloaded network data (network_origin.csv) is already saved in HDFS environment. User can use this file for learning purpose. <b>For this learning lab, no need to change this file name.</b> </br>
* OUTPUT: The output file name that your code will generate.  </br>
<b>N.B</b> Enter any name as an output file name. For example, <b>network_transform_result.csv</b> is used as a output file name. Output of the program would be saved in this file and the file would be saved in Hadoop environment directly. <b>Change this file name based on your choice. </b>
 
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/runScriptFile.PNG?raw=true)
N.B: final status: SUCCEEDED indicates that the script ran successfully by the IDE.

After executing the above script, DLP's Cloud IDE will generate the output file and saved directly in the Hadoop platform. We can view the output file using visualisation tool called Tableau.
