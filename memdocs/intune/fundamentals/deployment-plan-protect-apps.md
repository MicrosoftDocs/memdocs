---
# required metadata

title: Add, configure, and protect apps with Intune
titleSuffix: Microsoft Intune
description: Add, configure, and protect apps with Intune.
author: erikre
ms.author: erikre
manager: dougeby
ms.date: 12/02/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite:
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: 
  - M365-identity-device-management 
  - highpri
---
# Step 2 - Add, configure, and protect apps with Intune

Managing applications on devices in your organization is a central part to a secure and productive enterprise ecosystem. You can use Microsoft Intune to manage the apps that your company's workforce uses. By managing apps, you help control which apps your company uses, as well as the configuration and protection of the apps. This functionality is called mobile application management (MAM). MAM in Intune is designed to protect organization data at the application level, including custom apps and store apps. App management can be used on organization-owned devices and personal devices. When it is used with personal devices, only organization-related access and data is managed. This type of app management is called MAM without enrollment (MAM-WE), or from a end-user perspective, bring your own device (BYOD).

## MAM configurations

Microsoft Endpoint Manager supports two MAM configurations:
- **MAM without device management**: MAM without device enrollment, or MAM-WE, allows IT administrators to manage apps using MAM and app protection policies on devices not enrolled with Intune MDM. This means apps can be managed by Intune on devices enrolled with third-party EMM providers. To manage apps using MAM-WE, customers should use the Intune console in the Microsoft Endpoint Manager admin center. Also, apps can be managed by Intune on devices enrolled with third-party enterprise mobility management (EMM) providers or not enrolled with an MDM at all.
- **MAM with MEM**: IT administrators can only manage apps using MAM and app protection policies on devices that are enrolled with Intune mobile device management (MDM). To manage apps using MDM + MAM, customers should use the Intune console in the Microsoft Endpoint Manager admin center.

When apps are managed in Intune, administrators can do the following:
- **Protect company data at the app level.** You can add and assign mobile apps to user groups and devices. This allows your company data to be protected at the app level. You can protect company data on both managed and unmanaged devices because mobile app management doesn't require device management. The management is centered on the user identity, which removes the requirement for device management.
- **Configure apps to start or run with specific settings enabled.** In addition, you can update existing apps already on the device.
- **Assign policies to limit access and prevent data from being used outside your organization.** You choose the setting for these policies based on your organization's requirements. For example, you can:
  - Require a PIN to open an app in a work context.
  - Control the sharing of data between apps.
  - Prevent the saving of company app data to a personal storage location.
- **Support apps on a variety of platforms and operating systems.** Each platform is different. Intune and Configuration Manager provides available settings specifically for each supported platform.
- **See reports about which apps are used, and track their usage.** In addition, Intune and Configuration Manager provides endpoint analytics to help you assess and resolve problems.
- **Do a selective wipe by removing only organization data from apps.**
- **Ensure personal data is kept separate from managed data.** End-user productivity isn't affected and policies don't apply when using the app in a personal context. The policies are applied only in a work context, which gives you the ability to protect company data without touching personal data.

### MAM without device management

Mobile Application Management (MAM) app protection policies allows you to manage and protect your organization's data within an application. Many productivity apps, such as the Microsoft Office apps, can be managed by Intune MAM. See the official list of Microsoft Intune protected apps available for public use.

Your employees use mobile devices for both personal and work tasks. While making sure your employees can be productive, you want to prevent data loss, intentional and unintentional. You'll also want to protect company data that is accessed from devices that are not managed by you.

You can use Intune app protection policies independent of any mobile-device management (MDM) solution. This independence helps you protect your company's data with or without enrolling devices in a device management solution. By implementing app-level policies, you can restrict access to company resources and keep data within the purview of your IT department.

### MAM with MEM

MDM, in addition to MAM, makes sure that the device is protected. For example, you can require a PIN to access the device, or you can deploy managed apps to the device. You can also deploy apps to devices through your MDM solution, to give you more control over app management.

There are additional benefits to using MDM with App protection policies, and companies can use App protection policies with and without MDM at the same time. For example, consider an employee that uses both a phone issued by the company, and their own personal tablet. The company phone is enrolled in MDM and protected by App protection policies while the personal device is protected by App protection policies only.

If you apply a MAM policy to the user without setting the device state, the user will get the MAM policy on both the BYOD device and the Intune-managed device. You can also apply a MAM policy based on the managed state. So when you create an app protection policy, next to Target to all app types, you'd select No. Then do any of the following:

Apply a less strict MAM policy to Intune managed devices, and apply a more restrictive MAM policy to non MDM-enrolled devices.
Apply a MAM policy to unenrolled devices only.

## Add apps to Intune

The first step when providing apps to your organization is to add the apps to Intune before assigning them to devices or users from Intune. While you can work with many different app types, the basic procedures are the same. With Intune, you can add different app types, including apps written in-house (line-of-business), apps from the store, apps that are built in, and apps on the web.

