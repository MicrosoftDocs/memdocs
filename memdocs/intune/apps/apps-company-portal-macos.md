---
# required metadata

title: Add the Company Portal for macOS app
titleSuffix: Microsoft Intune
description: Add the macOS Company Portal app.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/29/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- macOS
- highpri
---

# Add the macOS Company Portal app

To manage devices, install optional apps, and gain access to resources protected by Conditional Access on macOS devices with user affinity, users must install and sign in to the Company Portal app. You can provide instructions to your users to install Company Portal for macOS or install it on devices already enrolled directly from Intune.

You can use any of the following options to install the Company Portal for macOS app:
- [Instruct users to download and install Company Portal](#instruct-users-to-download-and-install-company-portal)
- [Install Company Portal for macOS as a macOS LOB app](#install-company-portal-for-macos-as-a-macos-lob-app)
- [Install Company Portal for macOS by using a macOS Shell Script](#install-company-portal-for-macos-by-using-a-macos-shell-script)

To help keep the apps more secure and up to date once installed, the Company Portal app comes with Microsoft AutoUpdate (MAU).

> [!NOTE]
> The Company Portal app can only be installed automatically on devices using Intune that are already enrolled using direct enrollment or Automated Device Enrollment. For personal device or manual enrollment, the Company Portal app must be downloaded and installed to initiate enrollment. See [Instruct users to download and install Company Portal](#instruct-users-to-download-and-install-company-portal).
## Instruct users to download and install Company Portal

You can instruct users to download, install, and sign in to Company Portal for macOS. For instructions on downloading, installing, and signing into the Company Portal, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

> [!NOTE]
> When you download the Intune Company Portal for macOS devices version 2.18.2107 and later, it installs the new universal version of the app that runs natively on Apple Silicon Macs. The same app will install the x64 version of the app on Intel Mac machines.

## Install Company Portal for macOS as a macOS LOB app

Company Portal for macOS can be downloaded and installed using the [macOS LOB apps](lob-apps-macos.md) feature. The version downloaded is the version that will always be installed and may need to be updated periodically to ensure users get the best experience during initial enrollment.

1. Download Company Portal for macOS from https://go.microsoft.com/fwlink/?linkid=853070. 

2. Follow the instructions to create a macOS LOB app in [macOS LOB apps](lob-apps-macos.md).

> [!NOTE]
> Once installed, the Company Portal for macOS app will automatically update using Microsoft AutoUpdate (MAU).
## Install Company Portal for macOS by using a macOS Shell Script

Company Portal for macOS can be downloaded and installed using the [macOS Shell Scripts](macos-shell-scripts.md) feature. This option will always install the current version of Company Portal for macOS, but will not provide you with application install reporting you might be used to when deploying applications using [macOS LOB apps](lob-apps-macos.md).

1. Download a sample script to install Company Portal for macOS from [Intune Shell Script Samples - Company Portal](/mem/intune/apps/macos-shell-scripts).

2. Follow instructions to deploy the macOS Shell Script using [macOS Shell Scripts](macos-shell-scripts.md). 
    - Set **Run script as signed-in user** to **No** (to run in the system context).
    - Set **Maximum number of retries if script fails** to **3**.

> [!NOTE]
> The script will require Internet access when it runs to download the current version of the Company Portal for macOS. 

## Signing into the Company Portal for macOS when using Setup Assistant with Modern Authentication 

For macOS devices running 10.15 and later, when creating an Automated Device Enrollment profile, you can now choose a new authentication method: **Setup Assistant with modern authentication**. The user has to authenticate using Azure AD credentials during the setup assistant screens. This will require an additional Azure AD login post-enrollment in the Company Portal app to gain access to corporate resources protected by Conditional Access and for Intune to assess device compliance. The Company Portal can be installed in any of the three ways documented here for Setup Assistant with modern authentication. 

Use one of the ways documented above to deploy the macOS Company Portal to the devices enrolling with Setup Assistant with modern authentication so that the end user can authenticate and complete Azure AD registration.

Users must sign into the Company Portal to complete Azure AD authentication and gain access to resources protected by Conditional Access. User affinity is established when users complete the enrollment and reach the home screen of the macOS device. If the tenant has multi-factor authentication turned on for these devices or users, the users will be asked to complete multi-factor authentication during enrollment during Setup Assistant. Multi-factor authentication is not required, but it is available for this authentication method within Conditional Access if needed.

For more information about configuring Setup Assistant with modern authentication for macOS, see [Create an Apple enrollment profile](../enrollment/device-enrollment-program-enroll-macos.md#create-an-apple-enrollment-profile).

## Next steps
- To learn more about assigning apps, see [Assign apps to groups](apps-deploy.md).
- To learn more about configuring Automated Device Enrollment, see [Device Enrollment Program - Enroll macOS](../enrollment/device-enrollment-program-enroll-macos.md).
- To learn more about configuring Microsoft AutoUpdate settings on macOS, see [Mac Updates](/windows/security/threat-protection/microsoft-defender-atp/mac-updates).
