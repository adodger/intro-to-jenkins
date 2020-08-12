# Chapter 9 - Distributed Builds Architecture

## Chapter Overview
In this chapter, we will go over the distributed builds architecture and explain how you can scale your Jenkins build infrastructure.

## Learning Objectives
By the end of this chapter, you should be able to:

* Explain what the distributed builds are.
* Understand terminology related to the distributed builds.
* Set up a distributed build architecture.

## Why Distributed Build Architecture?
Up until now, we have run all the builds on the Jenkins master. So far it worked well for us. However, what if you need to run hundreds of builds every day? Well, you can try scaling your Jenkins server vertically by adding more resources (CPU, memory, etc), but you will eventually cap out of resources as you can scale a server vertically only up to a certain point.

The next thing that probably comes to your mind is adding more Jenkins masters. There are two major issues with this approach. First, it is going to create an administrative overhead to configure and keep track of all the Jenkins masters, and their corresponding builds, configurations, etc. Secondly, you may be developing applications that need to be supported on a variety of OS platforms, and you may need to run builds on various platforms. For instance, consider a situation when your application needs to be built and tested on Linux, Windows and MacOS. You won’t be able to achieve this because each Jenkins master is tied to a specific operating system.

Besides scaling, there is also a major security flaw associated with running your builds on the Jenkins masters. All Jenkins jobs run with administrator privileges, and a malicious actor can potentially access or delete any private information compromising the security of your data.

The solution to the above problems is a distributed build architecture that allows you to have a single Jenkins master and leverage additional servers to perform the builds.

## Distributed Builds Terminology
Before we deep dive into distributed build architecture, let’s quickly review some terminology related it.

* Master: A machine where Jenkins is installed. It centrally stores all the configurations, loads plugins and renders the Jenkins UI.

* Agent: A machine which connects to the Jenkins master and performs various operations as directed by the Jenkins master.

* Node: A machine that can allocate an executor and run Jenkins Pipelines. Examples are Jenkins masters and Agents. You will notice that nodes and agents are sometimes used synonymously.

* Executor: A Jenkins executor is one of the basic building blocks which allows a build to run on a node. You can configure more than one executor for every node. The number of executors is set based on the number of CPUs, IO performance and other hardware characteristics of a node and the type of builds you have configured to run. The number of executors determines the number of concurrent builds that can be run at any given point in time.

It is Jenkins security best practice to set the number of executors to 0 on the Jenkins master, and not run any builds on it.

## Distributed Builds Architecture
In a distributed environment, all the Jenkins jobs are configured centrally on the Jenkins master. The Jenkins master accepts all the requests for builds and manages the build environment, but offloads the bulk of work (execution of the builds) to the configured agents.

There are many advantages to this approach:

* It allows you to run builds for multiple OS platforms. For example, if you need to run a build on Windows platform, all you need to do is add a new Windows agent and connect it to your Jenkins master.
* It lets you scale your build infrastructure on demand by adding more build agents.
* It helps you mitigate security risk by restricting the information that an agent can request from the Jenkins master.

<img src="https://courses.edx.org/assets/courseware/v1/1a557e9e68386331c61bc0ac23563a99/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/DB-Arch.png" alt="" />

Please note that there are some requirements for this setup.

The Jenkins master needs to be able to communicate with the agent to offload the build job. The agent executes all the tasks, and passes information (artifacts, build log, etc.) back to the Jenkins master which essentially requires a bi-directional communication between the Jenkins master and the agents.

All Jenkins agents require Java to be installed as there is a **slave.jar** file that needs to be run on all the agents. The Java version of the agent must be the same as the Java version installed on the Jenkins master.

The **slave.jar** file is located at ```<Your Jenkins URL>/jnlpJars/slave.jar```.

Other than these requirements, there is no need for a shared file system, a shared subnet, etc.

## Connect a Build Agent
To connect a new Jenkins agent, you will need to navigate to Jenkins > Manage Jenkins > Manage Nodes and Clouds.

<img src="https://courses.edx.org/assets/courseware/v1/2282462bcbe0722c1a8071e7378ed0ab/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/manage-nodes.png" alt="" />

Next, select New Node.

<img src="https://courses.edx.org/assets/courseware/v1/110913f139ba4fc21fe8c9b2cc9ac6ca/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-new-node.png" alt="" />

Enter Node name, select Permanent Agent and click OK to proceed to the configuration screen.

<img src="https://courses.edx.org/assets/courseware/v1/1364e455ccb2c5c477cde50be5e1e91e/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/name-the-new-agent.png" alt="" />

## Configure a Build Agent
On the configuration screen, you are required to enter the following:

* Description: A meaningful description of the agent.
* Number of executors: Set this number based on the CPU cores on the agent.
* Remote root directory: An absolute path to a root directory on the agent. This directory will be used as a temporary root directory for building jobs.

## Configure a Build Agent: Labels
Labels are used to group multiple agents into one logical group. For example, if you need to run builds on a Linux agent, you can assign each Linux agent a label called "linux". You can also use multiple labels for each agent. For example, a Linux agent that also runs Ruby builds can have two labels, "linux" and "ruby". Be sure to not use special characters for label names.

