# Chapter 1 - CI/CD Overview

## Chapter Overview
According to Watts S. Humphrey, the father of software quality and Capability Maturity Model Integration (CMMI), every business is a software business.

All software businesses need to deliver software in a timely, reliable, and repeatable manner. In this chapter, we will give an overview of Continuous Integration and Continuous Delivery, and Continuous Deployment, and explain how these practices help you achieve your software delivery goals.

## Learning Objectives
By the end of this chapter, you should be able to:

* Explain the fundamental concepts of DevOps, Continuous Integration (CI), Continuous Delivery (CD), and Continuous Deployment.
* Understand the basics of Continuous Delivery pipelines.
* Distinguish different tools available for CI/CD and explain why Jenkins is a good choice.

## Software Development Life Cycle
Software development follows a flow, starting with identifying new features, planning, doing the actual development, committing the source code changes, running builds and tests (unit, integration, functional, acceptance, etc.), and deploying to production.


<img alt="Software Development Life Cycle" src="https://courses.edx.org/assets/courseware/v1/28e4961641eda805d66ab06b7e2e7fcf/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/SDLC-1.1.png" />

#### Software Development Life Cycle

With a traditional waterfall software delivery approach, developers could work independently for a very long time. They would not have a clue about how many issues they would run into during the integration phase.

In order to address this issue, the Agile software development model was introduced. Agile changed the way software development teams worked. One of the key principles of this methodology was delivering working software frequently. The focus moved to releasing incremental software, rather than big bang waterfall releases which took months and years.

Delivering software frequently meant producing stable code for every incremental release. It was quite a challenge to integrate changes from various developers on the teams. This led to software teams looking for better approaches. Continuous Integration (CI) offered a ray of hope and started to gain in popularity.

## Continuous Integration (CI)
Continuous Integration is an agile engineering practice originating from the extreme programming methodology. It primarily focuses on automated build and test for every change committed to the version control system by the developers.

According to Martin Fowler,

*"Continuous Integration (CI) is a software development practice where members of a team integrate their work frequently; usually each person integrates at least daily - leading to multiple integrations per day. Each integration is verified by an automated build (including test) to detect integration errors as quickly as possible"*.

<img alt="Continous Integration" src="https://courses.edx.org/assets/courseware/v1/21f9ea8042190ab6d963c90b1c9da340/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/ci-process.png">

#### Continous Integration

In order to implement Continuous Integration, you will need:

* **A version control system**: It stores all the source code checked in by the teams, and acts as the single source of truth.
* **Automated build and unit test**: It is not sufficient if the code written by a developer works only on his/her machine. Every commit that makes it to the version control system should be built and tested by an independent continuous integration server.
* **Feedback**: Developers should get feedback on their commits. Anytime a developer’s change breaks the build, they can take the necessary action (example: email notifications).
* **Agreement on ways of working**: It is important that everyone on the team follows the practice of checking-in incremental changes rather than waiting till they are fully developed. Their priority should be to fix any build issues that may arise with the checked-in code.

## DevOps Movement
Continuous Integration primarily solves the development part of the workflow. However, there is more to software delivery than just feature development and integrating the changes. There is testing (manual, automated) and release process (actual deployment to customer or production).

In the pre-DevOps era, each team was responsible for their own work. The development team would take care of feature development. That’s where their job ended. They would then throw it on over to the quality assurance (QA) team. The QA team would run all the extended test suites (manual and automated). If things worked fine, they would hand the features off to the operations team, who would then ultimately roll out the new features into production and manage them.

Each of these teams worked in silos. The release processes were mostly manual and error prone leading to longer and painful release cycles. Every time something went wrong, a massive amount of time was spent trying to get to the root cause of the issue, let alone the blame game. All this resulted in a lot of wasted time at various levels of the organization.

In reality, every single team should be equally responsible for the release of the new software, which means all these teams need to work in close collaboration with each other. The DevOps movement, which originated from Agile software development, strongly emphasizes the need for collaboration amongst the various teams involved in the software delivery process. In addition to close collaboration, automation of each of the stages of the software delivery process and constant feedback cycles are also considered extremely important. Continuous Delivery provides a framework to achieve the goals of DevOps through automation, and continuous feedback loops.

<img alt="Dev and Ops Collaboration" 
src="https://courses.edx.org/assets/courseware/v1/2a090d00931b4125c61ec18c4676b643/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/continuous-delivery-latest.png" />

#### Dev and Ops Collaboration

## Continuous Delivery
Continuous Delivery is a logical extension of Continuous Integration. While Continuous Integration lets you automate the software build and test process, Continuous Delivery automates the full application delivery process by taking any change in code (new features, bug fixes, etc.) all the way from development (code commit) to deployment (to environments such as staging and production). It ensures that you are able to release new changes to your customers quickly in a reliable and repeatable manner.

According to Martin Fowler, who coined the term Continuous Delivery,

*"Continuous Delivery is a software development discipline where you build software in such a way that the software can be released to production at any time.

You’re doing continuous delivery when:

a. Your software is deployable throughout its lifecycle.
b. Your team prioritizes keeping the software deployable over working on new features.
c. Anybody can get fast, automated feedback on the production readiness of their systems any time somebody makes a change to them.
d. You can perform push-button deployments of any version of the software to any environment on demand.

(...)

To achieve continuous delivery you need:

* a close, collaborative working relationship between everyone involved in delivery (often referred to as a DevOps culture)
* extensive automation of all possible parts of the delivery process, usually using a deployment pipeline*".
*We will cover this in a bit more detail later in this chapter.

Incorporating Continuous Delivery practices will make your overall release process painless, reduce the time to market for new features, and increase the overall quality of software thereby leading to greater customer satisfaction. It can also significantly reduce your software development costs as your teams will prioritize releasing new features over debugging defects.

