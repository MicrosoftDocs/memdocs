---
# required metadata

title: Deployment guide to manage iOS/iPadOS devices in Microsoft Intune
description: Learn the recommended processes to manage iOS/iPadOS devices in Microsoft Intune.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/11/2021
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

# Deployment guide: Manage iOS/iPadOS devices in Microsoft Intune

Intune supports mobile device management (MDM) of iPads and iPhones to give users secure access to work email, data, and apps. This guide provides iOS-specific guidance to help you set up enrollment and deploy apps and policies to users and devices.      



## Prerequisites  

Before you begin, complete these prerequisites to enable iOS/iPadOS device management in Intune. For more detailed information about how to set up, onboard, or move to Intune, see the [Intune setup deployment guide](deployment-guide-intune-setup.md).          

* [Add users](users-add.md) and [groups](groups-add.md)
* [Assign licenses to users](licenses-assign.md) 
* [Set mobile device management authority](mdm-authority-set.md) 
* [Have Global Administrator or Intune administrator Azure Active Directory permissions](role-based-access-control.md)  
* [Set up Apple MDM push (APNs) certificate](../enrollment/apple-mdm-push-certificate-get.md)  

## Plan for your deployment  

The [Microsoft Intune planning guide](intune-planning-guide.md) provides guidance and advice to help you determine goals, use-case scenarios, and requirements. It also describes how to create plans for rollout, communication, support, testing, and validation.  

## Leverage the iOS/iPadOS security configuration framework 

The iOS/iPadOS security configuration framework is a series of recommendations for device compliance and configuration policy settings. These recommendations help you tailor your organization's mobile device security protection to your specific needs.

Microsoft Intune uses a taxonomy for this framework that's similar to the one used for security configurations in Windows 10. It applies to both personally owned and supervised devices, and includes the recommended settings for basic, enhanced, and high-level security. Each security level builds off the previous one and offers more protection than the last. 

The security levels for personally owned devices are:  

* Basic security (Level 1) – This configuration is recommended as the minimum security configuration for personal devices from which users access work or school data. This configuration enforces password policies, defines device lock characteristics, and disables certain device functions (such as untrusted certificates). 

* Enhanced security (Level 2) – This configuration is recommended for devices from which users access sensitive or confidential information. This configuration enacts data sharing controls. It's applicable to most mobile users accessing work or school data on a device.  

* High security (Level 3) – This configuration is recommended for devices used by specific users or groups who are uniquely high risk. For example, users who handle highly sensitive data where unauthorized disclosure causes considerable material loss to the organization. This configuration enacts stronger password policies than the previous levels, disables more device functions, and enforces additional data transfer restrictions. 

The security levels for supervised devices are:  

* Basic security (Level 1) – This configuration is recommended as the minimum security configuration for supervised devices where users access work or school data. This level is achieved by enforcing password policies, defining device lock characteristics, and disabling certain device functions (such as untrusted certificates). 

* Enhanced security (Level 2) – This configuration is recommended for devices from which users access sensitive or confidential information. This configuration enacts data sharing controls and blocks access to USB devices. It's applicable to most mobile users accessing work or school data on a device. 

* High security (Level 3) – This configuration is recommended for devices used by specific users or groups who are uniquely high risk.  For example, users who handle highly sensitive data where unauthorized disclosure causes considerable material loss to the organization. This configuration enacts stronger password policies, disables more device functions, enforces additional data transfer restrictions, and requires apps to be installed through the Apple volume purchase program (VPP). 

For more information about the security framework, including specific recommendations and the minimum apps that must be protected, see the articles listed in the following table. 

| Task | Detail | 
| ---- | ------ | 
| [Learn about the iOS/iPadOS framework deployment methodology](../enrollment/ios-ipados-framework-deployment-methodology.md)|Learn about the Microsoft-recommended methodology for deploying the security configuration framework. |       
| [Disallow personal accounts for Microsoft apps on iOS/iPadOS devices](../enrollment/ios-ipados-app-configuration-policies.md) |Configure an app policy that prevents users from signing into a personal account on a work or school device. |  
| [Configure device compliance security settings](../enrollment/ios-ipados-device-compliance-security-configurations.md)|Apply these security settings to configure a basic or high security level on personally owned and corporate owned devices. |  
|[Configure device security settings for personal devices ](../enrollment/ios-ipados-personal-device-security-configurations.md)  | Apply these settings to configure a basic, enhanced, or high security level on personally owned devices. | 
|[Configure device security settings for supervised devices ](../enrollment/ios-ipados-supervised-device-security-configurations.md)  | Apply these settings to configure a basic, enhanced, or high security level on supervised devices. | 


## Create compliance rules  

