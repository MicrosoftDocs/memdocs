---
# required metadata

title: Mobile Application Management for Microsoft Edge on unmanaged Windows devices
titleSuffix: 
description: Use Microsoft Edge on personal Windows devices to enable protected MAM access to org data.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/06/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- Windows
- highpri
ms.custom: intune-azure
---

# Data protection for Windows MAM
<!-- Use Mobile Application Management on unmanaged Windows  -->

You can enable protected Mobile Application Management (MAM) access to org data on personal Windows devices. This capability uses the following functionality:
- Intune Application Configuration Policies (ACP) to customize the org user experience
- Intune Application Protection Policies (APP) to secure org data and ensure the client device is healthy
- Windows Security Center client threat defense integrated with Intune APP to detect local health threats on personal Windows devices
- Application Protection Conditional Access to ensure the device is protected and healthy before granting protected service access via Entra ID (AAD)

> [!NOTE]
> For more information about MAM, see [Mobile Application Management (MAM) basics](../apps/app-management.md#mobile-application-management-mam-basics).

Both end-users and organizations need to have protected organizational access from personal devices. Organizations need to ensure that corporate data is protected on personal, unmanaged devices. As an Intune admin, you have the responsibility to determine how members (end-users) of your organization access corporate resources in a protected way from an unmanaged device. You need to ensure when accessing organizational data, that the unmanaged devices are healthy, the applications adhere to your organization data's protection policies, and that the end-user’s unmanaged assets on their device aren't impacted by your organization's policies. 

As the Intune admin, you need to have the following app management functionality:
- Ability to deploy app protection policies to apps/users protected by the Intune APP SDK, including the following:
    - Data protection settings 
    - Health Checks (aka Conditional Launch) settings 
- Ability to require app protection policies via Conditional Access  
- Ability to perform additional client health verification via Windows Security center by doing the following:
    - Designating Windows Security Center risk level for allowing end users to access corporate resources
    - Setting up tenant-based connector to Microsoft Intune for Windows Security Center
- Ability to deploy a selective wipe command to protected applications

Members of your organization (end-users) expect to have the following functionality for their accounts:
- Ability to log in to Entra ID (AAD) to access sites protected by Conditional Access 
- Ability to verify health status of the client device, in the case where a device is considered unhealthy 
- Ability to have access revoked to resources when a device remains unhealthy 
- Ability to be informed, with clear remediation steps, when access is controlled by an administrator policy 

> [!NOTE]
> For information related to Entra ID (AAD), see [Require an app protection policy on Windows devices](/azure/active-directory/conditional-access/how-to-app-protection-policy-windows).

## Conditional Access Compliance 
Preventing data loss is a part of protecting your organizational data. Data loss prevention (DLP) is only effective if your org data cannot be accessed from any unprotected system or device. App Protection Conditional Access uses Conditional Access (CA) to ensure App Protection Policies (APP) are supported and enforced in a client application before allowing access to protected resources (such as org data).  APP CA will allow end-users with personal Windows devices to use APP managed applications, including Microsoft Edge, to access Entra ID (AAD) resources without fully managing their personal device.

This MAM service syncs compliance state per user, per app, and per device to the Entra ID (AAD) CA service. This includes the threat information received from the Mobile Threat Defense (MTD) vendors starting with Windows Security Center.

> [!NOTE]
> This MAM service uses the same conditional access compliance workflow that is used to [manage Microsoft Edge on iOS and Android devices](../apps/manage-microsoft-edge.md).

When a change is detected, the MAM service updates the device compliance state immediately. The service also includes MTD health state as part of the compliance state.

> [!NOTE]
> The MAM service evaluates the MTD state in the service. This is done independently from the MAM client and client platform.

The MAM Client communicates the client heath state (or health metadata) to the MAM Service upon check-in. The health state includes any failure of APP Health Checks for **Block** or **Wipe** conditions. In addition, AAD guides end-users through remediation steps when they attempt to access a blocked CA resource.

### Conditional Access Compliance
Organizations can use Entra ID (AAD) Conditional Access policies to ensure that users can only access work or school content using policy managed applications on Windows. To do this, you'll need a conditional access policy that targets all potential users. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection).

Follow the steps in [Require approved client apps or app protection policy with mobile devices](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection#require-approved-client-apps-or-app-protection-policy-with-mobile-devices), which allows Microsoft Edge for Windows, but blocks other mobile device web browsers from connecting to Microsoft 365 endpoints.

>[!NOTE]
> This policy ensures mobile users can access all Microsoft 365 endpoints from within Edge for Windows. This policy also prevents users from using InPrivate to access Microsoft 365 endpoints.

With Conditional Access, you can also target on-premises sites that you have exposed to external users via the [Entra ID (AAD) Application Proxy](/azure/active-directory/active-directory-application-proxy-get-started).

> [!NOTE]
> To leverage app-based conditional access policies, the Microsoft Authenticator app must be installed on Windows devices. For more information, see [App-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md).

## Threat Defense Health

The health status of a personal owned device is verified before allowing access to your org data. MAM threat detection can be connected with Windows Security Center. Windows Security Center provides a client device health assessment to Intune APP via a service-to-service connector. This assessment supports gating of the flow and access to org data on personal unmanaged devices.

The health state includes the following details:
- User, app, and device identifiers
- A predefined health state
- The time of last health state update

The health state is only sent for MAM enrolled users.  End users may stop sending data by signing out of their org account in protected applications.  Administrators may stop sending data by removing the Windows Security Connector from Microsoft Intune.

## Create Intune app protection policies

App Protection Policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario.

As an admin, you can configure how data is protected through APP. This configuration applies to the native Windows application interaction with the data. APP settings are segmented into three categories:
-	**Data Protection** - These settings control how data can move into and out of an org context (account, document, location, services) for the user.
<!-- -	**Access** - These settings control how the user must verify their identity before interacting with org data. -->
-	**Health Checks** (Conditional Launch) - These settings controls the device conditions required to access org data and the remediation action(s) if the conditions aren't met.

To help organizations prioritize client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for mobile app management. 

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

For more information on the available settings, see [Windows app protection policy settings](app-protection-policy-settings-windows.md).

## Next steps

- [What are app protection policies?](app-protection-policy.md)
- [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md)