## Continuous Deployment
Oftentimes, the terms Continuous Delivery and Continuous Deployment are used synonymously by many, but in reality these concepts have a different meaning.

While Continuous Delivery gives you the capability to deploy to production frequently, it does not necessarily mean that you are automating the deployment. You may need manual approval prior to deploying to production, or your business may not want to deploy frequently.

Continuous Deployment, however, is an automated way of deploying your releases to production. You need to be doing continuous delivery in order to be able to perform automated deployment. Companies like Netflix, Amazon, Google, and Facebook automatically deploy to production multiple times a day.

<img src="https://courses.edx.org/assets/courseware/v1/d470b2a1c6d1fa12330b5d671f2abac3/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/deliveryvsdeployment.png" alt="Continuous Integration, Continuous Delivery, Continuous Deployment" />

#### Continuous Integration, Continuous Delivery, Continuous Deployment

Whether you are doing Continuous Delivery or Continuous Deployment, you know by now that you need a deployment pipeline. Next, let us take look at what deployment pipeline is.

## Deployment Pipelines
Deployment pipelines (or Continuous Delivery pipelines) are the cornerstone of Continuous Delivery as they automate all the stages (build, test, release, etc.) of your software delivery process.

There are numerous benefits to using Continuous Deployment pipelines. An automated pipeline allows all stakeholders to monitor the progress, eliminates the overhead of all the manual work, provides quick feedback, and more importantly builds confidence on the code quality.

<img src="https://courses.edx.org/assets/courseware/v1/8b0aeb949c200eaabe8b0b6c89534381/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/basic-deployment-pipeline.png" alt="Continuous Delivery Pipeline (CDP)" />

#### Continuous Delivery Pipeline (CDP)

The deployment pipeline run starts with a developer committing source code change into a version control repository. The CI server detects the new commit, compiles the code, and runs unit tests. The next stage is deploying the artifacts (files generated from a build) to staging or a feature test environment where you run additional functional, regression, and acceptance tests. Once all the tests are successful, you are ready to deploy into production. In case of failure during any stage, the workflow stops and an immediate feedback is sent back to the developer.

## Tools for Deployment Pipeline
In order to automate the various stages of your deployment pipeline, you will need multiple tools. For example:

* a version control system such as Git to store your source code
* a Continuous Integration (CI) tool such as Jenkins to run automated builds
* test frameworks such as xUnit, Selenium, etc., to run various test suites
* a binary repository such as Artifactory to store build artifacts
* configuration management tools such as Ansible
* a single dashboard to make the progress visible to everyone
* frequent feedback in the form of emails, or Slack notifications.

And that’s not all. You will also need a single tool that can bring all these tools together to achieve CI/CD goals which is to automate software delivery.

## CI/CD Tools
There is a large number of open source (free) and enterprise (paid) CI/CD tools available in the market. Here is a matrix that compares some of the most popular CI/CD tools based on the type of offering (paid or free), licensing (open source or closed source), hosting (on-premise or cloud), and extensions/plugins.

<table style="width: 800px; margin-left: auto; margin-right: auto; border: 2px solid white;" height="395" align="center" border="0">
<tbody>
<tr>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="20%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>CI/CD Tools</strong></span></p>
</td>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="20%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Feature: <br>Pricing</strong></span></p>
</td>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="20%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Feature: <br>Licensing</strong></span></p>
</td>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="20%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Feature:<br>Hosting</strong></span></p>
</td>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="20%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><strong style="color: #ffffff;">Feature:&nbsp;<br>Extensions/<br>Plugins</strong></p>
</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Atlassian Bamboo</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">On-premises</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">**</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Bitbucket Pipelines</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Cloud/<br>On-premises</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">**</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>AWS CodePipeline</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">*</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Azure Pipelines</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">**</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Circle CI</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">On-premises/<br>Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">***</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>CloudBees Core</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">On-premises/<br>Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">*****</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>GitHub Actions</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">On-premises/<br>Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">***</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>GitLab CI/CD</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Free/Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">OSS/Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">On-premises/<br>Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">*</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Google Cloud Build</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">**</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Jenkins</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Free</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">OSS</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">On-premises/<br>Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">*****</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Travis CI</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Paid</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Closed</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">On-premises/<br>Cloud</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">***</td>
</tr>
</tbody>
</table>

Note: Stars depict the number of extensions or plugins. A single star implies a very low number and five stars indicate the highest number of extensions.

## GitLab CI/CD vs Jenkins
As you can see, there are only two free options, GitLab CI/CD and Jenkins. However, GitLab community edition does not give you the flexibility to use a version control repository of your choice and does not offer very many integrations through the plugins. On the other hand, Jenkins is a free and open source tool that has stood the test of time. It has been around for over 15 years. It has a large and active open source community constantly rolling out new releases, bug fixes, etc. There are many online sources (documentation, Google groups, etc.) for help.

Jenkins can be installed on any operating system on-premise, or in cloud. Its solid integration with many other third tools makes it an excellent choice.

<img src="https://courses.edx.org/assets/courseware/v1/b9d0dab26bf46bb6a9bb0da854cbe3c9/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/jenkins-automation-server.png" alt="Jenkins Automation Server" />

#### Jenkins Automation Server

## Summary
By now, you should know:

* Fundamentals of Continuous Integration, Continuous Delivery, and Continuous Deployment
* Fundamentals of CI/CD pipelines
* The value that CI/CD adds to your software delivery process
* What tools are available for CI/CD
* Why Jenkins is a good choice for your CI/CD workflow.

In the next chapter, we will discuss how to get started with Jenkins.