The users of apps and devices at your company (your company's workforce) might have several app requirements. Before adding apps to Intune and making them available to your workforce, you may find it helpful to assess and understand a few app fundamentals. There are various types of apps that are available for Intune. You must determine app requirements that are needed by the users at your company, such as the platforms and capabilities that your workforce needs. You must determine whether to use Intune to manage the devices (including apps) or have Intune manage the apps without managing the devices. Also, you must determine the apps and capabilities that your workforce needs, and who needs them. The information in this article helps you get started.

Before adding apps to Intune, consider reviewing the support app types and assess your app requirements. For more information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

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

For more information about app configuration, see [App configuration policies for Microsoft Intune](/mem/intune/apps/app-configuration-policies-overview?azure-portal=true) and [Plan for and configure application management in Configuration Manager](/mem/configmgr/apps/plan-design/plan-for-and-configure-application-management?azure-portal=true).

## Protect apps using Intune

One of the primary ways that Intune provides mobile app security is through policies. App protection policies allow you to do the following actions:
- Use Azure AD identity to isolate organization data from personal data. So personal information is isolated from organizational IT awareness. Data accessed using organization credentials are given additional security protection.
- Help secure access on personal devices by restricting actions users can take with organizational data, such as copy-and-paste, save, and view.
- Create and deploy on devices that are enrolled in Intune, enrolled in another mobile device management (MDM) service, or not enrolled in any MDM service. 

> [!NOTE]
> App protection policies are designed to apply uniformly across a group of apps, such as applying a policy across all Office mobile apps. 

Organizations can use app protection policies with and without MDM at the same time. For example, consider an employee that uses both a tablet issued by the company, and their own personal phone. The company tablet is enrolled in MDM and protected by app protection policies while their personal phone is protected by app protection policies only.

### Apps without management

When apps are used without restrictions, company and personal data can get intermingled. Company data can end up in locations like personal storage or transferred to apps beyond your purview and result in data loss. One of the primary reasons to use either **MAM without device enrollment** or **Intune MDM + MAM** is to help protect your organization's data.

## App management without device management

This scenario allows you to manage the apps that your organization uses without enrolling the devices (that contain the apps) to be managed.  

You can use App protection policies to prevent company data from saving to the local storage of the device. You can also restrict data movement to other apps that aren't protected by App protection policies. App protection policy settings include:
- Data relocation policies like  **Save copies of org data**, and **Restrict cut, copy, and paste**.
- Access policy settings like **Require simple PIN for access**, and **Block managed apps from running on jailbroken or rooted devices**.

For BYOD devices not enrolled in any MDM solution, app protection policies can help protect company data at the app level.
However, there are some limitations to be aware of, such as:
- You can't deploy apps to the device. The end user has to get the apps from the store.
- You can't provision certificate profiles on these devices.
- You can't provision company Wi-Fi and VPN settings on these devices.

For more information about app protection in Intune, see [App protection policies overview](/mem/intune/apps/app-protection-policy?azure-portal=true).

### App management with device management

This scenario allows you to manage the apps that your organization uses with the added benefit of enrolling the devices to be managed.  

On enrolled devices that use an MDM service, app protection policies can add an extra layer of protection. For example, a user signs in to a device with their organization credentials. Their organization identity allows access to data that's tied to their personal identity. As that organization data is used, app protection policies control how the data is saved and shared. When users sign in with their personal identity, those same protections (access and restrictions) aren't applied. In this way, IT has control of organization data, while end users maintain control and privacy over their personal data.

The MDM solution adds value by providing the following:
- Enrolls the device
- Deploys the apps to the device
- Provides ongoing device compliance and management

The App protection policies add value by providing the following:
- Help protect company data from leaking to consumer apps and services
- Apply restrictions like *save-as*, *clipboard*, or *PIN*, to client apps
- Wipe company data when needed from apps without removing those apps from the device

## Apps you can manage with Intune

Any app that has been integrated with the [Intune SDK](../developer/app-sdk.md) or wrapped by the [Intune App Wrapping Tool](../developer/apps-prepare-mobile-application-management.md) can be managed using Intune app protection policies. See the official list of [Microsoft Intune protected apps](apps-supported-intune-apps.md) that have been built using these tools and are available for public use.

The Intune SDK development team actively tests and maintains support for apps built with the native Android, iOS/iPadOS (Obj-C, Swift), Xamarin, and Xamarin.Forms platforms. While some customers have had success with Intune SDK integration with other platforms such as React Native and NativeScript, we do not provide explicit guidance or plugins for app developers using anything other than our supported platforms.

## End-user requirements to used managed apps

The following list provides the end-user requirements to use app protection policies on an Intune-managed app:

- The end user must have an Azure Active Directory (Azure AD) account. See [Add users and give administrative permission to Intune](../fundamentals/users-add.md) to learn how to create Intune users in Azure Active Directory.
- The end user must have a license for Microsoft Intune assigned to their Azure Active Directory account. See [Manage Intune licenses](../fundamentals/licenses-assign.md) to learn how to assign Intune licenses to end users.
- The end user must belong to a security group that is targeted by an app protection policy. The same app protection policy must target the specific app being used. App protection policies can be created and deployed in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Security groups can currently be created in the [Microsoft 365 admin center](https://admin.microsoft.com).
- The end user must sign into the app using their Azure AD account.