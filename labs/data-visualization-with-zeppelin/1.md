# **Basic data visualisation using Apache Zeppelin**

# **Introduction about Apache Zeppelin**
Zeppelin A web-based notebook that enables interactive data analytics. You can make beautiful data-driven, interactive and collaborative documents with SQL, Scala and more. </br>

Interactive browser-based notebooks enable data engineers, data analysts and data scientists to be more productive by developing, organising, executing, and sharing data code and visualising results without referring to the command line or knowing the cluster details. Notebooks allow users to not only execute but also interactively work with long workflows. Zeppelin provides a &quot;Modern Data Science Studio&quot; that supports Spark and Hive out of the box. In addition, Zeppelin supports multiple languages in the back-end, with a growing ecosystem of data sources. Zeppelin notebooks provide interactive snippet-at-time experiences to data scientists.

Apache Zeppelin website : https://zeppelin.apache.org/

</br>

# **Lab Overview**
In this learning lab, a user can learn the use of Python functions and write interactive python code from Zeppelin notebook. 

Below are the main points, which user can learn and perform from this learning lab. </br>
1. Learn how to interactively write and run python code in Zeppelin. </br>
2. Learn how to use numpy library for createing calculative cosine value</br>
3. Learn how to plot data with matplotlib library. </br>

# **Prerequisites**
User needs to know below basic knowledge.</br>
1. Basic knowledge of python.</br>
2. Basic knowledge of mathematic</br>
3. Chrome Browser. </br>

<b>N.B</b> Follow the below steps and execute the codes in Zeppelin notebook interface. </br>

## Step 1: Start Zeppelin Notebook from Data Learning Platform (DLP) </br>

1. From DLP home page, click <b>Drill</b> button from top-right corner of the screen to choose interactive analysis environment.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/image1DrillButton.PNG?raw=true)

2. Select Zeppelin from the pop-up box
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/image2-ChooseZeppelin.png?raw=true)
3. Allow pop-up blocker to open Zeppelin tool in another tab. Select the Allow radio button and click on <b>Done</b> button. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/image3AllowPopup.PNG?raw=true)

## Step 2: Create Zeppelin development environment </br>
1. Above steps will Zeppelin home page. We need to create our own notebook by clicking on <b>Create new note</b> link. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/image4WelcomeZeppelinPage.png?raw=true)

2. Create a notebook with a new name in the pop-up dialogue box. 
Input a valid name based on your choice and click on the <b>Creat Note</b> button.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/image5CreateNewNotbook.png?raw=true)

3. A newly created notebook will open.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/image6ZeppelineNotebookEditor.PNG?raw=true)

</br>
<b>*Upto this steps, we have created our environment on Zeppelin. Now we will try to use some Python functions and view the output directly from Zeppelin. Python is already installed in out DLP platform. In our example code, we will try to view the Cosine signal data.*</b>

## Step 3: Create cosine signal data. 
**Preparing Python code for data generation** </br>
Input the code as given below. After entering code in Zeppelin notebook UI, click on the <b>Execute</b> button to execute the code. </br>
The details about the code is in below: </br>
i) Import numpy library from Zeppelin UI. </br>
*Numpy is the fundamental package for scientific computing with python. It contains very powerful mathematical functions. In this learning lab, we will use the function that is defined in Numpy to create cosine signal data. Before we use these functions, we should import Numpy library.* </br>
ii) Define a numpy array which should be eventually distributed along (-Pi, Pi). The syntax of numpy.linspace is as below.
numpy.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)
</br>
Reference URL is : http://docs.scipy.org/doc/numpy/reference/generated/numpy.linspace.html </br>

Return evenly spaced numbers over a specified interval.
Returns num evenly spaced samples, calculated over the interval [start, stop]. </br>
iii) Define an array y=cos(x). </br>
iv) Printing all the <b>cosine</b> values from array. </br>

```json
%python
import numpy as np                                                     #Import numpy library
x = np.linspace( -np.pi, np.pi , 1000)                                 #Define a numpy array which should be eventually distributed along (-Pi, Pi).
y = np.cos(x)                                                          #Define an array y = cos(x)
print x,y                                                              #Print the cosine signal data
```
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/pythonCodeLoadData1.png?raw=true)


</br>
After executing the above code, user can view the cosine signal data in Zeppelin.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/pythonCodeLoadDataOutput1.PNG?raw=true)

## Step 4: Plotting the cosine signal.
In the previous step, we have created the cosine signal data. Now we need to plot those cosine signal data. <b>Matplotlib</b> is a python 2D plotting library that produces publication quality figures in a variety of hardcopy formats and interactive environments across platforms. In this learning lab, we will use the function of Matplotlib library to plot the figure. </br>
Below is the python code which will help to draw the Cosine curve by plotting the cosine data. </br>
Details about the code for drawing the Cosine curve is in below:</br>
i)   Import Matplotlib, StringIO library in Zeppelin. </br>
ii)  Plot the cosine signal in memory. </br>
iii) Create StringIO object for reading string buffer data from memory. </br>
iv)  Create an image with cosine data reading from memory in svg format. </br>
v)   Get the starting memory address of the image which has created in step iv. </br>
vi)  Show cosine signal curve in Zeppelin UI. </br>
```json
%python
import matplotlib.pyplot as plt                                        #Import matplotlib library
import StringIO

plt.plot(x,y)                                                          #Plot the cosine signal in memory

img = StringIO.StringIO()                                              #Create StringIO object which named img
plt.savefig(img, format='svg')                                         #Save the figure in svg format
img.seek(0)                                                            #Get the memory of the figure
print "%html <div style='width:300pt'>" + img.buf + "</div>"           #Show the cosine signal curve
```
Copy the above code in Zeppelin notebook UI and execute the code by clicking on the <b>Execute</b> button. This code will generate and display the Cosine curve on Zeppelin.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-visualization-with-zeppelin/assets/images/visualizationScreen2.PNG?raw=true)

   
