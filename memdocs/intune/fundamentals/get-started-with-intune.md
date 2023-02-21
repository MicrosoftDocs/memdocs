---
# required metadata

title: Get started with Microsoft Intune
description: See an overview of the steps to start using Intune. Plan your move and deployment of Intune, determine your licensing needs and any platform requirements, use compliance and conditional access, deploy apps, create device configuration profiles, and enroll your devices to be managed. Get more information on mobile application management for BYOD or personal devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/25/2022
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
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Get started with Microsoft Intune

Microsoft Intune is a cloud-based service that helps you manage your devices and apps. For more information about what Microsoft Intune can do for your organization, go to [What is Microsoft Intune](what-is-intune.md).

This article provides an overview of the steps to start using Intune, including:

- Step 1: Plan your move and deployment of Intune
- Step 2: Determine your licensing needs and any platform requirements
- Step 3: Set up Intune
- Step 4: Use compliance and conditional access
- Step 5: Target apps for enrollment
- Step 6: Create device configuration profiles
- Step 7: Enroll your devices to be managed
- Protect organization app data on personal devices
- Cloud-attach with Configuration Manager

## Step 1 - Plan your Intune deployment

A successful adoption or migration to Microsoft Intune starts with a plan. Your plan depends on your organization's current device management solution, business goals, and technical requirements.

Intune gives you options to manage access to your organization using Mobile Device Management (MDM) or Mobile Application Management (MAM). MDM is when users "enroll" their devices in Intune. Once enrolled, they're managed devices, and can receive any policies, rules, and settings used by your organization. For example, you can install specifics apps, create a password policy, install a VPN connection, and more.

If users with their own personal devices will access organization resources, then you need to protect any apps that access your organization data using mobile application management (MAM), at a minimum. You can create MAM policies for Outlook, Teams, SharePoint, and other apps. MAM policies are discussed more later in this article ([Protect organization app data on personal devices](#protect-organization-app-data-on-personal-devices)).

To help you plan your Intune deployment, use the [Planning guide to move to Microsoft Intune](intune-planning-guide.md). It covers personal devices, licensing considerations, creating a rollout plan, communicating changes to your users, and more.

The following articles are good resources:

- [Planning guide to move to Microsoft Intune](intune-planning-guide.md)
- [Move to cloud-native endpoints](/mem/cloud-native-endpoints-overview)
- [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md)

> [!TIP]
> For some online training, go to:
>
> - [Microsoft Endpoint Manager fundamentals](/training/paths/endpoint-manager-fundamentals/)
> - [Plan your migration to Microsoft Endpoint Manager](/training/modules/paths-to-modern-endpoint-management/)
> - [Determine your endpoint management implementation](/training/modules/determine-endpoint-implementation/)

## Step 2 - Determine your licensing and get your prerequisites

The next step is to determine your license needs and any other prerequisites for your Intune deployment. The following list provides some of the most common prerequisites:

- **Intune subscription**: Included with some Microsoft 365 subscriptions. You also get access to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), which is a web-based console for managing your devices, apps, and users.
- **Microsoft 365 apps**: Included with Microsoft 365 and is used for productivity apps, including Outlook and Teams.
- **Azure Active Directory (Azure AD) premium**: Included with some Microsoft 365 subscriptions. Azure AD is used for the identity management for users, groups, and devices, which comes with your Intune and Microsoft 365 subscription. Azure AD Premium gives you more features commonly used by organizations, including conditional access, multi factor authentication (MFA), and dynamic groups.
- **Windows Autopilot**: Included with some Microsoft 365 subscriptions. Windows Autopilot gives you modern OS deployment for Windows 10/11 client devices.
- **Platform specific prerequisites**: Depending on the platforms of your devices, there will probably be other requirements. For example, if you manage iOS/iPadOS and macOS devices, you need an Apple MDM push certificate and possibly an Apple token. If you're managing Android devices, you may need a managed Google Play account. If you're using certificate authentication, you may need a SCEP or PKCS certificate.

The following articles are good resources:

- [Planning guide to move to Microsoft Intune](intune-planning-guide.md)
- [Microsoft Intune licensing](licenses.md)
- [Azure AD plans and pricing](https://www.microsoft.com/security/business/identity-access/azure-active-directory-pricing)
- [Windows Autopilot licensing](/mem/autopilot/licensing-requirements)
- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)
- [Deployment guide: Enroll iOS/iPadOS devices in Microsoft Intune](deployment-guide-enrollment-ios-ipados.md)
- [Deployment guide: Enroll macOS devices in Microsoft Intune](deployment-guide-enrollment-macos.md)
- [Deployment guide: Enroll Windows devices in Microsoft Intune](deployment-guide-enrollment-windows.md)

## Step 3 - Set up Intune

Intune uses many features in Azure AD, including your domain, your users, and your groups. You can also create new users and new groups to fit your organization needs. For example, you can create a group called **iOS devices** or **All HR users**. If you have Azure AD Premium, you can use [dynamic groups](groups-add.md) to automatically add users and devices to groups based on rules you create.

This step focuses on setting up Intune and getting it ready for you to manage your devices. Here's an overview:

1. **[Confirm your devices are supported](supported-devices-browsers.md)**. Confirm your Android, iOS/iPadOS, macOS, and Windows devices are supported. If your organization includes devices that aren't supported, then the policies aren't applied to those devices.

2. **[Customize your domain name](custom-domain-name-configure.md)**. By default, a domain named something like `your-domain.onmicrosoft.com` is automatically created in Azure AD. The `onmicrosoft.com` part of the domain can be customized for your organization. When you customize, it also gives users a familiar domain when connecting to Intune and using organization resources.

3. **[Sign in to Intune](account-sign-up.md)**. When you sign in, you may be prompted to enter information about your organization. Intune can be opened directly from the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) or the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?linkid=2024339).

