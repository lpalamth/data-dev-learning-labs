# **Data Transformation from DLP using Talend**

# **Introduction about Transformation**
<b>Data transformation</b> is the process of converting data or information from one format to another, usually from the format of a source system into the required format of a new destination system. 

# **Lab Overview**
In our learning lab, we are trying to use Talend Open Source Big data tool to perform the transformation operation on CSV data file and save the data directly to Hadoop platform. Source data should be selected from DLP's Hadoop platform and the respective transformation would be applied from DLP's browser. In this learning lab, we will learn the transformation operation in below ways:  </br>

**Section A:** Download and Install Talend Open Studio for Big Data tool.</br>
**Section B:** Develop a Transformation Job using Talend Open Studio for Big Data Tool in user's local computer. </br>
**Section C:** Build Transformation Job using Talend Big Data Tool in user's local computer. </br>
**Section D:** Upload the transformation job in DLP platform.</br>
**Section E:** Execute transformation from DLP platform and visualise the data. </br>

# **Lab Overview**
1)	Using Talend Open Source Big Data Tool to create a ETL(Extraction, Transformation and Load) Job. </br>
2)	Managing (Upload, Execute, Delete, Share) Talend jobs from DLP platform. </br>
3)	Visualize transformed data from DLP platform. </br>

# **Prerequisites**
1) User must have to know the basic knowledgre of ETL. </br>
2) Java 1.7+ should be pre-installed in User's computer. </br>
3) Proper internet connectivity with User's computer. </br>
4) Chrome Browser. </br>

<b>N.B:</b> In below, each section(Section A, B,C,D) are describing in details in step wise manner. User need to follow each step carefully.

**Section A: Download and Install Talend Open Studio for Big Data tool.** </br>
</br>
<b>Step 1: JDK installation in User's computer.</b> </br>
For executing Talend, JDK is required and need to be pre-installed in user's computer. Use the command(java -version) in the command prompt. This command will show the JDK version installed in user's computer. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/javaVersion.PNG?raw=true)
</br>

![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/javaVersionUnix.PNG?raw=true)

If java is not installed, then from the below-mentioned URL, download Java and installed it. </br>
http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

</br>
<b>Step 2: Download Talend Open Studio for Big Data tool.</b> </br>
Visit the below website for downloading the Talend Open Source Big data tool. 
https://www.talend.com/landing-download-ppc/big-data 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/DownloadTalendTool.PNG?raw=true)
Input your details as mentioned on the form and click on <b>Download Now</b> details there and click on button to download the tool. 
</br></br>
<b>Step 3: Unzip the downloaded zip file and Start Talend.</b></br>
Talend tool will be downloaded in a zip file. It will take 10/15 minutes time to download based on your interest speed. On completion of the download, unzip the file and double-click on Talend executable file which will open Talend Open Source Big Data transformation tool.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/CreateTalendJob.PNG?raw=true)
</br></br>
<b>Step 4: Create Talend Project.</b></br>
Execute Talend executable file after unzipping the downloaded Talend tool from talend website. User can create a New Talend Project by selecting <b>Create a New Project.</b> and giving a Project name in the specified text box. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/CreateTalendJob.PNG?raw=true)
This will create a new Talend project and the designer UI will appear. In next steps, the details about the Talend Designer UI are described.
</br></br>
<b>Step 5: Introduction about Talend Designer UI.</b></br>
After creating a new Talend job, the designer UI will appear. The details about the UI are given in below.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/talendUIdesign.png?raw=true)
</br>
**Job Design::** Job Creation Panel for creating a new transformation job. Details of creating new Talend job will be described in next steps.</br>
**Designer Palette::** For designing a new job, the user can use this area to drag and drop different components from Pallate. </br>
**Talend Components Palette::** Talend Open source Big data tool provides 900+ components for different transformation operation. The User can select component(s) from this palette and place those in the canvas area and connect them. Execution flow of job should be done based on the connection of each component which describes the data flow also.
</br>
</br>
**Section B: Develop a Transformation Job using Talend Open Studio for Big Data Tool in user's local computer.**</br></br>
In this section, we will learn the process of creating a new transformation Job using Talend Open Studio for Big data tool. 
**As use case, we will perform a transformation on a CSV file by selecting few specific columns from the source file and save the transformed output file in DLP's hadoop platform by editing some fields.** </br></br>
<b>Step 1: Create a Talend Job.</b></br>
Right click on <b>Job Designs</b> from left panel and click on <b>Create Job</b>
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/createJobStep1.PNG?raw=true)
</br></br>
<b>Step 2: Input Job Name</b></br>
After Step 1, New Job details entry form will appear where user need to input the Job name and details about the job. Click on the <b>Finish</b> button after entering all the necessary details in that form.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/TalendJobNameAndDetails.PNG?raw=true)

