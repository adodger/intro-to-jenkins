# Chapter 3 - Jenkins Dashboard

## Chapter Overview
The Jenkins dashboard is the main entry point for your Jenkins user interface. In this chapter, we will give an overview of the Jenkins dashboard - the information it displays to the end users and its core capabilities.

## Learning Objectives
By the end of this chapter, you should be able to:

* Discuss what are the primary components of Jenkins dashboard.
* Discuss the functionality of various components.
* Navigate to different areas of the Jenkins user interface to perform various CI/CD operations.

## Dashboard Sections
The Jenkins dashboard is what you see when you first log in to the Jenkins user interface. Let's explore the dashboard and understand some of its core capabilities.

The dashboard primarily consists of the following sections:

* Header
* Side Navigation
* All View for Jobs/Projects
* Monitoring Builds
* Footer

<img src="https://courses.edx.org/assets/courseware/v1/f3015a1311e95b43bb12275b7ac426e3/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/jenkins-dashboard-latest.png" alt="Jenkins Dashboard" />


Let’s take a look at each of these, starting with the header.


## Dashboard Sections: Header
The main header includes the following components:

* Breadcrumbs
* Edit description
* Enable/disable auto refresh
* Context search box
* Logged in user dropdown

### Breadcrumbs
Breadcrumbs are a secondary navigation system that show a user's location on the Jenkins user interface. These allow you to quickly navigate to specific pages (or links) within the current hierarchy.

<img src="https://courses.edx.org/assets/courseware/v1/574cb415c9cd20ec0093ecf4d2545cd8/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/breadcrumbs.png" alt="Jenkins Breadcrumbs" />


### Add/Edit Description
You can use this to add/edit some text to the Jenkins dashboard, jobs, build, etc. The text can be a note, a reminder, or anything that can be useful to your team.

### Enable/Disable Auto Refresh
This is self-explanatory. Enabling auto refresh will refresh your Jenkins UI every 10 seconds. On the other hand, you will need to manually refresh your browser if you disable this feature.

### Context Search Box
The context search box lets you search for content Jenkins wide. By default, the search is case-insensitive, and it comes in very handy as you can quickly search for specific text, Jenkins jobs, builds, etc.

For example, if you need to search for build number 4 for a Jenkins job named "frontend-app", you can just type **frontend-app 4**.

<img src="https://courses.edx.org/assets/courseware/v1/54aada3e2f7831292cc61d5de1e62089/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Context_Search.png" alt="search context" />


If you need to get directly to the configuration page for this job, then you can type in **frontend-app configure**.

<img src="https://courses.edx.org/assets/courseware/v1/10dd3cf70e628eebe23ae44664466497/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Context_Search2.png" alt="search with configure" />


### Logged in User Dropdown
At the very top-right corner of the header, you will notice a dropdown menu linked to your username.

* Builds: This displays all the builds for the user.
* Configure: This gives you the ability to configure your own settings, ssh keys, email address, custom views, any many more.
* My Views: The "All view" is the default view for all users. However, you can create your own custom view and set your default view to your custom view.
* Credentials: You can view user credentials for your own account or any other authorized credentials.

<img src="https://courses.edx.org/assets/courseware/v1/16d8b366d7a7f0873bd80f96e1f0c16c/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/User_dropdown_menu.png" alt="user menu" />


### Side Navigation
The side navigation bar provides initial top level configuration options. At minimum, you should be able to view the default configuration items.

* New Item: This is used to create new Jenkins jobs.
* People: This lets you view/modify all the user accounts that have access to the Jenkins UI.
* Build History: Clicking this will open a new subpage, which displays the build jobs, their status, and trend.
* Manage Jenkins: This is where you can perform a variety of administration tasks such as configuring Jenkins, managing plugins, configuring global tools, security, etc.
* Credentials: This option lets you centrally create and manage credentials. These credentials are used by your Jenkins instance, plugins, build jobs, etc.

