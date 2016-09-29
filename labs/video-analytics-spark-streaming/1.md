# **Video Analytics Using Spark Streaming**

# **Introduction about Spark Streaming and Real-time Data processing.**
Spark Streaming is a key component of Spark, a massively successful open source project in the recent years. Spark Streaming is an extension of the core Spark API that enables scalable, high-throughput, fault-tolerant stream processing of live data streams. Data can be ingested from many sources like Kafka, Flume, Twitter, or TCP sockets, and can be processed using complex algorithms expressed with high-level functions like map-reduce, join and window. Finally, processed data can be pushed out to file systems, databases, and live dashboards. 

# **Lab Overview**
Our application is using micro service for video data ingestion. It will read the video data from mockup video source and forward the data to Kafka broker. Our sample code will read the video data from Kafka broker and detect the face image and save that image(s) into HDFS platform. The User can view the face image from DLP platform.

In this lab, we will integrate Spark Streaming and Kafka, detect a human face using OpenCV from a video streaming, and then save the result to an image file in Hadoop environment. 

For simplicity in the lab exercise, we use a mockup video source. In real application, User can use a live video streaming from a real camera and write a video source service for reading the streaming data from a camera and send the data from the camera to kafka for replacing  the mockup video source. 
Please find the current lab scenario as below:</br>
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/mockVideoSource.png?raw=true)


## **Lab Objectives**

- Learn how to integrate the Spark Streaming with Kafka.
- Learn how to perform video analytic functions in a real-time stream application.
- Learn how to save a file to HDFS.

## **Prerequisites**

- Knowledge of Java language, Maven.
- Knowledge of OpenCV faces detection function.
- Studied platform user guide.
- Basic knowledge of how Spark Streaming works.
- Chrome Browser.


## Step 1: Explore Data Learning Platform(DLP)

<font color='red'>Request access to the Data Learning Platform by sending a message to:</font> [datalearningplatform@cisco.com](mailto:datalearningplatform@cisco.com)

1. In DLP website, go to the development area by clicking <b>"Development Hub"</b>. 
2. Select the workspace called <b>"wksp-video-lab"</b> and Click the <b>"Launch"</b> button.
3. It will open a new browser tab with pre-loaded video streaming code.

![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/WorkspaceSelection.PNG?raw=true)

N.B: This sample code can be used for exploring the process.

## Step 2: Sample Code for Detecting face from mockup video source.

<b>Our video streaming program is used to detect the video streaming from a source. Below Java program is used to read the video data, then detect the face and save the face images to HDFS.</b><br>

Select App.java from Left Panel and the code will open on right Panel.
![alt-tag](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/sourceCode.PNG?raw=true)


