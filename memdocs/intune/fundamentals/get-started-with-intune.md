---
# required metadata

title: Getting started with Microsoft Intune
description: Learn about the Microsoft Intune deployment, enrollment, configuration, policies, service updates, and more.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/27/2022
ms.topic: overview
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
  - get-started
  - intro-get-started
ms.collection:
  - M365-identity-device-management
  - highpri
  - highseo
---

# Get started with Microsoft Intune

As part of your Microsoft 365 license, you also get Microsoft Intune for cloud-based app management, device management, and security. 

This article provides an overview of the Microsoft Intune architecture, deployment, enrollment, configuration, policies, service updates, and more.


For more information about what Microsoft Intune can do for your organization, go to [What is Microsoft Intune](what-is-intune.md).

## Cloud attach with Configuration Manager

Microsoft Endpoint Configuration Manager helps you protect on-premises Windows Server, devices, apps, and data. If you need to manage only cloud-based endpoints, you can use Microsoft Intune. If you need to manage only on-premises endpoints, such as the computers your organization has attached to your internal network, you can use Configuration Manager. However, if you need to manage a combination of both cloud and on-premises endpoints, you can use cloud attach to use both Intune and Configuration Manager from Microsoft Endpoint Manager.

There are two steps to cloud attach your on-premises devices:

1. [Tenant attach](./configmgr/tenant-attach/index.yml): Register your Intune tenant with your Configuration Manager deployment.
2. [Co-management](./configmgr/comanage/index.yml): Concurrently managing Windows client devices with both Configuration Manager and Microsoft Intune.

These steps are incremental steps on the journey to having full cloud attachment. You get immediate value through tenant attach and you get more value through co-management.

## Step 1 - Plan your Intune deployment

A successful adoption or migration to Microsoft Intune starts with a plan. This plan depends on your organization's current device management solution, business goals, and technical requirements. Additionally, you should include key stakeholders who will support and collaborate with the plan.

Intune gives you options to manage access to your organization using Mobile Device Management (MDM) or Mobile Application Management (MAM). MDM is when users "enroll" their devices in Intune. Once enrolled, they are managed devices, and can receive any policies, rules, and settings used by your organization. For example, you can install specifics apps, create a password policy, install a VPN connection, and more.

If users with their own personal devices will access organization resources, then you need to protect any apps that access your organization data using MAM, at the very least. You can create MAM policies for Outlook, Teams, SharePoint, and other business apps.

You may want to treat devices differently, depending on their use. For example, you may want different plans for users in Human Resources (HR) or users in Sales.

The following articles can help:

- [Planning guide to move to Microsoft Intune](intune-planning-guide.md)
- [Move to cloud-native endpoints](/mem/cloud-native-endpoints-overview)
- [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md)

> [!TIP]
> To go through some online training, go to:
>
> - [Microsoft Endpoint Manager fundamentals](/training/paths/endpoint-manager-fundamentals/)
> - [Plan your migration to Microsoft Endpoint Manager](/training/modules/paths-to-modern-endpoint-management/)
> - [Determine your endpoint management implementation](/training/modules/determine-endpoint-implementation/)

## Step 2 - Determine your licensing and get your prerequisites

The next step is to determine your license needs and any other prerequisites for your Intune deployment. The following list provides some of the most common prerequisites:

- **Intune subscription**: Included with some Microsoft 365 subscriptions. It also gives you access to the Endpoint Manager admin center.
- **Microsoft 365 apps**: Included with Microsoft 365 and is used for productivity apps, including Outlook and Teams.
- **Azure Active Directory (Azure AD) premium**: Included with some Microsoft 365 subscriptions. Azure AD is used for the identity management for users, groups, and devices, which comes with your Intune and Microsoft 365 subscription. Azure AD Premium gives you additional features commonly used by organizations, including conditional access, multi factor authentication (MFA) and dynamic groups.
- **Windows Autopilot**: Included with some Microsoft 365 subscriptions. Windows Autopilot gives you modern OS deployment for Windows 10/11 client devices.
- **Platform specific prerequisites**: If you manage iOS/iPadOS and macOS devices, you need an Apple MDM push certificate and possibly an Apple token. If you're managing Android devices, you may need a managed Google Play account. If you're using certificate authentication, then may need a SCEP or PKCS certificate.

  There may be additional requirements depending on your organization's needs. 

