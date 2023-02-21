---
# required metadata

title: Deployment guide to manage Android devices in Microsoft Intune
description: Learn the recommended processes to manage Android devices in Microsoft Intune.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 09/16/2021
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

# Deployment guide: Manage Android devices in Microsoft Intune

Intune supports the mobile device management (MDM) of Android devices to give people secure access to work email, data, and apps. This guide provides Android-specific resources to help you set up enrollment in Intune and deploy apps and policies to users and devices. 

## Prerequisites  

Before you begin, complete these prerequisites to enable Android device management in Intune. For more detailed information about how to set up, onboard, or move to Intune, see the [Intune setup deployment guide](deployment-guide-intune-setup.md).          

* [Add users](users-add.md) and [groups](groups-add.md)
* [Assign licenses to users](licenses-assign.md) 
* [Set mobile device management authority](mdm-authority-set.md) 
* [Have Global Administrator or Intune administrator Azure Active Directory permissions](role-based-access-control.md)  
 

## Plan for your deployment  

Use the [Microsoft Intune planning guide](intune-planning-guide.md) for help with planning, designing, and implementing Microsoft Intune in your organization. The guide provides information to help you:

* Determine goals, use-case scenarios, and requirements.
* Create rollout and communication plans.
* Create support, testing, and validation plans.  

## Leverage the Android Enterprise security configuration framework  

The Android Enterprise security configuration framework is a series of recommendations for device compliance and configuration policy settings. These recommendations can help you tailor your organization's mobile device security protection to your specific needs. You can apply them to devices that are fully managed or personally owned with work profiles. 

The taxonomy for this framework is similar to the one used for security configurations in iOS. It includes recommended settings for basic, enhanced, and high-level security. Each security level builds off the previous one to offer more protection than the last. 

The security levels for personally owned devices with work profile are:  

* Basic security (Level 1) – This configuration is recommended as the minimum security configuration for personal devices where users access work or school data. This configuration introduces password requirements, separates work and personal data, and validates Android device attestation. 

* High security (Level 3) – This configuration is recommended for devices used by specific users or groups who are uniquely high risk. For example, users who handle highly sensitive data where unauthorized disclosure causes considerable material loss to the organization. This configuration introduces mobile threat defense or Microsoft Defender Advanced Threat Protection (ATP), enforces stricter Android version requirements, enforces stronger password policies, and further restricts work and personal separation. 

The security levels for fully managed devices are:  

* Basic security (Level 1) – This configuration is recommended as the minimum security configuration for supervised devices where users access work or school data. It enforces password requirements, minimum Android version, and certain device restrictions.

* Enhanced security (Level 2) – This configuration is recommended for devices from which users access sensitive or confidential information. It enforces stronger password policies and disables user and account capabilities. It's applicable to most mobile users accessing work or school data on a device. 

* High security (Level 3) – This configuration is recommended for devices used by specific users or groups who are uniquely high risk.  For example, users who handle highly sensitive data where unauthorized disclosure causes considerable material loss to the organization. This configuration enforces stricter Android version requirements and other device restrictions, and introduces mobile threat defense or Microsoft Defender ATP.  

For more information about the security framework, see the articles listed in the following table. 

| Task | Detail | 
| ---- | ------ | 
| [Learn about the Android Enterprise framework deployment methodology](../enrollment/framework-deployment-methodology.md)|Learn about the Microsoft-recommended methodology for deploying the security configuration framework. |      
| [Configure device enrollment restrictions for personally owned devices](../enrollment/android-work-profile-security-settings.md)|Apply these restrictions to configure a basic or high security level for devices that are personally owned with work profile. | 
| [Disallow personal accounts on Android Enterprise devices](../enrollment/android-app-configuration-policies.md) |Prevent people on work or school devices from signing into Microsoft apps with a personal account. |  
|[Configure security settings for personally owned devices ](../enrollment/android-work-profile-security-settings.md)  | Apply these settings to configure a basic or high security level on devices that are personally owned with work profile. | 
|[Configure security settings for fully managed devices ](../enrollment/android-fully-managed-security-settings.md)  | Apply these settings to configure a basic, enhanced, or high security level on corporate-owned, fully managed devices. | 

## Create compliance rules  

