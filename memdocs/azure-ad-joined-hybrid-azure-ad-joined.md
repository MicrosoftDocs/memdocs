---
# required metadata

title: Join your cloud native endpoints to Azure AD
titleSuffix: Microsoft Endpoint Manager
description: When moving to or using cloud native endpoints, use Azure AD joined endpoints. When you Azure AD join you endpoints, you can use Windows Autopilot to provision or get devices ready for organization use. Learn more about the benefits to IT admins and end-users.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 04/28/2022
ms.topic: conceptual
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer: ahamil, jasandys, wicale
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
---

# Azure AD joined (AADJ) vs. Hybrid Azure AD joined (HAADJ) in cloud native endpoints

**TO DO:**

- ??Still need a checklist of when/when not to use AADJ??
- ??Still need a checklist of when/when not to use HAADJ??

When moving to cloud native endpoints, you need to understand the differences between Azure AD joined and hybrid Azure AD joined devices.

To summarize:

- **Azure AD joined**: Device are joined to a Azure AD. For more specific information, see [Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join) (opens another Microsoft website).

- **Hybrid Azure AD joined**: Device are registered in Azure AD and joined to an on-premises AD domain. For more specific information, see [Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (opens another Microsoft website).

This article describes the differences between Azure AD joined and hybrid Azure AD joined devices. For an overview of cloud native endpoints, and their benefits, go to [What are cloud native endpoints?](cloud-native-endpoints-overview.md).

## Azure AD joined

When an endpoint, like a Windows 10/11 device is Azure AD joined, it establishes a trust with Azure AD, and has an identity (`device-id`) in Azure AD. The endpoint is managed and controlled by the organization.

The endpoint is joined to Azure AD. It's not joined to an on-premises AD domain.

To join Windows endpoints to Azure AD, you have some options:

- **Use [Windows Autopilot](/mem/autopilot/)**. Windows Autopilot guides users through the Windows Out of Box Experience (OOBE). When users enter their their work or school account, the endpoint joins Azure AD.

  All devices registered with Windows Autopilot are automatically considered organization owned devices. Windows Autopilot is one of the most adopted approaches by organizations, big and small, to get their devices joined to Azure AD, and managed by IT.  

- **Use Windows Out of Box Experience (OOBE)**. When users enter their work or school account on the device, the endpoint automatically joins Azure AD.

- **Use the Settings app**. On the device, end users open the Settings app (**Accounts** > **Access work or school** > **Connect**), and use their work or school account.

- **Use a Window Provisioning Package**. For more information, see:

  - [Provisioning packages for Windows](/windows/configuration/provisioning-packages/provisioning-packages)
  - [Bulk join a Windows device to Azure AD and Microsoft Endpoint Manager using a provisioning package - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/intune-customer-success/bulk-join-a-windows-device-to-azure-ad-and-microsoft-endpoint/ba-p/2381400) blog post

### Organization IT benefits

- Using conditional access, you can allow or restrict access to organization resources that meet, or don't meet your requirements.
- Settings and work data roam through enterprise compliant clouds. No personal Microsoft accounts, like Hotmail are used, and can be blocked.
- Using Windows Hello for Business, you can reduce the risk of credential theft.

### End user benefits

- To authenticate end users with Azure AD and the Windows endpoint, users need a work or school account. No personal accounts are used.
- Get single sign-on (SSO) to Microsoft 365 and SaaS apps with an internet connection.
- Use the convenience and security of Windows Hello for Business to sign in to their Windows endpoint.

  When they sign in with Windows Hello for Business, users automatically use SSO to many of their online and on-premises apps and resources.

- OS settings roam across all Azure AD joined devices.

  > [!IMPORTANT]
  > End users working remotely on Azure AD joined devices don't need a VPN to sign-on when cached credentials expire on the device. On hybrid Azure AD joined devices, they do need a VPN to sign in when cached credentials expire.

### Azure AD joined resources

- [What is device identity in Azure Active Directory?](/azure/active-directory/devices/overview)
- [What is an Azure AD joined device?](/azure/active-directory/devices/concept-azure-ad-join)
- [How Azure AD device registration works](/azure/active-directory/devices/device-registration-how-it-works)
- [How to plan your Azure Active Directory join implementation](/azure/active-directory/devices/azureadjoin-plan)
- [Windows Hello for Business documentation - Windows security](/windows/security/identity-protection/hello-for-business/)

## Hybrid Azure AD joined

[Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid) are joined to your on-premises Active Directory domain (AD domain) and are registered with Azure Active Directory (Azure AD). These devices **require** a network line-of-sight to your on-premises domain controllers for initial sign-in and for device management.

If the devices can't connect to the domain controller, then users might be prevented from signing in, and may not receive policy updates.

Many organizations with existing domain joined devices want the benefits and features of Azure AD and Endpoint Management. For these organizations, registering these existing devices with Azure AD might be the best option. When you register existing devices in Azure AD, a [device identity](/azure/active-directory/devices/overview) is created, and your devices are hybrid Azure AD joined.

### Hybrid Azure AD joined resources

For information on how to register your existing domain joined devices to Azure AD, see:

- [Configure hybrid Azure Active Directory join for managed domains](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)
- [Configure hybrid Azure Active Directory join for federated domains](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)

For new, refurbished, or refreshed Windows devices, Microsoft recommends [Azure AD joined](#azure-ad-joined) (in this article).

## Which option is right for your organization

??Still need a checklist of when/when not to use AADJ, and when/when not to use HAADJ??

## Next steps

- [What are cloud native endpoints?](cloud-native-endpoints-overview.md)
- [Tutorial: Get started with cloud native Windows endpoints with Microsoft Endpoint Manager](cloud-native-windows-endpoints.md)
- [Cloud native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
- [High level planning guide to move to cloud native endpoints](cloud-native-endpoints-planning-guide.md)
- [Known issues and important information](cloud-native-endpoints-known-issues.md)
