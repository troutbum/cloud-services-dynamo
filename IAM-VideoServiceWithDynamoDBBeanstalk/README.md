## Running the Video Service Application
## on AWS Elastic Beanstalk

To run the application:

1. Right-click build.gradle
2. Gradle->Tasks Quick Launcher
3. Tasks:  build
4. Creates WAR file in build/libs
   using the name and version specified in build.gradle
5. Note that this application does not need to be hard-wired with 
   Amazon AWS account credentials.  Instead, IAM is used
   to provide access management

## Deploying the Application to Amazon Elastic Beanstalk

This application will use a DynamoDB table called "Videos"
As specified in Video.java with this AWS annotation:
  @DynamoDBTable(tableName = "Videos")


## Accessing the Service
To view a list of the videos that have been added, open your browser to the following
URL

GET
http://iamvideosvc.elasticbeanstalk.com/video

POST /video/ HTTP/1.1
Host: iamvideosvc.elasticbeanstalk.com
Content-Type: application/json
Cache-Control: no-cache
Postman-Token: 427f9434-a63e-58d0-852a-33adb4aec656

{"name":"myvideo1","url":"http://amazon.com/myvideo1.mpg","duration":1234}



## What to Pay Attention to

In this version of the VideoSvc application, we are using DynamoDB to store data.
See the Video class for the annotation changes that this requires. 

See the Application class for the configuration of your Amazon AWS credentials.
In this case, using IAM and the method InstanceProfileCredentialsProvider()
to dynamically provide access to DynamoDB using a EC2 instance profile and a
IAM role with access policies.

An ApplicationServletInitializer class has been added to boostrap the application 
when it is deployed to a stand-alone Tomact instance in Amazon Elastic Beanstalk.