4. **[Choose your mobile device management configuration](mdm-authority-set.md)**. The first time you use Intune, you must enable device management. Intune can be used as a cloud-only service, hybrid with Intune and Configuration Manager, or Basic Mobility and Security for Microsoft 365. You can choose the setup that works best for your organization.

5. **[Add users](users-add.md)** and **[add groups](groups-add.md)**.

   You can manually add users or use hybrid identity and Azure AD Connect to sync your on-premises user accounts with Intune. You can also give admin roles to specific users. Users are required unless your devices are "userless" devices, such as kiosk or dedicated devices commonly used by frontline workers.

   Azure AD groups can simplify how you manage devices and users in Intune.
   
   For example, your organization wants to require a specific app on Android devices. You can create an Android devices group and deploy a policy with this app to your group.

6. **[Assign licenses](licenses-assign.md)**. For users or devices to enroll in Intune, they require an Intune license.

The following articles are good resources:

- [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md)
- [Set up Microsoft Intune](setup-steps.md)
- [Azure AD Connect sync: Understand and customize synchronization](/azure/active-directory/hybrid/how-to-connect-sync-whatis)

## Step 4 - Check for compliance and turn on conditional access

MDM solutions like Intune can set rules that devices should meet, and can report the compliance states of these rules. These rules are called compliance policies. They establish a baseline of what every device must have to be considered compliant. When you combine compliance policies with conditional access, you can require devices meet certain security requirements before they can access your organization's data.

For example, you can choose an acceptable (or unacceptable) threat level, block jailbroken or rooted devices, require a password length, and more. If these devices don't meet your rules, meaning they aren't compliant, then you can use conditional access to block access to your resources.

If you prefer, you can enroll your devices before checking compliance. It's up to you. When users enroll their devices in Intune, then enrollment process can automatically deploy your compliance policies. When enrollment completes, admins can check the compliance status and get a list of devices that don't meet your rules.

Microsoft recommends creating a baseline of compliance and conditional access policies, and then deploying these policies during enrollment.

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you create your policies and assign them to your groups. As a best practice, start small, and use a staged approach. For example, create an iOS/iPadOS policy that blocks jailbroken devices. Apply the policy to a pilot or test group. After initial testing, add more users to the pilot group. For more guidance, go to the [Microsoft Intune planning guide](intune-planning-guide.md).

The following articles are good resources:

- [Get started with device compliance policies in Microsoft Intune](../protect/device-compliance-get-started.md)
- [Learn about conditional access and Intune](../protect/conditional-access.md)
- [App-based conditional access with Intune](../protect/app-based-conditional-access-intune.md)
- [Conditional access scenarios](../protect/conditional-access-intune-common-ways-use.md)

## Step 5 - Add and target apps for enrollment

Every organization has a base set of apps that should be installed on devices. Your organization may require a specific email app, web browser, or VPN app. You can use Intune to assign these apps to your users before they enroll their devices. When users enroll their devices, the app policies are automatically deployed. When enrollment completes, the apps install and are ready to use.

If you prefer, you can enroll your devices, and then assign apps. It's up to you. For example, your organization may have a new app that it wants installed on devices. Admins add the user or device to the group that'll use that app. The next time users check for new apps, they'll see the new app available.

For key productivity apps, Microsoft recommends creating a baseline of app policies and then assigning these policies during enrollment.

Intune supports a wide range of apps, including store apps, line-of-business (LOB) apps, Win32 apps, and more. You can manage app deployment using the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Also, you can connect to your managed Google Play, the Apple App Store, and the Microsoft Store to deploy apps from these locations.

The following articles are good resources:

- [What is app management in Microsoft Intune?](../apps/app-management.md)
- [Windows 10/11 app deployment using Microsoft Intune](../apps/apps-windows-10-app-deploy.md)

## Step 6 - Configure device features

Your organization may have a base set of device features that should be configured or should be blocked. These settings are added to device configuration policies. You can create device configuration policies that add a VPN connection, block access to personal cloud storage, turn off bluetooth discovery, and more. You can also configure device features that help protect your organization's devices, including requiring device encryption and requiring strong passcodes.

You can use Intune to configure these device features before users enroll their devices. When users enroll their devices, these device features can be automatically configured, and ready to use.

If you prefer, you can enroll your devices before creating device configuration policies. It's up to you. When users enroll their devices in Intune, the enrollment process can install your device configuration policies, like a VPN connection. When enrollment completes, the feature is ready to use.

For key device configuration features, such as VPN or Wi-Fi, Microsoft recommends creating the policies and then deploying these policies during enrollment.

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can create different policies based on your device platform - Android, iOS/iPadOS, macOS, and Windows. For example, you can:

- Use endpoint protection on Windows 10/11 devices to enable different BitLocker options, including encryption.
- Use the restricted apps feature on iOS/iPadOS devices to create a list of approved apps that can be installed. Or, create a list of prohibited apps.
- Use the kiosk settings to choose which apps can be used on Android devices running in kiosk mode.
- Apply a Wi-Fi connection and its settings, including the security type, on macOS devices.

Remember, start small, and use a staged approach. Assign the profile to a pilot or test group. Then, assign the profile to more pilot groups. For more guidance, go to the [Microsoft Intune planning guide](intune-planning-guide.md).

The following articles are good resources:

- [Apply features and settings on your devices using device profiles](../configuration/device-profiles.md)
- [Use the settings catalog to configure settings](../configuration/settings-catalog.md)
- [Manage endpoint security in Microsoft Intune](../protect/endpoint-security.md)
- Security configuration framework with recommendations for [Android Enterprise](../enrollment/android-configuration-framework.md) and [iOS/iPadOS](../enrollment/ios-ipados-configuration-framework.md)
- [Windows security baselines](/windows/security/threat-protection/windows-security-baselines)

## Step 7 - Enroll your devices

To manage devices, the devices must be enrolled in Intune to receive the compliance & conditional access policies, app policies, device configuration policies, and security policies you create. As an admin, you create enrollment policies for your users and devices. Each device platform (Android, iOS/iPadOS, macOS, and Windows) has various enrollment options. You choose what's best for your environment, your scenarios, and how your devices are used.

Depending on the enrollment option you choose, users can enroll themselves. Or, you can automate enrollment so users only need to sign in to the device with their organization account.

When a device enrolls, it's issued a secure MDM certificate. This certificate communicates with the Intune service.

Different platforms have different enrollment requirements. The following articles can help you learn more about device enrollment, including platform-specific guidance:

- [What is device enrollment in Intune?](../enrollment/device-enrollment.md)
- [Enrolled device management capabilities of Microsoft Intune](../enrollment/device-management-capabilities.md)
- [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md)
- [Deployment guide: Enroll Android devices in Microsoft Intune](deployment-guide-enrollment-android.md)
- [Deployment guide: Enroll iOS/iPadOS devices in Microsoft Intune](deployment-guide-enrollment-ios-ipados.md)
- [Deployment guide: Enroll macOS devices in Microsoft Intune](deployment-guide-enrollment-macos.md)
- [Deployment guide: Enroll Windows devices in Microsoft Intune](deployment-guide-enrollment-windows.md)

## Protect organization app data on personal devices

It's common for users to access their organization email & calendar, attend work meetings, and use other organization apps on their personal devices. To help keep organization data secure on these devices, you can use app protection policies and multi-factor authentication (MFA). App protection policies help protect organization data on personal devices. MFA helps protect your organization's data from unauthorized access.

Intune's app protection policies are part of a mobile application management (MAM) approach designed to protect organization app data on personal devices. 

These app protection policies can also be used on devices enrolled Intune, or enrolled and managed by a third party partner MDM solution. This scenario is more common for apps that need an extra layer of security, including apps that have sensitive data.

The [Microsoft Intune planning guide](intune-planning-guide.md) has some guidance on managing access on personal devices.

There's an official list of Microsoft apps and supported third party partner apps that support app protection policies. See the official list at [Microsoft Intune protected apps list](../apps/apps-supported-intune-apps.md).

MFA is a feature of Azure AD that must be enabled in your Azure AD tenant. Then, you can configure MFA for your apps. For more information, go to:

- [How it works: Azure AD multi-factor authentication](/azure/active-directory/authentication/concept-mfa-howitworks)
- [Tutorial: Secure user sign-in events with Azure AD multi-factor authentication](/azure/active-directory/authentication/tutorial-enable-azure-mfa)

To get an overview of app protection policies and how they work, go to:

- [Deployment guide: Mobile Application Management (MAM) for unenrolled devices in Microsoft Intune](deployment-guide-enrollment-mamwe.md)
- [Microsoft Intune planning guide](intune-planning-guide.md)
- [App protection policies overview](../apps/app-protection-policy.md)
- [Tutorial: Enable Azure AD multi-factor authentication on apps](/azure/active-directory/authentication/tutorial-enable-azure-mfa)
- [Data protection framework using app protection policies](../apps/app-protection-framework.md)

## Cloud attach with Configuration Manager

Microsoft Configuration Manager helps protect on-premises Windows Server, devices, apps, and data. If you need to manage a combination of cloud and on-premises endpoints, you can cloud attach your Configuration Manager environment to Intune.

There are two steps to cloud attach your on-premises devices:

1. [Tenant attach](/mem/configmgr/tenant-attach/prerequisites): Register your Intune tenant with your Configuration Manager deployment. Your Configuration Manager devices are shown in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). On these devices, you can run different actions, including installing apps and run Windows PowerShell scripts using the web-based admin center.
2. [Co-management](/mem/configmgr/comanage/overview): Manage Windows client devices with Configuration Manager and Microsoft Intune. Some workloads are managed by Configuration Manager, and some workloads are managed by Intune. For example, you can use Configuration Manager to manage Windows updates, and use Intune to manage conditional access policies.

If you currently use Configuration Manager, you get immediate value through tenant attach, and you get more value through co-management.

For guidance on the Microsoft Intune setup that's right for your organization, go to [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md).

## Next steps

- [Planning guide to move to Microsoft Intune](intune-planning-guide.md)
- [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md)
- [Get started with device compliance policies](../protect/device-compliance-get-started.md)
- [What is app management in Microsoft Intune](../apps/app-management.md)
- [Apply features and settings on your devices using device profiles](../configuration/device-profiles.md)
- [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md)
- [Deployment guide: Mobile Application Management (MAM) for unenrolled devices in Microsoft Intune](deployment-guide-enrollment-mamwe.md)