Use compliance policies to define the rules and conditions that users and devices should meet to access your organization's protected resources. You can also create Conditional Access policies, which work alongside your device compliance results to block access to resources from noncompliant devices. For a detailed explanation about compliance policies and how to get started, see [Use compliance policies to set rules for devices you manage with Intune](../protect/device-compliance-get-started.md). 

The following tasks apply to both Android Enterprise and Android device administrator platforms.

| Task | Detail | 
| ---- | ------ | 
| [Create a compliance policy](../protect/create-compliance-policy.md)|Get step-by-step guidance on how to create and assign a compliance policy to user and device groups.   |       
| [Add actions for noncompliance](../protect/actions-for-noncompliance.md) |Choose what happens when devices no longer meet the conditions of your compliance policy. You can add actions for noncompliance when you configure a device compliance policy, or later by editing the policy. |  
| Create [a device-based](../protect/create-conditional-access-intune.md) or [app-based](../protect/app-based-conditional-access-intune-create.md) Conditional Access policy.|Specify the app or services you want to protect and define the conditions for access.
|[Block access to apps that don't use modern authentication](../protect/app-modern-authentication-block.md)  | Create an app-based Conditional Access policy to block apps that use authentication methods other than OAuth2.  For example, you can block apps that use basic and form-based authentication. Before you block any access, sign in to Azure AD and review the [authentication methods activity report](/azure/active-directory/authentication/howto-authentication-methods-activity) to see if users are using basic authentication to access essential things (like meeting room calendar kiosks) you forgot about or are unaware of. |  

 
## Configure endpoint security  
Use the Intune endpoint security features to configure device security and to manage security tasks for devices at risk.  

The following tasks apply to both Android Enterprise and Android device administrator platforms. 

| Task | Detail | 
| ---- | ------ | 
|[Manage devices with endpoint security features](../protect/endpoint-security-manage-devices.md)|Use the **Endpoint security** settings in Intune to effectively manage device security and remediate issues for devices.|
|[Enable the mobile threat defense (MTD) connector for enrolled devices](../protect/mtd-connector-enable.md)|Enable the MTD connection in Intune so that MTD partner apps can work with Intune and your MTD device compliance policies. If you're not using Microsoft Defender for Endpoint, consider enabling the connector so that you can use another mobile threat defense solution. You can also [enable the MTD connector for devices not enrolled in Intune](../protect/mtd-enable-unenrolled-devices.md).| 
|[Create MTD app protection policy](../protect/mtd-app-protection-policy.md)|Create an Intune app protection policy that assesses risks and limits a device's access to work or school apps.| 
|[Create MTD device compliance policy](../protect/mtd-device-compliance-policy-create.md)|Create an Intune app protection policy that assesses risk and limits a device's corporate access based on the threat level.|
|[Add and assign MTD apps](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)|Add and deploy MTD apps in Intune. These apps work with your device compliance and app protection policies to identify and help remediate device threats. You can also [assign MTD apps to devices not enrolled in Intune](../protect/mtd-add-apps-unenrolled-devices.md). |   

## Configure device settings     

Use Microsoft Intune to enable or disable settings and features on devices. To configure and enforce these settings, create a device profile and then assign the profile to groups in your organization. Devices receive the profile once they enroll.  

| Task | Detail | Platform | 
| ---- | ------ | ------ | 
| [Create a device profile in Microsoft Intune](../configuration/device-profile-create.md) | Learn about the different types of device profiles you can create for your organization.| Android Enterprise, Android device administrator  |
|[Configure Wi-Fi profile](../configuration/wi-fi-settings-configure.md)|This profile enables people to find and connect to your organization's Wi-Fi network. For a description of the settings in this area, see the Wi-Fi settings reference for [Android Enterprise Wi-Fi settings](../configuration/wi-fi-settings-android-enterprise.md) or [Android device administrator Wi-Fi settings](../configuration/wi-fi-settings-android.md).|Android Enterprise, Android device administrator |
|[Configure VPN profile](../configuration/vpn-settings-configure.md)|Set up a secure VPN option, such as Microsoft Tunnel, for people connecting to your organization's network. For a description of the settings in this area, see the VPN settings reference for [Android Enterprise VPN settings](../configuration/vpn-settings-android-enterprise.md) or [Android device administrator VPN settings](../configuration/vpn-settings-android.md). | Android Enterprise, Android device administrator  |
|[Configure email profile](../configuration/email-settings-configure.md)|Configure email settings so that people can connect to a mail server and access their work or school email. For a description of the settings in this area, see [Android Enterprise email settings](../configuration/email-settings-android-enterprise.md) or [Android device administrator email settings](../configuration/email-settings-android.md).| Android Enterprise, Android device administrator  |
|[Restrict device features](../configuration/device-restrictions-configure.md)|Protect users from unauthorized access and distractions by limiting the device features they can use at work or school. For a description of the settings in this area, see [Android Enterprise device settings](../configuration/device-restrictions-android-for-work.md) or [Android device administrator device settings](../configuration/device-restrictions-android.md).|Android Enterprise, Android device administrator |
|[Configure custom settings for Android device administrator](../configuration/custom-settings-android.md)|Add or create custom settings that aren't built in to Intune, such as a per-app VPN profile and web protection with Microsoft Defender for Endpoint.|Android device administrator |
|[Configure Samsung Knox apps](../configuration/samsung-knox-apps-allow-block.md)|Create a custom profile to allow and block apps for Samsung Knox Standard devices.| Android device administrator|
|[Create custom profile for Android Enterprise](../configuration/custom-settings-android-for-work.md)|Add or create custom settings that aren't built in to Intune for personally owned devices.|Android Enterprise|
|[Configure Zebra Mobility Extensions (MX) profile](../configuration/android-zebra-mx-overview.md)|Use Zebra's Mobility Extensions (MX) profiles to customize or add more Zebra-specific settings in Intune.| Android device administrator |
|[Create OEMConfig configuration profile](../configuration/android-oem-configuration-overview.md)|Use OEMConfig to add, create, and customize OEM-specific settings for Android Enterprise devices.| Android Enterprise |
|[Customize branding and enrollment experience](../apps/company-portal-app.md)|Customize the Intune Company Portal and Microsoft Intune apps with your organization's branding to create a familiar experience for people enrolling their devices.|Android Enterprise, Android device administrator |  


## Set up secure authentication methods   
Set up authentication methods in Intune to ensure that only authorized people access your internal resources. Intune supports multi-factor authentication, SCEP and PKCS certificates, and derived credentials. Certificates can also be used for signing and encryption of email using S/MIME.  

| Task | Detail | Platform | 
| ---- | ------ | ------ | 
|[Require multi-factor authentication (MFA)](../enrollment/multi-factor-authentication.md)| Require people to supply two forms of credentials at time of enrollment.| Android Enterprise |
|[Create a trusted certificate profile](../protect/certificates-trusted-root.md)|Create and deploy a trusted certificate profile before you create a SCEP, PKCS, or PKCS imported certificate profile. The trusted certificate profile deploys the trusted root certificate to devices using SCEP, PKCS, and PKCS imported certificates.| Android Enterprise, Android device administrator |  
|[Use SCEP certificates with Intune](../protect/certificates-scep-configure.md)| Learn what’s needed to use SCEP certificates with Intune, and configure the required infrastructure. After you do that, you can [create a SCEP certificate profile](../protect/certificates-profile-scep.md) or [set up a third-party certification authority with SCEP](../protect/certificate-authority-add-scep-overview.md).| Android Enterprise | 
|[Use PKCS certificates with Intune](../protect/certificates-pfx-configure.md)| Configure required infrastructure (such as on-premises certificate connectors), export a PKCS certificate, and add the certificate to an Intune device configuration profile. | Android Enterprise, Android device administrator | 
|[Use imported PKCS certificates with Intune](../protect/certificates-imported-pfx-configure.md)|Set up imported PKCS certificates, which enable you to [set up and use S/MIME to encrypt email](../protect/certificates-s-mime-encryption-sign.md). | Android Enterprise, Android device administrator |
|[Set up a derived credentials issuer](../protect/derived-credentials.md)| Provision Android devices with certificates that are derived from user smart cards. | Android Enterprise | 

## Deploy apps  

As you set up apps and app policies, think about your organization's requirements, such as the platforms you'll support, the tasks people need to do, the type of apps they need to complete those tasks, and the groups who need those apps. You can use Intune to manage the whole device (including apps) or use Intune to manage apps only.  

| Task | Detail | Platform | 
| ---- | ------ | ------ | 
|[Add Google Play Store apps](../apps/store-apps-android.md) | Add Android apps from the Google Play Store. | Android device administrator|
|[Add managed Google Play apps](../apps/apps-add-android-for-work.md) | Add store apps, line-of-business (LOB) apps, and web apps through the managed Google Play Store.| Android Enterprise|
|[Add Android Enterprise system apps](../apps/apps-ae-system.md) | Use Intune to enable and disable Android Enterprise system apps. | Android Enterprise|  
|[Add web apps](../apps/web-app.md) | Add web apps to Intune and assign to groups. | Android device administrator|
|[Add built-in apps](../apps/apps-add-built-in.md) | Add built-in apps to Intune and assign to groups. | Android Enterprise, Android device administrator| 
|[Add line-of-business apps ](../apps/lob-apps-android.md)|Add Android line-of-business (LOB) apps to Intune and assign to groups.| Android device administrator|
|[Assign apps to groups ](../apps/apps-deploy.md)|Assign apps to users and devices. | Android Enterprise, Android device administrator|
|[Include and exclude app assignments ](../apps/apps-inc-exl-assignments.md)|Control access and availability to an app by including and excluding selected groups from assignment.|  Android Enterprise, Android device administrator|
| [Create an Android app protection policy](../apps/app-protection-policies.md) | Keep your organization's data contained within managed apps like Outlook and Word. For details about each setting, see [Android app protection policy settings](../apps/app-protection-policy-settings-android.md). | Android Enterprise, Android device administrator| 
| [Validate your app protection policy](../apps/app-protection-policies-validate.md) | Validate that your app protection policy is correctly set up and working before deploying it org-wide. |   Android Enterprise, Android device administrator|
|[Create an app configuration policy](../apps/app-configuration-policies-use-android.md)  | Apply custom configuration settings to Android apps on enrolled devices. You can also apply these types of policies [to managed apps, without device enrollment](../apps/app-configuration-policies-managed-app.md). |  Android Enterprise, Android device administrator|
|[Configure Microsoft Edge](../apps/manage-microsoft-edge.md) | Use Intune app protection and configuration policies with Microsoft Edge for Android to ensure that corporate websites are accessed with safeguards in place. | Android Enterprise, Android device administrator |
|[Configure Google Chrome](../apps/apps-configure-chrome-android.md) | Use an Intune app configuration policy to configure Google Chrome on Android devices enrolled in Intune. | Android Enterprise |
| [Configure Microsoft Managed Home Screen app ](../apps/app-configuration-managed-home-screen-app.md)|Set up Managed Home Screen on corporate-owned Android Enterprise dedicated devices enrolled via Intune and running in multi-app kiosk mode. |Android Enterprise|
| [Configure Microsoft Launcher app ](../apps/configure-microsoft-launcher.md)|Configure Microsoft Launcher to customize the home screen experience on your organization's fully managed devices. |Android Enterprise| 
| [Configure Microsoft Office apps](../apps/manage-microsoft-office.md)| Use Intune app protection and configuration policies with Office apps to ensure that corporate files are accessed with safeguards in place. |Android Enterprise| 
|[Configure Microsoft Teams](../apps/manage-microsoft-teams.md) |Use Intune app protection and configuration policies with Teams to ensure that collaborative team experiences are accessed with safeguards in place. | Android Enterprise|
|[Configure Microsoft Outlook](../apps/app-configuration-policies-outlook.md) | Use Intune app protection and configuration policies with Outlook to ensure corporate email and calendars are accessed with safeguards in place.| Android Enterprise|


## Enroll devices  

Enrolling devices allows them to receive the policies you create, so have your Azure AD user groups and device groups ready.  

Intune supports the following enrollment methods for Android devices:  

* Bring-your-own-device (BYOD): Android Enterprise personally owned devices with a work profile
* Android Enterprise corporate owned dedicated devices 
* Android Enterprise corporate owned fully managed 
* Android Enterprise corporate owned work profile 
* Android device administrator 

For information about each enrollment method and how to choose one that's right for your organization, see the [Android device enrollment guide for Microsoft Intune](deployment-guide-enrollment-android.md). 

| Task | Detail | Platform |
| ---- | ------ | ------ | 
|[Connect Intune account to managed Google Play account](../enrollment/connect-intune-android-enterprise.md)| To enable Android Enterprise management in Intune, connect your Intune tenant account to your managed Google Play account. |  Android Enterprise|
|[Set up work profile enrollment for personally owned devices ](../enrollment/android-work-profile-enroll.md)|Set up work profile management for personally owned devices. This enrollment method creates a separate area on the device for work-related data so that personal things remain unaffected.| Android Enterprise| 
|[Set up work profile enrollment for corporate-owned devices](../enrollment/android-corporate-owned-work-profile-enroll.md)|Set up work profile management for corporate-owned devices intended for work and personal use. This enrollment method creates a separate area on the device for work-related data so that personal things remain unaffected. | Android Enterprise|
|[Set up enrollment for dedicated devices](../enrollment/android-kiosk-enroll.md)| Set up enrollment for corporate-owned, single-use, kiosk-style devices.    |   Android Enterprise|
|[Set up enrollment for fully managed devices](../enrollment/android-fully-managed-enroll.md)|Set up enrollment for corporate-owned devices that are associated with a single user and used exclusively for work.| Android Enterprise |
|[Enroll dedicated, fully managed, or corporate-owned work-profile devices](../enrollment/android-dedicated-devices-fully-managed-enroll.md)|After you've set up Intune for Android Enterprise enrollment, enroll devices using one of the five supported enrollment methods. |Android Enterprise|  
|[Set up device administrator enrollment](../enrollment/android-enroll-device-administrator.md)|Set up Android device administrator enrollment. This method of managing devices has been superseded by Android Enterprise, so we don't recommend enrolling new devices this way.| Android device administrator|  
|[Use Samsung Knox Mobile Enrollment to automatically enroll Android devices](../enrollment/android-samsung-knox-mobile-enroll.md)|Set up Intune for Samsung Knox Mobile Enrollment (KME), which enables you to automatically enroll large numbers of corporate-owned Android devices.  | Android Enterprise, Android device administrator|
|[Identify devices as corporate-owned](../enrollment/corporate-identifiers-add.md)| Assign corporate-owned status to devices to enable more management and identification capabilities in Intune. Corporate-owned status cannot be assigned to devices enrolled through Apple Business Manager. | Android Enterprise, Android device administrator |
|[Change device ownership](../enrollment/corporate-identifiers-add.md#change-device-ownership)|After a device has been enrolled, you can change its ownership label in Intune to corporate-owned or personal-owned. This adjustment changes the way you can manage the device.| Android Enterprise, Android device administrator| 
|[Troubleshoot enrollment problems](/troubleshoot/mem/intune/troubleshoot-android-enrollment)|Troubleshoot and find resolutions to problems that occur during enrollment.|Android Enterprise, Android device administrator|   




## Run remote actions  

After devices are set up, you can use remote actions in Intune to manage and troubleshoot devices from a distance. Availability varies by device platform. If an action is absent or disabled in the portal, then it isn't supported on the device.  

| Task | Detail | 
| ---- | ------ | 
|[Run remote actions in Intune](../remote-actions/device-management.md)|Learn how to drill down and remotely manage and troubleshoot individual devices in Intune. This article lists all remote actions available in Intune and links to those procedures.|
|[Remediate vulnerabilities identified by Microsoft Defender for Endpoint](../protect/atp-manage-vulnerabilities.md)|Integrate Intune with Microsoft Defender for Endpoint to take advantage of Defender's threat and vulnerability management, and use Intune to remediate endpoint weakness identified by Defender's vulnerability management capability.|   
| [Wipe corporate data from Intune-managed apps](../apps/apps-selective-wipe.md) | Selectively remove work-related data from a device. |     

## Next steps

Check out these enrollment tutorials to learn how to do some of the top tasks in Intune. Tutorials are 100 – 200 level content for people new to Intune or a specific scenario.    

* [Walk through Intune in Microsoft Endpoint Manager](tutorial-walkthrough-endpoint-manager.md) 
* [Configure Slack to use Intune for enterprise mobility management (EMM) and app configuration](../apps/tutorial-configure-slack-enterprise-grid.md) 

For the iOS/iPadOS version of this guide, see [Deployment guide: Manage iOS/iPadOS devices in Microsoft Intune](deployment-guide-platform-ios-ipados.md).
