# Chapter 5 - Jenkins Security

## Chapter Overview
Your Jenkins server hosts your organizational Intellectual Property (IP) such as your source code, build artifacts, etc. In this chapter, you will learn how to incorporate security practices to secure your Jenkins automation server.

## Learning Objectives
By the end of this chapter, you should be able to:

* Explain the importance of Jenkins security.
* Discuss the key global security features in Jenkins.
* Talk about the security realms for authentication.
* Enable authorization.
* Manage credentials that are used to authenticate to various other services.

## Why Security?
For any organization, their intellectual property (IP) is a valuable data and it is important to protect it. Confidentiality, availability, and integrity, also known as the CIA triad, are the fundamental principles of information security.

* Confidentiality determines the secrecy of your IP, and prevents unauthorized access to restricted data.
* Integrity ensures that your IP is accurate and reliable, and it has not been modified from its original state while in transit or at rest.
* Availability is the ability of the users to access your IP. Information is of no use if it cannot be accessed.

<img src="https://courses.edx.org/assets/courseware/v1/1fb3fe907a750cab2016ce2ad579e57d/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/cia-triad.png" alt="" />

Your Jenkins server hosts your organizational intellectual property (IP) such as your source code, build artifacts, etc. Your Jenkins environment is also a fully distributed build system with Jenkins server and agents (more on this in a later section of this course) and each network connection is a potential point of entry. A malicious user could access your Jenkins environment to launch a Distributed Denial of Service (DDoS) attack or a bot or do any other mischief.

Let's explore some of the key Jenkins security features built upon the CIA triad, and how these can be used to mitigate potential threats.

## Securing Jenkins
Starting with Jenkins v2.0, security is enabled by default, and you are required to create an administrator user account in order to be able to login to Jenkins. This is set up as part of the Post Install Setup Wizard.

Many of the global security features are configured on the Configure Global Security page.

<img src="https://courses.edx.org/assets/courseware/v1/581cd56d1d4719ec1e93c741a0204ac6/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/configure-global-security.png" alt="" />

Let’s take a look at some of the security features that are enabled by default on this page.

## CSRF Protection
According to OWASP,

"Cross-Site Request Forgery (CSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they are currently authenticated".

Enabling CSRF protection will protect your Jenkins environment from malicious attacks.

<img src="https://courses.edx.org/assets/courseware/v1/c03144ffcb74f36479ee122ffe2cede5/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/CSRF.png" alt="" />

## Agent-to-Master Security
In a distributed build environment where Jenkins server leverages additional resources (Agents) for running the builds, the agents can request any information from the server. Enabling Agent > Master Access Control allows a Jenkins administrator to control what specific information is allowed by the Agents.

<img src="https://courses.edx.org/assets/courseware/v1/df20f390706d7039ebcb1749571a4de6/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Agent-Master_Security.png" alt="" />

## JNLP Port
In a distributed set up, Jenkins uses a TCP port to communicate with the Agents. This port is disabled by default. If needed, you can enable it by selecting either a **fixed port** or a **random port**.

<img src="https://courses.edx.org/assets/courseware/v1/75ab5161da01adb071c764d87e1adb78/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/JNP_Port.png" alt="" />

## Markup Formatter
Jenkins allows user input in many configuration areas. Setting the Markup Formatter to plain text by default will eliminate any unsafe HTML or JavaScript.

<img src="https://courses.edx.org/assets/courseware/v1/71f4a8915c37032b5aa342221d510f26/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/markup-formatter.png" alt="" />

Let’s now take a look at some of the other security features that can be configured on the Configure Global Security page.

## Authentication
Authentication is an act of validating that users are who they claim to be, essentially confirming the identity of users. Usernames and passwords are the most basic form of authentication.

Jenkins supports many different authentication systems through security realms. A security realm tells Jenkins which referential to use for authentication.

There are four security realms which are supported out of the box. These are:

* Delegate to servlet container
* Jenkins' own user database
* LDAP
* Unix user/group database

<img src="https://courses.edx.org/assets/courseware/v1/92acfa91a1864579ed29ab1ea6e7e1a9/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Screen_Shot_2020-01-30_at_9.33.03_AM.png" alt="" />


#### Delegate to servlet container
This realm delegates authentication to the servlet engine running Jenkins. For instance, Tomcat, JBoss, websphere, etc., have their own authentication mechanisms. If using this realm, you will need to look into the servlet container’s authentication documentation. Example: Apache Tomcat 9 configuration documentation "Realm Configuration How-To".

#### Jenkins’ own user database
This security realm uses Jenkins local database and is enabled by default when you initially install Jenkins.

If you select this security realm, you do have the option of letting your users sign up. However, please refrain from assigning any significant privileges, such as edit, administrator, etc., to authenticated users, as this can pose a big security risk.

<img src="https://courses.edx.org/assets/courseware/v1/310b75ccb89e0aa38a6533cf3ed2d2f9/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Jenkins__own_user_database.png" alt="" />

