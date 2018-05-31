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



## Transition Office 365 workload to Intune using co-management
<!--1357841-->
You can now transition the Office 365 workload from Configuration Manager to Microsoft Intune after enabling co-management. To transition this workload, go to the co-management properties page and move the slider bar from Configuration Manager to Pilot or All. For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).

There is also a new global condition, **Are Office 365 applications managed by Intune on the device**. This condition is added by default as a requirement to new Office 365 applications. When you transition this workload, co-managed clients don't meet the requirement on the application, thus don't install Office 365 deployed via Configuration Manager.

### Known issue
- This workload transition currently only applies to Office 365 deployments. Configuration Manager continues to manage Office 365 updates.<!--510876--> For more information including a possible workaround, see the Configuration Manager version 1802 release note [Changing Office 365 client setting doesn’t apply](/sccm/core/servers/deploy/install/release-notes#changing-office-365-client-setting-doesnt-apply).



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
- The icon for an update deployed with this setting incorrectly displays with a red X as if the update is invalid. For more information, see [Icons used for software updates](/sccm/sum/understand/software-updates-icons). <!--515556-->  
- This setting is only integrated with the Deploy Software Updates Wizard. It isn't currently available with automatic deployment rules. <!--515558-->  



## Office Customization Tool integration with the Office 365 Installer
<!--1358149-->
The Office Customization Tool is now integrated with the Office 365 Installer in the Configuration Manager console. When creating a deployment for Office 365, you can now dynamically configure the latest Office manageability settings. The Office Customization Tool is updated at the same time as the release of new builds of Office 365. You can now take advantage of new manageability settings in Office 365 as soon as they are available. 

### Prerequisites
- The computer running the Configuration Manager console needs internet access via HTTPS port 443. The Office 365 Client Installation Wizard uses a Windows standard web browser API to open https://config.office.com. If an internet proxy is used, the user must be able to access this URL.

### Try it out!
 Try to complete the tasks. Then send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, go to the **Software Library** workspace, and select the **Office 365 Client Management** node.
2. Click the **Office 365 Installer** tile in the dashboard to launch the Office 365 Client Installation Wizard. For more information, see [Deploy Office 365 apps](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).
3. On the **Office Setting** page, click **Go To Office Web Page**. Use the online Office Customization Tool to specify settings for this deployment. 
4. Click **Submit** in the upper right corner when complete. Finish the Office 365 Client Installation Wizard.



## Improvements to cloud management gateway
This release includes the following improvements to the cloud management gateway (CMG):

### Simplified client bootstrap command line
<!--1358215-->
When installing the Configuration Manager client on the internet via a CMG, fewer command-line properties are now required. For more information on one example of this scenario, see the [Command line to install Configuration Manager client](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) when preparing for co-management. 

The following command-line properties are required in all scenarios:
  - CCMHOSTNAME  
  - SMSSITECODE  

The following properties are required when using Azure AD for client authentication instead of PKI-based client authentication certificates:
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

The following property is required if the client will roam back to the intranet:
  - SMSMP  

The following example includes all of the above properties:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).

### Download content from a CMG
<!--1358651-->
Previously, you had to deploy a cloud distribution point and CMG as separate roles. Now in this release, a CMG can also serve content to clients. This functionality reduces the required certificates and cost of Azure VMs. To enable this feature, enable the new option to **Allow CMG to function as a cloud distribution point and serve content from Azure storage** on the **Settings** tab of the CMG properties. 

### Trusted root certificate isn't required with Azure AD
<!--503899-->
When you create a CMG, you're no longer required to provide a [trusted root certificate](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) on the Settings page. This certificate isn't required when using Azure Active Directory (Azure AD) for client authentication, but used to be required in the wizard.

> [!Important]  
> If you're using PKI client authentication certificates, then you still must add a trusted root certificate to the CMG.



## Improvements to secure client communications
<!--1358278,1358279-->
This release continues to iterate on [improved secure client communications](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications) by removing additional dependencies on the network access account. When you enable the new site option to **Use Configuration Manager-generated certificates for HTTP site systems**, the following scenarios don't require a network access account to download content from a distribution point:
- OS deployment task sequence running from boot media or PXE
- OS deployment task sequence running from Software Center



## Software Center infrastructure improvements
<!--1358309-->
Application catalog roles are no longer required to display user-available applications in Software Center. This change helps you reduce the server infrastructure required to deliver applications to users. Software Center now relies upon the management point to obtain this information, which helps larger environments scale better by assigning them to [boundary groups](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

### Try it out!
 Try to complete the tasks. Then send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked.

1. Remove all application catalog roles from the site. These roles include the application catalog web service point and the application catalog website point.
2. Deploy an application as available to a user collection.
3. Use Software Center as a targeted user to browse for, request, and install the application.

### Known issue
- Don't configure the site to **Use Configuration Manager-generated certificates for HTTP site systems**, as it currently conflicts with this feature.<!--bugID--> For more information on this setting, see [improved secure client communications](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).



## Provision Windows app packages for all users on a device
<!--1358310-->
You can now provision an application with a Windows app package for all users on the device. One common example of this scenario is provisioning an app from the Microsoft Store for Business and Education, like Minecraft: Education Edition, to all devices used by students in a school. Previously, Configuration Manager only supported installing these applications per user. After signing in to a new device, a student would have to wait to access an app. Now when the app is provisioned to the device for all users, they can be productive more quickly.

> [!Important]  
> Be careful with installing, provisioning, and updating different versions of the same Windows app package on a device, which may cause unexpected results. This behavior may occur when using Configuration Manager to provision the app, but then allowing users to update the app from the Microsoft Store. For more information, see the next step guidance when you [Manage apps from the Microsoft Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps). 

### Try it out!
 Try to complete the tasks. Then send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked.

1. Create a new application. This app must be from a Windows app package, or an offline-licensed app, which you've synchronized from the Microsoft Store for Business and Education. 
2. On the **General Information** page of the Create Application Wizard, enable the option to **Provision this application for all users on the device**.  

   > [!Tip]  
   > If you are modifying an existing application, this setting is on the **User Experience** tab of the application properties.  

3. Deploy the application to a device collection.
4. Sign in to a targeted device with different user accounts and launch the application.

> [!Note]  
> If you need to uninstall a provisioned application from devices to which users have already signed on, you need to create two uninstall deployments. Target the first uninstall deployment to a device collection that contains the devices. Target the second uninstall deployment to a user collection that contains the users who have already signed on to devices with the provisioned application. When uninstalling a provisioned app on a device, Windows currently doesn't uninstall that app for users as well. 



## Improvements to the Surface dashboard
<!--1358654-->
This release includes the following improvements to the [Surface dashboard](/sccm/core/clients/manage/surface-device-dashboard):
- The Surface dashboard now displays a list of relevant devices when graph sections are selected.
   - Clicking on the **Percent of Surface Devices** tile opens a list of Surface devices.
   - Clicking on a bar in the **Top Five Firmware Versions** tile opens a list of Surface devices with that specific firmware version.
- When viewing these device lists from the Surface dashboard, you can right-click a device and perform common actions.



## Hardware inventory default unit revision
<!--514442-->
In [Configuration Manager version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), the default unit used in many reporting views changed from megabytes (MB) to gigabytes (GB). Due to [improvements to hardware inventory for large integer values](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvement-to-hardware-inventory-for-large-integer-values), and based on customer feedback, this default unit is now MB again.



## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
