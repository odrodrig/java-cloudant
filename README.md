# Java Cloudant Sample

This application demonstrates how to use the Bluemix Cloudant NoSQL Database service. It helps users organize their favorite files. The UI talks to a RESTful JAX-RS CRUD backend API.

## Section 4. Building and Running the app in the command-line

In this section, we will use the maven cli and the ibmcloud cli to build and deploy our application. 
If you are interested in using Eclipse to build and deploy the application, the instructions can be found in Appendix D.

1.	Navigate to the directory where you cloned the project.
2.	Execute full Maven build to create the `target/JavaCloudantApp.war` file:
```bash
   $ mvn clean install
```

3.	Download and start a local Liberty server with the application:
```bash
   $ mvn liberty:run-server
```

4.	 Once the server is running, the application will be available under http://localhost:9080/JavaCloudantApp
You should be able to load the page but there will be a red Error underneath the Help link.
At this point the application only partially functions because it can’t find the service credentials for the Cloudant database in the environment. When running in IBM Cloud, we bind the service instance to the application, this will make the service credentials available to the application through environment variables.
5.	Update the application details in the `manifest.yml` file. IBM Cloud will reference the manifest when deploying the application to get the application name, memory allocation, services to bind, and more. Open the manifest.yml file and make the following edits:
•	Change the name of your application to something unique. Typically adding your initials to the beginning of the app name should be enough. 
•	Change the Cloudant service name under services. You can find the Cloudant service name by going to the IBM Cloud dashboard and finding the Cloudant instance.
	

Your manifest.yml should look similar to the one below except for the different app name and service name. Be sure to save your changes.



Here’s a little explanation of what is going on in each of the fields in this manifest:
*	Name – Application name
*	Memory – The memory allocation of the application. IBM Cloud Lite accounts only have 256MB to play with so you may need to stop other apps that are running to make space available. 
*	Path – This is where IBM Cloud will look for your application. In this case, we are pointing to our WAR file in the target directory.
*	Services – Any services listed here will be bound to your application during deployment. It is important to note that the services must have been created beforehand in order for this to work.

6.	Now time to deploy. Ensure you are still targeting the correct region, org, and space by running the following command:
```bash
$ ibmcloud target
```
	

7.	Run the following command to push the application to IBM Cloud:
$ ibmcloud app push
	

Right away you will notice that your manifest.yml file has been recognized and the attributes you specified will be used for the deployment.
The deployment will take a minute or two but when it’s done, you should see the following:


8.	Go to your IBM Cloud dashboard and look for your newly created app and click on it. 
9.	Find the Visit App URL link at the top of the page and click on it to go to the application.
10.	Now you can play with the app check out the awesome sample.txt file and even upload your own files.

## Section 5. Updating and redeploying the app

Now that we have an app deployed, let’s go through the steps to make an update and push the change.
1.	Open your application in a code editor and navigate to the following file:
```
../src/main/webapp/index.html
```

2.	Find the appTitle on line 15 that starts with “Favorites Organizer ...”.
3.	Add a few exclamation points to the end of the title to show how excited we really are.

4.	Save your changes
5.	In your terminal run the following command to build the application:
```bash
$ mvn clean install
```

6.	Deploy the application again by running the following command:
```bash
$ ibmcloud app push
```

7.	After your app has successfully deployed, refresh the page in the browser and you should see you new more exciting title. 


## Developing and Deploying using Eclipse

IBM® Eclipse Tools for IBM Cloud provides plug-ins that can be installed into an existing Eclipse environment to assist in integrating the developer's integrated development environment (IDE) with IBM Cloud.

1. Download and install  [IBM Eclipse Tools for IBM Cloud](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_IBM_Cloud).

2. Import this sample into Eclipse using `File` -> `Import` -> `Maven` -> `Existing Maven Projects` option.

3. Create a Liberty server definition:
  - In the `Servers` view right-click -> `New` -> `Server`
  - Select `IBM` -> `WebSphere Application Server Liberty`
  - Choose `Install from an archive or a repository`
  - Enter a destination path (/Users/username/liberty)
  - Choose `WAS Liberty with Java EE 7 Web Profile`
  - Continue the wizard with default options to Finish

4. Run your application locally on Liberty:
  - Right click on the `JavaCloudantApp` sample and select `Run As` -> `Run on Server` option
  - Find and select the localhost Liberty server and press `Finish`
  - In a few seconds, your application should be running at http://localhost:9080/JavaHelloWorldApp/

5. Create a Bluemix server definition:
  - In the `Servers` view, right-click -> `New` -> `Server`
  - Select `IBM` -> `IBM Bluemix` and follow the steps in the wizard.
  - Enter your credentials and click `Next`
  - Select your `org` and `space` and click `Finish`

6. Run your application on Bluemix:
  - Right click on the `JavaCloudantApp` sample and select `Run As` -> `Run on Server` option
  - Find and select the `IBM Bluemix` and press `Finish`
  - A wizard will guide you with the deployment options.
  - Select your Cloudant service on the Services step
  - In a few minutes, your application should be running at the URL you chose.

Now you have your code running locally and on the cloud!