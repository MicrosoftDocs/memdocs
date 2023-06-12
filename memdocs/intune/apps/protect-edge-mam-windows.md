---
# required metadata

title: Mobile Application Management for Microsoft Edge on unmanaged Windows devices
titleSuffix: 
description: Use Microsoft Edge on personal Windows devices to enable protected MAM access to org data.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/08/2023
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
<!-- Use Mobile Application Management for Microsoft Edge on unmanaged Windows  -->

You can enable protected Mobile Application Management (MAM) access to org data via Microsoft Edge on personal Windows devices. This capability uses the following functionality:
- Intune Application Configuration Policies (ACP) to customize the org user experience in Microsoft Edge
- Intune Application Protection Policies (APP) to secure org data and ensure the client device is healthy when using Microsoft Edge
- Windows Defender client threat defense integrated with Intune APP to detect local health threats on personal Windows devices
- Application Protection Conditional Access to ensure the device is protected and healthy before granting protected service access via Azure AD

> [!NOTE]
> For more information about MAM, see [Mobile Application Management (MAM) basics](../apps/app-management.md#mobile-application-management-mam-basics).

Both end-users and organizations need to have protected organizational access from personal devices. Organizations need to ensure that corporate data is protected on personal, unmanaged devices. As an Intune admin, you have the responsibility to determine how members (end-users) of your organization access corporate resources in a protected way from an unmanaged device. You need to ensure when accessing organizational data, that the unmanaged devices are healthy, the applications adhere to your organization data's protection policies, and that the end-user’s unmanaged assets on their device aren't impacted by your organization's policies. This capability is available by using Microsoft Edge to access corporate data on Windows client devices.

As the Intune admin, you need to have the following app management functionality:
- Ability to deploy app protection policies to apps/users protected by the Intune APP SDK 
- Ability to configure app Health Checks (aka Conditional Launch) and Access policies to apps/users protected by the Intune APP SDK 
- Ability to define sites protected by Conditional Access and protection policy 
- Ability to designate risk level for allowing end users to access corporate resource 
- Ability to set up tenant-based connector for Mobile Threat Defense (MTD)  
- Ability to deploy a selective wipe command to protected applications 

Members of your organization (end-users) expect to have the following functionality for their accounts:
- Ability to log in to Azure Active Directory (AAD) to access sites protected by Conditional Access 
- Ability to view health data on device, in the case where a device is considered unhealthy 
- Ability to have access revoked to resources when a device remains unhealthy 
- Ability to be informed, with clear remediation steps, when access is controlled by an administrator policy 

Data protection for Windows MAM involves the following key areas:
- **Defender Client and Service**: Responsible for retrieving and syncing client health data on the unmanaged Windows 10 device.
- **Endpoint Manager Client and Service**: Mobile Application Management (MAM), Mobile Threat Defense (MTD), and Intune admin console.
- **Microsoft Edge**: Web-browser on client device responsible for enforcing policy configuration and protection.
- **Azure Active Directory**: Responsible for authenticating user and enforcing compliance state.
- **Web Account Manager (WAM)**: Windows framework responsible for all accounts on a device, including interfacing with identity providers (IDPs).

## Conditional Access Compliance 
Preventing data loss is a part of protecting your organizational data. Data loss prevention (DLP) is only effective if your org data cannot be accessed from any unprotected system or device. App Protection Conditional Access uses Conditional Access (CA) to ensure App Protection Policies (APP) are supported and enforced in a client application before allowing access to protected resources (such as org data).  APP CA will allow end-users with personal Windows devices to use APP managed applications, including Microsoft Edge, to access Azure AD resources without fully managing their personal device.

This MAM service syncs compliance state per user, per app, and per device to the Azure Active Directory (AAD) CA service. This includes the threat information received from the Mobile Threat Defense (MTD) vendors starting with Windows Defender. 

> [!NOTE]
> This MAM service uses the same conditional access compliance workflow that is used to [manage Microsoft Edge on iOS and Android devices](../apps/manage-microsoft-edge.md).

When a change is detected, the MAM service updates the device compliance state immediately. The service also includes MTD health state as part of the compliance state.

> [!NOTE]
> The MAM service evaluates the MTD state in the service. This is done independently from the MAM client and client platform.

The MAM Client communicates the client heath state (or health metadata) to the MAM Service upon check-in. The health state includes any failure of APP Health Checks for **Block** or **Wipe** conditions. In addition, AAD guides end-users through remediation steps when they attempt to access a blocked CA resource.

### Apply Conditional Access
Organizations can use Azure AD Conditional Access policies to ensure that users can only access work or school content using Microsoft Edge for Windows. To do this, you'll need a conditional access policy that targets all potential users. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection).

Follow the steps in [Require approved client apps or app protection policy with mobile devices](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection#require-approved-client-apps-or-app-protection-policy-with-mobile-devices), which allows Microsoft Edge for Windows, but blocks other mobile device web browsers from connecting to Microsoft 365 endpoints.

>[!NOTE]
> This policy ensures mobile users can access all Microsoft 365 endpoints from within Edge for Windows. This policy also prevents users from using InPrivate to access Microsoft 365 endpoints.

With Conditional Access, you can also target on-premises sites that you have exposed to external users via the [Azure AD Application Proxy](/azure/active-directory/active-directory-application-proxy-get-started).

> [!NOTE]
> To leverage app-based conditional access policies, the Microsoft Authenticator app must be installed on Windows devices. For more information, see [App-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md).

## Threat Defense Health

The health status of a personal owned device is verified before allowing access to your org data. MAM threat detection is tightly integrated with Windows Defender. As part of CA, this service can block remote resource access and APP can block access (or remove local org data). Windows Defender provides a client device health assessment ("heartbeat") to the MAM service. This assessment supports both APP and CA gating of the flow and access to org data on personal unmanaged devices.

> [!NOTE]
> This MAM service uses the same threat defense health workflow that is used to [manage Microsoft Edge on iOS and Android devices](../apps/manage-microsoft-edge.md).

As part of threat defense health, this MAM Service supports registration and heath state reporting for threat detection products. The health state includes the following details:
-	User, app, and device identifiers
-	A predefined health state
-	The time of last health state update

> [!IMPORTANT]
> You should use only one MTD solution per platform. For related information, see [Mobile Threat Defense integration with Intune](../protect/mobile-threat-defense.md).

To avoid sending health data for non-MAM users, the MAM Client will trigger the Windows Defender client with the enrolled user information following MAM enrollment. This prevents sending health data for non-MAM users. Microsoft Defender Cloud Service registers a unique method to trigger health data reporting with the Intune MTD Connector Service when setting up the MTD connector. 

## Create Intune app protection policies

App Protection Policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario.

As an admin, you can configure how data is protected through APP. This configuration applies to the native Windows application interaction with the data. APP settings are segmented into three categories:
-	**Data Protection** - These settings control how data can move into and out of an org context (account, document, location, services) for the user.
<!-- -	**Access** - These settings control how the user must verify their identity before interacting with org data. -->
-	**Health Checks** (Conditional Launch) - These settings controls the device conditions required to access org data and the remediation action(s) if the conditions aren't met.

To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for mobile app management. The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, such as APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

For more information on the available settings, see [Windows app protection policy settings](app-protection-policy-settings-windows.md).

## Next steps

- [What are app protection policies?](app-protection-policy.md)
- [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md)
