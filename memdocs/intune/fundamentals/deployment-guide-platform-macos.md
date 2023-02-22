---
# required metadata

title: Deployment guide to manage macOS devices in Microsoft Intune
description: Learn the recommended processes to manage macOS devices in Microsoft Intune.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/16/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Deployment guide: Manage macOS devices in Microsoft Intune

Secure access to work email, data, and apps on macOS devices. This article guides you through macOS-specific tasks to help you enable Intune mobile device management for macOS, configure policies, and deploy apps.  


## Prerequisites  

Complete the following prerequisites to enable macOS device management in Intune:      

* [Add users](users-add.md) and [groups](groups-add.md)
* [Assign licenses to users](licenses-assign.md) 
* [Set mobile device management authority](mdm-authority-set.md) 
* [Have Global Administrator or Intune administrator Azure Active Directory permissions](role-based-access-control.md)  
* [Set up Apple MDM push (APNs) certificate](../enrollment/apple-mdm-push-certificate-get.md)  

 For more detailed information about how to do the initial setup, onboard, or move to Microsoft Intune, see the [Intune setup deployment guide](deployment-guide-intune-setup.md).    

## Plan for your deployment  

Use the [Microsoft Intune planning guide](intune-planning-guide.md) to define your device management goals, use-case scenarios, and requirements. It will also help you plan for rollout, communication, support, testing, and validation. For example, because the Company Portal app for macOS isn't available in the App Store, we recommend having a communication plan so that end users know how to install Company Portal and enroll their devices.    

## Enroll devices  

Configure the enrollment methods and experience for company-owned and personal macOS devices. This step ensures that devices receive Intune policies and configurations after they enroll. Intune supports Bring Your Own Device (BYOD) enrollment, Apple Automated Device Enrollment, and direct enrollment for corporate devices. For information about each enrollment method and how to choose one that's right for your organization, see the [macOS device enrollment guide for Microsoft Intune](deployment-guide-enrollment-macos.md). 
 