```json
package DDP.VideoLabs;

//import java libraries
import java.io.BufferedInputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.URI;
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import org.joda.time.DateTime;

//import spark libraries
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.function.Function;
import org.apache.spark.streaming.Durations;
import org.apache.spark.streaming.api.java.JavaDStream;
import org.apache.spark.streaming.api.java.JavaPairInputDStream;
import org.apache.spark.streaming.api.java.JavaStreamingContext;
import org.apache.spark.streaming.kafka.KafkaUtils;

//import opencv libraries
import org.opencv.core.Core;
import org.opencv.core.Mat;
import org.opencv.core.MatOfRect;
import org.opencv.core.Size;
import org.opencv.imgcodecs.Imgcodecs;
import org.opencv.imgproc.Imgproc;
import org.opencv.objdetect.CascadeClassifier;

//import kafka libraries
import kafka.serializer.DefaultDecoder;
import kafka.serializer.StringDecoder;
import scala.Tuple2;

//import hadoop libraries
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FSDataOutputStream;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IOUtils;

public class App 
{
    public static void main( String[] args ) throws InterruptedException
    {
    	if (args.length != 4)
    	{
    		System.out.println("please set parameter value for kafka, topic, username and running application duration");
    		return;
    	}
    	//set parameter value for kafka, topic, username and running application duration
    	String kafka = args[0];
        String topics = args[1];
        final String username = args[2];
        int duration = Integer.parseInt(args[3]);
        
      	//Integrate the Spark Streaming with Kafka
        SparkConf sparkConf = new SparkConf().setAppName("JavaVideoLabs");
        final JavaStreamingContext jssc = new JavaStreamingContext(sparkConf, Durations.seconds(2));

        HashSet<String> topicsSet = new HashSet<String>(Arrays.asList(topics.split(",")));
        HashMap<String, String> kafkaParams = new HashMap<String, String>();
        kafkaParams.put("metadata.broker.list", kafka);
        kafkaParams.put("group.id", "groupid");
        kafkaParams.put("consumer.id", "consumerid");

        //Get the video data from kafka topic
        JavaPairInputDStream<String, byte[]> messages = KafkaUtils.createDirectStream(
                jssc,
                String.class,
                byte[].class,
                StringDecoder.class,
                DefaultDecoder.class,
                kafkaParams,
                topicsSet
        );
        

        //Detect the face from video data and save the face image to HDFS          
        JavaDStream<String> content = messages.map(new Function<Tuple2<String, byte[]>, String>() {
           	private static final long serialVersionUID = 1L;
			//@Override
            public String call(Tuple2<String, byte[]> tuple2) throws IOException {
                System.loadLibrary(Core.NATIVE_LIBRARY_NAME);
                if ((tuple2 == null) || (tuple2._2().length < 1000))
                	return "";
                
                Mat image = new Mat(new Size(640, 480), 16);
                image.put(0, 0, tuple2._2()); 
                                    
                // Detect faces in the image using OpenCV.
                Mat mGrey = new Mat();
                Imgproc.cvtColor( image, mGrey, Imgproc.COLOR_BGR2GRAY); 
                CascadeClassifier faceDetector =
                        new CascadeClassifier(GetResourceFilePath("/haarcascade_frontalface_alt.xml").toString());
                MatOfRect faceDetections = new MatOfRect();
                faceDetector.detectMultiScale(mGrey, faceDetections);
                int len = faceDetections.toArray().length;
                System.out.println(String.format("Detected %s faces", len));
                if (len > 0)
                {
	                SaveImageToHDFS(image, username);
	                return "face";
	              
                } else
                    return "";
           
            }
        });
        
        //The application will stop execution when its run time is bigger than the time which has passed as parameter "duration" 
        DateTime start = new DateTime();
        
        content.count().print();
       
        jssc.start();
        DateTime end;
        while (true) {
            end = new DateTime();
            if (end.getMillis()-start.getMillis() > duration * 60000) {
                jssc.stop(true, true);
                break;
            }
	        Thread.sleep(2000);            
        }

        jssc.awaitTermination();
    }
    
    public static void SaveImageToHDFS(Mat img, String username) throws IOException
    {	 
    	 //Save the face image as a temporary file
    	 DateTime now = new DateTime();
    	 int year = now.getYear();
    	 int month = now.getMonthOfYear();
    	 int day = now.getDayOfMonth();
    	 int hour = now.getHourOfDay();
    	 int minute = now.getMinuteOfHour();
    	 int second = now.getSecondOfMinute();
    	 String time = ""+year+month+day+hour+minute+second;
    	 String tmpFile = "/tmp/" + username + time + ".jpg";
         Imgcodecs.imwrite(tmpFile, img);
         
         //Save the temporary file for face image to HDFS
         String hdfsAddr = "hdfs://172.16.10.16:8020/ddp/"+username+"/"+"face.jpg";
         Configuration config = new Configuration();
         FileSystem fs = FileSystem.get(URI.create(hdfsAddr), config);
         Path path = new Path(hdfsAddr);
         FSDataOutputStream out = fs.create(path, true);
         InputStream is = new BufferedInputStream(new FileInputStream(tmpFile));
         IOUtils.copyBytes(is, out, config);
         is.close();
         out.close();
         fs.close();
         
         //Delete the temporary file
         File f = new File(tmpFile);
     	 if (f.exists() && !f.isDirectory())
     		f.delete();
         System.out.println("write file to hdfs");
    }
    
    //Read the resource file from the jar file then save it as temporary file
    public static String GetResourceFilePath(String filename) {
        InputStream inputStream = null;
        OutputStream outputStream = null;
        String tempFilename = "/tmp" + filename;
        try {
        	File f = new File(tempFilename);
        	if (f.exists() && !f.isDirectory())
        		return tempFilename;
        	
            // read this file into InputStream
            inputStream = App.class.getResourceAsStream(filename);
            if (inputStream == null)
                System.out.println("empty streaming");
            // write the inputStream to a FileOutputStream
            outputStream =
                    new FileOutputStream(tempFilename);

            int read;
            byte[] bytes = new byte[102400];

            while ((read = inputStream.read(bytes)) != -1) {
                outputStream.write(bytes, 0, read);
            }
            outputStream.flush();

            System.out.println("Load XML file, Done!");

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (inputStream != null) {
                try {
                    inputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (outputStream != null) {
                try {
                    // outputStream.flush();
                    outputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }

            }

        }
        return tempFilename;
    }
    
}


```   

