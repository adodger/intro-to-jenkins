# Chapter 4 - Jenkins Plugins

## Chapter Overview
One of the reasons for Jenkins’s popularity as a CI/CD tool is its large plugin ecosystem. In this chapter, we will give an overview of Jenkins plugins and explain how to manage them.

## Learning Objectives
By the end of this chapter, you should be able to:

* Discuss about Jenkins plugins ecosystem.
* Install plugins.
* Upgrade plugins.
* Uninstall plugins.

## What Exactly Are Plugins?
Jenkins uses plugins to provide much of the user-needed functionality. Many Jenkins features such as integrating source code management tools, build tools, reporting tools, code coverage, static analysis, notifications are all implemented as plugins.

Essentially, all the Jenkins plugins are Java Archive (JAR) files with either an **.hpi** or **.jpi** extension. For example, Git plugin (**git.hpi**), Maven plugin (**maven-plugin.jpi**).

They may have optional or required dependencies on other plugins, and they can be upgraded or downgraded (although this is generally not recommended).

<img src="https://courses.edx.org/assets/courseware/v1/9bc04c72532e8c0b6c29086aa20d0bec/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/git-plugin-dependencies.png" alt="" />

Currently, there are 1000+ plugins available for use. You can view a list of all the available plugins on the Jenkins Plugins Index page https://plugins.jenkins.io/.

The long list of plugins can be overwhelming for new Jenkin users. With Jenkins versions 2.0 and above, the post-install wizard automatically recommends plugins that have been validated, and the ones that the Jenkins community finds most useful for CI/CD workflow. We strongly recommend that you select this option as this will set up all the essential plugins for you right off the bat.

<img src="https://courses.edx.org/assets/courseware/v1/5a06cb5165851c4a8f538d343560aabb/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Post_Install_Wizard_-_Install_plugins.png" alt="" />

The one-time post-install wizard setup gets you started with essential plugins. This is great. But what if you need to install a new plugin for a new functionality that you are looking for, or upgrade an existing plugin to work with newer Jenkins core versions? Or maybe you no longer need a plugin that is already installed? Let us explore how to manage plugins on your Jenkins server.

## Managing Plugins
You can administer plugins using the **Plugin Manager**. You can easily navigate to Plugin Manager from Jenkins > Manage Jenkins > Manage Plugins.

<img src="https://courses.edx.org/assets/courseware/v1/f6df0ef022e43ad6b06a944ab62b5f1b/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Manage-Plugins.png" alt="" />

Using the Plugin Manager, you can perform a variety of administrative tasks such as installing, deleting, updating, enabling or disabling plugins.

You might want to note that the Plugin Manager leverages the open source update site. An update site is similar to a package manager. It stores all the plugins and plugin metadata. This enables plugin installation from within Jenkins. So, how does Jenkins know which update center it is pointing to? Look under the Advanced tab of the Plugin Manager page.

<img src="https://courses.edx.org/assets/courseware/v1/820fd3e05dac984820c5f1479e7e42ca/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Update_Site.png" alt="" />

What if your Jenkins is behind a firewall, and does not have direct access to the Internet? In that case, you will need to configure an HTTP proxy server.

You can do it in the Advanced tab. Enter the HTTP proxy server name, proxy port, and username used to authenticate with the proxy, and the password to configure your proxy settings. Click the Advanced button on the bottom right to enable the Test URL to **validate proxy** configuration fields. Finally, click the Submit button to submit the configuration.

<img src="https://courses.edx.org/assets/courseware/v1/3632e89b363b740f6d0e8fe03ad08f2e/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/http-proxy.png" alt="" />

Let us explore the capabilities of the plugin manager.

## Install Plugins
The *Available* tab under the plugin manager lists all the plugins that are available for installation. This list can be pretty long, so make use of the filter to search for specific plugins you would like to install.

You can install and start using most plugins almost immediately by checking the box adjacent to the plugin and clicking Install without restart. However, we recommend that you always restart your Jenkins master after installing a new plugin by clicking *Download now and install after restart*. Application restart ensures all components are properly initialized.

