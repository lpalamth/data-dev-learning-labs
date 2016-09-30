
# **Interactively Static (CSV) Data Explore using Zeppelin**

# **Introduction about Apache Zeppelin**
Zeppelin A web-based notebook that enables interactive data analytics. You can make beautiful data-driven, interactive and collaborative documents with SQL, Scala and more. </br>

Interactive browser-based notebook enables data engineers, data analysts and data scientists to be more productive by developing, organising, executing, and sharing data code and visualising results without referring to the command line or knowing the cluster details. Notebooks allow users to not only execute but also interactively work with long workflows. Zeppelin provides a &quot;Modern Data Science Studio&quot; that supports Spark and Hive out of the box. In addition, Zeppelin supports multiple languages in the back-end, with a growing ecosystem of data sources. Zeppelin notebooks provide interactive snippet-at-time experiences to data scientists.

Apache Zeppelin website : https://zeppelin.apache.org/

</br>

# **Lab Overview**
In this lab, we will use a pre-loaded static data and explore data using interactive way using Zeppelin. The data should be residing into Hadoop environment and Zeppelin will interact with the data using Spark by forming RDD on the data set or pre-loaded file. We will use Spark code from Zeppelin for developing RDD and use SQL syntax to display data in different format. Zeppelin provides the beautiful graph to displaying data which should be more understandable to the user.

</br>
<b>Target audience:</b>
Users who are more intendent to know the insight-out of the data in more interactive way, can learn and use Zeppelin from DLP platform.  
</br>
## **Lab Objectives**

- Learn to interactively analyse Big Data by using Zeppelin
- Explore the way to read &amp; format (CSV) HDFS files by using Spark
- Learn how to save DataFrame into a temporary SQL table for consequent queries
- Explore interactive SQL analysis and visualisation on tables in Zeppelin

## **Prerequisites**

- Basic knowledge of zeppelin
- Basic programming skill of Spark (e.g. scala, RDD, DataFrame, SparKSQL, etc.)
- Basic understanding of SQL queries
- Chrome Browser.

## Step 1: Explore Data Learning Platform(DLP)

<font color='red'>Request access to the Data Learning Platform by sending a message to:</font> [datalearningplatform@cisco.com](mailto:datalearningplatform@cisco.com)


1. From DLP home page, select the pre-loaded file <b>(bank-full.csv)</b> click <b>Drill</b> button from top-right corner of the screen to choose interactive analysis environment.
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/selectionRawDataFile.PNG?raw=true)
2. In the popup frame with Zeppelin and Jupyter as options, click Zeppelin.
3. Follow the pop-out chrome page to begin the interactive analysis and visualization using Zeppelin

![alt-tag](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/selectZappline.PNG?raw=true)

Browser may block Zeppelin. In this case, allow browser to open Zeppelin by selecting the <b>Always allow pop-up from http://xxx.xxx.xxx.xxx </b> and click on <b>Done</b> button. </br>
<b>IP address of DLP platform may differ based on the usages of server.</b>
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/popUpBlockerAllowed.PNG?raw=true)

## Step 2: Develop in Zeppelin notebook

1. On the Zeppelin homepage, create your own notebook by clicking on <b>Create new note</b>;.
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/welcome-to-zeppelin.PNG?raw=true)

2. Create and name your new notebook in the pop-up dialog.
![Figure](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/create-note.png?raw=true)

3. In your newly created notebook, a typical Zeppelin interactive development and visualisation working environment.

![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/zeppelinNotebookOpen.PNG?raw=true)


Note: You can use the top-right tool buttons do corresponding configurations (e.g., set paragraph width, copy visual report link, etc.) when necessary.

## Step 3: Data Refinement & using Zeppelin to load the data
We will use Spark code to create RDD on bank-full.csv file in this step. bank-full.csv file already loaded in Hadoop environment. We need use below Spark code for this purpose.  </br>
Following functions are going to perform using Spark Code
-    Remove the header using filter function, and transform data from csv format into RDD of Bank objects.
-    Convert RDD to DataFrame and create a temporary table with name “bank”.
</br>

<b>Below steps are describing the process of uploading sample spark code with sample data file which is residing in Hadoop and execute the code for creating RDD and temporary table called "bank".</b> </br>

