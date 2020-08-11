# Chapter 6 - Jenkins Jobs

## Chapter Overview
Jobs are at the heart of the Jenkins build process. In this chapter, we will go over the basics of a Jenkins job.

## Learning Objectives
By the end of this chapter, you should be able to:

* Explain what a Jenkins job is.
* Distinguish the different types of Jenkins jobs.
* Describe an anatomy of a Jenkins job.

## What Is a Jenkins Job?
A Jenkins job is a sequential set of tasks that are defined by a user. Typical steps include retrieving the latest source code from version control, compiling it, running unit tests, building and storing the artifacts, and notifying the end users of the outcome of the build.

On the Jenkins UI, the term "job" is used synonymously with "project". Note that both of these are runnable tasks controlled and monitored by Jenkins.

## Jenkins Job Types
There are many different job types available in Jenkins including:

* **Freestyle Project**: This is the default project type, most flexible to configure, and is included as part of the core Jenkins.
* **Maven Project**: This one is useful for building Maven projects. It requires the **Maven Integration plugin** to be installed.
* **Pipeline and Multibranch Pipeline**: These are useful for creating end-end CI/CD pipelines. These require **Pipeline** and **Multibranch plugins** to be installed.
* **External Job**: It is useful when you want to monitor a process that is running outside of Jenkins, and you would like to track its progress from the Jenkins dashboard.
* **Multi-Configuration Project**: This is useful for projects with a large number of configurations. It requires the **Matrix Project plugin** to be installed

## Create a New Jenkins Job
To create a new Jenkins job, click Jenkins > New Item from the side navigation bar on the Jenkins dashboard.

<img src="https://courses.edx.org/assets/courseware/v1/8915b567ba798380eca457c4df9046ef/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/jenkins-create-project.png" alt="" />

This opens up a new subpanel listing various job types. Enter a name for the Jenkins job, select the appropriate job type from the list, and click OK.

<img src="https://courses.edx.org/assets/courseware/v1/c6eced1c44a2c32b9242a3f96f814b94/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/create-jenkins-job.png" alt="" />

## Anatomy of a Jenkins Job
A Jenkins job typically includes the following components.

* Global Project Options
* Source Code Management
* Build Triggers
* Build
* Post-build Actions

Let’s take a closer look at each of these components.

## Anatomy of a Jenkins Job: Global Project Options
The **General** section lists the global project options for each Jenkins job. Let's discuss what information is included.

#### Meta-information
Meta-information is basically information about the job. For a Jenkins job, job name and job description are meta-information. Be sure not to input any JavaScript in the description field as it can pose a security risk.

#### Build history management
Every time you run a Jenkins job, it stores the build log, artifacts, metadata, etc., on the disk. Over a period of time, this can take up a lot of disk space. To cap disk space consumption, you can set a build log retention by clicking the box adjacent to *Discard old builds*. Then you will be presented with two options of setting a policy for discarding builds:

* Days to keep builds
* Max # of builds to keep

Note that these two policies can be active at the same time. For example, you can keep builds for 7 days, but only up to a limit of 30 builds. If either limit is exceeded, then any builds beyond that limit will be discarded.

You can also set a retention policy for build artifacts by clicking the Advanced button.

<img src="https://courses.edx.org/assets/courseware/v1/6f6f3235d76de0c9e06940dc50e50e9a/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/discard_builds.png" alt="" />

Have you noticed this Question mark icon next to almost all the configuration fields? This is an inline form of help that Jenkins offers. Click the icon to learn more about the configuration field. Once you are done, click the icon again to hide the help text.

<img src="https://courses.edx.org/assets/courseware/v1/760d7e59b62a8fce6455cf690b30d437/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Artifacts-retention.png" />

#### Build management
The General section also provides configuration options for general build management. Click the Advanced button to view all the options.

<img src="https://courses.edx.org/assets/courseware/v1/17a41c1cf0554069a0167adc01a263c1/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/advanced-global-options.png" alt="" />

Some of the most common configurations are listed below.

* Quiet period: Setting a wait time between builds.
* Retry Count: Setting a count for the number of times Jenkins will try to checkout from the configured SCM system until it succeeds.
* Disable this project: Disable a job if you no longer need to build the job. You can enable it if needed at a later time.