## Step 3: Maven package and submit the spark task to Hadoop cluster.

Once we finish the above code, we can select <b>“package”</b> in the CMD menu, and click on <b>Blue Button</b> ![alt-tag](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/BlueButton.PNG?raw=true). This will package the application.

![alt-tag](https://github.com/prakdutt/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/BuildProject.PNG?raw=true)

After successful packaging, select <b>run.sh</b> from left panel and select <b>“run”</b> and click the blue button again to execute it.

![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/script_code.png?raw=true)

<b>There are  the four(4) Input parameters that are used in run.sh</b>.  <br>
These parameters are described in run.sh file as below:
<b>172.16.10.10:9092 ddp_video_user_1 $HADOOP_USER_NAME 5</b>

Parameter 1: 172.16.10.10:9092 -> kafka broker<br>
Parameter 2: ddp_video_user_1 -> kafka topic with user id padded together. If user id is user_2 then the value would be as <b>ddp_video_user_2</b><br>
Parameter 3: $HADOOP_USER_NAME -> login username. <br>
Parameter 4: 5 -> Spark streaming application running duration in minutes for detecting faces from stream data against the specified login userid.</br>

<b>This script (run.sh) submit the spark task to cluster.</b>

## Step 4: Start the Video source micro service from DLP platform.
Below steps is using to start the micro service to push the video streaming data to Kafka broker. </br>
1. From DLP platform, clicking on  <b>App Stack Hub</b>, it will open an UI in right panel. Select <b>Stack Library</b> and select <b>videolabs_User_7</b>. </br>
   N.B: Here <b>videolabs_User_7</b> is names with Logged UserID. If User_2 logged in, then this text would be as <b>videolabs_User_2</b></br>
2. Check the <b>Health</b> status..  It should be in <b>Stop</b> status at the beginning.</br> If the status is in <b>Running</b> state, it is required to stop first and then start the service.  Health status would be checked where <b>App Name</b> is mentioned as <b>videosource</b></br>
3. Click on Right green button to start the service.  </br>   
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/VideoVideoSrouce.PNG?raw=true) </br>
4. On clicking on Green action button, the status of <b>Health</b>  would be changed to <b>waiting</b> state first. </br>
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/VideoVideoSrouceWaitingState.PNG?raw=true) </br>
5. After the waiting state, status of <b>Health</b> would be in <b>Running</b> state. </br>
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/VideoVideoSrouceRunningState.PNG?raw=true) </br>

## Step 5: View the file which has face images in DLP Platform

The spark task detects the face(s) from the video streaming and save them into the Hadoop file system, you can view them in DLP following the below steps. 

1. From the DLP home page, go to the <b>Data Repository</b>.
2. Find the face.jpg image file in the data list.
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/face1.jpg?raw=true)
3. Click the preview button to display the image.  
</br>
Here face.jpg is an generated image file which is created in a regular <b>time interval</b> and stored in DLP's Hadoop platform. Check the <b>Time Created</b> field against then face.jpg image. User can notice that the <b>Time Created</b> field is updating at a regular time interval.
4. Previewing image in two different time interval. The image would be display in popup. Here two images are showing in this documentation. Below two images are generated at <b>2016-09-29 03:15:40</b> and <b>2016-09-29 03:16:04 time.</b>
![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/faceImage.PNG?raw=true)
![alt-img](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/faceImage2.PNG?raw=true)
<b>N.B: For learning, we only use small set of data for streaming in our sample application, different face image are getting generated and saved in the hadoop platform based on every changes of timestamp. This process will continue till the stream data get finished.</b></br>

## Step 6: Stop the video source micro service. </br>
After displaying the images from DLP environment, we need to stop the video source micro-service from <b>App Stack Hub</b>. Click on Red Stop button once. The stop button would be selected against the <b>App Name</b> where <b>videosource</b> is mentioned.
</br></br>
**N.B: Here videolabs_User_7 is names with Logged UserID. If the login id is User_2, then this text would be as videolabs_User_2.**

![alt-tag](https://github.com/CiscoDevNet/data-dev-learning-labs/blob/master/labs/video-analytics-spark-streaming/assets/stopProcess.PNG?raw=true)

**Input**  : The stream data from mockup video source from DLP.  
**Output** : Preview the faced image file from Hadoop environment. 

From this we have learned how to how to integrate the SparkStreaming with Kafka and how to save the file to HDFS.

There are few more examples and exercise are available in the below-mentioned link. This is for your reference.

[http://spark.apache.org/docs/latest/streaming-programming-guide.html](http://spark.apache.org/docs/latest/streaming-programming-guide.html)

