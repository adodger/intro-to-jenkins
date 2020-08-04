# Chapter 2 - Jenkins Installation Basics

## Chapter Overview
In this chapter, we will go over the prerequisites required to install Jenkins, and explain how you can set up a Jenkins automation server.

## Learning Objectives
By the end of this chapter, you should be able to:

* Understand prerequisites for installing Jenkins.
* Install Jenkins on various operating systems.
* Complete post-installation steps to access the Jenkins user interface.

## Jenkins and Java
Jenkins is written in Java, a platform-independent programming language. Like with any other Java application, it can be installed on a variety of operating systems such as Linux, Windows, MacOS, etc.

## Prerequisite for Installing Jenkins
Prior to installing Jenkins, you need to ensure that your system at least meets minimum hardware and software requirements:

* 256MB RAM
* 1 GB of disk space (10 GB if running as a Docker container)
* Java 8 or Java 11
* Modern web browsers - Google Chrome, Mozilla Firefox, Microsoft Internet Explorer, Apple Safari.

These minimum requirements are good enough to get you started, say for dev or test purposes. However, these need to be fine-tuned for production as production systems need a lot more resources. Jenkins Documentation has sensible recommendations on setting the hardware requirements for your production system.

## Installation Channels
Jenkins is distributed via many channels:

* Standalone WAR
* Unix package managers (RPM, DEB, etc.)
* Windows installers
* Containers

Installing Jenkins is fairly straightforward, and a typical installation takes about 10 minutes. On the next pages, we will explore installing Jenkins using each of the above-mentioned distribution channels.

To learn more, read Jenkins' "Installation Platform" section.

## Installation Channels: Standalone WAR
Using this method, Jenkins runs as a standalone application in its own process with its embedded Java servlet container, Jetty. This standalone application can be downloaded as a Java WAR (Web Application Archive) file with .war extension. This WAR file can run on any operating system, Linux, Windows, Mac OS, etc.

Here are the steps to launch Jenkins as a standalone war:

* Download the **jenkins.war** file from the Jenkins project page https://www.jenkins.io/download/.
* Launch a terminal window, and run the following command: ```java -jar jenkins.war```

By default, Jenkins uses port 8080. Your Jenkins application will be available at ```http://<Your IP Address>:8080```. You can pass additional JVM arguments by specifying **JENKINS_OPTS** and **JAVA_OPTS** to the Java call as shown below: ```java ${JAVA_OPTS} -jar jenkins.war ${JENKINS_OPTS}```

Here is an example of using startup flags:
```
java -Dhudson.footerURL=http://example.org -jar jenkins.war \
--httpPort=8083 --prefix=/ci --httpListenAddress=127.0.0.1
```

In this example:

* setting the Java system property **(JAVA_OPTS) -Dhudson.footerURL=http://example.org** will change the default footer on the Jenkins UI to http://example.com
* ```--httpPort, --prefix```, and ```--httpListenAddress``` are the flags provided as **JENKINS_OPTS**
* ```--httpPort=8083``` will set the Jenkins port to 8083 instead of the default 8080
* ```--prefix=/ci``` will add a prefix to the end of the Jenkins URL
* ```--httpListenAddress=127.0.0.1``` binds Jenkins to the IP address.

Finally, a Jenkins service launched by above command will be reachable only on http://127.0.0.1:8083/ci.

For a list of all the available **JAVA** and **JEKINS** options see "Jenkins Features Controlled with System Properties".


## Installation Channels: Linux Package Managers
Linux package managers provide a stable and automated way to install, and manage a variety of programs. You can use Linux package managers, such as RPM, DEB, OpenSUSE, etc., to install Jenkins.

The standalone WAR file **(jenkins.war)** still forms the basis for the package manager installation. However, it has some added benefits such as automatic creation of Jenkins user, start-up scripts, log rotation, etc.

Here is an example of how you can install Jenkins on Ubuntu using the APT package manager. You will need to import the GPG key for the APT repo, add the repo to the list of sources, update the package index, and install.

```
Import the GPG key for Jenkins repo
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key \
| sudo apt-key add -
# Add the repo to list of sources
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
/etc/apt/sources.list.d/jenkins.list'
#Update package index
sudo apt-get update
#Install Jenkins
sudo apt-get install jenkins
```

You can start, stop, and check the status of Jenkins by running the systemctl command:
```
systemctl start|stop|status jenkins
```

