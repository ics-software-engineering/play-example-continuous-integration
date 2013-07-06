Summary
=======

The goal of this project is to illustrate how to set up a Play application, hosted on GitHub, 
to use CloudBees for continuous integration. In addition, it illustrates how to incorporate 
quality assurance tools (Checkstyle, PMD, FindBugs, and Jacoco) into continuous integration.
Finally, it also illustrates how to trigger deployment from your CI process.

Note that this procedure is tedious and complicated for first-time users of CloudBees.  Luckily, 
once you have successfully set up your first Play application on GitHub to use CloudBees for CI,
you can use it as a template for setting up future projects, and the procedure is much easier. 

One Time Configuration (OTC) Steps
==================================

OTC Step 1: Set up your GitHub account and host your Play application
---------------------------------------------------------------------

Begin by setting up an account on GitHub and hosting your Play application using it.  Follow the 
[excellent instructions](https://help.github.com/articles/set-up-git) if you 
haven't done this before.  

You might want to fork this play-example-continuous-integration repo if you want to quickly set up a basic Play application 
with which to play with continuous integration.   This repo also includes the quality 
assurance tool enhancements documented in [play-example-quality-assurance](http://ics-software-engineering.github.io/play-example-quality-assurance/).

OTC Step 2: Set up your CloudBees account and create a sample Play application
------------------------------------------------------------------------------

**Step 2A: Create a ClickStart Play Application**

Now set up an account on CloudBees. After you have created your account, use [ClickStart](https://developer.cloudbees.com/bin/view/RUN/ClickStart) 
to automagically create a sample Play application.  While running the Play ClickStart, CloudBees will:
  * Create a git repo to hold the source for the sample app.
  * Create a database connected to the sample app.
  * Set up a Jenkins build job for the sample app.
  * Build the sample app using the Jenkins job.
  * Deploy the sample app to the CloudBees hosting platform.
  
This, clearly, is pretty sweet, and you'll want to keep this sample app around for reference purposes. 
Doing the ClickStart also provides a sanity check that you can create, build, and deploy Play apps
on CloudBees.

**Step 2B: Install CloudBees SDK**

Now install the [CloudBees SDK](http://developer.cloudbees.com/bin/view/RUN/BeesSDK). 

Once installed, download the code for the sample Play app you created using ClickStart to your local
workspace. To do this successfully, you will need to provide your public key to CloudBees so it
can authenticate you when you pull the code using git. Here are some useful references:
  * [How to set your public key for git access in CloudBees](http://wiki.cloudbees.com/bin/view/DEV/How+to+set+your+Public+Key+for+Git+Access)
  * [Git Troubleshooting on CloudBees](http://wiki.cloudbees.com/bin/view/DEV/Git+-+Getting+Started#HTroubleshooting)
  * [Help for "Permission denied (public key)"](https://help.github.com/articles/error-permission-denied-publickey)
  
Once you've downloaded the application, invoke "play test" to see that the system compiles and 
runs its tests successfully in your local environment.  
   
Once you are comfortable with a "vanilla" version of a Play application on CloudBees, it is now time
to start customizing it for continuous integration with GitHub.

OTC Step 3: Configure CloudBees Jenkins plugins
-----------------------------------------------

**Step 3A: Install GitHub plugin**

In CloudBees, click on the "Builds" button in the nav bar to bring up your Jenkins instance, then 
click on "Manage Jenkins" in the left side menu bar. This brings you to the following page:

<img src="https://raw.github.com/ics-software-engineering/play-example-continuous-integration/master/images/manage-jenkins.png"/>

Click on "Manage plugins", click on "Available", find "GitHub Plugin", and then install and restart your Jenkins instance.
After doing that, you should see the following near the bottom of the list of "Installed" plugins in Jenkins:

<img src="https://raw.github.com/ics-software-engineering/play-example-continuous-integration/master/images/github-plugin.png"/>

Now go back to the "Manage Jenkins" page, and instead of clicking on "Manage Plugins", click on 
"Configure System". You'll find a "Git plugin" section halfway down the page. Provide your user.name
and user.email values as illustrated below:

<img src="https://raw.github.com/ics-software-engineering/play-example-continuous-integration/master/images/git-plugin-config.png"/>

Scroll down to the bottom of the page, and make sure that "Manually manage hook URLs" is selected:

<img src="https://raw.github.com/ics-software-engineering/play-example-continuous-integration/master/images/manually-manage-hook-url.png"/>


**Step 3B: Install QA plugins (Optional)**

Part of the allure of continuous integration is the ability to run quality assurance tools such 
as Checkstyle, PMD, FindBugs, and Jacoco in the cloud and to see trends in the issues reported
by those tools over time. To provide good reporting on these tools, you will want to install their
associated plugins as well.  This is an optional step.

Following the same process as before, go to the "Manage Jenkins" page, click on "Manage Plugins", 
and install the "Static Analysis Utilities", "Static Analysis Collector Plug-in", "FindBugs Plug-In", 
"Jenkins JaCoCo Plugin", "PMD Plugin", and "Checkstyle Plugin". Restart Jenkins. When all of these have been 
installed, the "Available" tab in the Manage Plugins page should contain the following:

<img src="https://raw.github.com/ics-software-engineering/play-example-continuous-integration/master/images/qa-plugins.png"/>

**Step 3C: Install and configure build status badge (Optional)**

It's nice to be able to display the status of continuous integration in your GitHub page.  Here's 
an example from the bottom of the [play-example-quality-assurance project's README page](https://github.com/ics-software-engineering/play-example-quality-assurance):

<img src="https://raw.github.com/ics-software-engineering/play-example-continuous-integration/master/images/build-status-badge.png"/>

If you want this (and of course you do), you must first install the "embeddable-build-status" plugin
to Jenkins.  Go to "Manage Jenkins", then "Manage Plugins", then install embeddable-build-status.
Restart Jenkins.  Once Jenkins has restarted, you should see the following near the bottom of the 
"Available" tab in the Manage Plugins page:

<img src="https://raw.github.com/ics-software-engineering/play-example-continuous-integration/master/images/embeddable-build-status.png"/>

Now you must configure Jenkins to support anonymous access by following the instructions [here](https://developer.cloudbees.com/bin/view/DEV/AnonymousAccess).
In brief, you must:
  1. Provide the Jenkins anonymous role with "Job/Read" access.
  2. Flip the switch for anonymous access by going to "Manage Jenkins", then "Configure System", then clicking "Enable read-only access for anonymous users", and finally clicking "Save".


OTC Step 4: Tell GitHub your CloudBees public key
-------------------------------------------------

In order for the CloudBees Jenkins server to obtain your GitHub project via git, GitHub needs
to be given your CloudBees public key. Follow the instructions [here](http://wiki.cloudbees.com/bin/view/DEV/How+to+use+Private+GitHub+Repositories+with+CloudBees). 
Though these instructions say they are necessary for private GitHub repositories, actually you need
to do this even if your repository is public.  In brief:
  1. In CloudBees, go to Jenkins, then click on "Manage Jenkins", then click on "Configure System".  In the "CloudBees DEV@Cloud Authorization" section, there is a field named "CloudBees Public Key". Copy the contents of that field.   
  2. In GitHub, go to Account Settings, click on "SSH Keys", then click "Add SSH Key", then paste your CloudBees public key and name it something like "CloudBees".

When you're done, your GitHub SSH Key page should look something like this:

<img src="https://raw.github.com/ics-software-engineering/play-example-continuous-integration/master/images/github-public-keys.png"/>











