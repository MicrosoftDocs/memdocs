---
# required metadata

title: Mobile Application Management (MAM) for unenrolled devices in Microsoft Intune
description: Use mobile application management without enrollment to deploy apps, and protect organization data within the apps. Get an overview of the administrator and end user tasks for this enrollment option.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/14/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: 
  - M365-identity-device-management
  - highpri
  - highseo
---

# Deployment guide: Mobile Application Management (MAM) for unenrolled devices in Microsoft Intune

MAM for unenrolled devices uses app configuration profiles to deploy or configure apps on devices without enrolling the device. When combined with app protection policies, you can protect data within an app.

MAM for unenrolled devices is commonly used for personal or bring your own devices (BYOD). Or, used for enrolled devices that need extra security. MAM is an option for users who don't enroll their personal devices, but still need access to organization email, Teams meetings, and more.

MAM is available on the following platforms:

- Android
- iOS/iPadOS

> [!NOTE]
> To deploy or assign apps to Windows devices, the Windows devices must be enrolled in Microsoft Intune. For any additional requirements, including supported app types, go to [Windows 10/11 app deployment using Microsoft Intune](../apps/apps-windows-10-app-deploy.md).

This article provides recommendations on when to use MAM. It also includes an overview of the administrator and user tasks. For more specific information on MAM, see [Microsoft Intune app management](../apps/app-management.md).

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]

## Before you begin

For an overview, including any Intune-specific prerequisites, see [Deployment guidance: Enroll devices in Microsoft Intune](deployment-guide-enrollment.md).

## MAM 

Use for personal or bring your own devices (BYOD). Or, use on organization-owned devices that need specific app configuration, or extra app security.

| Feature | Use this enrollment option when |
| --- | --- |
| You want to configure specifics apps, and control access to these apps, such as Outlook or Microsoft Teams. | ✔️ |
| Devices are personal or BYOD. | ✔️ |
| You have new or existing devices. | ✔️ |
| Need to manage a few devices, or a large number of devices (bulk enrollment). | ✔️ |
| Devices are associated with a single user. | ✔️ |
| Devices are managed by another MDM provider. | ✔️ |
| You use the device enrollment manager (DEM) account. | ✔️ |
| Devices are owned by the organization or school. |  ❌ <br/><br/> Not recommended as the *only* enrollment method for organization-owned devices. Organization-owned devices should be enrolled and managed by Intune. If you want extra security for specific apps, then use enrollment and MAM together. |
| Devices are user-less, such as kiosk, or dedicated device. | ❌ <br/><br/>Typically, user-less or shared devices are organization-owned. These devices should be enrolled and managed by Intune. |

### MAM administrator tasks

This task list provides an overview. For more specific information, see [Microsoft Intune app management](../apps/app-management.md).

- Be sure your devices are [supported](supported-devices-browsers.md).
- In the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), [add your apps](../apps/apps-supported-intune-apps.md) or [configure your apps](../apps/app-configuration-policies-overview.md). When the apps are on the device, the apps are considered "managed" by Intune. After you add or configure the app, create an [app protection policy](../apps/app-protection-policy-settings-ios.md). For example, create a policy that allows or blocks features within the app, such as copy and paste.
- Tell users how to get different apps. For example, you can:

  - Direct users to the Company Portal web site at `portal.manage.microsoft.com`. When they sign in with their organization credentials, they see a list of apps, including required apps. They can get apps from this site.
  - Have users download and install the Company Portal app from the app store. Once authenticated, users can install apps, including required apps.

### MAM end user tasks

The specific tasks depend on how you tell users to install the apps.

- To install the apps, users can:

  - Go to the app store, and download the app.
  - Go to the app store, and download the Company Portal app. The Company Portal app authenticates the user. Open the Company Portal app, and sign in with their organization credentials (`user@contoso.com`). They see a list of available apps, including required apps.
  - Go to the Company Portal web site at `portal.manage.microsoft.com`, and sign in with their organization credentials (`user@contoso.com`). After users sign in, they see a list of available apps, including required apps.

- After the app is installed, they open the app, and are prompted to sign in with their organization credentials (`user@contoso.com`). When users sign in, they may have to restart the app. After the restart, the app data is "managed" by Intune.

- Some platforms may require specific apps to install other apps, such as Outlook or Teams. For example, on iOS devices, users must install a broker app, such as the Microsoft Authenticator app. On Android devices, users must install the Company Portal app.

## Next steps

- [Android enrollment guide](deployment-guide-enrollment-android.md)
- [iOS/iPadOS enrollment guide](deployment-guide-enrollment-ios-ipados.md)
- [Linux enrollment guide](deployment-guide-enrollment-linux.md)
- [macOS enrollment guide](deployment-guide-enrollment-macos.md)
- [Windows enrollment guide](deployment-guide-enrollment-windows.md)