<img src="https://courses.edx.org/assets/courseware/v1/1c7d2ef83f1f44797f73de5e4e6698a3/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Side-Navigation-Bar.png" alt="side navigation" />

Note that any plugins you install may add additional configuration items here. It is also worth noting that each subpage within Jenkins will have its own configuration options. For example, if you click on the Manage Jenkins link on the side navigation bar, the subpage will show the configuration options specific to Manage Jenkins.

<img src="https://courses.edx.org/assets/courseware/v1/dcb5a320c5b645942900ef8756cd4c99/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Manage_Jenkins_Subpage.png" alt="" />


### All View for Jobs/Projects
This view lists every single job that is configured on the Jenkins instance. It also displays the overall state of each Jenkins job.

<img src="https://courses.edx.org/assets/courseware/v1/aca238777c75a632be660634718a3393/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/All_Jenkins_Jobs.png" alt="view jobs" />

For a given job in this list, the following information is indicated:

* Build Status (S): Uses color codes (described below in more detail).
* Health/Build Stability (W): Uses weather icons (described below in more detail).
* Job Name
* Last Success: Displays when was the last time the job built successfully, and the related build number.
* Last Failure: Displays when was the last time the build failed, and the related build number.
* Last Duration: How long did the latest build take to run?
* build (icon): To start a build.

### Build Status
<table style="width: 600px; margin-left: auto; margin-right: auto; border: 2px solid white;" height="395" align="center" border="0">
<tbody>
<tr>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="50%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Build Status</strong></span></p>
</td>
<td style="font-size: 16px; padding-left: 15px; border: 2px solid white;" width="50%" align="padding-left" bgcolor="#003f60">
<p align="padding-left"><span style="color: #ffffff;"><strong>Color Code</strong></span></p>
</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Build is currently in progress</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Flashing Blue/Grey</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Build is successful</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Blue</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Aborted build</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Grey</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Failed build</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Red</td>
</tr>
<tr>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">
<p>Unstable build</p>
</td>
<td style="font-size: 16px; border: 2px solid white; padding-left: 15px;" bgcolor="#e8e8e8">Yellow</td>
</tr>
</tbody>
</table>

### Health/Build Stability
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

### Jobs Table Footer
The jobs table footer lists links to the legend of all the icons on the jobs table and their definitions, as well as RSS feeds for all builds, failed builds, and latest builds.

<img src="https://courses.edx.org/assets/courseware/v1/2a9c51f3bd9c36a61729f422ebfe9210/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Jobs_Table_Footer.png" alt="jenkins footer" />

### Monitoring Builds
This section provides overall visibility into your Jenkins job executions. It lets you know if your Jenkins server has too many or too little resources, and can be very useful for IT capacity planning purposes. Monitoring builds has two subsections, Build Queue and Build Executor Status.

### Build Queue
The Build Queue section displays all the jobs that are currently queued and waiting for an executor to free up. You can click on the queued job to retrieve more information on the job. Alternatively you can cancel the job by clicking on the red colored X icon, which is displayed next to the job.

### Build Executor Status
The Build Executor Status lists all the builds that are currently in progress by each configured agent. You can click on the progress bar to view the build console output. You can also view the Jenkins Node dashboard which lists all the nodes (master, agents) by clicking on the Build Executor link.

We will cover additional nodes and agents later in this course.

<img src="https://courses.edx.org/assets/courseware/v1/86d2ecf3788919a53c42a84394011763/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/build-queue.png" alt="" />

### Page Footer
At the very bottom right corner of the Jenkins UI is a link for Rest API. This link will provide you with some basic information on how to use Rest API to programmatically interact with Jenkins. Using Rest API is an alternative to performing various operations via the Jenkins UI.

<img src="https://courses.edx.org/assets/courseware/v1/33fd08631672c80def69d50f3a82c810/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Footer.png" alt="" />