How do we use these labels in Jenkins jobs? Let's see.

#### For Freestyle Jobs
Check the toggle for Restrict where this project can be run under the General section, then enter the label name for the Label Expression.

<img src="https://courses.edx.org/assets/courseware/v1/0cb98da4a57a21b622b03ea4b0b11ac1/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/restrict-jobs-labels.png" alt="" />

#### For Pipeline Jobs
Bring up the Pipeline editor for your Pipeline job. Under Pipeline Settings, select the type of agent from the Agent dropdown menu and enter a name for the Label.

<img src="https://courses.edx.org/assets/courseware/v1/030781ff6c1e83ee1357ce1818348dde/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Screen_Shot_2020-05-16_at_7.27.33_AM.png" alt="" />

## Configure a Build Agent: Usage
You have two options to choose from:

* Use this node as much as possible: This is rather self-explanatory.
* Only build jobs with label expressions matching this node: Reserve this node for all the jobs that are restricted to certain nodes using node names and labels.

## Configure a Build Agent: Launch Method
You can choose one of the following launch methods based on your requirement:

* Launch agents via SSH
* Launch agent by connecting it to the master
* Launch agent via execution of command on the master

We will now discuss each of these methods in more detail.

#### Launch Agents via SSH
As the name suggests, SSH connectivity is used to launch an agent. This is supported by default on all Linux and MacOS systems. You can also install OpenSSH on the latest versions of Windows systems (see Microsoft Documentation to learn more).

In order to use this launch method, you need the following:

* Install **SSH** and ensure that the **SSHD** is running successfully on the agent
* Set up a user account that can be used to log into the agent
* Add Jenkins master’s public key to the agent’s **authorized_keys** file.

Note that once the connection is established Jenkins will automatically copy the **slave.jar** file onto the agent.

<img src="https://courses.edx.org/assets/courseware/v1/27bdb0197a8cd19e4695f6b207affef2/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/ssh-launch-method.png" alt="" />

#### Launch Agent by Connecting It to the Master
This launch method is useful for cases where agents are Windows OS-based, or they are behind a firewall and unable to use SSH to connect.

In order to use this launch method, you need to configure the port that Jenkins master will use to listen for incoming agent connections on the Configure Global Security page.

<img src="https://courses.edx.org/assets/courseware/v1/c21335d279af0a5f649fe3aef700f8d2/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/jnlp-port.png" alt="" />

Once you configure the agent, you have the option of launching it with or without the GUI. It is best to run the agent without using the GUI.

<img src="https://courses.edx.org/assets/courseware/v1/d4290749c42f7f3d4650d46af8227ec8/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/jnlp-agent.png" alt="" />

Launch Agent via Execution of Command on the Master

You can use a command on the master to launch an agent as long as Jenkins master is able to execute the commands remotely using SSH, RSH, etc. Both this and the Launch Agents via SSH method have similar requirements for setup.

Instead of using a single command, you can also create a shell script on the agent which includes a set of commands such as setting JDK path, location of **slave.jar** file, etc., to be run on the agent and execute this script remotely from the Jenkins master.

<img src="https://courses.edx.org/assets/courseware/v1/7de8e540a68818037e6a3456954f7963/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/launch-method-command-master.png" alt="" />

## Configure a Build Agent: Availability
You can choose one of the following options:

* Keep this agent online as much as possible
* Bring this agent online and offline at specific times
* Bring this agent online when in demand, and take offline when idle.

Optionally, you can specify additional Node Properties such as environment variables, tool locations, etc . Once you are done configuring, click Save to save the configuration.

<img src="https://courses.edx.org/assets/courseware/v1/ef5263e5272c9c8b1d7f027cd5e05d65/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/config-screen.png" alt="" />

## View and Manage Jenkins Agents
You can view and manage all the configured agents from Jenkins > Manage Nodes and Clouds page.

<img src="https://courses.edx.org/assets/courseware/v1/0927f3b87f4f8f51a1b113fd56f9b06b/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/manage-jenkins-agents.png" alt="" />

Next, you can click on the selected agent to view all the projects associated with this agent.

<img src="https://courses.edx.org/assets/courseware/v1/18e0c18e7067b07a1d2eb97260b358f0/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/project-associations.png" alt="" />

## Verify Job Execution on an Agent
If you restrict a job to use a certain agent or a label, you can verify if the job is picking the right agent from the Build Executor Status on the main Jenkins dashboard.

<img src="https://courses.edx.org/assets/courseware/v1/c998774e1b56ff196fb342c4cf15b095/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/java-app.png" alt="" />

## Load Statistics
You can view the overall load on your build infrastructure by going to the Jenkins > Manage Jenkins > Load Statistics page.

<img src="https://courses.edx.org/assets/courseware/v1/0d2f0b4218aa8a2a23af561ffda734e4/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/load-statistics.png" alt="" />

Load statistics provide you with the following metrics:

* Number of online executors: A total number of executors that have been configured to run a build and are currently online.
* Number of busy executors: Number of executors currently running a build.
* Number of available executors: Number of executors currently available to run a build.
* Queue length: Number of jobs in the build queue that are waiting for an executor to free up.
