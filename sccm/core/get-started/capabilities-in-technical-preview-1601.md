---
title: "Capabilities in Technical Preview 1601"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1601."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
caps.latest.revision: 7
author: Brendunsms.author: brendunsmanager: angrobe
robots: noindex,nofollow
---
# Capabilities in Technical Preview 1601 for System Center Configuration Manager*Applies to: System Center Configuration Manager (Technical Preview)*
This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1601. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.  

 **Known Issues for this Technical Preview:**  

-   When you manage **Client Update Options** to promote a pre-production client to production, the  text for the checkbox   displays a client version of zero (0) instead of the actual client build number. The correct pre-production client version is shown on the surface above this option, and is the client version that is promoted to production when you select this option.  

-   When updating to Technical Preview 1601 and choosing to test the Configuration Manager client in a pre-production collection, the client package for the collection will not be upgraded. This issue is for Technical Preview 1601 only.  

     To workaround this issues, do one of the follow:  

    -   Run the following SQL script on the primary site's database:  

        ```  
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Add a new distribution point site system role to your lab  site. The new distribution point will upgrade the pre-production collection with the new client package.  

**The following are new features you can try out with this version.**  

##  <a name="bkmk_hybrid1"></a> Improvements to Microsoft Intune integration  
In the 1601 Technical Preview, we have added support for the following features:  

### Improvements to Conditional Access  

-   **Conditional access support for PCs that are managed by System Center Configuration Manager**  

     You can now set conditional access policies for PCs managed by System Center Configuration Manager, which will require that the PCs be compliant with the compliance policy in order to access Exchange Online and SharePoint Online services.  With this new functionality, you can also register PCs with Azure AD through the  compliance policy, and to monitor and report on Azure AD registration.  

    > [!NOTE]  
    >  Conditional Access is not yet supported on Windows 10.  

    Following are the prerequisites  to use this feature:  

    -   Azure Active Directory Premium subscription and ADFS Sync.  

    -   A Microsoft Intune Subscription. The Microsoft Intune Subscription  should be configured in Configuration Manager Console.  

    -   [Prerequisites for Azure AD auto-registration](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    To use the option, you must create a compliance policy in Configuration Manager with specific rules described below, and set a conditional access policy in the Intune console.  Also, to make sure only compliant PCs are allowed access, you must set the Windows PC requirement to **Devices must be compliant** option. Following are the compliant policy rules that are applicable to PCs managed by System Center Configuration manager.  

    -   **Require registration in Azure ActiveDirectory:** This rule checks if the user’s device is  work place joined to Azure AD, and if not, the device is automatically registered in Azure AD. Automatic registration is only supported on Windows 8.1. For Windows 7 PCs, deploy an MSI to perform the auto registration. For more information, see [here](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **All required updates installed with a deadline older than a certain number of days:** This rule checks to see  if the user’s device has all required updates (specified in the **Required automatic updates** rule) within deadline and grace period specified by you, and automatically install the any pending required updates.  

    -   **Require BitLocker drive encryption:** This is a check to see if the primary drive (e.g. C:\\) on the device is BitLocker encrypted. If Bitlocker encryption is not enabled on the primary device access to email and SharePoint services is blocked.  

    -   **Require Antimalware:** This is a check to see if the antimalware software (System Center Endpoint Protection or Windows Defender only) is enabled and running.  
         If it is not enabled, access to email and SharePoint services is blocked.  

    End-users who are blocked due to non compliance will view compliance information in the SCCM Software Center and will initiate a new policy evaluation when compliance issues are remediated.  

-   **Conditional access with Health Attestation Service** You can now restrict access to email and 0365 services based on the health of the devices as reported by the Health Attestation Service.  Additionally, devices that are managed by Intune are included in the device health reports.  

    A new compliance rule has been added to the configuration manager console that  allows you to specify if the devices should be allowed or blocked access based on their health status.  To create this rule, open the **Create Compliance Policy Wizard**,  and add a new rule.  Select the **Reported as health by Health Attestation Service** for the  condition, and set the value to **True**.  This will make sure that only devices that are reported as healthy will have access to your company resources. For details about Health Attestation Service and how the health of the devices is reported in Intune, see [Device Health Attestation](#bkmk_devicehealth).  

-   **New compliance policy settings:** The new compliance policy settings help improve security and protection on devices that are used to access company email and SharePoint services:  

    -   **Require automatic updates:** You can require devices with Windows 8.1 or later to allow  automatic install of updates and also specify the class of updates that are installed.  You can either choose to: install only updates marked as important, or  install all recommended updates.  

         To create a rule for automatic updates, open the **Create Compliance Policy Wizard**,  and add a new rule.  Select  **Minimum classification of required updates** as the condition, and set the value to one of the available values: **None**, **Recommended**, and **Important**.  

        -   **None:** Updates are not automatically installed.  

        -   **Recommended:** All recommended updates are installed  

        -   **Important:** Only updates classified as important are installed.  

    -   **Require a password to unlock mobile devices:** When this setting is set to **Yes**, the end-users must enter a password before they can access their device.  

         To create a rule for password to unlock mobile devices,  open the **Create Compliance Policy Wizard**,  and add a new rule. Select **Require a password to unlock an idle device** as the condition, and set the value to **True**.  

    -   **Minutes of inactivity before password is required:**  Specifies the idle time before the user must re-enter their password.  

         To create this rule, open the **Create Compliance Policy Wizard**,  and add a new rule. **Select Minutes of inactivity before password is required** as the condition, and set the value to one of the available options: 1 minute, 5 minutes, 15 minutes, 30 minutes,  I hour.  

-   **Default rule override - Always allow Intune enrolled and compliant devices to access Exchange on-premises:**  

     When you check this option, devices that are enrolled in Intune and compliant with the compliance policies are allowed to access Exchange on-premises. This rule overrides the Default Rule, which means that even if you set the Default Rule to quarantine or block access, enrolled and compliant devices will still be able to access Exchange on-premises.  
     Use this setting when you want enrolled and compliant devices to always have access to email through  Exchange on-premises.  

     This is supported on the following platforms:  Windows Phone 8 and later,  iOS 6 and later. Android 4.0 and later, Samsung KNOX Standard 4.0 and later.  

     To use this option, go to the **General** page of the **Configure Conditional Access Policy Wizard** for  Exchange on-premises.  

##  <a name="bkmk_clientStatus"></a> Client online status  
Beginning with technical preview 1601, you can identify at a glance whether a client is online or offline in the Configuration Manager console. With updated icons and columns in the console device listings, you can assess the status of clients in your environment to identify problem areas and other issues that might need your attention.  

A client is online if it is currently connected to a Configuration Manager management point site system role. As long as the management point is receiving ping-like messages from the client, its status is online. If the management doesn’t receive a message for 5 minutes or so, the client’s status changes to offline.  

### Icons for client status  

|||  
|-|-|  
|![online status icon for clients](media/online-status-icon.png)|Client is online.|  
|![offline status icon for clients](media/offline-status-icon.png)|Client is offline.|  
|![unknown status icon for clients](media/unknown-status-icon.png)|Client status is unknown.|  

### Prerequisites  
 Client online status has no prerequisites. You can start using it as soon as Configuration Manager technical preview 1601 is installed.  

### Limitations  
 Client online status is only available for Windows computers with the  Configuration Manager client installed. Client online status is not supported for Mac computers, Linux or UNIX computer, or devices managed with On\-premises Mobile Device Management.  

### To view client online status  

1.  In the Configuration Manager console, go to **Assets and Compliance > Overview > Devices**.  

2.  Right-click in the column header, and then click one of the client online status fields to add it to the device view. The fields are  

    -   **Device Online Status** indicates whether the client is currently online or offline.  

    -   **Last Online Time** indicates when the client online status changed from offline to online.  

    -   **Last Offline Time** indicates when the status changed from online to offline.  

 To show recent changes to client status, refresh the console.  

##  <a name="bkmk_appmgmt1601"></a> Improvements to application management  
 In the 1601 Technical Preview we have added support for the following features:  

### Manage volume-purchased apps for iOS devices  
 Some app stores give you the ability to purchase multiple licenses for an app you want to run in your company. This helps you reduce the administrative overhead of tracking multiple purchased copies of apps.  

 Configuration Manager now helps you manage apps you purchased through such a program by importing the license information from the app store and tracking how many of the licenses you have used.  

 For details, see [Manage apps you purchased through a volume-purchase program with Configuration Manager](https://technet.microsoft.com/library/mt627954.aspx).  

### iOS - App Configuration for applications<br />Hybrid  
 Some iOS applications support pre-configuring settings such as a server or database that the application should connect to. Configuration Manager now supports deploying app configuration policies to the device which enable the user to use the app immediately without needing to know this information. Developers must enable this functionality in their apps.  

 A limited number of publicly released apps currently support pre-configuring settings; you might also have in-house developed line of business apps that support these.  

#### Prerequisites for this scenario  

-   You must have added a Microsoft Intune subscription to Configuration Manager.  

-   You must have added a valid Apple APNs certificate to the Intune subscription.  

-   You must have deployed an iOS application that supports application configuration.  

#### Try it out!  
 Once the prerequisites above are met, you must create a Configuration Manager application that uses an iOS deployment type. The app you use must support application configuration. Refer to the application’s vendor documentation to learn what specific items (name/value pairs), you can configure.  

 Then, you associate the app configuration policy with the iOS deployment type during app deployment. You can also deploy the policy from the **App Configuration Policies** node, targeted to an existing app and collection.  

 Try to complete the following tasks and then use the feedback information near the top of this topic to let us know how they worked:  

-   If you have an iOS app that supports app configuration, consult the app vendor's documentation to find out the name and value pairs you must specify to configure the application.  

-   Start the **Create App Configuration Policy** wizard. On the **iOS Policy** page of the wizard, try adding the name and value pairs you found from the app vendor documentation or you can import an XML file containing the required values.  

-   In the **Deploy Software** wizard, on the **App Configuration Policy** page, associate the app configuration policy you created with a compatible deployment type from the application.  

##  <a name="bkmk_compliance1601"></a> Improvements to compliance settings  
 In the 1601 Technical Preview we have added support for the following features:  

### Microsoft Edge browser settings  
 New settings for the Microsoft Edge browser have been added to the **Windows 8.1 and Windows 10** configuration item (settings apply to Windows 10 devices only).  

 To see the new settings, choose **Microsoft Edge** from the configuration item **Device Settings** page of the **Create Configuration Item** wizard.  

 For more information, see [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### Compliance settings for Windows 10 Team devices  
 Use these new compliance settings to configure devices that run Windows 10 team, such as Surface Hub Devices.  

 To see the new settings, choose **Windows 10 Team** from the configuration item **Device Settings** page of the **Create Configuration Item** wizard.  

 For more information, see [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### Android - Kiosk Mode for Samsung KNOX Standard<br />Hybrid  
 Kiosk mode lets you lock a device to only allow certain features to work. For example, you can allow a device to only run one managed app that you specify, or you can disable the volume buttons on a device. These settings might be used for a demonstration model of a device, or a device that is dedicated to performing only one function, such as a point of sale device. These settings are not available for Samsung KNOX Standard devices in the **Windows 8.1 and Windows 10** configuration item (settings apply to Windows 10 devices only).  

 To see the new settings, choose **Kiosk Mode - Samsung KNOX** from the configuration item **Device Settings** page of the **Create Configuration Item** wizard.  

 For more information, see [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
