# Chapter 7 - Freestyle Jobs

## Chapter Overview
In this chapter, we will go over Freestyle jobs and explain how you can use them to create CI/CD workflow.

## Learning Objectives
By the end of this chapter, you should be able to:

* Describe what a Jenkins Freestyle job is.
* Configure a Freestyle job.

## What Is a Jenkins Freestyle Job?
A Freestyle job is by far the most versatile of all the Jenkins job types. It allows you to build any type of project (Ant, Maven, Gradle, shell script, Makefile), and it is included in Jenkins by default without the need to install additional plugins.

## Create a New Freestyle Job
For our example Freestyle job, we will use a small Java application. We will configure all the necessary tasks for this job such as retrieving the Java source code from version control, compiling and building it, running tests, publishing the code coverage and static analysis reports and notifying the team about the status of the build.

Let’s get started.

To create a new Freestyle job, click Jenkins > New Item on the side navigation bar of the Jenkins dashboard.

<img src="https://courses.edx.org/assets/courseware/v1/8915b567ba798380eca457c4df9046ef/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/jenkins-create-project.png" alt="" />

This opens up a new subpanel listing various project types. Enter a name for the job, select Freestyle project from the list of available project types, and click OK.

<img src="https://courses.edx.org/assets/courseware/v1/d74bf8e9c3ec282132a679c184261e62/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/freestyle-job.png" alt="" />

This will take you to the configuration page for the new Freestyle job you have just created.

Next, we will configure our Freestyle job **java-app** to build a Maven project. Maven is a software project management tool used to build Java projects.


## Configure Freestyle Job
The **java-app** project requires Java version 8. You can specify this dependency under the General section of java-app job configuration. However, you need to ensure that the Java 8 is first installed on your Jenkins server.

Jenkins allows you to easily manage various tools and their versions all under Jenkins > Manage Jenkins > Global Tool Configuration page.

<img src="https://courses.edx.org/assets/courseware/v1/3588431e97fff5c00d3242c031965380/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Global-Tool-Configuration.png" alt="" />

On this page, click the **Add JDK** button under the JDK installations section to configure multiple JDK versions.

<img src="https://courses.edx.org/assets/courseware/v1/143bb99545d9f89a2d36a57da256db16/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-jdk.png" alt="" />

<img src="https://courses.edx.org/assets/courseware/v1/143bb99545d9f89a2d36a57da256db16/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-jdk.png" alt="" />

Next, follow these steps:

* Add a Name for the Java version you are trying to install.
* Check the toggle for Install automatically.
* Choose the JDK Version from the dropdown.
* Enter the credentials for your Oracle account.
* Check the License Agreement checkbox.
* Click Save.

<img src="https://courses.edx.org/assets/courseware/v1/9b080f04e9b32f69f8b45272481aa812/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/addd-java-8.png" alt="" />

Note that you can also use other Installers to install different versions of JDK. Just click the downward arrow on the Add Installer dropdown to view all the available options.

Once you have configured the JDK tool version, this will show up under the **General** section of your **java-app** project configuration page.

<img src="https://courses.edx.org/assets/courseware/v1/ace2481e05077f565140ea8bd29f1e8d/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/jdk-versions-jenkins-job.png" alt="" />

## Source Code Management
To build the **java-app** project, you need to fetch its source code from a version control system. The source code for our **java-app** project is hosted on GitHub.

Next, we will configure the Git repository:

* Scroll down to the Source Code Management section.
* Select "Git".
* Enter Repository URL (git@github.com:dhgautam/demo-javapp.git).
* Select Credentials to authenticate to the SCM repository.
* Click Add > Jenkins to add the SCM credentials.

<img src="https://courses.edx.org/assets/courseware/v1/162e45c5e7a2c86d88700bd8d5428042/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-credentials.png" alt="" />

Once the SCM credentials are added, you can view and select them from the credentials dropdown list.

<img src="https://courses.edx.org/assets/courseware/v1/75e070df26d82c269abd564c785eab76/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/choose-credenitals.png" alt="" />

For our **java-app** project, we will select the **master** branch. Click Save to save your SCM configuration.

<img src="https://courses.edx.org/assets/courseware/v1/150faf8130eab2199c48c4b7c702cc62/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/addl-options-scm.png" alt="" />

Note that you can also choose a specific branch in a repository, a repository browser, and advanced options for integrating with your repository. Next, we will configure the build triggers for our **java-app** job.

## Build Triggers
For our java-app project, we will use **Poll SCM** build trigger and set the polling to every 15 minutes.

<img src="https://courses.edx.org/assets/courseware/v1/28c1a0428d17cd61b67a5f81258c71b6/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/poll-scm.png" alt="" />

## Build Environment
We will just add a timestamp to the build console output. To enable this, check the toggle for Add timestamps to the Console Output.

<img src="https://courses.edx.org/assets/courseware/v1/a74ecced8c30e46cddc2ce170b962af1/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/enable-timestamp.png" alt="" />

## Build
In this section, we will compile and build our **java-app** project, run tests, and generate the required reports for code quality and code code coverage.

We will start with adding a build step, Add build step > Invoke top-level Maven targets.

<img src="https://courses.edx.org/assets/courseware/v1/28e3feb1bdf49b4decbf1d2e47804d5b/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-steps.png" alt="" />

This will add a new build step and configure it as follows:

* Maven Version: maven3