This will create a new job. Job name can be viewed under <b>Job Designs</b> section. Job Name is showing in the red marked area in Talend tool.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/TalendjobDisplayingJobDesigns.png?raw=true)
</br></br>
<b>Step 3: Check the raw data file from DLP platform.</b>
We are going to use Users11.csv file as a source file which is already placed in the DLP platform. This CSV file has multiple columns and we need to pickup few columns from this CSV file and generate a new file with data. Below UI is showing Users11.csv file in DLP platform. </br>
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/Users11csvfile.png?raw=true)
</br>
Click on eye shaped <b>View</b> button to view the columns and records of Users11 csv file. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/Users11csvfileRecords.PNG?raw=true)
</br></br>
<b>Step 4: Design a job in Talend tool.</b></br>
In the Talend tool from, drag and drop components in designer canvas from pallate. </br>
**tHDFSConnection :** *This component is use to make a connection with Hadoop platform.* </br>
**tHDFSInput :** *This component is use to read a file from Hadoop platform.* </br>
**tHDFSOutput :** *This component is use to write a file in Hadoop platform.* </br>
**tJavaRow :** *This component is use to write custom java code.*</br>
**tMap :** *This component is use to map fields from two differnet data source.* </br>
<b>N.B :</b>*User can notice that the component name became tHDFSConnection_1. This indicate that there are one tHDFSConnection component placed in the designer area.* </br>
After placing the above mentioned components in the designer area, the UI would be looks like below. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/TalendJobcomponents.PNG?raw=true)

Click on the <b>Contexts(TalendNewJob)</b> tab from the Talend tool. Here <b>TalendNewJob</b> is the talend job name.
Contexts tab is a area where we can define the parameters which we like to pass to talend job. For our talend job, we need to pass four(4) parameters. Click on the <b>+</b> symbol four times and it will create four places for four parameters. Click on each parameter name and change the name as described in the below image. 

![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/contextvariables.png?raw=true)
Details about the context parameters are below. </br>
**hdfsuri_namenodepath:** *This parameter is used to contain the hdfs name node URI. Syntax of this parameter is hdfsuri_[any text].* </br>
**hdfspass_namenodepass:** *This parameter is used to contain the name node passwords. Syntax of this parameter is hdfspass_[any text].* </br>
**input_hdfsinputfile:** *This parameter is used to contain the hdfs path of user selected file. In this example, Users11 csv file path would be saved in this parameter. Syntax of this parameter is input_[any text].* </br>
**output_hdfsoutputfile:** *This parameter is used to contain hdfs path for output file name which should be generated by transformation job. Syntax of this parameter is output_[any text].* </br>

**Setting property for tHDFSConnection component.** </br>
After the above step, <b>Double click</b> on the <b>tHDFSConnection</b> component. Component section will appear in Talend designer studio. We need to set respective properties for this component.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/ComponentProperty.PNG?raw=true)
</br>
a) Change the Distribution to Cloudera as our DLP platform is build on Cloudera. </br>
b) Change Distribution version to Cloudera CDH5.4. </br>
c) Change name node uri as <b>context.hdfsuri_namenodepath</b> </br>
d) Change User name as <b>context.hdfspass_namenodeusername</b> </br>
e) <b>Use Datanode Hostname</b> should be unchecked.

</br>
**Setting property for tHDFSInput component.** </br>
After setting the tHDFSConnection component properties, now we have to set the required properties for tHDFSInput component.
<b>Double clicking</b> on tHDFSInput will display the Component tab as the below image. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/ComponentPropertytHDFSInput.PNG?raw=true)
</br>
Below changes are required to apply in tHDFSInput component tab. </br>
a) Click the checkbox named <b>Use an existing Connection.</b>.  </br>
b) Change the <b>File name</b> as context.input_hdfsinputfile. </br>
c) <b>Field seperator</b> should be comma(,).
</br>
**Setting Schema in tHDFSInput component based on Input file.**</br>
Users11.csv is out input file which are already pre-loaded in DLP's Hadoop platform. These file have multiple columns/fields. We need to set the columns/fields based our choice as a schema in tHDFSInput component.
</br>
Double click on tHDFSInput component. It will open the Component's property section. Click on <b>ellipsis</b> button in <b>Edit Schema.</b> It will open a entry form where user can define the Schama which should be defined in the source file. As Users11.csv is the source file, by clicking on <b>+</b> symbol, user can enter the field's name accordingly. Based on user's choice, user can insert the field name's here. For our example, we have entered below field's name. </br>
```json
UserID,
Email,
Username,
Country,
AccessLevel,
LastLoginDate,
FirstName,
LastName
```
**N.B: There should not be any Space in Field name.**
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/InputFileSchema.PNG?raw=true)
Enter the field names and click on <b>OK</b> to save the schema for tHDFSInput component.

