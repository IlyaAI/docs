---
title: Deploy your first Java web app
position: 3
description: How to deploy your first Java web app with Octopus Deploy.
---

You can use Octopus Deploy to deploy Java web apps files to your web app server. In this quick-start we’ll deploy a Java war file from the built-in Octopus Deploy Library to Apache Tomcat. We’ll run through the following steps:

1. Applying the versioning scheme.
1. Uploading the app to the built-in Octopus repository.
1. Defining a process in Octopus Deploy.
1. Creating a release.
1. Deploying the app.
1. Updating the app.
1. Redeploying the app.

We recommend that you configure your existing build tool to push packages automatically to the built-in repository, but for the purposes of this quick-start, we’re going to do this step manually.

### What you need

To complete this quick-start you need:

* Access to a working instance of [Octopus Deploy](/docs/getting-started/quick-start/install-a-trial-version-of-octopus-deploy.md).
* A machine running:
	* [Octopus Tentacle](/docs/getting-started/quick-start/configure-your-infrastructure.md).
	* A Java web app server.
* A sample war file to deploy.

### Upload the app to the Octopus Deploy Library

**Octopus Deploy** has a built-in repository that we will use to upload our war file, from there we can deploy it to the web app directory on our server.  

1. Apply the version number 0.0.1 to the war file. For instance, octopus-0.0.1.war.
1.  If you’re not already logged into the **Octopus Web Portal** do so now, and navigate to the **Library** and select **Packages**.

	![library packages](library-packages.png width="500")

1. Click **Upload packages** and browse to the file you want to upload and click **Upload**.

Octopus will give the package an ID based on the filename you uploaded. In our example, *octopus-0.0.1.war* the package ID is *octopus-0*.  


### Define a project

A project is a collection of deployment steps and configuration variables that you want to run during deployment.

1. Navigate to the **Projects** menu {{Projects>All}} and click **Add project**.
1. Give the project a name and description, and save the project. For instance, *Web app*.

### Define the deployment process

A deployment process specifies the steps to deploy an application. Here we'll define the process to deploy our web app.

1. Select **Process** and then click **Add your first step**.
1. Select **Deploy Java Archive**.

	![Deploy Java archive](deploy-java-archive.png width="500")
1. Name the step. For instance, *Deploy archive*.
1. Select roles under **Runs on targets in role**. We defined this as *Test-server* when we configured our test infrastructure.
1. Select the **Package-ID**. This will autocomplete when you start to type. The package ID in our example is *octopus-0*.
1. Tick **Custom Deploy Directory** and add the path to the web app directory in your server. For instance, *C:Users\test\Desktop\tomcat\webapps*.
1. For the **Deployed Package File Name** we need to enter the name of the war file without the version number. This ensures the path to the web app doesn’t change with every new release. For instance, *octopus.war*.
1. **Save** the process.  

### Create a release

1. Click **Create release** from the projects dashboard.
1. The details for the process are automatically filled in on the create release screen.

![Create release](create-release.png width="500")

1.  Add a note for the release notes, and click **save**.

### Deploy the release

1. Click **Deploy to Test Environment**, and then click **Deploy now**.
2. Progress is displayed on the screen.
4. Navigate to the sample app on your web server: *localhost:8080/octopus*.

### Update the app

In this step, we’ll update the app and upload it to the built-in repository ready to be deployed.

1. Edit the war file to include a change. For instance, add the string *Version 0.0.2*.
2. Increment the version number in the filename: *octopus-0.0.2.war*.
3. Upload the new file to the **Octopus Deploy Library**. From the **Library** page, select **Packages**, and click **Upload package**.
4. Browse to the file *octopus-0.0.2.war* and click **upload**.

Note, on the packages page, the latest version for the package *octopus-0* is now **0.2**.

### Create the next release and deploy

Next, we’ll release the updated version of the app.

1. Navigate to the project you defined earlier in this quick-start: {{Projects>Web App}}.
2. Click **Create a release**. Add a note for the release notes, and click **Save**.
3. Click **Deploy to Test Environment**, and then click **Deploy now**.
2. Task progress is displayed on the screen.

### Test it worked

Navigate to the sample app on your web server: *localhost:8080/octopus*, and you’ll see the updated app.
