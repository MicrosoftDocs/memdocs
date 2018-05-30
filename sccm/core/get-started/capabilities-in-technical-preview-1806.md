---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager Technical Preview version 1806.
ms.date: 06/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Capabilities in Technical Preview 1806 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1806. You can install this version to update and add new capabilities to your technical preview site. 

Review the [Technical Preview](/sccm/core/get-started/technical-preview) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**The following are new features you can try out with this version.**  



## Configure Windows Defender SmartScreen settings for Microsoft Edge
<!--1353701-->
This release adds three settings for [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) to the [Microsoft Edge browser compliance settings policy](/sccm/compliance/deploy-use/browser-profiles). The policy now includes the following additional settings on the **SmartScreen Settings** page:
- **Allow SmartScreen**: Specifies whether Windows Defender SmartScreen is allowed. For more information, see the [AllowSmartScreen browser policy](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Users can override SmartScreen prompt for sites**: Specifies whether users can override the Windows Defender SmartScreen Filter warnings about potentially malicious websites. For more information, see the [PreventSmartScreenPromptOverride browser policy](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Users can override SmartScreen prompt for files**: Specifies whether users can override the Windows Defender SmartScreen Filter warnings about downloading unverified files. For more information, see the [PreventSmartScreenPromptOverrideForFiles browser policy](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## Sync MDM policy from Microsoft Intune for a co-managed device
<!--1357377-->
Starting in this release when you [switch a co-management workload](/sccm/core/clients/manage/co-management-switch-workloads), the co-managed devices automatically synchronize MDM policy from Microsoft Intune. This sync also happens when you initiate the **Download Computer Policy** action from Client Notifications in the Configuration Manager console. For more information, see [Initiate client policy retrieval using client notification](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## Package Conversion Manager 
<!--1357861-->
Package Conversion Manager is now an integrated tool that allows you to convert legacy Configuration Manager 2007 packages into Configuration Manager current branch applications. Then you can use features of applications such as dependencies, requirement rules, and user device affinity.

> [!Tip]  
> Legacy documentation for the existing functionality in Package Conversion Manager is available on [TechNet](https://technet.microsoft.com/library/hh531519.aspx). Relevant information is in process to migrate to the docs.microsoft.com library.

### Try it out!
 Try to complete the tasks. Then send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked.

> [!Important]  
> If you previously installed an older version of Package Conversion Manager, first uninstall it before upgrading your site. The new integrated version doesn't require installation, but may conflict with existing versions.  

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Application Management** and select **Packages**.  
2. Select a package. The following three options are available in the **Package Conversion** group of the ribbon:  
     - **Analyze Package**: Start the conversion process by analyzing the package.
     - **Convert Package**: Some packages can easily be converted into applications with this action.
     - **Fix and Convert**: Some packages require issues to be fixed before converting into applications.  

   For more information on these actions, see [How to Analyze and Convert Packages](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29).  

3. Go to the **Monitoring** workspace and select **Package Conversion Status**. This new dashboard shows the overall analysis and conversion state of packages in the site. A new background task automatically summarizes the analysis data.  

   > [!Tip]  
   > Package Conversion Manager doesn't require you to schedule analysis of packages. This action is now handled by the integrated summarization task.  



## Deploy software updates without content
<!--1357933-->
You can now deploy software updates to devices without first downloading and distributing software update content to distribution points. This feature is beneficial when dealing with extremely large update content, or when you always want clients to get content from the Microsoft Update cloud service. Clients in this scenario can also download content from peers that already have the necessary content in their cache.

### Try it out!
 Try to complete the tasks. Then send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked.

1. Start a software update deployment per normal. For more information, see [Deploy software updates](/sccm/sum/deploy-use/deploy-software-updates).
2. In the Deploy Software Updates Wizard, on the **Deployment Package** page, select the new option for **No deployment package**.

### Known issues
- The icon for an update deployed with this setting incorrectly displays with a red X as if the update is invalid. For more information, see [Icons used for software updates](/sccm/sum/understand/software-updates-icons). <!--bugID-->  
- This setting is only integrated with the Deploy Software Updates Wizard. It isn't currently available with automatic deployment rules. <!--bugID-->  



## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
