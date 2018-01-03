---
title: "The content library cleanup tool"
titleSuffix: "Configuration Manager"
description: "Use the content library cleanup tool to remove orphaned content no longer associated with a System Center Configuration Manager deployment."
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: 4
author: aczechowski
ms.author: aaroncz
manager: angrobe
---
# The Content library cleanup tool for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

 Beginning with version 1702, you can use a command line tool (**ContentLibraryCleanup.exe**) to remove content that is no-longer associated with any package or application from a distribution point (orphaned content). This tool is called the content library cleanup tool, and replaces older versions of similar tools released for past Configuration Manager products.  

The tool only affects the content on the distribution point that you specify when you run the tool. The tool cannot remove content from the content library on the site server.

You can find **ContentLibraryCleanup.exe** in the *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* folder on the site server at a central administration site or primary site.

## Requirements  
 The tool can only run against a single distribution point at a time.  
 - It can run directly on the computer that hosts the distribution point you want to clean, or remotely from another server.
 - The user account that runs the tool must have direct role-based administration permissions that are equal to a Full Administrator on the Configuration Manager hierarchy. The tool does not work when the account receives these permissions as a member of a Windows security group that has the Full Administrator permissions.

## Modes of operation
You can run the tool in the following two modes. We recommend you run the tool in *What-If* mode so you can review the results before you run the tool in *delete mode*:
  1.	**What-If mode**:   
      If you do not specify the **/delete** switch, the tool runs in What-If mode and identifies the content that would be deleted from the distribution point.
   - When run in this mode the tool does not delete any data.
   - Information about the content that would be deleted is written to the tools log file, and you are not prompted to confirm each potential deletion.  
      </br>   

  2. **Delete mode**:   
    When you run the tool with the **/delete** switch, the tool runs in delete mode.

     - When run in this mode, orphaned content that is found on the specified distribution point can be deleted from the distribution point’s content library.
     - 	Before deleting each file, you must confirm that the file should be deleted.  You can select, **Y** for yes, **N** for no, or **Yes to all** to skip further prompts and delete all orphaned content.  
     </br>

When the tool runs in either mode, it automatically creates a log with a name that includes the mode the tool runs in, the name of the distribution point, and the date and time of operation. The log file automatically opens when the tool finishes.

By default, the log file is written to the temp folder of the user account that runs the tool, on the computer where the tool is run. You can use the **/log** switch to redirect the log file to another location, including a network share.


## Run the tool
To run the tool:
1. Open an administrative command prompt to a folder that contains **ContentLibraryCleanup.exe**.  
2. Next, enter a command line that includes the required command line switches, and optional switches you want to use.

**Known issue**
When the tool is run, an error like the following might be returned when any package or deployment has failed, or is in progress:
-  *System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.*

**Workaround:** None. The tool cannot reliable identify orphaned files when content is in progress or has failed to deploy. Therefore, the tool will not allow you to clean-up content until that issue is resolved.

### Command line switches  
The following command line switches can be used in any order.   

|Switch|Details|
|---------|-------|
|**/delete**  |**Optional** </br> Use this switch when you want to delete content from the distribution point. You are prompted before content is deleted. </br></br> When this switch is not used, the tool logs results about what content would be deleted, but does not delete content from the distribution point. </br></br> Example: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Optional** </br> This switch runs the tool in a quiet mode that suppresses all prompts (like the prompts to delete content), and does not automatically open the log file. </br></br> Example: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;distribution point FQDN>**  | **Required** </br> Specify the fully qualified domain name (FQDN) of the distribution point that you want to clean. </br></br> Example:  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;primary site FQDN>**       | **Optional** when cleaning content from a distribution point at a primary site.</br>**Required** when cleaning content from a distribution point at a secondary site. </br></br>The tool connects to the parent primary site to run queries against SMS_Provider. These queries let the tool determine what content should be on the distribution point so it can identify the content that is orphaned and can be removed. This connection to the parent primary site must be made for distribution points at a secondary site because the required details are not available directly from the secondary site.</br></br> Specify the FQDN of the primary site that the distribution point belongs to, or of the parent primary parent when the distribution point is at a secondary site. </br></br> Example: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;primary site code>**  | **Optional** when cleaning content from a distribution point at a primary site.</br>**Required** when cleaning content from a distribution point at a secondary site. </br></br> Specify the site code of the primary site that the distribution point belongs to, or of the parent primary site when the distribution point is at a secondary site.</br></br> Example: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Optional** </br> Specify the location where the tool writes the log file. This can be a local drive or on a network share.</br></br> When this switch is not used, the log file is placed in the temp folder of the user, on the computer where the tool runs.</br></br> Example of local drive: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Example of network share: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|
