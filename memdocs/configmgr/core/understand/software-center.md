---
title: Software Center user guide
titleSuffix: Configuration Manager
description: Learn about the features and functionality of Software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529


---

# Software Center user guide

*Applies to: Configuration Manager (current branch)*

Your organization's IT admin uses Software Center to install applications, software updates, and upgrade Windows. This user guide explains the functionality of Software Center for users of the computer.

General notes about Software Center functionality:

- This article describes the latest features of Software Center. If your organization is using an older but still supported version of Software Center, not all features are available. For more information, contact your IT admin.

- Your IT admin may disable some aspects of Software Center. Your specific experience may vary.

- If multiple users are using a device at the same time, say via multiple remote desktop sessions, the user with the lowest session ID will be the only one to see all available deployments in Software Center. Users with higher session IDs may not see some of the deployments in Software Center. For example, the users with higher session IDs may see deployed Applications, but not deployed Packages or Task Sequences. Meanwhile the user with the lowest session ID will see all deployed Applications, Packages, and Task Sequences.

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="bkmk_open"></a> How to open Software Center

For the simplest method to start Software Center on a Windows 10 computer, press **Start** and type `Software Center`. You may not need to type the entire string for Windows to find the best match.

If you navigate the Start menu, look under the **Microsoft Endpoint Manager** group for the **Software Center** icon.

![Microsoft Endpoint Manager start menu icons](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> The Start menu path changed in version 1910. In version 1906 and earlier, the folder name is **Microsoft System Center**. When you update Configuration Manager to version 1910 or later, make sure to update any internal documentation that you maintain to include this new location.

## Applications

Select the **Applications** tab to find and install applications that your IT admin deploys to you or this computer.

- **All**: Shows all applications that you can install
- **Required**: Your IT admin enforces these applications. If you uninstall one of these applications, Software Center reinstalls it.
- **Filters**: Your IT admin may create categories of applications. If available, select the drop-down list to filter the view to only those applications in a specific category. Select **All** to show all applications.
- **Sort by**: Rearrange the list of applications. By default this list sorts by **Most recent**. Recently available applications are listed with a **New** tag that is visible for 7 days.
- **Search**: Still can't find what you're looking for? Enter keywords in the Search box to find it!
- **Switch the view**: Select the icons to switch the view between list view and tile view. By default the applications list shows as graphic tiles.
    - Tile view: Your IT admin can customize the icons. Below each tile displays the application name, publisher, and version.
    - List view: This view displays the application icon, name, publisher, version, and status.

### Install multiple applications

<!-- 1357126 -->
Install more than one application at a time instead of waiting for one to finish before starting the next. Not all applications qualify:

- The app is visible to you
- The app isn't already downloading or installed
- Your IT admin doesn't require approval to install the app

To install more than one application at a time:

1. To enter multi-select mode in the list view, select the multi-select icon ![Software Center multi-select icon](media/software-center-multi-select-apps.png) in the upper right corner.
2. Select two or more apps to install by selecting the checkbox to the left of the apps in the list.
3. Select the **Install Selected** button.

The apps install as normal, only now in succession.


## Updates

Select the **Updates** tab to view and install software updates that your IT admin deploys to this computer.  

- **All**: Shows all updates that you can install
- **Required**: Your IT admin enforces these updates.
- **Sort by**: Rearrange the list of updates. By default this list sorts by **Application name: A to Z**.

To install updates, select **Install All**.

To only install specific updates, select the icon to enter multi-select mode. Check the updates to install, and then select **Install Selected**.


## Operating Systems

Select the **Operating Systems** tab to view and install versions of Windows that your IT admin deploys to this computer.  

- **All**: Shows all Windows versions that you can install
- **Required**: Your IT admin enforces these upgrades.
- **Sort by**: Rearrange the list of updates. By default this list sorts by **Application name: A to Z**.


## Installation status

Select the **Installation status** tab to view the status of applications. You may see the following states:

- **Installed**: Software Center already installed this application on this computer.
- **Downloading**: Software Center is downloading the software to install on this computer.
- **Failed**: Software Center encountered an error in trying to install the software.
- **Scheduled to install after**: Shows the date and time of the device's next maintenance window to install upcoming software. Maintenance windows are defined by your IT admin.<!--1358131-->
    - The status can be seen in the **All** and the **Upcoming** tab.
    - You can install before the maintenance window time by selecting the **Install Now** button.


## Device compliance

Select the **Device compliance** tab to view the compliance status of this computer.

Select **Check compliance** to evaluate this device's settings against the security policies defined by your IT admin.


## Options

Select the **Options** tab to view additional settings for this computer.

### Work information

Indicate the hours that you typically work. Your IT admin may schedule software installations outside your business hours. Allow at least four hours each day for system maintenance tasks. Your IT admin can still install critical applications and software updates during business hours.

- Select the drop-down lists to select the earliest and latest hours that you use this computer. By default these values are from **5 AM** through **10 PM**

- Select the checkbox next to the days of the week that you typically use this computer. Software Center only selects the weekdays by default.  

Specify whether you regularly use this computer to do your work. Your administrator might automatically install applications or make additional applications available to primary computers. <!--3485366-->

- Select **I regularly use this computer to do my work** if the computer you're using is a primary computer.

### Power management

Your IT admin may set power management policies. These policies help your organization conserve electricity when this computer isn't in use.

To make this computer exempt from these policies, select the checkbox **Do not apply power settings from my IT department to this computer**. This setting is disabled by default; the computer applies power settings.

### Computer maintenance

Specify how Software Center applies changes to software before the deadline

- **Automatically install or uninstall required software and restart the computer only outside of the specified business hours**: This setting is disabled by default.
- **Suspend Software Center activities when my computer is in presentation mode**: This setting is enabled by default.
- **Sync Policy**: Select this button when instructed by your IT admin. This computer checks with the servers for anything new, such as applications, software updates, or operating systems.

### Remote Control

Specify remote access and remote control settings for your computer

- **Use remote access settings from your IT Department**: This checkbox is selected by default.
- **Level of remote access allowed**: Select from the following 3 options
    - **Do not allow remote access**
    - **View only**
    - **Full**: This level is enabled by default.
- **Allow remote control of this computer by administrators when I am away**. This setting is set to **Yes** by default.
- **When an administrator tries to control this computer remotely**: This setting has two options
    - **Ask for permission each time**: This option is selected by default.
    - **Do not ask for permission**
- **Show the following during remote control**: Both options are selected by default
    - **Status icon in the notification area**
    - **A session connection bar on the desktop**
- **Play sound**: This setting has three options
    - **When session begins and ends**: This setting is selected by default.
    - **Repeatedly during session**
    - **Never**

    For more info, see [Introduction to Remote Control](../clients/manage/remote-control/introduction-to-remote-control.md)
    

## Custom tab in Software Center

Your IT admin might have added an additional tab to Software Center. This tab is named by your admin and leads to a web site they specify. For instance, you might have a tab called "Help Desk" that leads to your organization's help desk web site. <!--1358132-->