**Setting property for tHDFSoutput component.** </br>
After setting the tHDFSInput component properties, now we have to set the required properties for tHDFSOutput component.
<b>Double clicking</b> on this component will display the Component tab as described in below image.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/ComponentPropertytHDFSoutput.PNG?raw=true)
Below changes are required to apply in tHDFSoutput component tab. </br>
a) Click the checkbox named <b>Use an existing Connection.</b> </br>
b) Change the <b>File name</b> as context.output_hdfsoutputfile </br>
c) <b>Field seperator</b> should be comma(,). </br>

**Setting Schema in tHDFSOutput component based on Input file.**</br>
Following the same procedure, user need to set the schema for output file in tHDFSOutput component. Double clicking on tHDFSOutput component will help to open the Component property section. Click on <b>ellipsis</b> button in <b>Edit Schema</b> section will allow user to enter the field names for output file.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/outputSchema.PNG?raw=true)
</br></br>
*Here we are trying to merge First Name and Last Name into one field called FullName in the output file.*</br>
```json
UserID,
Email,
Username,
Country,
AccessLevel,
LastLoginDate,
FirstName,
LastName,
FullName
```

</br>
</br>
**Making connection between each component.**</br>
In this step, we will learn the process of making connections between each component based on the data flow. 
Right Click on <b>tHDFSConnection</b> component and select <b>Trigger->On Subjob OK</b>.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/thdfsConnection1.PNG?raw=true)
After that click on <b>tHDFSInput</b>. This will make an arrow from <b>tHDFSConnection</b> to <b>tHDFSInput</b>. See the below image.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/connector03.PNG?raw=true)
Now Right click on <b>tHDFSInput</b> component and select <b>Row->Main</b> and then click on <b>tHDFSOutput</b> compoment. See the below image.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/connector04input.png?raw=truee)
Follow the above way to build connection from one component to another component. Flow of data would be like below</br>
</b>tHDFSConnection_1->tHDFSInput_1->tJavaRow_1->tMap_1->tHDFSOutput_1</b> </br>
<b>Output connector name from tMap_1 to tHDFSOutput is output. When connecting from tMap to tHDFSOut, prompt message will ask the output connector name. Enter "output" as a output connector name.</b>
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/connectionFinalImage.PNG?raw=true)
Click on <b>tJavaRow</b> components and Click on <b>Edit Schema</b> and add a new field name <b>FullName</b> and set the <b>Type</b> as <b>String</b>. Add the below code in the code area. Follow the below image.</br>
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/tJavaRowJavaCode.PNG?raw=true)
```json
//Code generated according to input schema and output schema
output_row.UserID = input_row.UserID;
output_row.Email = input_row.Email;
output_row.Username = input_row.Username;
output_row.Country = input_row.Country;
output_row.AccessLevel = input_row.AccessLevel;
/*output_row.LastLoginDate = TalendDate.parseDate("MM/dd/yyyy",input_row.LastLoginDate).toString();*/
output_row.LastLoginDate = input_row.LastLoginDate;
output_row.FirstName = input_row.FirstName;
output_row.LastName = input_row.LastName;
output_row.FullName = StringHandling.UPCASE(input_row.FirstName + " " + input_row.LastName);
```
Click on <b>tMap_1</b> component and map the fields by draging from left to right. Click on <b>Country</b> field and add below line of code as described in the below image. This will print <b>NoCountry</b> as text where in source file, Country field is empty. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/tmapConnector.PNG?raw=true)
</br>
Similarly click <b>Edit Schema</b> on <b>tHDFSOutput_1</b> and Sync the Schema.

</br>
We just learn the process of creating a Talend job in Talend Open source big data tool. We will now learn the process of building job and export the job in zip format so that we can upload the job in DLP platform for further processing.
