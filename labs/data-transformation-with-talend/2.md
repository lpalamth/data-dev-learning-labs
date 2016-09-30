**Section C: Build Transformation Job using Talend Big Data Tool in user's local computer.** </br>
In this section, the user will learn the process of building and exporting job which user has created already in the previous section from Talend tool. 

**Below steps for exporting job from Talend tool**</br>
1) Right click on the job name and select <b>Build Job</b> from the menu. It will open a UI from where user can select the type of build process.</br>
![build-job](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/buildJob1.png?raw=true)
2) Click on the <b>Browse...</b> button where you want to save the job as a zip format. The file would be saved as a zip format. </br>
3) Select <b>Standalone Job</b> from <b>Select the build type</b> list box.</br>
4) Uncheck <b> Extract the zip file</b> </br>
5) <b>Shell launcher</b> and <b>Context script</b> checked as default.
![build-job](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/buildJob2.png?raw=true)
3) Click on <b>Finish</b> button. </br>
Above steps will build and export the talend job in user's local machine.

**Section D: Upload the transformation job in DLP platform** </br>
In this section, the user can learn the process of uploading transformation job in DLP platform. Follow the steps as described in below.</br>
1) From DLP platform, select checkbox against <b>User11.csv</b> file and click on <b>Transform</b>
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/selectingSourceFile1.PNG?raw=true)
2) It will open Transformation interface in another tab of your browser. User can preview the content of the source file(Users11.csv) here. There are three sections available. </br>
   a) In-build Transformation functions: System defined transformation functions would be available here. </br>
   b) My transformation functions: User's uploaded transformation functions would be available here.</br>
   c) Community Provided functions: User can share their transformation function(s) for community people. All those transformation jobs would be available here which are shared any any user. </br>
<b>N.B: a & c has not implemented yet. </b> </br>
3) Click on <b>Upload</b> icon. See the below image. It will open a pop-up entry form.
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/selectingSourceFile3.PNG?raw=true)
4) Select the talend job which you had created in Section <><> and enter the job name and short description,job type as private and then press <b>Upload</b> button to upload the job. 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/selectingSourceFile5.PNG?raw=true)
5) Above step will upload the job in hadoop environment from your local machine and extract it for execution. This process will take 3/4 minutes to upload the file. A successfull prompt message will apear to notify that job upload process is done successful. Sit back until you received the successful message as below image. Click on <b>OK</b> button and close the Job upload form.</br> 
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/data-transformation-with-talend/assets/images/selectingSourceFile8.PNG?raw=true)
</br></br>