The following articles can help:

- [Planning guide to move to Microsoft Intune](intune-planning-guide.md)
- [Microsoft Intune licensing](licenses.md)
- [Azure AD plans and pricing](https://www.microsoft.com/security/business/identity-access/azure-active-directory-pricing)
- [Windows Autopilot licensing](/mem/autopilot/licensing-requirements)
- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)
- [Deployment guide: Enroll iOS/iPadOS devices in Microsoft Intune](deployment-guide-enrollment-ios-ipados.md)
- [Deployment guide: Enroll macOS devices in Microsoft Intune](deployment-guide-enrollment-macos.md)
- [Deployment guide: Enroll Windows devices in Microsoft Intune](deployment-guide-enrollment-windows.md)

## Step 3 - Set up Intune

Intune uses many features in Azure AD, including your domain, your users, and your groups. You can also create new users and new groups to fit your company needs. For example, you can create a group called **iOS devices** or **All HR users**. If you have Azure AD Premium, use [dynamic groups](groups-add.md) to automatically add users and devices to groups based on rules you create.

This step focuses on setting up Intune and getting it ready for you to manage your devices.

1. **[Confirm your devices are supported](supported-devices-browsers.md)**. Confirm your iOS, macOS, Android, and Windows devices are supported by Intune. If your organization includes devices that aren't supported, then the policies aren't applied to those devices.

2. **[Customize your domain name](custom-domain-name-configure.md)**. By default, a domain named something like `your-domain.onmicrosoft.com` is automatically created in Azure AD. `onmicrosoft.com` can be customized for your organization. When you customize, it also gives users a familiar domain when connecting to Intune and using resources.

3. **[Sign in to Intune](account-sign-up.md)**. When you sign in, you may be prompted to enter information about your organization. Intune is included with Microsoft 365, and can be opened directly from the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) or the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?linkid=2024339).

4. **[Choose your mobile device management configuration](mdm-authority-set.md)**. The first time you use Intune, you must enable device management. Intune can be used as a cloud-only service, a hybrid with Intune and Microsoft Endpoint Configuration Manager, or Basic Mobility and Security for Microsoft 365. You can choose which setup works best for your organization.

5. **[Add users](users-add.md)** and **[add groups](groups-add.md)**.

   You can manually add users or use hybrid identity and Azure AD Connect to sync your on-premises user accounts with Intune. You can also give admin roles to specific users. Users are required unless your devices are "userless" devices, such as kiosk or dedicated devices.

   Azure AD groups are used to simplify how you manage devices and users in Intune. Using groups, you can do many different tasks. For example, your organization wants to require a specific app on Android devices. You can create an Android devices group and deploy a policy with this app to the group.

6. **[Assign licenses](licenses-assign.md)**. For users or devices to enroll in Intune, they require an Intune license.

The following articles can help:

- [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md)
- [Set up Microsoft Intune](setup-steps.md)

## Step 4 - Check for compliance and turn on conditional access

MDM solutions like Intune can set rules that devices should meet, and can report the compliance states of these rules. These rules are called compliance policies. They establish a baseline of what every device must have to be considered compliant. When you combine compliance policies with conditional access, you can require devices meet certain security requirements before they can access your organization's data.

For example, you can choose an acceptable (or unacceptable) threat level, block jailbroken or rooted devices, require a password length, and more. If these devices don't meet your rules, meaning they aren't compliant, then you can block access to your resources.

If you prefer, you can enroll your devices before checking compliance. It's up to you. When users enroll their devices in Intune, then enrollment process can automatically deploy your compliance policies. When enrollment completes, admins can check the compliance status and get a list of devices that don't meet your rules. Microsoft recommends creating compliance and conditional access policies, and then deploying these policies during enrollment.

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you create your policies and assign them to your groups. As a best practice, start small, and use a staged approach. For example, create an iOS/iPadOS policy that blocks jailbroken devices. Apply the policy to a pilot or test group. After initial testing, add more users to the pilot group. For more guidance, go to the [Microsoft Intune planning guide](intune-planning-guide.md).

