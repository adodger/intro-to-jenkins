# Chapter 8 - Pipeline Jobs

## Chapter Overview
In this chapter, we will go over Pipeline jobs and explain how you can use them to create CI/CD workflows.

## Learning Objectives
By the end of this chapter, you should be able to:

* Explain what a Pipeline job is.
* Configure a Pipeline workflow.

## Freestyle vs Pipeline Jobs
You should have noticed by now that Jenkins is mostly UI-centric, meaning all the jobs are manually configured through the UI. If you recall from Chapter 1, Continuous Delivery heavily relies on seamless end-to-end automation. Although Freestyle jobs provide you with a lot of flexibility to configure jobs, they are not quite suitable to orchestrate complex CD scenarios. For example, if you want to build and test on a variety of OS platforms in parallel, or when you are waiting for some manual approval prior to deployment, etc.

Although you can create job hierarchies with Freestyle jobs for representing multi-stage workflows, such strategy requires you to spread job configuration across multiple jobs. Thus making it difficult to manage and maintain them as a simple change in one job might adversely affect the others. But that's not all, you might find it challenging to visualize a workflow spanning multiple Freestyle jobs.

This is where Jenkins Pipelines come to your rescue by helping you:

* Create a set of instructions written as a code to model complex workflows.
* Provide a single-place visualization of different stages of your workflow.
* Keep all the Pipeline code stored in SCM, so you can apply SCM best practices such as versioning, tracking and auditing to the job configuration itself.

## Pipelines
Pipeline is a new Jenkins job type and a new way to model and visualize CI/CD workflow for a project. It is created by writing a bunch of instructions in a file called **Jenkinsfile**. The Jenkins Pipeline uses a domain-specific language based on Apache Groovy to create, edit, view, and run CD pipelines.

A Jenkinsfile can use either of the following two syntaxes:

* Declarative Pipelines: They require the Blue Ocean plugin to be installed. You can easily create your Jenkinsfile using the Blue Ocean graphical pipeline editor. It also provides you with a great visualization of your pipeline runs.

* Scripted Pipelines: With scripted pipelines, you have the option of creating the Jenkinsfile using the classic Jenkins UI. This means you will be creating the Jenkins job using the Pipeline job type. While scripted pipelines offer a lot of flexibility, they also require you to have a knowledge of Apache Groovy.

It is worth noting that there is a lot of commonality in the syntactical components between declarative and scripted pipelines.

It is best to start out with declarative pipelines, and as you get comfortable with them, you can move on to scripted pipelines. For the remainder of this chapter, we will focus on declarative pipelines.

## Pipelines Terminology
Prior to creating Pipelines, you need to know a few basic pipeline-related terms. Let's take a look at them:

* Master: A machine where Jenkins is installed. It centrally stores all the configurations, loads plugins and renders the Jenkins UI.

* Agent: A machine which connects to the Jenkins Master and performs various operations as directed by the Jenkins Master.

* Node: A machine that can allocate an executor and run Jenkins Pipelines. Examples are Jenkins Masters and Agents.

* Step: A single task that tells Jenkins what to do at a given point in time. Examples include: executing a simple shell script and windows batch script.

* Stage: It is composed of logically distinct steps. Build, Test, Deploy are all examples of Stages. Stages are used for visualization of the Pipeline status/progress.

For a complete list of pipeline-related terms, see Jenkins' Pipeline Glossary.

## Creating a Pipeline
We will now talk about creating pipelines using the Blue Ocean graphical editor. Let's start by creating a Pipeline to simulate a CI/CD workflow with the following set of stages:

* Build: In this stage, source code is compiled and built, and an artifact is generated.

* Test: In this stage, tests will be run in parallel on two different OS platforms, Linux and Windows.

* Deploy Staging: In this stage, the artifacts will be deployed to a staging environment (essentially a pre-production server). If everything is good, we will request for approval to deploy to production.

* Deploy Production: In this stage, artifacts will be deployed to the production environment.

