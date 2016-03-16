Progress Corticon Docker Official Images
===================
Base docker image to run a corticon server using tomcat-7.

Supported tags
------------------------
* corticon/docker
* corticon/docker:5.5.latest
* corticon/docker:5.5.2.4

What is Progress Corticon?
===================
Progress Corticon is a high-powered business rules engine without limits. It expands automated business rules capabilities and delivers a quicker, easier and more cost-effective decision automation solution -unencumbered by technology and business constraints. For more information, please see [Progress Corticon](https://www.progress.com/corticon)

How to use this image
===================
To use the different Corticon images  create a Dockerfile. Start with Corticon image of your choice. You can start by using any of the supported tags listed above or start with the latest.
    # Using the latest Corticon Image
       FROM suvasri/corticon
    # You need to add the license file to the Corticon Work directory
       ADD CcLicense.jar /opt/corticon/work/        


Please contact [Corticon License](https://www.progress.com/company/contact) if you don't have a valid license or would like to request one.

To deploy decision services. Copy the decision service .eds files and the .cdd file to the CDD directory
    # Copy decision services to the CDD directory
      ADD Order.eds /opt/corticon/work/cdd/
      ADD Allocation.eds /opt/corticon/work/cdd 
      ADD OrderProcessing.cdd /opt/corticon/work/cdd/     
When the Corticon Server starts up, it will discover and deploy the decision services into the docker image.

To enable the Corticon Server to use brms,properties. Copy the brms.properties file to the Corticon Work directory
    # Add brms.properties to CORTICON_WORK
      ADD brms.properties /opt/corticon/work/
This will create your corticon server using the properties specified in the brms.properties file. For more information about the brms.properties file refer to [Corticon Documentation](https://documentation.progress.com/output/ua/Corticon/)

To change the user settings for the Corticon Web Console. 
     # Add the serverconsole-user.xml to the CcServerSandbox/ServerConsole directory
       ADD serverconsole-user.xml /opt/corticon/work/CcServerSandbox/ServerConsole/
For more information about the serverconsole-user.xml please see [Corticon Documentation](https://documentation.progress.com/output/ua/Corticon/)

To deploy an .eds which uses your extensions. Copy the extensions.jar to the Corticon Work Directory/CorticonExtensions as shown below
     # Add extensions jar to the Corticon Work Directory/CorticonExtensions
       ADD [YOUR_EXTENSIONS_JAR_NAME].jar /opt/corticon/work/CorticonExtensions/

Replace **[YOUR_EXTENSIONS_JAR_NAME] ** with the extensions jar name.

This is all that is needed in your Docker file.

How to build this image
===================
The following command builds the Corticon's Docker image using the Dockerfile created from the above options
```  
 $docker build -t corticon .
```
The above command builds the Docker image and registers it in the local image repository. This image is now ready to be deployed.

Deploying the Corticon Image
===================
Once the image is available in the local registry, the process of provisioning a container and deploying the image is trivial.
```  
$ docker run –p 8080:8080 corticon
```
The above command creates the container using the Docker defaults for CPU shares, memory size and other resources. The -p flag maps the host's port to the containers's port. We are mapping the host's 8080 port to the container's 8080 port.

Once the container is started Corticon server can be accessed using the host’s IP. e.g.
``` 
http://192.168.99.100:8080/axis/
``` 
License
===================
View license information for the software contained in this image.
User Feedback
===================
Documentation
-------------------------------
Be sure to familiarize yourself with README.md before attempting a pull request. Documentation can also be found on Github repo. For Corticon related documentation refer to [Progress Corticon Documentation](https://documentation.progress.com/output/ua/Corticon/)

Issues
----------------------------
If you have any problems with or questions about this image, please contact us through corticon-docker@progress.com
