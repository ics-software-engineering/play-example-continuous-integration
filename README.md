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

Begin by setting up an account on GitHub and hosting your Play application there.  Follow the 
[excellent instructions](https://help.github.com/articles/set-up-git) if you 
haven't done this before.  

You might want to fork this project if you want to quickly set up a basic Play application 
with which to play with continuous integration.   This project also includes the quality 
assurance tool enhancements documented in [play-example-quality-assurance](http://ics-software-engineering.github.io/play-example-quality-assurance/).

Step 2: Set up your CloudBees account and create a sample Play application
--------------------------------------------------------------------------

Now set up an account on CloudBees. After you have created your account, use [ClickStart](https://developer.cloudbees.com/bin/view/RUN/ClickStart) 
to automagically create a sample Play application.  After running the Play ClickStart, CloudBees has:
  * Created a repository for the sample app.
  * Created a database connected to your app.
  * Set up a Jenkins build job for your app.
  * Built your app using the Jenkins job.
  * Deployed your built app to the CloudBees hosting platform.
  
This, clearly, is pretty cool.  