<img src="https://courses.edx.org/assets/courseware/v1/84f76eb0b043a2f38f6553c7d8612fa7/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/pipeline-job-flow.png" alt="" />

We will also configure two post-build actions:

* Archive build artifacts
* Email notification in case of a build failure

Let's get started with creating the Pipeline.

## Creating a Pipeline: Open the Blue Ocean Editor
Once you install the Blue Ocean plugin, you should be able to view the Open Blue Ocean link on the side navigation. Click on this link to navigate to the Blue Ocean UI.

Note that Jenkins officially supports the latest versions of Google Chrome, Mozilla Firefox, Microsoft Internet Explorer, and Apple Safari web browsers. However, Chrome and Firefox seem to be the most consistent performers.

<img src="https://courses.edx.org/assets/courseware/v1/02feadafa5f8fcb9cdef8a905bef0dbe/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/blueocean-top-level-link.png" alt="" />

In the Blue Ocean UI, click **Create a new Pipeline**.

<img src="https://courses.edx.org/assets/courseware/v1/dc2e5166e4a586da246e79f91b857fcd/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/first-screen.png" alt="" />

## Creating a Pipeline: Configure SCM
Next, you will see a screen prompting you to configure your source code repository:

* Choose "Git" for Where do you store your code?

* Enter the Repository URL: git@github.com:<your_username>/demo-pipeline.git

* Click Copy to clipboard to copy the SSH key. Be sure to register the SSH key onto your Git server. Otherwise, you will not be able to authenticate to the repository. Note that Blue Ocean Pipeline editor only supports SSH protocol to connect to remote Git repositories since the Pipeline editor automatically saves the Pipeline code as a Jenkinsfile in the configured repository.

* Finally, click on the Create Pipeline button.

IMPORTANT: When you test this in your environment, please fork the Github repository and use your forked repository to configure your Pipeline job. This forked repository comes preloaded with the required build scripts.

<img src="https://courses.edx.org/assets/courseware/v1/0a81a97711cf2d6dcaf6fc4a6e6d7f04/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/configure-scm-pipeline-demo.png" alt="" />

To learn how to configure other SCM types, please refer to the Jenkins Documentation.

Since this is the first time you are creating a Pipeline, you will see a pop up message stating that there are no Jenkinsfiles in the SCM repository. Once you create and configure the Pipeline, its configuration code will get stored in the SCM repository as a Jenkinsfile.

<img src="https://courses.edx.org/assets/courseware/v1/4738b12b6f3a119236c7a6c35832c720/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/no-jenkinsfiles.png" alt="" />

Next, we will configure the stages for our Pipeline.

## Creating a Pipeline: Build Stage
If you recall Pipeline terminology, stages are composed of steps. As part of the Build stage, we will add two steps.

1. Print Message: This will print **Build demo-app**
2. Shell Script: This will run a build shell script

Click the **+** icon in the Pipeline editor to add a new stage.

<img src="https://courses.edx.org/assets/courseware/v1/d6f989736221817c50c59ca686d139a2/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/blueocean-ui.png" alt="" />

This will open a configuration panel for the new stage. Enter "Build" for Name your stage. Click on the Add step button below which opens the Choose step type panel.

<img src="https://courses.edx.org/assets/courseware/v1/239b920042c0bc1b4accf33ffd2f600f/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/configure-build-stage.png" alt="" />

In this panel, choose the Print Message step. This will open the Print Message configuration panel.

<img src="https://courses.edx.org/assets/courseware/v1/45cb3aebf149b983555f69e9d0bdfb83/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-print-message-step.png" alt="" />

Enter Build demo-app for the value, and click the top-left back arrow icon (←) to return to the main Pipeline editor.

<img src="https://courses.edx.org/assets/courseware/v1/605e945713a0390fe65877e20f7cbfea/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-actual-message-print-message.png" alt="" />

Next, we will add another step to incorporate our build script. Choose Shell Script from Choose Step type. This will open the Shell script configuration panel.

