---
# required metadata

title: Add, configure, and protect apps with Intune
titleSuffix: Microsoft Intune
description: Add, configure, and protect apps with Intune.
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/16/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite:
search.appverid: MET150
ms.custom: 
ms.collection: 
- M365-identity-device-management 
- highpri
- tier1
---
# Step 2 - Add, configure, and protect apps with Intune

The next step when deploying Intune is to add and protect apps that access organization data.

:::image type="content" source="./media/deployment-plan-protect-apps/deployment-plan-add-apps.png" alt-text="Diagram that shows getting started with Microsoft Intune with step 2, which is adding and protect apps using Microsoft Intune.":::

Managing applications on devices in your organization is a central part to a secure and productive enterprise ecosystem. You can use Microsoft Intune to manage the apps that your company's workforce uses. By managing apps, you help control which apps your company uses, as well as the configuration and protection of the apps. This functionality is called mobile application management (MAM). MAM in Intune is designed to protect organization data at the application level, including custom apps and store apps. App management can be used on organization-owned devices and personal devices. When it is used with personal devices, only organization-related access and data is managed. This type of app management is called MAM without enrollment, or from an end-user perspective, bring your own device (BYOD).

## MAM configurations

When apps are used without restrictions, company and personal data can get intermingled. Company data can end up in locations like personal storage or transferred to apps beyond your purview and result in data loss. One of the primary reasons to use either **MAM without device enrollment** or **Intune MDM + MAM** is to help protect your organization's data.

Microsoft Intune supports two MAM configurations:

- **[MAM without device management](#mam-without-device-management)**
- **[MAM with device management](#mam-with-device-management)**

### MAM without device management

This configuration allows your organization's apps to be managed by Intune, but doesn't enroll the devices to be managed by Intune. This configuration is commonly referred to as **MAM without device enrollment**. IT administrators can manage apps using MAM by using Intune configuration and protection policies on devices not enrolled with Intune mobile-device management (MDM).

> [!NOTE]
> This configuration includes managing apps with Intune on devices enrolled with third-party enterprise mobility management (EMM) providers. You can use Intune app protection policies independent of any MDM solution. This independence helps you protect your company's data with or without enrolling devices in a device management solution. By implementing app-level policies, you can restrict access to company resources and keep data within the purview of your IT department.

Mobile Application Management (MAM) is ideal to help protect organization data on mobile devices used by members of your organization for both personal and work tasks. While making sure your members of your organization can be productive, you want to prevent data loss, intentional and unintentional. You also want to protect company data that is accessed from devices that are not managed by you. MAM allows you to manage and protect your organization's data within an application.

> [!TIP]
> Many productivity apps, such as the Microsoft Office apps, can be managed by Intune MAM. See the official list of [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md) available for public use.

For BYOD devices not enrolled in any MDM solution, app protection policies can help protect company data at the app level.
However, there are some limitations to be aware of, such as:

- You can't deploy apps to the device. The end user has to get the apps from the store.
- You can't provision certificate profiles on these devices.
- You can't provision company Wi-Fi and VPN settings on these devices.

For more information about app protection in Intune, see [App protection policies overview](../apps/app-protection-policy.md).

### MAM with device management

This configuration allows your organization's apps and devices to be managed. This configuration is commonly referred to as **MAM + MDM**. IT administrators can manage apps using MAM on devices that are enrolled with Intune MDM.

MDM, in addition to MAM, makes sure that the device is protected. For example, you can require a PIN to access the device, or you can deploy managed apps to the device. You can also deploy apps to devices through your MDM solution, to give you more control over app management.

There are additional benefits to using MDM with app protection policies, and companies can use app protection policies with and without MDM at the same time. For example, a member of your organization could have both a phone issued by the company and their own personal tablet. The company phone could be enrolled in MDM and protected by app protection policies while the personal device is protected by app protection policies only.

On enrolled devices that use an MDM service, app protection policies can add an extra layer of protection. For example, a user signs in to a device with their organization credentials. As that organization data is used, app protection policies control how the data is saved and shared. When users sign in with their personal identity, those same protections (access and restrictions) aren't applied. In this way, IT has control of organization data, while end users maintain control and privacy over their personal data.

The MDM solution adds value by providing the following:

- Enrolls the device
- Deploys the apps to the device
- Provides ongoing device compliance and management

The App protection policies add value by providing the following:

- Help protect company data from leaking to consumer apps and services
- Apply restrictions like *save-as*, *clipboard*, or *PIN*, to client apps
- Wipe company data when needed from apps without removing those apps from the device

### Benefits of MAM with Intune

When apps are managed in Intune, administrators can do the following:

- **Protect company data at the app level.** You can add and assign mobile apps to user groups and devices. This allows your company data to be protected at the app level. You can protect company data on both managed and unmanaged devices because mobile app management doesn't require device management. The management is centered on the user identity, which removes the requirement for device management.
- **Configure apps to start or run with specific settings enabled.** In addition, you can update existing apps already on the device.
- **Assign policies to limit access and prevent data from being used outside your organization.** You choose the setting for these policies based on your organization's requirements. For example, you can:
  - Require a PIN to open an app in a work context.
  - Block managed apps from running on jailbroken or rooted devices
  - Control the sharing of data between apps.
  - Prevent the saving of company app data to a personal storage location by using data relocation policies, like **Save copies of org data**, and **Restrict cut, copy, and paste**.
- **Support apps on a variety of platforms and operating systems.** Each platform is different. Intune provides available settings specifically for each supported platform.
- **See reports about which apps are used, and track their usage.** In addition, Intune provides endpoint analytics to help you assess and resolve problems.
- **Do a selective wipe by removing only organization data from apps.**
- **Ensure personal data is kept separate from managed data.** End-user productivity isn't affected and policies don't apply when using the app in a personal context. The policies are applied only in a work context, which gives you the ability to protect company data without touching personal data.

## Add apps to Intune

The first step when providing apps to your organization is to add the apps to Intune before assigning them to devices or users from Intune. While you can work with many different app types, the basic procedures are the same. With Intune, you can add different app types, including apps written in-house (line-of-business), apps from the store, apps that are built in, and apps on the web.

The users of apps and devices at your company (your company's workforce) might have several app requirements. Before adding apps to Intune and making them available to your workforce, you may find it helpful to assess and understand a few app fundamentals. There are various types of apps that are available for Intune. You must determine app requirements that are needed by the users at your company, such as the platforms and capabilities that your workforce needs. You must determine whether to use Intune to manage the devices (including apps) or have Intune manage the apps without managing the devices. Also, you must determine the apps and capabilities that your workforce needs, and who needs them. The information in this article helps you get started.

Before adding apps to Intune, consider reviewing the support app types and assess your app requirements. For more information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

> [!TIP]
> To better understand app types, app purchases, and app licenses for Intune, see the solution [Purchase and add apps for Microsoft Intune](/microsoft-365/solutions/apps-guide-overview?toc=%2Fmem%2Fintune%2Ftoc.json&bc=%2Fmem%2Fintune%2Fbreadcrumb%2Ftoc.json). This solution content also provides recommended steps to assess app requirements, create app categories, purchases apps, and add apps. Additionally, this solution content explains how to manage apps and app licenses.

### Add Microsoft apps

Intune includes a number of Microsoft apps based on the Microsoft license that you use for Intune. To learn more about the different Microsoft enterprise licenses available that include Intune, see [Microsoft Intune licensing](licenses.md). To compare the different Microsoft apps that are available with Microsoft 365, see the [licensing options available with Microsoft 365](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans). To see all the options for each plan (including the available Microsoft apps), download the full [Microsoft subscription comparison table](https://go.microsoft.com/fwlink/?linkid=2139145) and locate the plans that include Microsoft Intune.

One of the available app types is Microsoft 365 apps for Windows 10 devices. By selecting this app type in Intune, you can assign and install Microsoft 365 apps to devices you manage that run Windows 10. You can also assign and install apps for the Microsoft Project Online desktop client and Microsoft Visio Online Plan 2, if you own licenses for them. The available Microsoft 365 apps are displayed as a single entry in the list of apps in the Intune console within Azure.

Add the following core Microsoft apps to Intune:

- Microsoft Edge
- Microsoft Excel
- Microsoft Office
- Microsoft OneDrive
- Microsoft OneNote
- Microsoft Outlook
- Microsoft PowerPoint
- Microsoft SharePoint
- Microsoft Teams
- Microsoft To Do
- Microsoft Word

For more information about adding Microsoft apps to Intune, go to the following topics:

- [Add apps to Microsoft Intune](../apps/apps-add.md)
- [Add Microsoft 365 Apps to Windows 10/11 devices with Microsoft Intune](../apps/apps-add-office365.md)

### Add store apps (optional)

Many of the standard store apps displayed within the Intune console are freely available for you to add and deploy to members of your organization. In addition, you can purchase store apps for each device platform.

The following table provides the different categories available for store apps:

| Store   app category | Description |
|---|---|
| Free store apps | You can freely add these apps to Intune and deploy them to the members of your organization. These apps do not require any additional cost to use.   |
| Purchased apps | You must purchase licenses for these apps before adding to Intune. Each device platform (Windows, iOS, Android) offers a standard method to purchase licenses for these apps. Intune provides methods to manage the app license for each end user.  |
| Apps requiring an account, subscription, or license from the app developer | You can freely add and deploy these apps from Intune, however the app may require an account, subscription, or license from the app vendor. For a list of apps that support Intune management functionality, see [Partner productivity apps](../apps/apps-supported-intune-apps.md#partner-productivity-apps) and [Partner UEM apps](../apps/apps-supported-intune-apps.md#partner-uem-apps). <b>**NOTE:** For apps that may require an account, subscription, or license, you must contact the app vendor for specific app details.   |
| Apps included with your Intune license | The license you use with Microsoft Intune may include the app licenses you require.  |

> [!NOTE]
> In addition to purchasing app licenses, you can create Intune policies that allow end users to add personal accounts to their devices to purchase unmanaged apps.

For more information about adding Microsoft apps to Intune, go to the following topics:

- [Add Microsoft Store apps to Microsoft Intune](../apps/store-apps-microsoft.md)
- [Add iOS store apps to Microsoft Intune](../apps/store-apps-ios.md)
- [Add Android store apps to Microsoft Intune](../apps/store-apps-android.md)

## Configure apps using Intune

App configuration policies can help you eliminate app setup problems by letting you select configuration settings for a policy. That policy is then assigned to end users before they run a specific app. The settings are then supplied automatically when the app is configured on the end user's device. End users don't need to take action. The configuration settings are unique for each app.

You can create and use app configuration policies to provide configuration settings for both iOS/iPadOS or Android apps. These configuration settings allow an app to be customized by using app configuration and management. The configuration policy settings are used when the app checks for these settings, typically the first time the app is run.

An app configuration setting, for example, might require you to specify any of the following details:

- A custom port number
- Language settings
- Security settings
- Branding settings such as a company logo

If end users were to enter these settings instead, they could do this incorrectly. App configuration policies can help provide consistency across an enterprise and reduce helpdesk calls from end users trying to configure settings on their own. By using app configuration policies, the adoption of new apps can be easier and quicker.

The available configuration parameters are ultimately decided by the developers of the app. Documentation from the application vendor should be reviewed to see if an app supports configuration and what configurations are available. For some applications, Intune will populate the available configuration settings.

For more information about app configuration, go to the following topics:

- [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md)
- [Add app configuration policies for managed iOS/iPadOS devices](../apps/app-configuration-policies-use-ios.md)
- [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md)

### Configure Microsoft Outlook

The Outlook for iOS and Android app is designed to enable users in your organization to do more from their mobile devices, by bringing together email, calendar, contacts, and other files.

The richest and broadest protection capabilities for Microsoft 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Microsoft Entra ID P1 or P2 features, such as Conditional Access. At a minimum, you will want to deploy a Conditional Access policy that allows connectivity to Outlook for iOS and Android from mobile devices and an Intune app protection policy that ensures the collaboration experience is protected.

For more information about configuring Microsoft Outlook, go to the following topic:

- [Manage messaging collaboration access by using Outlook for iOS and Android with Microsoft Intune](../apps/app-configuration-policies-outlook.md)

### Configure Microsoft Edge

Edge for iOS and Android is designed to enable users to browse the web and supports multi-identity. Users can add a work account, as well as a personal account, for browsing. There is complete separation between the two identities, which is like what is offered in other Microsoft mobile apps.

For more information about configuring Microsoft Edge, go to the following topic:

- [Manage Microsoft Edge on iOS and Android with Intune](../apps/manage-microsoft-edge.md)

### Configure VPN

Virtual private networks (VPN) allow users to access organization resources remotely, including from home, hotels, cafes, and more. In Microsoft Intune, you can configure VPN client apps on Android Enterprise devices using an app configuration policy. Then, deploy this policy with its VPN configuration to devices in your organization.

You can also create VPN policies that are used by specific apps. This feature is called per-app VPN. When the app is active, it can connect to the VPN, and access resources through the VPN. When the app isn't active, the VPN isn't used.

For more information about configuring email, go to the following topic:

- [Use a VPN and per-app VPN policy on Android Enterprise devices in Microsoft Intune](../apps/app-configuration-vpn-ae.md)

## Protect apps using Intune

App protection policies (APP) are rules that ensure an organization's data remains safe or contained in a managed app. A policy can be a rule that is enforced when the user attempts to access or move "corporate" data, or a set of actions that are prohibited or monitored when the user is inside the app. A managed app is an app that has app protection policies applied to it, and can be managed by Intune.

Mobile Application Management (MAM) app protection policies allows you to manage and protect your organization's data within an application. Many productivity apps, such as the Microsoft Office apps, can be managed by Intune MAM. See the official list of Microsoft Intune protected apps available for public use.

One of the primary ways that Intune provides mobile app security is through policies. App protection policies allow you to do the following actions:

- Use Microsoft Entra identity to isolate organization data from personal data. So personal information is isolated from organizational IT awareness. Data accessed using organization credentials are given additional security protection.
- Help secure access on personal devices by restricting actions users can take with organizational data, such as copy-and-paste, save, and view.
- Create and deploy on devices that are enrolled in Intune, enrolled in another mobile device management (MDM) service, or not enrolled in any MDM service.

> [!NOTE]
> App protection policies are designed to apply uniformly across a group of apps, such as applying a policy across all Office mobile apps.

Organizations can use app protection policies with and without MDM at the same time. For example, consider an employee that uses both a tablet issued by the company, and their own personal phone. The company tablet is enrolled in MDM and protected by app protection policies while their personal phone is protected by app protection policies only.

For more information about app protection in Intune, go to the following topics:

- [App protection policies overview](../apps/app-protection-policy.md)
- [How to create and assign app protection policies](../apps/app-protection-policies.md).

### Levels of app protection

As more organizations implement mobile device strategies for accessing work or school data, protecting against data leakage becomes paramount. Intune's mobile application management solution for protecting against data leakage is App Protection Policies (APP). APP are rules that ensure an organization's data remains safe or contained in a managed app, regardless of whether the device is enrolled.

When configuring App Protection Policies, the different settings and options available allow organizations to customize the protection to their specific needs. Due to this flexibility, it may not be obvious which permutation of policy settings are required to implement a complete scenario. To help organizations prioritize client endpoint hardening endeavors, Microsoft has introduced a new taxonomy for [security configurations in Windows 10](https://aka.ms/secconframework), and Intune is leveraging a similar taxonomy for its APP data protection framework for mobile app management.  

The APP data protection configuration framework is organized into three distinct configuration scenarios:

- Level 1 enterprise basic data protection – Microsoft recommends this configuration as the minimum data protection configuration for an enterprise device.

- Level 2 enterprise enhanced data protection – Microsoft recommends this configuration for devices where users access sensitive or confidential information. This configuration is applicable to most mobile users accessing work or school data. Some of the controls may impact user experience.

- Level 3 enterprise high data protection – Microsoft recommends this configuration for devices run by an organization with a larger or more sophisticated security team, or for specific users or groups who are at uniquely high risk (users who handle highly sensitive data where unauthorized disclosure causes considerable material loss to the organization). An organization likely to be targeted by well-funded and sophisticated adversaries should aspire to this configuration.

#### Basic app protection (level 1)

Basic app protection in Intune (level 1) is the minimum data protection configuration for an enterprise mobile device. This configuration replaces the need for basic Exchange Online device access policies by requiring a PIN to access work or school data, encrypting the work or school account data, and providing the capability to selectively wipe the school or work data. However, unlike Exchange Online device access policies, the below App Protection Policy settings apply to all the apps selected in the policy, thereby ensuring data access is protected beyond mobile messaging scenarios.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users and mirror the default data protection and access requirements settings when creating an App Protection Policy within Microsoft Intune.

For specific data protection, access requirements, and conditional launch settings for basic app protection, go to the following topic:

- [Level 1 enterprise basic data protection](../apps/app-protection-framework.md#level-1-enterprise-basic-data-protection).

#### Enhanced app protection (level 2)

Enhanced app protection in Intune (level 2) is the data protection configuration recommended as a standard for devices where users access more sensitive information. These devices are a natural target in enterprises today. These recommendations do not assume a large staff of highly skilled security practitioners, and therefore should be accessible to most enterprise organizations. This configuration expands upon the configuration in Level 1 by restricting data transfer scenarios and by requiring a minimum operating system version.

The policy settings enforced in level 2 include all the policy settings recommended for level 1 but only lists those settings below that have been added or changed to implement more controls and a more sophisticated configuration than level 1. While these settings may have a slightly higher impact to users or to applications, they enforce a level of data protection more commensurate with the risks facing users with access to sensitive information on mobile devices.

For specific data protection and conditional launch settings for enhanced app protection, go to the following topic:

- [Level 2 enterprise enhanced data protection](../apps/app-protection-framework.md#level-2-enterprise-enhanced-data-protection).

#### High app protection (level 3)

High app protection for Intune (level 3) is the data protection configuration recommended as a standard for organizations with large and sophisticated security organizations, or for specific users and groups who will be uniquely targeted by adversaries. Such organizations are typically targeted by well-funded and sophisticated adversaries, and as such merit the additional constraints and controls described. This configuration expands upon the configuration in Level 2 by restricting additional data transfer scenarios, increasing the complexity of the PIN configuration, and adding mobile threat detection.

The policy settings enforced in level 3 include all the policy settings recommended for level 2 but only lists those settings below that have been added or changed to implement more controls and a more sophisticated configuration than level 2. These policy settings can have a potentially significant impact to users or to applications, enforcing a level of security commensurate with the risks facing targeted organizations.

For specific data protection, access requirements, and conditional launch settings for basic app protection, go to the following topic:

- [Level 3 enterprise high data protection](../apps/app-protection-framework.md#level-3-enterprise-high-data-protection).

### Protect Exchange Online email on managed devices

You can use device compliance policies with Conditional Access to make sure that your organization's devices can access Exchange Online email only if they're managed by Intune and using an approved email app. You can create an Intune device compliance policy to set the conditions that a device must meet to be considered compliant. You can also create a Microsoft Entra Conditional Access policy that requires devices to enroll in Intune, comply with Intune policies, and use the approved Outlook mobile app to access Exchange Online email.

For more information about protecting Exchange Online, go to the following topic:

- [Tutorial: Protect Exchange Online email on managed devices](../protect/tutorial-protect-email-on-enrolled-devices.md)

### End-user requirements to use app protection policies

The following list provides the end-user requirements to use app protection policies on apps managed by Intune include the following:

- The end user must have a Microsoft Entra account. See [Add users and give administrative permission to Intune](users-add.md) to learn how to create Intune users in Microsoft Entra ID.
- The end user must have a license for Microsoft Intune assigned to their Microsoft Entra account. See [Manage Intune licenses](licenses-assign.md) to learn how to assign Intune licenses to end users.
- The end user must belong to a security group that is targeted by an app protection policy. The same app protection policy must target the specific app being used. App protection policies can be created and deployed in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Security groups can currently be created in the [Microsoft 365 admin center](https://admin.microsoft.com).
- The end user must sign into the app using their Microsoft Entra account.

## Follow the minimum recommended baseline policies

1. [Set up Microsoft Intune](deployment-plan-setup.md)
2. 🡺 **Add, configure, and protect apps** (*You are here*)
3. [Plan for compliance policies](deployment-plan-compliance-policies.md)
4. [Configure device features](deployment-plan-configuration-profile.md)
5. [Enroll devices](deployment-guide-enroll.md)