<b>Step 3.1 </b>Copy below Spark Code in Zeppelin notebook for loading data file from Hadoop. </br>

```jason
val bankText = sc.textFile("hdfs://xx.xx.xx.xx:xxxx/yourPath/bank/bank-full.csv")  
//Replace the bank-full.csv file path.

case class Bank(age:Integer, job:String, marital : String, education : String, balance : Integer)

// split each line, filter out header (starts with "age"), and map it into Bank case class
 
val bank = bankText.map(s=>s.split(";")).filter(s=>s(0)!="\"age\"").map(  
       s=>Bank(s(0).toInt, 
            s(1).replaceAll("\"", ""),  
            s(2).replaceAll("\"", ""),  
            s(3).replaceAll("\"", ""),  
            s(5).replaceAll("\"", "").toInt  
        )  
)
bank.toDF().registerTempTable("bank")
```
Above code is used to load the data file from Hadoop and prepare RDD using Spark. The RDD is converted into a temporary table called "bank"

<b>Important point to notice.</b>
In the below code, we need to replace the bank-full.csv file path. The path is mentioned as below:
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/filePath.png?raw=true) 
</br>
<b> Steps are described in 3.2 and 3.3 </b> </br>

<b>We need to change this path accordingly.</b>
</br>
<b>Step 3.2 </b> Marked area are mentioned in below screen where we need to insert the actual bank-full.csv file path.</br>
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/sparkCode.png?raw=true)
<b>Step 3.3 </b>Copy the bank-full.csv file path from <b>Data Repository</b>.</br>
For changing the bank-full.csv file path, copy the path from <b>Data Repository</b> section and replace it in above code.
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/csvFilePath.PNG?raw=true)
</br>
<b>Step 3.4</b> Update the bank-full.csv file path in the Zeppelin notebook and execute the code.</br>
After replaceing the bank-full.csv file path in the spark code, paste the code in Zeppelin notebook editor and it would be like below. Click on the Execute button marked in Red in below image.
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/ZeppelineEditorWithSparkCode1.PNG?raw=true)
</br>
<b>Step 3.5</b> Spark code execution status from Zeppelin notebook.</br>
Below screen is showing that the spark RDD is created successfully and creation of a temporary table name "bank" is also done.
![Figure](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/sparkCodeRunSuccessfullyInZeppelin.png?raw=true)

## Step 4: Data Retrieval using SQL.

Data load process is done in above steps. We will use some sql queries to retrieve the data and display it in a different format. 
We will try three consecutive examples to check the output in Zeppelin.

<b>Example 1:</b> We want to see the age distribution of data which are stored in bank RDD. 
</br>Use the below query in Zeppelin Editor and execute the query in Zeppelin editor

```sql
%sql 
select age, count(1) from bank where age < 30 group by age order by age
```
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/sqlQuery1.PNG?raw=true)

Change the graph type to pie chart and view the output as below.
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/example1-1image.png?raw=true)

<b>Example 2:</b> Use the below SQL query to input run-time data as input box and display output. 

```sql
%sql
select age, count(1) from bank where age < ${maxAge=30} group by age order by age
```
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/Example-2image.png?raw=true)
</br>
Enter value as 21 in the input box, output would be like below.
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/Example-2-1.png?raw=true)

<b>N.B: User can try with any values and view the output.</b>

<b>Example 3:</b> Using dynamic sql query to select data from a drop down list box in Zeppelin is showing in this example. Paste the sql in Zeppelin's editor and execute the query after changing the values based on your choice.

You can make input box for setting age condition by replacing 30 with ${maxAge=30}.

```sql
%sql
select age, count(1) from bank where marital = "${marital=single,single|divorced|married}" group by age order by age
```
Now we want to see age distribution with certain marital status and add a combo box to select marital status.

![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/zepplelinListbox.PNG?raw=true)

By running the above paragraphs of SQL queries, you will get corresponding visual result like below:

![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-explore-using-zeppelin/assets/comboImageResult.PNG?raw=true)


 **Things to Try**

- Try with different queries.
- Try with inner queries.

From this, we have learned how to use the Zeppelin with different types of SQL queries.