<img src="https://courses.edx.org/assets/courseware/v1/d36bf62643165d1a406e31bd97f1cfde/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/shell-script-step.png" alt="" />

Enter ```sh run_build_script.sh``` in the configuration panel.

<img src="https://courses.edx.org/assets/courseware/v1/357e1abbe86de73c04407932a975ff93/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-shell-script.png" alt="" />

## Creating a Pipeline: Test Stage
Next, we will add two parallel stages to run tests on Linux and Windows platforms.

#### Linux Tests Stage
In the Pipeline editor, click the + icon next to the Build stage to add a new stage. This will open a configuration panel for the new stage. Enter "Linux Tests" for Name your stage and click on the Add step button below, which opens the Choose step type panel.

We will add two steps similar to the build stage.

* Print Message: Specify Run Linux tests in its configuration panel.
* Shell Script: Specify **sh run_linux_tests.sh** in its configuration panel.

Next, click the + icon below the Linux Tests stage to create a parallel Windows Tests stage.

<img src="https://courses.edx.org/assets/courseware/v1/35e8ec2108a54cab81889227d2815fa5/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-parallel-windows.png" alt="" />

#### Windows Tests Stage
As part of this stage, we will just configure a single step Print Message, and specify Run Windows tests in its configuration panel.

<img src="https://courses.edx.org/assets/courseware/v1/3f01c77537914f5b6ac68d78f903332d/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-deploy-staging.png" alt="" />

Once both tests are successfully run, we will deploy the artifacts to a staging environment. Click the + icon next to the Linux Tests stage to add a new stage and specify "Deploy Staging" for the name.

## Creating a Pipeline: Deploy a Staging Stage
As part of this stage, we will add two steps.

The first step is Print Message. To start off, specify Deploy to staging environment in its configuration panel.

Please note that it's a common practice to seek approval prior to deploying in a production environment. And while deploying to the staging environment cannot be accomplished in the Freestyle job, we can easily add this as a step in our Pipeline job.

In order to do that, choose Wait for interactive input step from Choose step type. Note that the list of step types can be long. You may want to use the search filter available on the Choose step type panel to quickly find the step.

<img src="https://courses.edx.org/assets/courseware/v1/a26d697a54c531d764799bb664ab8dcb/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Add_Wait_for_interactive_input_step.png" alt="" />

In the Deploy Staging / Wait for interactive input panel, specify Ok to deploy to production? in the Message field. Leave other settings with their default values. Click the top-left back arrow icon (←) to return to the Pipeline stage editor.

<img src="https://courses.edx.org/assets/courseware/v1/34d8811b4ffa1ac78ff019e05f768297/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/configure-input-message.png" alt="" />

Next, we will configure the Deploy Production stage, which is the last stage in the Pipeline. Click the + icon next to the Deploy Staging stage to add a new stage and specify "Deploy Production" for the name.

<img src="https://courses.edx.org/assets/courseware/v1/dc9d7876e56d56d87792dd269d1d3ea4/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-deploy-prod-stage.png" alt="" />

## Creating a Pipeline: Deploy a Production Stage
As part of this stage, we will add a single step, Print Message, and specify Deploy to Prod in its configuration panel.

<img src="https://courses.edx.org/assets/courseware/v1/940533eb6317fc55c3552b4b745ef3ba/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/deploy-to-prod.png" alt="" />

## Creating a Pipeline: Post-Build Actions
At the time of this writing, the post-build actions cannot be configured through the UI. You need to add them to the Jenkinsfile directly. You can open Jenkinsfile from the Pipeline editor by clicking Command+S on MacOS, Ctrl+S on Windows, or the equivalent on other operating systems.

Add the following code snippet after the stages block.
```

post {
  always {
   archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
  }

failure {
      mail to: 'ci-team@example.com',
      subject: "Failed Pipeline ${currentBuild.fullDisplayName}",
      body: " For details about the failure, see ${env.BUILD_URL}"
     }
  }
```

