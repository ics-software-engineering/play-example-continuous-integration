Summary
=======

The goal of this project is to illustrate how to set up a Play application, hosted on GitHub, 
to use CloudBees for continuous integration. In addition, it illustrates how to incorporate 
quality assurance tools (Checkstyle, PMD, FindBugs, and Jacoco) into continuous integration.
Finally, it also illustrates how to trigger deployment from your CI process.

Note that this procedure is tedious and complicated for first-time users of CloudBees.  Luckily, 
once you have successfully set up your first Play application on GitHub to use CloudBees for CI,
you can use it as a template for setting up future projects, and the procedures is much easier. 

Steps
=====

Step 1: Set up your GitHub account and host your Play application
-----------------------------------------------------------------

Begin by setting up an account on GitHub and hosting your Play application using it.  Follow the 
[excellent instructions](https://help.github.com/articles/set-up-git) if you 
haven't done this before.  

You might want to fork this play-example-continuous-integration repo if you want to quickly set up a basic Play application 
with which to play with continuous integration.   This repo also includes the quality 
assurance tool enhancements documented in [play-example-quality-assurance](http://ics-software-engineering.github.io/play-example-quality-assurance/).

Step 2: Set up your CloudBees account and create a sample Play application
--------------------------------------------------------------------------

**Step 2a: Create a ClickStart Play Application**

Now set up an account on CloudBees. After you have created your account, use [ClickStart](https://developer.cloudbees.com/bin/view/RUN/ClickStart) 
to automagically create a sample Play application.  While running the Play ClickStart, CloudBees will:
  * Create a git repo to hold the source for the sample app.
  * Create a database connected to the sample app.
  * Set up a Jenkins build job for the sample app.
  * Build the sample app using the Jenkins job.
  * Deploy the sample app to the CloudBees hosting platform.
  
This, clearly, is pretty sweet, and you'll want to keep this sample app around for reference purposes. 
ClickStart also ensures that you've set things up correctly.

**Step 2b: Install CloudBees SDK**

Once you have a sample app deployed using ClickStart, you should install the [CloudBees SDK](http://developer.cloudbees.com/bin/view/RUN/BeesSDK).   







