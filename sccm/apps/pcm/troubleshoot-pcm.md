---
title: Troubleshoot Package Conversion Manager
titleSuffix: Configuration Manager
description: Learn how to troubleshoot problems with the Package Conversion Manager in Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Troubleshoot Package Conversion Manager

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1357861-->

Use the information in this article to help you troubleshoot problems when using Package Conversion Manager.



## SMS Provider

Package Conversion Manager uses the SMS Provider. For more information, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

If the SMS Provider isn't working properly, the Configuration Manager console including the Package Conversion Manager doesn't work.



## Package readiness

Before converting a package to an application, analyze the package using the Package Conversion Manager **Analyze** function. After the analysis, add the **Readiness** column in the **Packages** node of the Configuration Manager console. The list of packages displays one of the following readiness states of the analyzed package:

 - **Automatic**: The package can be directly converted using the **Convert** function.      

    > [!NOTE]  
    > An automatic conversion doesn't convert WQL queries into application requirements. Use the **Fix and Convert** process to convert these queries.  

 - **Manual**: The package needs some additions or changes before you can convert it using the **Fix and Convert** function.  

 - **Not Applicable**: The package isn't suitable for conversion. Either correct any problems with the package, or continue to deploy it as a package.  

 - **Error**: The package contains errors. Manually correct these errors before you can analyze and convert it.  

The details pane of the **Packages** node in the Configuration Manager console shows any readiness issues. Select a package, and then select the **Summary** tab in the details pane.



## Log files

### PCMTrace.log

Each instance of Package Conversion Manager creates a log file. This file includes all of its actions, exceptions, and errors. 

**PCMTrace.log** is on the computer running Package Conversion Manager in the following path:  
`%UserProfile%\AppData\Local\Temp`

To configure the level of detail in this log, modify **Microsoft.ConfigurationManagement.exe.Config**. By default, this configuration file is located in the following path:  
`C:\Program Files\Microsoft Configuration Manager\AdminConsole\bin`  

In the `<switches>` element, use the **PcmLogging** trace switch setting. Set the this value to four levels of detail, from least detailed (`1`) to most detailed (`4`).



### SMSProv.log

In some situations, information relevant to troubleshooting the package conversion process is in the **SMSProv.log** file. This file captures information from the Configuration Manager SMS Provider.

By default, this log file is located on the Configuration Manager site server at the following path:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

If you see one of the following error messages, the **SMSProv.log** file may contain relevant troubleshooting information:

- `The SMS Provider reported an error`

- `Generic Failure`

These error messages typically indicate that an error occurred on the site server, and that the error information wasn't sent to the Configuration Manager console.

For more information, see [Technical reference for Package Conversion Manager error messages](/sccm/apps/pcm/error-messages).



## Changing package attributes after analysis

After you analyze a package and it has a readiness state of **Automatic** or **Manual**, the conversion process might fail if you change any of the relevant attributes.

For example, you analyze a package and its readiness state is **Automatic**. Then you add another program to the package. The package conversion might fail.

If you need to make changes to a package after analysis, rerun analysis before conversion. 



## See also

[Technical reference for Package Conversion Manager error messages](/sccm/apps/pcm/error-messages)