Click on the Update button to update the Jenkinsfile for our demo-pipeline application.

<img src="https://courses.edx.org/assets/courseware/v1/cc3c6259e25ff0a047861b9fff58ccfe/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-post-build.png" alt="" />

Your Jenkinsfile should look like this.

Click on the Save button at the top right to save your Pipeline configuration.

<img src="https://courses.edx.org/assets/courseware/v1/f3674921e68d85b747234bb45d2fb5be/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Save-pipeline.png" alt="" />

In the Save Pipeline dialog box, specify the commit message First Pipeline in the Description field. Leave all other fields set to their default values.

Click Save & run to run your pipeline. This will accomplish the following:

* Jenkinsfile which contains your Pipeline code will be committed to the master branch of the demo-app Git repository. You can also specify any other branch. If the branch does not exist, one will be created automatically.

* Jenkins will queue the Pipeline job.

* It will start executing the first stage (Build) defined in our Pipeline.

<img src="https://courses.edx.org/assets/courseware/v1/5cf3317096706c5989162867317e10a3/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/save-pipeline-commit-window.png" alt=""/>

When the main Blue Ocean interface appears, click on the row to see Jenkins build the **demo-pipeline** project.

<img src="https://courses.edx.org/assets/courseware/v1/3d7e89714c6dc00bfdf4aa2f4f8ad8f0/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/branch-indexing.png" alt="" />

At the very end of the Deploy Staging stage, you will be asked to decide if it is OK to deploy to Production? Click on the Proceed button to advance to the Deploy Production stage.

<img src="https://courses.edx.org/assets/courseware/v1/7bc17370c7067605f011e504a895958d/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/request-human-input.png" alt="" />

## Creating a Pipeline: Pipeline Visualization
The Blue Ocean UI displays different colors based on the status of a Pipeline run.

<table style="width: 600px; margin-left: auto; margin-right: auto; border: 2px solid white;" height="395" align="center" border="0">
<tbody>
<tr>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="50%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Status</strong></span></p>
</td>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="50%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Color Code</strong></span></p>
</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>In-progress</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Blue</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Passed</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Green</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Unstable</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Yellow</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Failed</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Red</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Aborted</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Grey</td>
</tr>
</tbody>
</table>

And a weather icon for the build trend.

