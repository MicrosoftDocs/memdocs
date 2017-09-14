---
title: "Create and run scripts with Configuration Manager | Microsoft Docs"
description: "Create and run scripts on client devices with Configuration Manager."
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: 14
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe

---

# Create and run PowerShell scripts from the Configuration Manager console

*Applies to: System Center Configuration Manager (Current Branch)*

In Configuration Manager, in addition to using packages and programs to deploy scripts, you can use the following functionality to take the following actions:

- Import PowerShell Scripts to Configuration Manager
- Edit the scripts from the Configuration Manager console (for unsigned scripts only)
- Mark scripts as Approved or Denied, to improve security
- Run scripts on collections of Windows client PCs, and on-premises managed Windows PCs. You don't deploy scripts, instead, they are run almost immediately on client devices.
- Examine the results returned by the script in the Configuration Manager console.

>[!TIP]
>In this version of Configuration Manager, scripts are a pre-release feature. To enable scripts, see [Pre-release features in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## Prerequisites

To run PowerShell scripts, the client must be running PowerShell version 3.0 or later. However, if a script you run contains functionality from a later version of PowerShell, the client on which you run the script must be running that version.

Configuration Manager clients must be running the client from the 1706 release, or later in order to run scripts.

To use scripts, you must be a member of the appropriate Configuration Manager security role.

- To import, and author scripts - Your account must have **Create** permissions for **SMS Scripts** in the **Compliance Settings Manager** security role.
- To approve, or deny scripts - Your account must have **Approve** permissions for **SMS Scripts** in the **Compliance Settings Manager** security role.
- To run scripts - Your account must have **Run Script** permissions for **Collections** in the **Compliance Settings Manager** security role.

For more information about Configuration Manager security roles, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration).

By default, users cannot approve a script they have authored. Because scripts are powerful, versatile, and can be deployed to many devices, you can separate the roles between the person that authors the script and the person that approves the script. These roles give an additional level of security against running a script without oversight. You can turn off this secondary approval, for ease of testing.

## Allow users to approve their own scripts

1. In the Configuration Manager console, click **Administration**.
2. In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.
3. In the list of sites, choose your site and then, on the **Home** tab, in the **Sites** group, click **Hierarchy Settings**.
4. On the **General** tab of the **Hierarchy Settings Properties** dialog box, clear the checkbox **Do not allow script authors to approve their own scripts**.

## Import and edit a script

1. In the Configuration Manager console, click **Software Librar**y.
2. In the **Software Library** workspace, click **Scripts**.
3. On the **Home** tab, in the **Create** group, click **Create Script**.
4. On the **Script** page of the Create **Script** wizard, configure the following settings:
	- **Script Name** - Enter a name for the script. Although you can create multiple scripts with the same name, using duplicate names makes it harder for you to find the script you need in the Configuration Manager console.
	- **Script language** - Currently, only PowerShell scripts are supported.
	- **Import** - Import a PowerShell script into the console. The script is displayed in the **Script** field.
	- **Clear** - Removes the current script from the Script field.
	- **Script** - Displays the currently imported script. You can edit the script in this field as necessary.
5. Complete the wizard. The new script is displayed in the **Script** list with a status of **Waiting for approval**. Before you can run this script on client devices, you must approve it.

### Script examples

Here are some examples that illustrate scripts you might want to use with this capability.

#### Create a folder

*New-Item "c:\scripts" -type folder name* 
 
 
#### Create a file

*New-Item c:\scripts\new_file.txt -type file name*


## Approve or deny a script

Before you can run a script, it must be approved. To approve a script:

1. In the Configuration Manager console, click **Software Library**.
2. In the **Software Library** workspace, click **Scripts**.
3. In the **Script** list, choose the script you want to approve or deny and then, on the **Home** tab, in the **Script** group, click **Approve/Deny**.
4. In the **Approve or deny** script dialog box, **Approve**, or **Deny** the script, and optionally enter a comment about your decision. If you deny a script, it cannot be run on client devices.
5. Complete the wizard. In the **Script** list, you see the **Approval State** column change depending on the action you took.

## Run a script
After a script is approved, it can be run against a collection you choose.

1. In the Configuration Manager console, click **Assets and Compliance**.
2. In the Assets and Compliance workspace, click **Device Collections**.
3. In the **Device Collections** list, click the collection of devices on which you want to run the script.
4. On the **Home** tab, in the **All Systems** group, click **Run Script**.
5. On the **Script** page of the **Run Script** wizard, choose a script from the list. Only approved scripts are shown.
6. Click **Next**, and then complete the wizard.

>[!IMPORTANT]
>The script is given a one-hour time period in which to run. If it does not run (for example if the PC is turned off) in this time period, you must run it again.

## Next steps

After you have run a script to client devices, use this procedure to monitor the success of the operation.

1. In the Configuration Manager console, click **Monitoring**.
2. In the **Monitoring** workspace, click **Script Status**.
3. In the **Script Status** list, you view the results for each script you ran on client devices. A script exit code of **0** generally indicates that the script ran successfully.