Note that a Jenkins settings file is created at **/etc/default/jenkins**. This is where you will modify many of the Java and Jenkins options. For example, if you want to change the Jenkins port from 8080 to 8083, this is where you would make the change. 

Few other things to note are the locations of Jenkins home directory, startup scripts, and log file.

The startup script is located at **/etc/init.d/jenkins**.

By default, Jenkins home directory is set to **/var/lib/jenkins**, and the log file is located under **/var/log/jenkins**. These can be changed in the Jenkins settings file to a location of your preference.

## Installation Channels: Windows Installers
The Microsoft Windows Jenkins MSI package comes complete with the Java Runtime Environment (JRE) prerequisite and Microsoft .NET 2.0 framework. This bundling provides a seamless Jenkins installation experience, and alleviates the need for any external prerequisite software installations.

By using the MSI installation package, the Jenkins installation wizard will automatically install itself as a Windows service. Running Jenkins as a Microsoft Windows service makes application management easier as Windows services provide an easy way to specify corrective steps in case of application crash.

Download the latest version of **Jenkins for Windows** http://mirrors.jenkins.io/windows/latest to a folder of your choice. Unzip the file to a folder and double click on the Jenkins exe file and follow the prompts to complete the installation.

This will set up Jenkins as a windows service. You can verify it by going to *Start > Control Panel > Administrative Tools > Services.

Note that the Jenkins settings file is located at **C:\Program Files\Jenkins\jenkins.xml**.

## Installation Channels: Application Containers
Since Jenkins is distributed as an ordinary WAR file, it is easy to deploy it on any standard Java application server such as Tomcat, Jetty, or GlassFish. Running Jenkins on an application server is arguably more complicated to set up and maintain. You also lose certain nice administration features such as the ability to upgrade Jenkins or restart the server directly from within Jenkins. On the other hand, your system administrators might be relieved from the overhead of managing multiple servers.

Application container install is a two step process:

1. Copy **jenkins.war** to **webapps** directory
2. Restart application web container

## Installation Channels: Docker Container
In order to run Jenkins as a container, you first need to install Docker on your operating system. Visit Docker's store website and click the Docker Community Edition box which is suitable for your operating system or cloud service. Follow installation instructions provided on the Docker website.

The next step is to download the Jenkins Docker image, either LTS or weekly.

## Installation Channels: Kubernetes
To run Jenkins in Kubernetes, you can make use of Helm charts. Helm is the package manager used to find, share and use software built for Kubernetes. You can find the official Helm chart for Jenkins on GitHub.

## Post Installation Setup Wizard
The post installation setup wizard begins as soon as you launch a freshly installed Jenkins instance. This setup wizard takes you through the steps to unlock Jenkins, customize it with plugins and create the first administrator user through which you can access the Jenkins user interface.

### Unlocking Jenkins
When you first access a new Jenkins instance, you are asked to unlock it using an automatically-generated password.

Follow the instructions on the screen and paste the password into the Administrator password field and click Continue to proceed to installing plugins.

<img src="https://courses.edx.org/assets/courseware/v1/bca564aefe56d9e49c648d47f86fd8ec/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/unlock-jenkins.png" alt="getting started jenkins" />

### Customizing Plugins
Before you can start using Jenkins, you will need to install plugins. On this screen, you have to select one of the two options:

* Install suggested plugins: This will install the recommended set of plugins, a set based on the most common use cases. We recommend that you select this option as this will quickly get you started with Jenkins.
* Select plugins to install: You will be required to select specific plugins based on your preference.

<img src="https://courses.edx.org/assets/courseware/v1/5a06cb5165851c4a8f538d343560aabb/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/install-plugins.png" alt="select plugins" />


### Creating the First Administrator User
After finishing customizing Jenkins with plugins step, Jenkins will let you create your first administrator user. When the Create First Admin User page appears, specify the details for your administrator user in the respective fields and click Save and Continue.

<img src="https://courses.edx.org/assets/courseware/v1/4e355e03950821455d58db99b61eb046/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/first-admin-user.png" alt="create admin user" />

### Accessing the Jenkins Home Page
You are now ready to access Jenkins home page at ```http:<YOUR IP ADDRESS>:<PORT>```.

<img src="https://courses.edx.org/assets/courseware/v1/3db2040fcb407964ce108d2c505a6669/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/jenkins-ui.png" alt="accessing jenkins home page" />