<table style="width: 600px; margin-left: auto; margin-right: auto; border: 2px solid white;" height="395" align="center" border="0">
<tbody>
<tr>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="70%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Health/Build Stability</strong></span></p>
</td>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="30%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Weather Icon</strong></span></p>
</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>If &gt; 80% of the build runs are successful</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8"><span id="docs-internal-guid-d035da01-7fff-60fb-b7c4-27dc495876d8"><span style="font-size: 12pt; font-family: Arial; color: #000000; background-color: transparent; font-variant-numeric: normal; font-variant-east-asian: normal; vertical-align: baseline; white-space: pre-wrap;"><span style="border: none; display: inline-block; overflow: hidden; width: 32px; height: 32px;"><img src="https://lh6.googleusercontent.com/w94Boctz0H9z4G6_v_9RgXLiAHdAt7qpZ326SpgaN9D8Ca7rygebfuOPl1p1XZAZiqHktCaA-IoXT9rEnpmxtrOQ4ptEvORGqxYCfqYdnsohPxhdDmatiQHFC5yj1pb3bXHcrflZ" width="32" height="32" style="margin-left: 0px; margin-top: 0px;"></span></span></span></td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>If 61% - 80% of the build runs are successful</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8"><span id="docs-internal-guid-27591845-7fff-1aa8-6e94-f3cfbfa82bd8"><span style="font-size: 12pt; font-family: Arial; color: #000000; background-color: transparent; font-variant-numeric: normal; font-variant-east-asian: normal; vertical-align: baseline; white-space: pre-wrap;"><span style="border: none; display: inline-block; overflow: hidden; width: 32px; height: 32px;"><img src="https://lh4.googleusercontent.com/XowZXioxnmsQyQ81wsbl_H1HUV2NljIYG66pkT0oXaEK0DJpTyksTyseZo5HMQz6V6IlfK-HoQqliXSx1_Njlvk4y8bj6p912qPFxQIA8eDHFiUd4j0ZFDRaJvgtvgTttrheZO-M" width="32" height="32" style="margin-left: 0px; margin-top: 0px;"></span></span></span></td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>If 41% - 60% of the build runs are successful</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8"><span id="docs-internal-guid-568a7f08-7fff-2ca8-9cf8-5f309be29146"><span style="font-size: 12pt; font-family: Arial; color: #000000; background-color: transparent; font-variant-numeric: normal; font-variant-east-asian: normal; vertical-align: baseline; white-space: pre-wrap;"><span style="border: none; display: inline-block; overflow: hidden; width: 32px; height: 32px;"><img src="https://lh6.googleusercontent.com/8jumu6B1LyNESTMvfbNoXR83nW6khHVuYRvd3z_iKhBiuO9rwQjY1s1eNjrr0GBmuWX3yifqv9Jt-orta-ysJwA4SqGqdA88eMbT5dOH5A7QsoyzeMxVuiyY3jDj9sOjlzmj6Fju" width="32" height="32" style="margin-left: 0px; margin-top: 0px;"></span></span></span></td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>If 21% to 40% of the build runs are successful</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8"><span id="docs-internal-guid-f4be34cd-7fff-4d11-460c-72e89ee91f70"><span style="font-size: 12pt; font-family: Arial; color: #000000; background-color: transparent; font-variant-numeric: normal; font-variant-east-asian: normal; vertical-align: baseline; white-space: pre-wrap;"><span style="border: none; display: inline-block; overflow: hidden; width: 32px; height: 32px;"><img src="https://lh3.googleusercontent.com/nAJ7IV58Gekh5lZTOYd4uqZSk6zvb2rmYn1-CCjGL1TpQOLxCXpnjSOnM-sO2nRWX3vRz_X3K-iflakbUbVnijcOVLr3WieucBU0OdvMg8kUiWvfqsWlard3F67gWuCAh5VzkdZ0" width="32" height="32" style="margin-left: 0px; margin-top: 0px;"></span></span></span></td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>If &lt; 21% of the build runs are successfully</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8"><span id="docs-internal-guid-992d2363-7fff-641a-6f5b-b2ffdfa9dc49"><span style="font-size: 12pt; font-family: Arial; color: #000000; background-color: transparent; font-variant-numeric: normal; font-variant-east-asian: normal; vertical-align: baseline; white-space: pre-wrap;"><span style="border: none; display: inline-block; overflow: hidden; width: 32px; height: 32px;"><img src="https://lh3.googleusercontent.com/3i-WjrGHMgntgP-n1jWop6Md5TPHHwrcdpPjDBMlhtQb3Upbau8bu_Lv0UreEcjv6DZBaNsx5caTSqc_i1k4fx_8NCn1Gr6jaVUYV_FAca4SottbV-jnLPpp0ZSKn2VEBfsDsy4F" width="32" height="32" style="margin-left: 0px; margin-top: 0px;"></span></span></span></td>
</tr>
</tbody>
</table>

Once Jenkins builds the demo-pipeline job successfully, you will notice that the Blue Ocean interface turns green.

You will also be able to view the various stages of the demo-pipeline as well as different steps, build metrics and logs downloaded per stage—all displayed in one place. In case there is an issue with a certain stage, you have the option to restart just that single stage without having to re-run the entire pipeline.

<img src="https://courses.edx.org/assets/courseware/v1/e8843313c5622ca1fe25047342f6e8f3/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/demoapp-pipeline-run.png" alt="" />

Now, you can fork the Github repository and set up a Pipeline job.

In this chapter, we have only scratched the surface of Jenkins Pipelines. In reality, Pipelines allow you to orchestrate more complex applications.