Any additional plugins you install may add to the list of global options.

<img src="https://courses.edx.org/assets/courseware/v1/b7c07972fe7cf4b0019a301775fbfe7f/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-mgmt-options.png" alt="" />

## Anatomy of a Jenkins Job: Source Code Management
This is the section where you specify the details of the version control repository for building your source code. You have the flexibility to select the **SCM** tool of your choice, but be sure to install the necessary plugin.

<img src="https://courses.edx.org/assets/courseware/v1/7eb6ef2316a48294aeb261da050f9821/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Configure_SCM.png" alt="" />


## Anatomy of a Jenkins Job: Build Triggers
Jenkins allows you to trigger builds automatically. Let's take a look at some of the options under the **Build Triggers** section.

#### Build periodically
You can schedule periodic builds using cron-like syntax. Here is an example of scheduling a build every 15 minutes.

<img src="https://courses.edx.org/assets/courseware/v1/f1641a6027b0c53d3359ffe3cb3e90fe/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-periodically.png" alt="" />

#### Build after other projects are built
You can also automatically build a project after another dependent project has been built successfully.

<img src="https://courses.edx.org/assets/courseware/v1/e31a15895033d5acedd1b34136927da4/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-after-other-projects.png" alt="" />

#### Poll SCM
You can poll SCM at a certain frequency using cron-like syntax. Jenkins will poll SCM at the set times to detect new commits. If there are any, then Jenkins will go ahead and run the build.

<img src="https://courses.edx.org/assets/courseware/v1/28c1a0428d17cd61b67a5f81258c71b6/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/poll-scm.png" alt="" />

It is worth noting that polling adds extra overhead as it scans the entire workspace before checking with the SCM system for any new changes.

#### Webhooks
Ideally, you would want to trigger a new build as soon as a source code change is detected so as to align with CI/CD goals. At the same time, you do not want to add polling overhead. The best way to navigate this is to let your SCM system handle it by configuring Webhooks. Here is a GitHub example describing **how to configure Webhooks**.

## Anatomy of a Jenkins Job: Build Environment
The Build Environment section allows you to specify additional options for your builds - cleaning up the workspace prior to starting a build, setting up the required environment variables used in the build, aborting builds that are stuck, adding timestamps to the build logs, etc.

These options are provided by various plugins - **Workspace Cleanup**, **Credentials Binding**, **Build Timeout** and **Timestamper** to name a few. The more plugins you install, the more options you will see under this section.

<img src="https://courses.edx.org/assets/courseware/v1/cd629aeef0004f8c584ba27fb61d1e7d/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-environment.png" alt="" />

## Anatomy of a Jenkins Job: Build
The **Build** section comprises the actual steps to build your source code, run various tests (unit, integration, etc.), code quality, code coverage, and many more.

Note: Your source code should include the test cases, and your build tool should be able to generate the required report for it. Jenkins can be used to display build tool generated test reports and trends.

<img src="https://courses.edx.org/assets/courseware/v1/28e3feb1bdf49b4decbf1d2e47804d5b/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-steps.png" alt="" />

Here is an example of using the Execute shell build step. You can configure the shell script in any way you like. You can also make use of environment variables. For a complete list, click See the list of available environment variables link. You can also set an exit code to mark the build as unstable.

<img src="https://courses.edx.org/assets/courseware/v1/005fd6140df581bf20f93eeca51d231c/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Execute_shell_build_step.png" alt="" />

You can add one or more build steps, and re-order them however you like simply by dragging and dropping them.

You may also choose to install plugins that suit your specific needs. Such plugins can contribute to additional build steps.

## Anatomy of a Jenkins Job: Post-Build Actions
Post-build actions are performed based on the result of the build status. Examples include notifying developers, publishing test reports, archiving build artifacts, triggering other build projects, automated deployment, etc.

<img src="https://courses.edx.org/assets/courseware/v1/7ae15cce1caa0bf9ed15a89af0759e75/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/post-build-actions.png" alt="" />

The list of post-build steps can vary depending on the plugins installed.