Use compliance policies to define the rules and conditions that users and devices should meet to access your protected resources. If you use Conditional Access, your Conditional Access policies can use your device compliance results to block access to resources from noncompliant devices. For a detailed explanation about compliance policies and how to get started, see [Use compliance policies to set rules for devices you manage with Intune](../protect/device-compliance-get-started.md).  

| Task | Detail | 
| ---- | ------ | 
| [Create a compliance policy](../protect/create-compliance-policy.md)|Get step-by-step guidance on how to create and assign a compliance policy to user and device groups.   |       
| [Add actions for noncompliance](../protect/actions-for-noncompliance.md) |Choose what happens when devices no longer meet the conditions of your compliance policy. You can add actions for noncompliance when you configure a device compliance policy, or later by editing the policy.    |  
| Create [a device-based](../protect/create-conditional-access-intune.md) or [app-based](../protect/app-based-conditional-access-intune-create.md) Conditional Access policy| Specify the app or services you want to protect and define the conditions for access. |  
|[Block access to apps that don't use modern authentication](../protect/app-modern-authentication-block.md)  | Create an app-based Conditional Access policy to block apps that use authentication methods other than OAuth2; for example, those apps that use basic and form-based authentication. Before you block access, however, sign in to Azure AD and review the [authentication methods activity report](/azure/active-directory/authentication/howto-authentication-methods-activity) to see if users are using basic authentication to access essential things you forgot about or are unaware of. For example, things like meeting room calendar kiosks use basic authentication.  |  

## Configure endpoint security  

Use the Intune endpoint security features to configure device security and to manage security tasks for devices at risk. 

| Task | Detail | 
| ---- | ------ | 
|[Manage devices with endpoint security features](../protect/endpoint-security-manage-devices.md)|Use the endpoint security settings in Intune to effectively manage device security and remediate issues for devices.|
|[Enable mobile threat defense (MTD) connector for unenrolled devices](../protect/mtd-enable-unenrolled-devices.md)|Enable the MTD connection in Intune so that MTD partner apps can work with Intune and your policies. If you're not using Microsoft Defender for Endpoint, consider enabling the connector so that you can use another mobile threat defense solution.  |  
|[Create MTD app protection policy](../protect/mtd-app-protection-policy.md)|Create an Intune app protection policy that assesses risk and limits a device's corporate access based on the threat level.|
|[Add MTD apps to unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md)|Make MTD apps available to people in your organization and configure Microsoft Authenticator for iOS/iPadOS. |  
|[Use Conditional Access to limit access to Microsoft Tunnel](../protect/microsoft-tunnel-conditional-access.md)|Use Conditional Access policies to gate device access to your Microsoft Tunnel VPN gateway. | 

## Configure device settings     

Use Microsoft Intune to enable or disable settings and features on iOS/iPadOS devices. To configure and enforce these settings, create a device configuration profile and then assign the profile to groups in your organization. Devices receive the profile once they enroll.  

| Task | Detail | 
| ---- | ------ | 
|[Create a device profile in Microsoft Intune](../configuration/device-profile-create.md) |Learn about the different types of device profiles you can create for your organization.|  
|[Configure device features](../configuration/device-features-configure.md)|Configure common iOS/iPadOS features and functionality for a work or school context. For a description of the settings in this area, see the [device features reference](../configuration/ios-device-features-settings.md).|
|[Configure Wi-Fi profile](../configuration/wi-fi-settings-configure.md)|This profile enables people to find and connect to your organization's Wi-Fi network. For a description of the settings in this area, see the [Wi-Fi settings reference](../configuration/wi-fi-settings-ios.md).|
|[Configure VPN profile](../configuration/vpn-settings-configure.md)|Set up a secure VPN option, such as Microsoft Tunnel, for people connecting to your organization's network. You can also [create a per-app VPN policy](../configuration/vpn-setting-configure-per-app.md) to require users to sign in to certain apps through a VPN connection. For a description of the settings in this area, see the [VPN settings reference](../configuration/vpn-settings-ios.md). |  
|[Configure email profile](../configuration/email-settings-configure.md)|Configure email settings so that people can connect to a mail server and access their work or school email. For a description of the settings in this area, see the [email settings reference](../configuration/email-settings-ios.md).|  
|[Restrict device features](../configuration/device-restrictions-configure.md)|Protect users from unauthorized access and distractions by limiting the device features they can use at work or school. For a description of the settings in this area, see the [device restrictions reference](../configuration/device-restrictions-ios.md).|
|[Configure custom profile](../configuration/custom-settings-ios.md)|Add and assign device settings and features that aren't built into Intune.|
|[Customize branding and enrollment experience](../apps/company-portal-app.md)|Customize the Intune Company Portal and Microsoft Intune app experience with your organization's own words, branding, screen preferences, and contact information.|
|[Configure software update policy](../protect/software-updates-ios.md)| Schedule automatic OS updates and installations for supervised iOS/iPadOS devices.|  


## Set up secure authentication methods   
Set up authentication methods in Intune to ensure that only authorized people access your internal resources. Intune supports multi-factor authentication, certificates, and derived credentials. Certificates can also be used for signing and encryption of email using S/MIME.   

| Task | Detail | 
| ---- | ------ | 
|[Require multi-factor authentication (MFA)](../enrollment/multi-factor-authentication.md)| Require people to supply two forms of credentials at time of enrollment.| 
|[Create a trusted certificate profile](../protect/certificates-trusted-root.md)|Create and deploy a trusted certificate profile before you create a SCEP, PKCS, or PKCS imported certificate profile. The trusted certificate profile deploys the trusted root certificate to devices and users using SCEP, PKCS, and PKCS imported certificates. |
|[Use SCEP certificates with Intune ](../protect/certificates-scep-configure.md)| Learn what’s needed to use SCEP certificates with Intune, and configure the required infrastructure. After you do that, you can [create a SCEP certificate profile](../protect/certificates-profile-scep.md) or [set up a third-party certification authority with SCEP](../protect/certificate-authority-add-scep-overview.md).|  
|[Use PKCS certificates with Intune](../protect/certificates-pfx-configure.md)|Configure required infrastructure (such as on-premises certificate connectors), export a PKCS certificate, and add the certificate to an Intune device configuration profile. | 
|[Use imported PKCS certificates with Intune](../protect/certificates-imported-pfx-configure.md)|Set up imported PKCS certificates, which enable you to [set up and use S/MIME to encrypt email](../protect/certificates-s-mime-encryption-sign.md). 
|[Set up a derived credentials issuer](../protect/derived-credentials.md)| Provision iOS/iPadOS devices with certificates that are derived from user smart cards.  




## Deploy apps  

As you set up apps and app policies, think about your organization's requirements, such as the platforms you'll support, the tasks people need to do, the type of apps they need to complete those tasks, and finally, the groups who need those apps. You can use Intune to manage the whole device (including apps) or use Intune to manage the apps only.   

| Task | Detail | 
| ---- | ------ | 
|[Add store apps](../apps/store-apps-ios.md) | Add iOS/iPadOS apps from the App Store to Intune, and assign to groups.  | 
|[Add web apps](../apps/web-app.md) | Add web apps to Intune and assign to groups. | 
|[Add built-in apps](../apps/apps-add-built-in.md) | Add built-in apps to Intune and assign to groups. | 
|[Add line-of-business apps ](../apps/lob-apps-ios.md)|Add iOS/iPadOS line-of-business (LOB) apps to Intune, and assign to groups.| 
|[Assign apps to groups ](../apps/apps-deploy.md)|Assign apps to users and devices.| 
|[Include and exclude app assignments ](../apps/apps-inc-exl-assignments.md)|Control access and availability to an app by including and excluding selected groups from assignment.| 
|[Manage iOS/iPadOS apps purchased through Apple Business Manager](../apps/vpp-apps-ios.md)|Synchronize, manage, and assign apps purchased through Apple Business Manager.| 
|[Manage iOS/iPadOS eBooks purchased through Apple Business Manager ](../apps/vpp-ebooks-ios.md)| Synchronize, manage, and assign books purchased through Apple Business Manager. | 
| [Create an iOS/iPadOS app protection policy](../apps/app-protection-policies.md) | Keep your organization's data contained within managed apps like Outlook and Word. See [iOS/iPadOS app protection policy settings](../apps/app-protection-policy-settings-ios.md) for details about each setting.|  
| [Create an app provisioning profile](../apps/app-provisioning-profile-ios.md) |Prevent app certificates from expiring by proactively assigning new provisioning profiles to devices that have apps nearing expiry.| 
|[Create an app configuration policy](../apps/app-configuration-policies-use-ios.md)  | Apply custom configuration settings to iOS/iPadOS apps on enrolled devices. You can also apply these types of policies [to managed apps without device enrollment](../apps/app-configuration-policies-managed-app.md). | 
|[Configure Microsoft Edge](../apps/manage-microsoft-edge.md) | Use Intune app protection and configuration policies with Edge for iOS/iPadOS to ensure corporate websites are accessed with safeguards in place. | 
| [Configure Microsoft Office apps](../apps/manage-microsoft-office.md)| Use Intune app protection and configuration policies with Office apps to ensure that corporate files are accessed with safeguards in place. | 
|[Configure Microsoft Teams](../apps/manage-microsoft-teams.md) |Use Intune app protection and configuration policies with Teams to ensure that collaborative team experiences are accessed with safeguards in place. | 
|[Configure Microsoft Outlook](../apps/app-configuration-policies-outlook.md) | Use Intune app protection and configuration policies with Outlook to ensure corporate email and calendars are accessed with safeguards in place.   

## Enroll devices  

 Enrolling devices allows them to receive the policies you create, so have your Azure AD user groups and device groups ready. 

For information about each enrollment method and how to choose one that's right for your organization, see the [iOS/iPadOS device enrollment guide for Microsoft Intune](deployment-guide-enrollment-ios-ipados.md). 

| Task | Detail | 
| ---- | ------ | 
|[Set up Apple Automated Device Enrollment (ADE) in Intune](../enrollment/device-enrollment-program-enroll-ios.md)|Set up an out-of-the-box enrollment experience for corporate-owned devices purchased through Apple School Manager or Apple Business Manager. For a detailed walkthrough of this process, see [Tutorial: Use Apple's Corporate Device Enrollment features in Apple Business Manager (ABM) to enroll iOS/iPadOS devices](..//enrollment/tutorial-use-device-enrollment-program-enroll-ios.md)|  
|[Set up Apple School Manager in Intune](../enrollment/apple-school-manager-set-up-ios.md)|Set up Intune to enroll devices you purchased through the Apple School Manager program.|  
|[Set up device enrollment with Apple Configurator ](../enrollment/apple-configurator-enroll-ios.md)| Create an Apple Configurator profile to enroll corporate-owned devices (with no user affinity) via direct enrollment; or to enroll wiped or new devices (with user affinity) via Setup Assistant. You'll need to export the Apple Configurator profile from Intune, which requires a USB connection to a Mac computer running Apple Configurator.|  
| [Identify devices as corporate-owned](../enrollment/corporate-identifiers-add.md)| Assign corporate-owned status to devices to enable more management and identification capabilities in Intune. Corporate-owned status cannot be assigned to devices enrolled through Apple Business Manager. | 
|[Set up Apple User Enrollment (in preview)](../enrollment/ios-user-enrollment.md)|Create a user enrollment profile to deploy the Apple user enrollment experience to devices using a managed Apple ID. Support for this feature is currently in preview. |   
|[Set up shared iPad devices](../enrollment/device-enrollment-shared-ipad.md)|Configure devices so that they can be used by more than one person (the type of setup you'd see in a library or educational environment).| 
|[Backup and restore devices](../enrollment/backup-restore-ios.md)|Back up and restore a device to prepare it for enrollment or migration in Intune, such as during Automated Device Enrollment setup.   |
|[Change device ownership](../enrollment/corporate-identifiers-add.md#change-device-ownership)|After a device has been enrolled, you can change its ownership label in Intune to corporate-owned or personal-owned. This adjustment changes the way you can manage the device.|  
|[Troubleshoot enrollment problems](/troubleshoot/mem/intune/troubleshoot-ios-enrollment-errors)|Troubleshoot and find resolutions to problems that occur during enrollment. |


## Run remote actions  

After devices are set up, you can use remote actions in Intune to manage and troubleshoot devices from a distance. Availability varies by device platform. If an action is absent or disabled in the portal, then it isn't supported on the device.  

| Task | Detail | 
| ---- | ------ | 
|[Take remote action on devices](../remote-actions/device-management.md)|Learn how to drill down and remotely manage and troubleshoot individual devices in Intune. This article lists all remote actions available in Intune and links to those procedures.   |
|[Use TeamViewer to remotely administer Intune devices](../remote-actions/teamviewer-support.md)|Configure TeamViewer within Intune, and learn how to remotely administer a device.  |  
|[Remediate vulnerabilities identified by Microsoft Defender for Endpoint](../protect/atp-manage-vulnerabilities.md)|Integrate Intune with Microsoft Defender for Endpoint to take advantage of Defender for Endpoint's threat and vulnerability management and use Intune to remediate endpoint weakness identified by Defender's vulnerability management capability.|  

## Next steps  
Check out these enrollment tutorials to learn how to do some of the top tasks in Intune. Tutorials are 100 – 200 level content for people new to Intune or a specific scenario.    

* [Walk through Intune in Microsoft Endpoint Manager](tutorial-walkthrough-endpoint-manager.md) 
* [Use Apple corporate device enrollment features in Apple Business Manager (ABM) to enroll iOS/iPadOS devices in Intune](../enrollment/tutorial-use-device-enrollment-program-enroll-ios.md)
* [Protect Exchange Online email on managed devices](../protect/tutorial-protect-email-on-enrolled-devices.md)
* [Protect Exchange Online email on unmanaged devices](../protect/tutorial-protect-email-on-unmanaged-devices.md)
* [Configure Slack to use Intune for EMM and app configuration](../apps/tutorial-configure-slack-enterprise-grid.md) 

For the Android version of this guide, see [Deployment guide: Manage Android devices in Microsoft Intune](deployment-guide-platform-android.md).