# Chapter 10 - What's Next

## Chapter Overview
By now you should have a solid understanding of the fundamentals of Jenkins.

In this chapter, we will take a look at some of the advanced topics related to Jenkins. And we will also discuss the next steps in your Jenkins learning journey.

## Learning Objectives
By the end of this chapter, you should be able to:

* Discuss advanced Jenkins topics.
* Understand how you can participate, contribute and advance in the field of Jenkins.

## CLI and REST API
You can perform a variety of operations using the Jenkins UI, but if you are looking to automate routine tasks, perform bulk updates, or troubleshoot, then Jenkins UI might not be the best solution.

Instead, you can use Jenkins built-in CLI (command line interface) which lets you automate many routine tasks such as creating jobs, updating jobs, triggering builds, creating build agents and many more.

You can also use REST API to perform these tasks. Jenkins currently supports the following:

* XML
* JSON with JSONP support
* Python

To learn more, please see documentation for CLI, REST API, and Python API. 

## Organizing Jenkins Jobs
As the number of jobs on the Jenkins instance grows, it becomes more difficult to view and keep track of them. Jenkins allows you to organize jobs via Folders and Views.You can logically separate jobs for one team, release, etc. You can also create new views and set them as default views.

To mitigate this issue, Jenkins allows you to organize jobs using Folders and Views, so you can logically separate jobs for one team, release, etc. You can also create new views and set them as default views. For further information, please see documentation for the Folders plugin.

## Monitoring Jenkins
Jenkins is an important piece of the CI/CD environment and should be actively monitored. You can use third party tools like Icinga or Nagios for monitoring purposes. Jenkins also provides plugins to monitor its performance, examples include Java Melody and Prometheus to name a few.

## Security
LDAP, Active Directory and Github Authentication are some of the Authentication realms you should try to configure as they simulate real-world scenarios.

Role-based authorization, offered via Role-based Authorization Strategy plugin, supports granular permissions for roles. This strategy allows permissions to be assigned at a business function level (role) rather than individual user/group level.

## Distributed Builds
With many organizations moving towards using public cloud to provision infrastructure on demand, you can use the same principle to scale your build infrastructure on demand via static and dynamic build agents. Some of the important plugins for this include Docker plugin and Kubernetes plugin.

## Jenkins Pipeline as Code
Pipelines are the future of CI/CD and there is a lot to be learned in this area. Please see the Pipelines Documentation for more information.

## Jenkins Community
There are many ways to participate and contribute to Jenkins, including:

* Attending meetings and sharing your experience with Jenkins
* Writing code
* Supporting other Jenkins users
* Translating
* Testing
* Improving Jenkins documentation
* Designing
* Reviewing code and documentation.

Visit Jenkins webpage for more information.
