# Step 3: View Data in Visualization Tool
Below step will describe the process of visualising the network data using Tableau. 
Switch to <b>Data Repository</b> tab and select your output file. This output file is the file name which we mentioned in run.sh file.
![alt tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/visializationNetworkData1.PNG?raw=true)

</br>Clicking on the eye button(as showing in the above picture), output file would be shown as below.
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/rawDataDisplay.PNG?raw=true)
After selecting the respective file, click on <b>Visualize</b> button to visualize the data in Tableau. Tableau will be open in a new tab.

# Step 4: Visualising in Tableau. 
For first time usages of this learning lab, the browser may block the Tableau visualisation page. Below steps are used to unblock Tableau in the browser:

	1. Click the pop-up blocker icon in the browser's address bar. 
	2. Click and Select Always allow pop-ups from "http://xx.xx.xx.xx"
	3. Click the "Done" button.
Follow the above steps as describe in below screen
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/unblockTablue.png?raw=true)

</br>

# Step 5: Tableau Interface.
The user can select the respective field(s) and view the data in graphical format here. For example, select ip_src(IP address of source devices) and ip_dest(IP address of destination devices) fields from Dimensions column and place it as shown in the below screen. It will generate the output which will describe that each dot marks is showing that there is a traffic between two devices. IP addresses of devices which are communicating with each other are marked on X-axis and Y-Axis respectively.
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/network-data-transformation/assets/images/tableauUIOnNetworkData.PNG?raw=true)

</br>
The User can select any other fields based on their own choice to display the output. 

Sample Code: Transform a network data file and store transformed file to HDFS.

Below is the sample code which is used for getting the CSV file of network data from HDFS environment, perform the transformation and store the transformed data into HDFS. 

```java
//Import the below libraries which are used to run the code.
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.FileUtil;
import org.apache.hadoop.fs.Path;
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import org.apache.spark.api.java.function.FlatMapFunction;

import java.util.Arrays;
//Class: TransformData. A class that transform the network data
public class TransformData {

    public static void main(String [] args) throws Exception {


  //three parameters here
        String filePath= args[0];
        String outputPath= args[1];
        String distFilePath= args[2];

        final String seperatorField = ",";

        //System.out.println("master address:"+master);
        System.out.println("input file path:"+filePath);
// here we are giving application name as “File transform”
        SparkConf conf = new SparkConf().setAppName("File transform");
        JavaSparkContext sc = new JavaSparkContext(conf);

        JavaRDD<String> textFile = sc.textFile(filePath);

        JavaRDD<String> cols = textFile.flatMap(new FlatMapFunction<String, String>() {
            public Iterable<String> call(String s) {
                String [] splits = s.split(seperatorField) ;

                String extractedCols = "";

                for(int i= 1 ;i<= 6 ;i ++ ){
                    extractedCols += splits[i ] + seperatorField ;
                }

                if(extractedCols.endsWith(seperatorField)){
                    extractedCols = extractedCols.substring(0,extractedCols.length() - 1)  ;
                }

                return Arrays.asList(extractedCols);
            }
        });


       cols.coalesce(1).saveAsTextFile(outputPath);

       boolean bool = getMergeInHdfs(outputPath,distFilePath);
        System.out.println("merge success:"+bool);



    }

    public static boolean getMergeInHdfs(String src, String dest) throws IllegalArgumentException, Exception {

        Configuration config = new Configuration();
        FileSystem fs = FileSystem.get(config);
        Path srcPath = new Path(src);
        Path dstPath = new Path(dest);

        // Check if the path already exists
        if (!(fs.exists(srcPath))) {
            System.out.println("Path " + src + " does not exists!");
            return false;
        }

        if ((fs.exists(dstPath))) {
            System.out.println("File Path " + dest + " exists!");
            return false;
        }

        return FileUtil.copyMerge(fs, srcPath, fs, dstPath, true, config, null);
    }
}
```

Above process is allowing to ingest any network data by writing code using cloud IDE and use Hadoop platform to store the data. Those data can be used by the user for further processing or developing a new application. 

<b> Thank you </b>