Note that we are using Maven version 3. To use this version, you need to install the Maven 3 version via Jenkins > Manage Jenkins > Global Tool Configuration.

* Goals: clean verify site

clean: will wipe out any existing compiled sources in the target directory and start the build from a clean state

* verify: will run any checks to verify the package is valid and meets quality criteria
* site: will generate **java-app** project code coverage and static analysis reports

Next, click on the Advanced button.

<img src="https://courses.edx.org/assets/courseware/v1/9c97f0dc3e3cd8b5b1a8a7210fc56636/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/mvn-goals.png" alt="" />

This will display additional configuration options. We will just specify the location of the POM file and leave all other fields set to their default values.

POM: java-demo-app/pom.xml

<img src="https://courses.edx.org/assets/courseware/v1/2cee73307c094924b656b5a509a1f448/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/mvn-build-goals.png" alt="" />

Click Save to save the configuration.

We are done with configuring the build step. Next, we will configure the post-build actions.

## Post-Build Actions
For our **java-app** project, we will configure the following post-build actions:

* Archive the build artifacts so we can use them later.
* View code coverage trends so we can see the percentage of code that is executed as part of the tests.
* View static analysis trends so we can measure the code defects.
* Notify the team on the build status so that developers and team members can get quick feedback on the build, and take any necessary actions.

Let's start with archiving the build artifacts.

#### Archive Build Artifacts
Our **java-app** project generates a **Java ARchive (JAR)** file. To archive the file for later use, choose Add post-build action > Archive the artifacts...

<img src="https://courses.edx.org/assets/courseware/v1/49f6d3246275225ed3eb98b7175010bf/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/archive-artifact-post-build.png" alt="" />

...and specify the location of the JAR file.

Files to to archive: **/target/*.jar

This will look for all files with **.jar** extension recursively under all target directories from the workspace’s root.

<img src="https://courses.edx.org/assets/courseware/v1/c7bb7d65c0030cd17353fd39bc006262/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/archive-artifacts.png" alt="" />

Next, we will configure publishing the code coverage reports that are generated as part of the build step.

#### Publish Code Coverage Report
For our java-app project, we are using JaCoCo, a code coverage tool for Java. To enable publishing JaCoCo reports, you first need to install the JaCoCo plugin. This will add a new option to record code coverage reports under post-build actions.

Next, choose Add post-build action > Record JaCoCo coverage report.

<img src="https://courses.edx.org/assets/courseware/v1/d060d755ed8c44bab018d3382bdd856e/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/post-build-jacoco.png" alt="" />

Configure the following and leave all other fields set to their default values:

<img src="https://courses.edx.org/assets/courseware/v1/649a889bf3814e68278637290057d26f/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/configure-jacoco.png" alt="" />

Next, we will add a new step to publish static analysis reports. And then finally, we will configure email notifications for our **java-app** job.

#### Static Analysis Reports
Our java-app project uses the following two tools: SpotBugs and PMD. Both of which help detect defects in Java code.

First, you need to install the Warnings Next Generation plugin. This will add a new option to record your static analysis reports under post-build actions.

Choose Add post-build action > Record compiler warnings and static analysis results.

<img src="https://courses.edx.org/assets/courseware/v1/46e6f2cb7b16f2d6868c64ec0a4567b1/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/compiler-warnings.png" alt="" />

Under the configuration for Static Analysis, click Add Tool.

<img src="https://courses.edx.org/assets/courseware/v1/4b80992cdbb92c600cb7ef87f15a2e15/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/record-compiler-warnings-add-tool.png" alt="" />

From the drop down menu, select SpotBugs.

<img src="https://courses.edx.org/assets/courseware/v1/01bc9cf9c2c5387d34b75e9da049453c/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/configure-spotbugs.png" alt="" />

Next, we will add the second tool - **PMD**. In order to do that, set Report Encoding to UTF-8 and leave all other fields set to their default values.

<img src="https://courses.edx.org/assets/courseware/v1/aa3fe881aacce17f0543061325021fc7/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/configure-PMD.png" alt="" />

#### Email Notifications
Jenkins provides out of the box email support to send notifications to team members.

Choose Add Post-build action > Email Notification, and specify the target recipients for the emails. Click Save to save your configuration.

<img src="https://courses.edx.org/assets/courseware/v1/2742c5a7f253253325ba78a50093062b/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/email-notification.png" alt="" />

You might want to take a look at the Email Extension plugin, if you are looking to customize your email notifications.

We are now done configuring the **java-app** freestyle job. It’s time to start a new build and see things in action!

## Build History
Click Build Now on the side navigation of the java-app job to trigger a new build.

<img src="https://courses.edx.org/assets/courseware/v1/39819dbc0becb975824b6ee87a1d18f5/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-now.png" alt="" />

Once the build is completed, you should be able to view all the relevant information such as build number, build date, SCM changes, name of the user who started the build, console output, artifacts, code coverage report, static analysis report, etc.

<img src="https://courses.edx.org/assets/courseware/v1/c1d8e605e79a3b9acf81fda484c9c500/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Build-1.png" alt="" />

When you run this job more than once, you can view the build history, code coverage and static analysis trends, etc., on the java-app project page.

<img src="https://courses.edx.org/assets/courseware/v1/712f099008adc43fcb44d605716d54b9/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-trend.png" alt="" />

We highly recommend that you configure your own Freestyle job. You can use the Java source code from the GitHub repository.
