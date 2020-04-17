---
title: How to troubleshoot Intune app protection policy deployment
description: Discusses how to troubleshoot issues that you may experience when you deploy Intune app protection policies. 
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid: 
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.prod: intune
ms.topic: article
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
---

# Troubleshooting app protection policy deployment in Intune

## Introduction

This article helps you understand and troubleshoot problems when you apply app protection policies in Microsoft Intune. Follow the sections that apply to your situation.

## Basic steps

### Collect initial data

Before you begin troubleshooting, you should collect some basic information that can help you better understand the problem and reduce the time to find a resolution.

Collect the following information:

- What policy setting isn't applied? Is any policy applied?
- What is the user experience? Have users installed and started the targeted app?
- When did the problem start? Has app protection ever worked?
- Which platform (Android or iOS) has the problem?
- How many users are affected? Are all devices or only some devices affected?
- How many devices are affected? Are all devices or only some devices affected?
- Although Intune app protection policy doesn't require a mobile device management (MDM) service, are affected users using Intune or a third-party EMM?
- Are all managed apps or only specific apps affected? For example, are LOB apps that have [Intune App SDK](https://docs.microsoft.com/intune/app-sdk-get-started) affected but store apps are not?

Now, let's start troubleshooting based on the answers to these questions.

### Verify prerequisites

The next step in troubleshooting is to check whether all prerequisites are met.

Although you can use Intune app protection policies independent of any MDM solution, the following prerequisites must be met:

- The user must have an Intune license assigned.
- The user must belong to a security group that is targeted by an app protection policy. The same app protection policy must target the specific app that's used.
- For Android devices, the Company Portal app is required to receive app protection policies.
- If you use [Word, Excel, or PowerPoint](https://products.office.com/business/office) apps, the following additional requirements must be met:
    - The user must have a license for [Office 365 Business or Enterprise](https://products.office.com/business/compare-more-office-365-for-business-plans) linked to the user's Azure Active Directory (Azure AD) account. The subscription must include the Office apps on mobile devices and can include a cloud storage account with [OneDrive for Business](https://onedrive.live.com/about/business/). Office 365 licenses can be assigned in the [Microsoft 365 admin center](https://admin.microsoft.com) by following [these instructions](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).
    - The user must have a managed location that's configured by using the granular **Save as** functionality. This command is located under the **Save Copies of Org Data** application protection policy setting. For example, if the managed location is [OneDrive](https://onedrive.live.com/about/), the OneDrive app should be configured in the user's Word, Excel, or PowerPoint app.
    - If the managed location is OneDrive, the app must be targeted by the app protection policy that's deployed to the user.

> [!NOTE]
> The Office mobile apps currently support only SharePoint Online and not SharePoint on-premises.

- If you use Intune app protection policies together with on-premises resources (Microsoft Skype for Business and Microsoft Exchange Server), you must enable [Hybrid Modern Authentication (HMA) for Skype for Business and Exchange](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

Intune app protection policies require that the identity of the user is consistent between the app and [Intune App SDK](https://docs.microsoft.com/intune/app-sdk-get-started). The only way to guarantee this consistency is through modern authentication. There are scenarios in which apps may work in an on-premises configuration without modern authentication. However, the outcomes are not consistent or guaranteed.

For more information about how to enable HMA for Skype for Business hybrid and on-premises configurations, see the following articles:

**Hybrid**
[Hybrid Modern Auth for SfB and Exchange goes GA](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

**On-premises**
[Modern Auth for SfB OnPrem with AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### Check app protection policy status

To check your app protection status, follow these steps:

1. Sign in to Intune.
1. Select **Client apps** > **Monitor** > **App protection status**, and then select the **Assigned users** tile.
1. On the **App reporting** page, select **Select user** to bring up a list of users and groups.
1. Search for and select one of the affected users from the list, then select **Select user**. At the top of the App reporting pane, you can see whether the user is licensed for app protection and has a license for O365. You can also see the app status for all the user's devices.
1. Make a note of such important information as the targeted apps, device types, policies, device check-in status, and last sync time.

> [!NOTE]
> App protection policies are applied only when apps are used in the work context. For example, when the user is accessing apps by using a work account.

For more information, see [How to validate your app protection policy setup in Microsoft Intune](https://docs.microsoft.com/intune/app-protection-policies-validate).

### Verify that user identity is consistent between app and Intune App SDK

In most scenarios, users log in to their accounts by using their user principal name (UPN). However, in some environments (such as on-premises scenarios), users might use some other form of sign-in credentials. In these cases, you might find that the UPN that's used in the app doesn't match the UPN object in Azure AD. When this issue occurs, app protection policies aren't applied as expected.

Microsoft’s recommended best practices are to match the UPN to the primary SMTP address. This practice enables users to log in to managed apps, Intune app protection, and other Azure AD resources by having a consistent identity. For more information, see [Azure AD UserPrincipalName population](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname).

If your environment requires alternative sign-in methods, see [Configuring Alternate Login ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), specifically [Hybrid Modern Authentication with Alternate-ID](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### Verify that the user is targeted

Intune app protection policies must be targeted to users. If you don't assign an app protection policy to a user or user group, the policy isn't applied.

To verify that the policy is applied to the targeted user, follow these steps:

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
1. Select **Client apps** > **Monitor** > **App protection status**, and then select the **User status** tile (based on device OS platform).
On the **App reporting** pane that opens, select **Select user** to search for a user.
1. Select the user from the list. You can see the details for that user.

When you assign the policy to a user group, make sure that the user is in the user group. To do this, follow these steps:

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
1. Select **Groups > All groups**, and then search for and select the group that's used for your app protection policy assignment.
1. Under **Manage**, select **Members**.
1. If the affected user isn't listed, review [Manage app and resource access using Azure Active Directory groups](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups) and your group membership rules. Make sure that the affected user is included in the group.
1. Make sure that the affected user isn't in any of the excluded groups for the policy.

> [!IMPORTANT]
> - The Intune app protection policy must be assigned to user groups and not device groups.
> - If the affected device uses Apple Device Enrollment Program (DEP), make sure that **User Affinity** is enabled. User Affinity is required for any app that requires user authentication under DEP.
> - If the affected device uses Android Enterprise, only work profiles will support app protection policies.


### Verify that the managed app is targeted

When you configure Intune app protection policies, the targeted apps must use [Intune App SDK](https://docs.microsoft.com/intune/app-sdk-get-started). Otherwise, app protection policies may not work correctly.

Make sure that the targeted app is listed in [Microsoft Intune protected apps](https://docs.microsoft.com/intune/apps-supported-intune-apps). For LOB or custom apps, verify that the apps use the latest version of [Intune App SDK](https://docs.microsoft.com/intune/apps-supported-intune-apps). Note the following:

For iOS, this practice is important because each version contains fixes that affect how these policies are applied and how they function. For more information, see [Intune App SDK iOS releases](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases).
For Android, this practice isn't as important. However, users must have the latest version of the Company Portal app installed because the Company Portal app works as the policy broker agent.

> [!NOTE]
> Starting in September 2019, Intune will move to support iOS apps that have Intune App SDK 8.1.1 and later versions. Apps built by using SDK versions that are earlier than 8.1.1 will no longer be supported. For more information, see [Plan for Change: Support for version 8.1.1 and higher of Intune App SDK for iOS](https://docs.microsoft.com/intune/whats-new#plan-for-change-support-for-version-811-and-higher-of-intune-app-sdk-for-ios-).

## More information

### Special requirements for Intune MDM-managed devices

When you create an app protection policy, you can target it to all app types or to the following app types:

- Apps on unmanaged devices
- Apps on Intune-managed devices
- Apps in the Android Work Profile

> [!NOTE] 
> To specify the app types, set **Target to all app types** to **No**, and then select from the **App types** list.

For iOS, the following additional [app configuration settings](https://docs.microsoft.com/intune/app-configuration-policies-use-ios) are required to target app protection policy (APP) settings to apps on Intune-enrolled devices:

- **IntuneMAMUPN** must be configured for all MDM (Intune or a third-party EMM)-managed applications. For more information, see Configure user UPN setting for Microsoft Intune or third-party EMM.
- **IntuneMAMDeviceID** must be configured for all third-party and LOB MDM-managed applications.
- **IntuneMAMDeviceID** must be configured as the device ID token. For example, key=IntuneMAMDeviceID, value={{deviceID}}. For more information, see [Add app configuration policies for managed iOS devices](https://docs.microsoft.com/intune/app-configuration-policies-use-ios).
- If only the **IntuneMAMDeviceID** value is configured, Intune APP will consider the device as unmanaged.

### Scenario: Policy changes are not working
The [Intune App SDK](https://docs.microsoft.com/intune/app-sdk-get-started) checks regularly for policy changes. However, this process may be delayed for any of the following reasons:

- The app hasn't checked in with the service.
- The Company Portal app has been removed from the device.

Intune app protection policy relies on user identity. Therefore, a valid login that uses a work or school account to the app and a consistent connection to the service are required. If the user hasn't signed in to the app, or the Company Portal app has been removed from the device, policies updates won't apply.

Additionally, changes and updates to app protection policy can take up to 8 hours to apply. If applicable, closing all apps and restarting the device usually forces the policy update to apply sooner.

To check app protection status, follow these steps:

1. Sign in to Intune.
1. Select **Client apps** > **Monitor** > **App protection status**, and then select the **Assigned users** tile.
1. On the App reporting page, select **Select user** to open a list of users and groups.
1. Search for and select one of the affected users from the list, then select **Select user**.
1. Review the policies that are currently applied, including the status and last sync time.
1. If the status is **Not checked in**, or if the display indicates that there has not been a recent sync, check whether the user has a consistent network connection. For Android users, make sure that they have the latest version of the Company Portal app installed.

> [!IMPORTANT]
> The [Intune App SDK](https://docs.microsoft.com/intune/app-sdk-get-started) checks every 30 minutes for selective wipe. However, changes to existing policy for users who are already signed in may not appear for up to 8 hours. To speed up this process, have the user log out of the app and then log back in or restart their devices.

Intune app protection policy includes multi-identity support. Intune can apply app protection policies to only the work or school account that's signed in to the app. However, only one work or school account per device is supported.

### Scenario: The policy is applied, but iOS users can still transfer work files to unmanaged apps
The **Open-in management** ( ![Open-in button](media/troubleshooting-app-protection/troubleshooting-app-protection.jpg) ) feature for iOS devices can limit file transfers between apps that are deployed through the MDM channel. The user may be able to transfer work files from managed locations such as OneDrive and Exchange to unmanaged apps or locations, depending on the configuration. The iOS **Open-in management** feature works outside other data transfer methods. Therefore, it isn't affected by **Save as** and **Copy/Paste** settings.

You can use Intune app protection policies together with the iOS **Open-in management** feature to protect company data in the following manner:

- **Employee-owned devices that are not managed by an MDM solution**: You can set the app protection policy settings to **Allow app to transfer data to only Policy Managed apps**. Configured in this way, the **Open-in** behavior in a policy-managed app provides only other policy-managed apps as options for sharing. For example, if a user tries to send a protected file as an attachment from OneDrive in the native mail app, that file is unreadable.

- **Devices that are managed by MDM solutions**: For devices that are enrolled in Intune or third-party MDM solutions, data sharing between apps by using app protection policies and other managed iOS apps that are deployed through MDM is controlled by Intune APP and by the iOS **Open-in management** feature.<br/><br/>
To make sure that apps you deploy by using an MDM solution are also associated with your Intune app protection policies, configure the user UPN setting as described in [Configure user UPN setting](https://docs.microsoft.com/intune/data-transfer-between-apps-manage-ios#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).<br/><br/>To specify how you want to allow data transfer to other apps, enable **Send Org data to other apps**, and then select your preferred level of sharing.<br/><br/>To specify how you want to allow an app to receive data from other apps, enable **Receive data from other apps**, and then select your preferred level of receiving data.

For more information about how to receive and share app data, see [Data relocation settings](https://docs.microsoft.com/intune/app-protection-policy-settings-ios#data-protection).

For more information, see [How to manage data transfer between iOS apps in Microsoft Intune](https://docs.microsoft.com/intune/data-transfer-between-apps-manage-ios).

## References

If you’re still looking for a solution to a related problem, or for more information about Intune, post a question in our [Microsoft Intune forum](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Many support engineers, MVPs, and members of our development team visit the forums. So, there’s a good chance that you can find someone who has the information that you need.

To open a support request for the Microsoft Intune product support team, see [How to get support for Microsoft Intune](https://docs.microsoft.com/intune/get-support).

For more information about Intune app protection policy, see the following articles:

- [Troubleshoot mobile application management](https://docs.microsoft.com/intune/troubleshoot-mam)
- [Frequently asked questions about MAM and app protection](https://docs.microsoft.com/intune/mam-faq)
- [Support Tip: Troubleshooting Intune app protection policy using log files on local devices](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

For all the latest news, information, and tech tips, go to our official blogs:

- [The Microsoft Intune Support Team Blog](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [The Microsoft Enterprise Mobility and Security Blog](https://cloudblogs.microsoft.com/enterprisemobility)