Here is an example of installing Warnings Next Generation plugin. Search for the specific plugin on the Available tab, check the box adjacent to the plugin name and click *Download now and install after restart* button.

<img src="https://courses.edx.org/assets/courseware/v1/00c55c5a01b2dc5402aae4f69d5fd6bf/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Install_plugin.png" alt="" />

An important note on plugins: Anyone in the open source community can contribute to plugins, and you need to ensure that the plugins are reliable. We strongly recommend that you check the usage stats of a plugin on the plugin site prior to installing it. This way, you can help rule out any potential bugs that may affect your Jenkins instance.

<img src="https://courses.edx.org/assets/courseware/v1/90f72e1524267a995f9caba3afbef802/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/Plugin_Usage_Stats.png" alt="" />

## Manual Upload
Another way to install plugins is to manually upload an **.hpi** or **.jpi** file using the upload plugin option on the Advanced tab.

<img src="https://courses.edx.org/assets/courseware/v1/63f18f2fa2cfc0faf42dfc38be5827d9/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/pasted_image_0.png" alt="" />

So, when should you use this option? This is especially useful for cases where you are using an older version of a plugin not currently available on the Jenkins update site, or if you developed your own custom plugin.

If your plugin has dependencies on some other plugins, be sure to install those plugins as well. Otherwise, your plugin may not work as expected.

## Installed Plugins
The *Installed* tab under Plugin Manager lists all the plugins installed on your Jenkins instance. It can be used to quickly verify if a specific plugin is already installed, or if you need to confirm which version of a plugin is installed, etc.

<img src="https://courses.edx.org/assets/courseware/v1/667ce9bd111d9915b832aee315b422ab/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/List_Installed_Plugins.png" alt="" />

## Uninstall Plugins
If you no longer need a plugin, you can uninstall it by selecting the specific plugin on the Installed tab and clicking the Uninstall button.

Here is an example of uninstalling a plugin. Let's say you want to remove the Violations plugin as it is deprecated. Use the filter on the Installed tab to search for Violations plugin, ensure that the box adjacent to Violations plugin is checked, and click Uninstall.

<img src="https://courses.edx.org/assets/courseware/v1/09e9c99ee25df54e969e6af64e5d074d/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/uninstall-plugins.png" alt="" />

Please note that uninstalling a plugin may leave behind some plugin configuration data. Navigate to Jenkins > Manage Jenkins > Manage Old Data. You can view and purge all the unwanted data here.

<img src="https://courses.edx.org/assets/courseware/v1/877df6116e397f5f2bf83d3aeff71097/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/unnamed.png" alt="" />

## Disable Plugins
Sometimes you may not want to remove a plugin altogether, but you just want to be able to disable its functionality. You can do so on the Installed tab by searching for the plugin, and unchecking the toggle under the Enabled column.

You might want to note that when you disable a plugin, it will still show up under the list of installed plugins. However, Jenkins does not really start the plugin, and any extensions contributed by this plugin are not visible.

If you need to re-enable the plugin at a later time, you just need to check the toggle under the Enabled column and restart your Jenkins server to make the plugin operational.

<img src="https://courses.edx.org/assets/courseware/v1/659feab4ca1d6f8cdbb2a66a47ec3272/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/disable-plugin.png" alt="" />

## Update Plugins
It is always a good practice to update the plugins frequently. New releases of plugins add enhanced functionality, security fixes, etc. Also, older versions of plugins may not be compatible with newer versions of Jenkins core.

The Updates tab lists all the installed plugins for which an update is available. You can update a specific plugin by checking the toggle under the Installed column, and clicking Download now and install after restart button.

Here is an example of upgrading Credentials plugin. The Installed column shows the version of the plugin that is currently installed on your Jenkins server. The Version column shows which version is available for upgrade. Check the box adjacent to Credentials and click Download now and install after restart button.

<img src="https://courses.edx.org/assets/courseware/v1/7551cdd93ce88c11609479e62d9aacad/asset-v1:LinuxFoundationX+LFS167x+2T2020+type@asset+block/update-plugins.png" alt="" />