The following articles can help you understand how to create & monitor compliance policies in Intune, how to integrate with mobile threat defense (MTD) services & network access control (NAC) solutions, and use conditional access:

- [Get started with device compliance policies in Microsoft Intune](../protect/device-compliance-get-started.md)
- [Create a compliance policy in Microsoft Intune](../protect/create-compliance-policy.md)
- [Intune reports for compliance, assignment failures, check-in status, and more](reports.md)
- [Learn about Conditional Access and Intune](../protect/conditional-access.md)
- [Enable Mobile Threat Defense connector in Microsoft Intune](../protect/mtd-connector-enable.md)
- [Enforce compliance for Microsoft Defender for Endpoint with Conditional Access in Intune](../protect/advanced-threat-protection.md)
- [Network access control integration with Microsoft Intune](../protect/network-access-control-integrate.md)
- [App-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md)
- [Conditional Access scenarios](../protect/conditional-access-intune-common-ways-use.md)
- [Monitor device compliance policies in Microsoft Intune](../protect/compliance-policy-monitor.md)

## Step 5 - Add and deploy apps

Every organization has a base set of apps that should be installed on devices. For example, your organization may require a specific email app, web browser, or VPN app. You can use Intune to deploy these apps to your users before they enroll their devices. When users enroll their devices, these apps can be automatically installed.

If you prefer, you can enroll your devices before installing apps. It's up to you. When users enroll their devices in Intune, then enrollment process can automatically deploy your apps. When enrollment completes, the apps are ready to use. For key productivity apps, Microsoft recommends creating app policies and then deploying these policies during enrollment.

Intune supports a wide range of apps, including store apps, line-of-business (LOB) apps, Win32 apps, and more. You can manage app deployment using the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Also, you can use Intune to orchestrate store app deployment with managed Google Play, the Apple App Store, and the Microsoft Store.

The following articles can help:

- [What is app management in Microsoft Intune](../apps/app-management.md)
- [Add apps to Microsoft Intune](../apps/apps-add.md)
- [Add and assign managed Google Play apps to Android Enterprise devices](../apps/apps-add-android-for-work.md)
- [Manage Android Enterprise system apps in Microsoft Intune](../apps/apps-ae-system.md)
- [Add iOS/iPadOS store apps to Microsoft Intune](../apps/store-apps-ios.md)
- [How to manage iOS/iPadOS and macOS apps purchased through Apple Business Manager](../apps/vpp-apps-ios.md)
- [Windows 10/11 app deployment using Microsoft Intune](../apps/apps-windows-10-app-deploy.md)
- [Protect your company app data with Microsoft Intune and Microsoft Graph](/graph/api/resources/intune-app-conceptual)

## Step 6 - Configure device features

Your organization may have a base set of device features that should be configured or should be blocked. For example, you can create device configuration policies that add a VPN connection, block access to personal cloud storage, turn off bluetooth discovery, and more. You can also configure device features that help protect your organization's devices, including requiring device encryption and requiring strong passcodes.

You can use Intune to configure these device features before users enroll their devices. When users enroll their devices, these device features can be automatically configured and ready to use.

If you prefer, you can enroll your devices before creating device configuration policies. It's up to you. When users enroll their devices in Intune, the enrollment process can install your device configuration policies, such as a VPN connection. When enrollment completes, the feature is ready to use. For key device configuration features, such as VPN or Wi-Fi, Microsoft recommends creating the policies and then deploying these policies during enrollment.

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can create different policies based on your device platform - Android, iOS/iPadOS, macOS, and Windows. For example, you can:

- Use endpoint protection on Windows 10 devices to enable different BitLocker options, including encryption.
- Use the restricted apps feature on iOS/iPadOS devices to create a list of approved apps that can be installed. Or, create a list of prohibited apps.
- Use the kiosk settings to choose which apps can be used on Android devices running in kiosk mode.
- Apply a Wi-Fi connection and its settings, including the security type, on devices running macOS.