Note that if you deselect the sign up option, only users with overall administrator privileges can create users.

#### LDAP
This realm delegates authentication to an external LDAP service. Most companies already have a Directory Service for authentication. This option is more common for larger installations in organizations which already have configured an external identity provider such as LDAP. This also supports Active Directory, OpenLDAP installations.

Key features of LDAP include:

* It is highly tunable. 
* Its binding can be sub-authenticated.
* You can take advantage of the caching mechanism to leverage load on LDAP servers.
* There's support available for LDAP replicas.

There are various other security realms available through plugins such as Github Authentication, Active Directory and BitBucket OAuth, to name a few. You can search these on the plugins page.

#### Unix user/group database
This realm delegates authentication to the underlying Unix/Linux machine, and it only works if you are running Jenkins on a Unix server.

If you enable this realm, your end users will have to login to Jenkins by entering their operating system username and password.

<img src="https://courses.edx.org/assets/courseware/v1/3f55ec3c0b4a7d37f612c055d147cf03/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Unix_user_group_database.png" alt="" />


## Authorization
Once a user/group is authenticated, you need to determine the actions this user/group should be able to perform. Authorization always occurs in the context of authentication.

<img src="https://courses.edx.org/assets/courseware/v1/21365980759b51dca26ef1f1d23b440e/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Setting_an_Authorization_Strategy.png" alt="" />

Some of these are lightweight authorization strategies, and some offer granular access controls.

## Lightweight Authorization
* *Anyone can do anything*: This allows both authenticated and anonymous users to do anything.

* *Legacy mode*: This allows administrators to perform any action. All other users are restricted to read only mode.

* *Logged-in users can do anything*: This is the default authorization strategy. It allows all authenticated users to perform any action.

As you can see, all of these options solely rely on the Authentication and provide no fine-grained access control.

Next, let's have a look at Authorization strategies which provide granular access control.

## Matrix-Based Security
This authorization strategy allows you to define actions allowed for each user or group globally by using a matrix. On the vertical axis is the users or groups, and on the horizontal axis, you configure the actions for the corresponding users/groups.

<img src="https://courses.edx.org/assets/courseware/v1/b3bde803d032e889ef294385c66f35e2/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Matrix-based_Security.png" alt="" />

You can add a new user or group by clicking the Add user or group button.

Hover the cursor over each privilege to display information about what that privilege entails, and click the appropriate boxes to define the access that is allowed for each defined user or group.

Notice that two rows are defined by default. The first row defines permissions for Anonymous Users (unauthenticated users) who access the Jenkins UI, and the second row defines permissions for Authenticated Users who access the Jenkins UI.

Note that all the permissions granted are additive, and they are grouped into various categories:

* Overall
* Credentials
* Agent
* Job
* Run
* View
* SCM
* Lockable
* Resources

Also, any plugins you install could add additional groupings.

## Project-based Matrix Authorization Strategy
Project-based Matrix Authorization is an extension of Matrix Authorization. In addition to assigning permissions globally, Project-based Matrix Authorization lets you define permissions for the individual Jenkins jobs.

<img src="https://courses.edx.org/assets/courseware/v1/56a9f843dcca161fde5ea6f4c95ac04b/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Project-based_Matrix_Authorization_Strategy.png" alt="" />

Permissions that are granted in the global configuration apply to all of Jenkins jobs, unless they opt out of inheriting global permissions.

## Credentials
Jenkins needs to authenticate itself against other services:

* SCM repositories for retrieving source code (or pushing it)
* Binary repositories for storing artifacts or fetching dependencies
* Remote secured services for authentication such as LDAP
* Deploy to secured environments.

With Credentials plugin, you can centrally manage credentials to authenticate to various services. When a credential is needed, Jenkins knows it and allows for easy selection.

Next, let us take a look at how to create credentials.

## Create Credentials
In order to create credentials, you need to have the **Credentials-Create permissions**. This is configured in the Authorization section of the Configure Global Security page.

<img src="https://courses.edx.org/assets/courseware/v1/2677c62bc07b5272ca1bd93934fb3d65/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Create_Credentials_Permissions.png" />

Next, navigate to <Your Username> > Credentials from the Jenkins dashboard header.

<img src="https://courses.edx.org/assets/courseware/v1/dfec7c58087de1b02c6fcfb94687ac48/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Create_Credentials.png" />

Click user under stores scoped to your username followed by Global credentials (unrestricted) domain.

<img src="https://courses.edx.org/assets/courseware/v1/dfec7c58087de1b02c6fcfb94687ac48/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Create_Credentials1.png" />

Create new credentials by filling in the details on the Add Credentials page.

<img src="https://courses.edx.org/assets/courseware/v1/162e45c5e7a2c86d88700bd8d5428042/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/add-credentials.png" />

To learn more, please refer to the Jenkins Credentials Documentation.
