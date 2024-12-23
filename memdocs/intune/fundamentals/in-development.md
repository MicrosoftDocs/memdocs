---
# required metadata

title: In development - Microsoft Intune
description: This article describes Microsoft Intune features that are in development.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 11/26/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
 
# optional metadata

#audience:

ms.reviewer: lebacon
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# In development for Microsoft Intune

To help in your readiness and planning, this article lists Intune UI updates and features that are in development but not yet released. Also:

- If we anticipate that you'll need to take action before a change, we'll publish a complementary post in the Office message center.
- When a feature enters production, whether it's in preview or generally available, the feature description will move from this article to [What's new](whats-new.md).
- Refer to the [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) for strategic deliverables and timelines.

This article and the [What's new](whats-new.md) article are updated periodically. Check back for more updates.

> [!NOTE]
> This article reflects our current expectations about Intune capabilities in an upcoming release. Dates and individual features might change. This article doesn't describe all features in development. It was last updated on the date shown under the title.

You can use RSS to be notified when this article is updated. For more information, see [How to use the docs](../../use-docs.md#notifications).
<!-- **RSS feed**: Find out when this article is updated by copying and pasting the following URL into your feed reader: `https://learn.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us` -->

<!-- Common categories: use this order:
## Microsoft Intune Suite
## App management
## Device configuration
## Device enrollment
## Device management
## Device security
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Tenant administration
## Notices
-->

<!-- ***********************************************-->

## Microsoft Intune Suite

### Use Copilot with Endpoint Privilege Manager to help identify potential elevation risks<!-- 27265509 -->

We’re adding support for Copilot to help you investigate Endpoint Privilege Manager (EPM) elevation details. Copilot will help you evaluate information from you EPM elevation requests to identify potential indicators of compromise by using information from [Microsoft Defender](/defender-endpoint/microsoft-defender-endpoint).

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md). To learn more about how you can use Copilot in Intune, see [Microsoft Copilot in Intune](../copilot/copilot-intune-overview.md).

### Endpoint Privilege Manager elevation rule support for file arguments and parameters<!--28077130 -->

Soon, the file elevation rules for Endpoint Privilege Manager (EPM) will support use of arguments or parameters that you want to allow. Arguments and parameters that aren't explicitly allowed will be blocked from use. This capability helps to improve control of the context for file elevations.

EPM is available as an [Intune Suite add-on-capability](../fundamentals/intune-add-ons.md).

<!-- ***********************************************-->

## App management

### Added protection for iOS/iPadOS app widgets<!-- 14614429 -->

To protect organizational data for MAM managed accounts and apps, Intune app protection policies now provide the capability to block data sync from policy managed app data to app widgets. App widgets can be added to end-user's iOS/iPadOS device lock screen, which can expose data contained by these widgets, such as meeting titles, top sites, and recent notes. In Intune, you'll be able to set the app protection policy setting **Sync policy managed app data with app widgets** to **Block** for iOS/iPadOS apps. This setting will be available as part of the **Data Protection** settings in app protection policies. This new setting will be an app protection feature similar to the **Sync policy managed app data with native app or add-ins** setting.

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device configuration

### Low privileged account for Intune Connector for Active Directory for Hybrid join Autopilot flows<!-- 28662823 -->

We're updating the Intune Connector for Active Directory to use a low privileged account to increase the security of your environment. The old connector will no longer be available for download but will continue to work until deprecation.

For more information, see [Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

<!-- *********************************************** -->

## Device enrollment

### Update to "Determine based on user choice" enrollment type profile behavior <!-- 29068674 iddraft idready idstaged -->

In Intune today, if an IT admin creates a "Determine based on user choice" enrollment type profile for BYOD enrollments, the user will be prompted to select between **I own this device** and **My company owns this device** to direct them to the appropriate enrollment method. Because fewer than 1% of Apple devices across all Intune tenants are currently enrolled this way, this change won't affect most enrolled devices.

Today, selecting **I own this device** results in the user enrolling via profile-based user enrollment with Company Portal to secure only work related apps. With WWDC 2024, Apple ended support for this enrollment method, subsequently Intune also ended support for the same. Read more about the changes here: [Support has ended for Apple profile-based user enrollment with Company Portal](../fundamentals/whats-new.md#support-has-ended-for-apple-profile-based-user-enrollment-with-company-portal)

We are updating the enrollment behavior for users who select **I own this device**. The new behavior for **I own this device** will result in an [account-driven user enrollment](../enrollment/apple-account-driven-user-enrollment.md), which also supports the use of only secure work related apps.

The behavior when selecting **My company owns this device** is unchanged and will continue to result in device enrollment with the Company Portal that supports securing the entire device.

Admin action: 

If you use **Determine based on user choice** enrollment type profile for BYOD scenarios, make sure you have completed the required **PREREQUISITES** to set up account driven user enrollment correctly. See [Set up account driven Apple User Enrollment](../enrollment/apple-account-driven-user-enrollment.md).

If you do not use **Determine based on user choice** enrollment type profile for BYOD scenarios, there are no action items

Applies to:

- iOS/iPadOS

<!-- *********************************************** -->

## Device management  

### Copilot assistant for device query<!-- 26933762 -->

You will soon be able to use Copilot to generate a KQL query to help you get data from across multiple devices in Intune. This capability will be available in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Devices** > **Device query** > **Query with Copilot**.

<!-- *********************************************** -->

## Device security

### Security baselines for HoloLens 2 in public preview<!-- 24914095 -->
 
We’re working to release a public preview of two security baselines for HoloLens 2. These baselines represent Microsoft’s best practice guidelines and experience from deploying and supporting HoloLens 2 devices to customers across various industries.  The baselines include:
 
- **Standard Security Baseline for HoloLens 2**:
  The standard security baseline for HoloLens 2 represents the recommendations for configuring security settings that are applicable to all types of customers irrespective of HoloLens 2 use case scenarios.
 
- **Advanced Security Baseline for HoloLens 2**:
  The advanced security baseline for HoloLens 2 represents the recommendations for configuring security settings for the customers who have strict security controls of their environment and require stringent security policies to be applied to any device used in their environment.  
 
To learn more about security baselines with Intune, see [Use security baselines to configure Windows devices in Intune](../protect/security-baselines.md).

### Linux support for Endpoint detection and response exclusion settings<!-- 26549863 -->

We are adding a new Endpoint Security template under Endpoint detection and response (EDR) for the Linux platform, that will be supported through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario.

The template will support settings related to global exclusion settings. Applicable to antivirus and EDR engines on the client, the settings can configure exclusions to stop associated real time protection EDR alerts for the excluded items. Exclusions can be defined by the file path, folder, or process explicitly defined by the admin in the policy.

Applies to:

- Linux

### New Microsoft Tunnel readiness check for auditd package<!-- 28148207 -->

We're updating the [Microsoft Tunnel readiness tool](../protect/microsoft-tunnel-prerequisites.md#run-the-readiness-tool) to detect if the **auditd** package for Linux System Auditing (LSA) is installed on your Linux Server. When this check is in place, the mst-readiness tool will raise a warning if the audit package isn't installed. Auditing isn't a required prerequisite for the Linux Server, but recommended.

For more information on *auditd* and how to install it on your Microsoft Tunnel server, see [Linux system auditing](../protect/microsoft-tunnel-prerequisites.md#linux-system-auditing).


### Support for Intune Device control policy for devices managed by Microsoft Defender for Endpoint<!-- 15466620 -->

You'll be able to use the endpoint security policy for *Device control* (Attack surface reduction policy) from the Microsoft Intune with the devices you manage through the [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md) capability.

- **Device control** policies are part of endpoint security [Attack surface reduction policy](../protect/endpoint-security-asr-policy.md).

Applies to the following when you use the *Windows 10, Windows 11, and Windows Server* platform:

- Windows 10
- Windows 11

When this change takes effect, devices that are assigned this policy while managed by Defender for Endpoint but not enrolled with Intune, will now apply the settings from the policy. Check your policy to make sure only the devices you intend to receive this policy will get it.

<!-- *********************************************** -->

<!-- ## Intune apps -->

<!-- *********************************************** -->

<!-- ## Role-based access control -->

<!-- *********************************************** -->

## Monitor and troubleshoot

### Device Query for Multiple Devices<!--25234456 -->

We're adding Device query for multiple devices. This feature allows you to gain comprehensive insights about your entire fleet of devices using Kusto Query Language (KQL) to query across collected inventory data for your devices.

Device query for multiple devices will be supported for devices running Windows 10 or later. This feature will be included as part of Advanced Analytics.

Applies to:

- Windows

<!-- *********************************************** -->

<!-- ## Tenant administration -->

<!-- *********************************************** -->

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## See also

For details about recent developments, see [What's new in Microsoft Intune](whats-new.md).