| Task | Detail | 
| ---- | ------ | 
|[Set up enrollment for user-owned (BYOD) devices](../enrollment/macos-enroll.md)| Complete the prerequisites in this article to enable enrollment for user-owned devices. You'll also find enrollment resources and links to share with device users so that they're supported throughout the enrollment experience. This enrollment method is for organizations that have *Bring Your Own Device* (BYOD) policies. BYOD lets people use their personal devices for work-related things. | 
|[Set up Apple Automated Device Enrollment (ADE)](../enrollment/device-enrollment-program-enroll-macos.md)|Set up an out-of-the-box enrollment experience that automates enrollment on corporate-owned devices purchased through Apple School Manager or Apple Business Manager. This method is ideal for organizations that have a large number of devices to enroll, because it eliminates the need to touch and configure each device individually.  |  
|[Set up direct enrollment for corporate devices](../enrollment/device-enrollment-direct-enroll-macos.md)| Set up an enrollment experience for corporate-owned devices that are unaffiliated with a single user, like devices used in a shared space or retail setting. Direct enrollment doesn't wipe the device so it's ideal to use when devices don't need access to local user data. You'll need to transfer the enrollment profile to the Mac directly, which requires a USB connection to a Mac computer running Apple Configurator.|  
|[Add a device enrollment manager](../enrollment/device-enrollment-manager-enroll.md)| People designated as device enrollment managers (DEM) can enroll up to 1,000 corporate-owned mobile devices at a time. DEM accounts are useful in organizations that enroll and prepare devices before handing them out to users. | 
| [Identify devices as corporate-owned](../enrollment/corporate-identifiers-add.md)| You can assign corporate-owned status to devices to enable more management and identification capabilities in Intune. Corporate-owned status cannot be assigned to devices enrolled through Apple Business Manager. | 
|[Change device ownership](../enrollment/corporate-identifiers-add.md#change-device-ownership)|After a device has been enrolled, you can change its ownership label in Intune to corporate-owned or personal-owned. This adjustment changes the way you can manage the device.|  
|[Troubleshoot enrollment problems](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune)|Troubleshoot and find resolutions to problems that occur during enrollment. |

## Create compliance rules  

Create compliance policies to define the rules and conditions that users and devices must meet to access your protected resources. This is how you ensure that devices accessing your data meet your standards. Intune marks devices that fall short of your requirements as *non-compliant* and takes action (such as sending the user a notification, restricting access, or wiping the device) according to your configurations.  

If you create a Conditional Access policy, it can work alongside your device compliance results to block access to resources from noncompliant devices. For a detailed explanation about compliance policies and how to get started, see [Use compliance policies to set rules for devices you manage with Intune](../protect/device-compliance-get-started.md).  

| Task | Detail | 
| ---- | ------ | 
| [Create a compliance policy](../protect/create-compliance-policy.md)|Get step-by-step guidance on how to create and assign a compliance policy to user and device groups.   |       
| [Add actions for noncompliance](../protect/actions-for-noncompliance.md) |Choose what happens when devices no longer meet the conditions of your compliance policy. You can add actions for noncompliance when you configure a device compliance policy, or later by editing the policy.    |  
| Create [a device-based](../protect/create-conditional-access-intune.md) or [app-based](../protect/app-based-conditional-access-intune-create.md) Conditional Access policy| Specify the app or services you want to protect and define the conditions for access. |  
|[Block access to apps that don't use modern authentication](../protect/app-modern-authentication-block.md)  | Create an app-based Conditional Access policy to block apps that use authentication methods other than OAuth2; for example, those apps that use basic and form-based authentication. Before you block access, however, sign in to Azure AD and review the [authentication methods activity report](/azure/active-directory/authentication/howto-authentication-methods-activity) to see if users are using basic authentication to access essential things you forgot about or are unaware of.  For example, things like meeting room calendar kiosks use basic authentication.  |  


## Configure device settings     

Use Microsoft Intune to enable or disable settings and features on macOS devices being used for work.  To configure and enforce these settings, create a device configuration profile and then assign the profile to groups in your organization. 

| Task | Detail | 
| ---- | ------ | 
|[Create a device profile in Microsoft Intune](../configuration/device-profile-create.md) |Learn about the different types of device profiles you can create for your organization.|  
|[Configure device features](../configuration/device-features-configure.md)|Configure common macOS features and functionality. For a description of the settings in this area, see the [device features reference](../configuration/macos-device-features-settings.md).|
|[Configure Wi-Fi profile](../configuration/wi-fi-settings-configure.md)|This profile enables people to find and connect to your organization's Wi-Fi network. For a description of the settings in this area, see the [Wi-Fi settings reference](../configuration/wi-fi-settings-macos.md).|
|[Configure wired network profile](../configuration/wired-networks-configure.md)|This profile enables people on desktop computers to connect to your organization's wired network. For a description of the settings in this area, see the [wired network reference](../configuration/wi-fi-settings-macos.md).|
|[Configure VPN profile](../configuration/vpn-settings-configure.md)|Set up a secure VPN option, such as Microsoft Tunnel, for people connecting to your organization's network.  For a description of the settings in this area, see the [VPN settings reference](../configuration/vpn-settings-macos.md). |  
|[Restrict device features](../configuration/device-restrictions-configure.md)|Protect users from unauthorized access and distractions by limiting the device features they can use at work or school. For a description of the settings in this area, see the [device restrictions reference](../configuration/device-restrictions-macos.md).|
|[Configure custom profile](../configuration/custom-settings-macos.md)|Add and assign device settings and features that aren't built into Intune.|
|[Add and manage macOS extensions](../configuration/kernel-extensions-overview-macos.md)|Add kernel extensions and system extensions, which enable users to install app extensions that extend the native capabilities of the operating system. For a description of the settings in this area, see the [macOS extensions reference](../configuration/kernel-extensions-settings-macos.md).|  
|[Customize branding and enrollment experience](../apps/company-portal-app.md)|Customize the Intune Company Portal and Microsoft Intune app experience with your organization's own words, branding, screen preferences, and contact information.|

## Configure endpoint security  

Use the Intune endpoint security features to configure device security and to manage security tasks for devices at risk. 

| Task | Detail | 
| ---- | ------ | 
|[Manage devices with endpoint security features](../protect/endpoint-security-manage-devices.md)|Use the endpoint security settings in Intune to effectively manage device security and remediate issues for devices.|
|[Use Conditional Access to limit access to Microsoft Tunnel](../protect/microsoft-tunnel-conditional-access.md)|Use Conditional Access policies to gate device access to your Microsoft Tunnel VPN gateway. | 
|[Add endpoint protection settings](../protect/microsoft-tunnel-conditional-access.md)| Configure common endpoint protection security features, including Firewall, Gatekeeper, and FileVault. For a description of the settings in this area, see the [endpoint protection settings reference](../protect/endpoint-protection-macos.md).   | 


## Set up secure authentication methods   
Set up authentication methods in Intune to ensure that only authorized people access your internal resources. Intune supports multi-factor authentication, certificates, and derived credentials. Certificates can also be used for signing and encryption of email using S/MIME.   

| Task | Detail | 
| ---- | ------ | 
|[Require multi-factor authentication (MFA)](../enrollment/multi-factor-authentication.md)| Require people to supply two forms of credentials at time of enrollment.| 
|[Create a trusted certificate profile](../protect/certificates-trusted-root.md)|Create and deploy a trusted certificate profile before you create a SCEP, PKCS, or PKCS imported certificate profile. The trusted certificate profile deploys the trusted root certificate to devices and users using SCEP, PKCS, and PKCS imported certificates. |
|[Use SCEP certificates with Intune ](../protect/certificates-scep-configure.md)| Learn what’s needed to use SCEP certificates with Intune, and configure the required infrastructure. After you do that, you can [create a SCEP certificate profile](../protect/certificates-profile-scep.md) or [set up a third-party certification authority with SCEP](../protect/certificate-authority-add-scep-overview.md).|  
|[Use PKCS certificates with Intune](../protect/certificates-pfx-configure.md)|Configure required infrastructure (such as on-premises certificate connectors), export a PKCS certificate, and add the certificate to an Intune device configuration profile. | 
|[Use imported PKCS certificates with Intune](../protect/certificates-imported-pfx-configure.md)|Set up imported PKCS certificates, which enable you to [set up and use S/MIME to encrypt email](../protect/certificates-s-mime-encryption-sign.md). 



## Deploy apps  

As you set up apps and app policies, think about your organization's requirements, such as the platforms you'll support, the tasks people do, the type of apps they need to complete those tasks, and who needs them. You can use Intune to manage the whole device (including apps) or use Intune to manage apps only.  

| Task | Detail | 
| ---- | ------ | 
|[Add Intune Company Portal app ](../apps/apps-company-portal-macos.md)|Learn how to get Company Portal on devices or instruct users how to do it on their own. | 
|[Add Microsoft Edge](../apps/apps-edge-macos.md) | Add and assign Microsoft Edge in Intune. | 
|[Add Microsoft 365 ](../apps/apps-add-office365-macos.md)| Add and assign Microsoft 365 apps in Intune. | 
|[Add line-of-business apps ](../apps/lob-apps-macos.md)| Add and assign macOS line-of-business (LOB) apps in Intune.| 
|[Assign apps to groups ](../apps/apps-deploy.md)|After you add apps to Intune, assign them to users and devices.|
|[Include and exclude app assignments ](../apps/apps-inc-exl-assignments.md)|Control access and availability to an app by including and excluding selected groups from assignment.| 
|[Use shell scripts on macOS devices](../apps/macos-shell-scripts.md)|Use shell scripts to extend device management capabilities in Intune beyond what's supported by the macOS operating system.| 


## Run remote actions  

After devices are set up, you can use remote actions in Intune to manage and troubleshoot macOS devices from a distance. The following articles introduce you to the remote actions in Intune. If an action is absent or disabled in the portal, then it isn't supported on macOS.  

| Task | Detail | 
| ---- | ------ | 
|[Take remote action on devices](../remote-actions/device-management.md)|Learn how to drill down and remotely manage and troubleshoot individual devices in Intune. This article lists all remote actions available in Intune and links to those procedures.   |
|[Use TeamViewer to remotely administer Intune devices](../remote-actions/teamviewer-support.md)|Configure TeamViewer within Intune, and learn how to remotely administer a device.  |  
|[Use security tasks to view threats and vulnerabilities](../protect/atp-manage-vulnerabilities.md)|Integrate Intune with Microsoft Defender for Endpoint to take advantage of Defender for Endpoint's threat and vulnerability management and use Intune to remediate endpoint weakness identified by Defender's vulnerability management capability.|  

## Next steps  

* Check out [Walk through Intune admin center](tutorial-walkthrough-endpoint-manager.md) for a tutorial about how to navigate and use Intune. Tutorials are 100 – 200 level content for people new to Intune or a specific scenario.   

* For tutorials about app deployment, see the following Microsoft Tech Community blogs written by the Intune Support Team:  

    *  [Deploying macOS apps with the Intune scripting agent](https://techcommunity.microsoft.com/t5/intune-customer-success/deploying-macos-apps-with-the-intune-scripting-agent/ba-p/2298072).  

    * [Deploying Microsoft 365 Apps for Mac with Microsoft Intune - A Deep Dive](https://techcommunity.microsoft.com/t5/intune-customer-success/deploying-microsoft-365-apps-for-mac-with-microsoft-endpoint/ba-p/2243040)


* For other versions of this guide, see:   

    *  [Deployment guide: Manage Android devices in Microsoft Intune](deployment-guide-platform-android.md)  
    *  [Deployment guide: Manage iOS devices in Microsoft Intune](deployment-guide-platform-ios-ipados.md)  
  