Remember, start small, and use a staged approach. Assign the profile to a pilot or test group. Then, assign the profile to more pilot groups.

The following articles can help:

- [Apply features and settings on your devices using device profiles](../configuration/device-profiles.md)
- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Assign device profiles in Microsoft Intune](../configuration/device-profile-assign.md)
- [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md)
- [Manage endpoint security in Microsoft Intune](../protect/endpoint-security.md)
- Security configuration framework with recommendations for [Android Enterprise](../enrollment/android-configuration-framework.md) and [iOS/iPadOS](../enrollment/ios-ipados-configuration-framework.md)
- [Windows security baselines](/windows/security/threat-protection/windows-security-baselines)

## Step 7 - Enroll your devices

To manage devices, the devices must be enrolled in Intune. As an administrator, you'll set up enrollment restrictions and policies for your users and devices. Each device platform (iOS, Android, macOS, and Windows) has a variety of options. You can have your users enroll themselves. Or, you can automate enrollment so users simply sign in to the device.

Enrollment is a key step when using Intune. [Enroll devices](https://docs.microsoft.com/intune/device-enrollment) lists the steps for the different devices.

Using Intune, you can manage devices and apps, and how they access organization data. To use Intune mobile device management (MDM), the devices must enroll in the Intune service. When they're enrolled, these devices are managed by your organization, and can receive your app and device policies, security policies, and compliance policies.

When a device enrolls, it's issued a secure MDM certificate. This certificate communicates with the Intune service.

Devices can be enrolled on the following platforms. For the specific versions, see [Supported operating systems](supported-devices-browsers.md):

- Android
- iOS/iPadOS
- macOS
- Windows

Different platforms may have other requirements. For example, iOS/iPadOS and macOS devices require an [MDM push certificate from Apple](../enrollment/apple-mdm-push-certificate-get.md).

The following articles can help you learn more about device enrollment for each platform:

- [What is device enrollment in Intune?](../enrollment/device-enrollment.md)
- [Enrolled device management capabilities of Microsoft Intune](../enrollment/device-management-capabilities.md)
- [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md)
- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)
- [Deployment guide: Enroll iOS/iPadOS devices in Microsoft Intune](deployment-guide-enrollment-ios-ipados.md)
- [Deployment guide: Enroll macOS devices in Microsoft Intune](deployment-guide-enrollment-macos.md)
- [Deployment guide: Enroll Windows devices in Microsoft Intune](deployment-guide-enrollment-windows.md)

## Protect your apps

Intune app protection policies (APP) allow you to protect organizational data within an application. You can implement mobile application management (MAM) in Intune to help protect sensitive data that's accessed from managed applications. See the official list of [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md) available for public use.

Together with app configuration capabilities, 

Apps on mobile devices are often the quickest way users get access to your corporate resources. 

There are challenges when using apps, as there are different devices, including personal devices and corporate devices. And, you want to protect your organization's resources and its data while also making sure users are productive.

Intune can manage apps, including add apps, assign them to different users or groups, and review other key details. For example, you can see which apps fail to install, check the version of an app, and more.

To get an overview of app protection policies and how they work, go to the following articles:

- [App protection policies overview](../apps/app-protection-policy.md)
- [Data protection framework using app protection policies](../apps/app-protection-framework.md)
- [Understand app protection policy delivery timing](../apps/app-protection-policy-delivery.md)
- [How to create and assign app protection policies](../apps/app-protection-policies.md)
- [How to manage data transfer between iOS apps in Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md)
- [How to monitor app protection policies](../apps/app-protection-policies-monitor.md)
- [Review client app protection logs](../apps/app-protection-policy-settings-log.md)
- [Frequently asked questions about MAM and app protection](../apps/mam-faq.yml)


[Deployment guide: Mobile Application Management (MAM) for unenrolled devices in Microsoft Intune](deployment-guide-enrollment-mamwe.md)
[Microsoft Intune planning guide](intune-planning-guide.md).

## Next steps

