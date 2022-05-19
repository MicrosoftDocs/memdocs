---
# required metadata

title: Join your cloud native endpoints to Azure AD
titleSuffix: Microsoft Endpoint Manager
description: When moving to or using cloud native endpoints, use Azure AD joined endpoints. When you Azure AD join you endpoints, you can use Windows Autopilot to provision or get devices ready for organization use. Learn more about the benefits to IT admins and end-users.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 05/18/2022
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

# Azure AD joined vs. Hybrid Azure AD joined in cloud native endpoints

> [!TIP]
> [!INCLUDE [cloud-native-endpoints-definitions](./includes/cloud-native-endpoints-definitions.md)]

Many critical and valuable services, including [Conditional Access](/azure/active-directory/conditional-access/overview) and [Azure AD single sign-on](/azure/active-directory/manage-apps/what-is-single-sign-on), require endpoints to have a cloud identity. For organization owned Windows endpoints, a cloud identity is created when the device is Azure AD joined or Hybrid Azure AD joined

When moving to cloud native endpoints, you need to understand the differences between Azure AD joined and hybrid Azure AD joined devices:

- **Azure AD joined** (AADJ): Device are joined to an Azure Active Directory (Azure AD). They're not joined to on-premises Azure AD.

  For more specific information, see [Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join) (opens another Microsoft website).

- **Hybrid Azure AD joined** (HAADJ): Device are registered in Azure AD and joined to an on-premises AD domain.

  For more specific information, see [Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (opens another Microsoft website).

This feature applies to:

- Windows cloud native endpoints

This article describes some of the differences between Azure AD joined and hybrid Azure AD joined devices. For an overview of cloud native endpoints, and their benefits, go to [What are cloud native endpoints?](cloud-native-endpoints-overview.md).

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

- [What is device identity in Azure AD?](/azure/active-directory/devices/overview)
- [What is an Azure AD joined device?](/azure/active-directory/devices/concept-azure-ad-join)
- [How Azure AD device registration works](/azure/active-directory/devices/device-registration-how-it-works)
- [How to plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan)
- [Windows Hello for Business documentation - Windows security](/windows/security/identity-protection/hello-for-business/)

## Hybrid Azure AD joined

[Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid) are joined to your on-premises AD domain and are registered with Azure AD. These devices **require** a network line-of-sight to your on-premises domain controllers for initial sign-in and for device management.

If the devices can't connect to the domain controller, then users might be prevented from signing in, and may not receive policy updates.

Many organizations with existing domain joined devices want the benefits and features of Azure AD and Endpoint Management. If your devices can't be fully cloud native yet, then you can register these existing devices with Azure AD. When you register existing devices in Azure AD, a [device identity](/azure/active-directory/devices/overview) is created, and your devices are hybrid Azure AD joined. They're not considered cloud native endpoints.

If your organization is ready and wants to be cloud native, then [Azure AD joined](#azure-ad-joined) (in this article) is the correct choice. Existing devices will need to be reset. For more specific information and guidance, go to the [High level planning guide](cloud-native-endpoints-planning-guide.md).

### Hybrid Azure AD joined resources

For information on how to register your existing domain joined devices to Azure AD, see:

- [Configure hybrid Azure AD join for managed domains](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)
- [Configure hybrid Azure AD join for federated domains](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)

## Which option is right for your organization

It depends on your environment, your hardware, and your organization goals. When making this decision, you need to consider the future, the long term impact, and the organization goals.

Consider the following scenarios:

| Scenario | AADJ or HAADJ |
| --- | --- |
| You have new endpoints or can reset existing endpoints | ✔️ Azure AD join <br/><br/> If you have new, refurbished, or refreshed Windows devices, then Azure AD joined is recommended. AADJ should be your default option. <br/><br/> There are some known blockers and challenges outside of Microsoft's control that may prevent your organization from fully adopting AADJ. There may also be unknown blockers that are specific to your organization and its configuration or expectations. Note that these blockers may be technical or they mat arise due to other, non-technical factors.<br/><br/>❌ Hybrid Azure AD join<br/><br/> You can use HAADJ for new endpoints, but it's typically not recommended. Windows 10/11 have modern features built-in to the OS, including modern management, modern authentication, and more. When joined using HAADJ, you might not get these features, and must use Group Policy Objects (GPO) to manage these endpoints, which can be complex, cumbersome, and possibly costly. <br/><br/>If you identify a potential blocker, then determine the scope, impact, and solution. The [High level planning guide to move to cloud native endpoints](cloud-native-endpoints-planning-guide.md) may help. |
| Endpoints can't be reset or reprovisioned |  ❌ Azure AD join <br/><br/> Existing devices joined to an on-premises AD domain must be reset to become Azure AD joined. If they can't be reset, then AADJ isn't possible. <br/>  <br/>✔️ Hybrid Azure AD join<br/> <br/>If you have existing endpoints that are joined to an on-premises AD domain, and can't be reset, then Hybrid Azure AD joined might be the easiest option for your organization. Devices get a cloud identity and can use cloud services that require a cloud identity. This option typically has minimal impact to end users. |
| You have new endpoints and have existing AD joined endpoints that can't be reset | ✔️ Azure AD join <br/><br/> AADJ should be your default option for new, refurbished, or refreshed Windows devices. <br/><br/> ✔️ Hybrid Azure AD join<br/> <br/> Hybrid Azure AD joined and Azure AD joined aren't mutually exclusive, and can coexist in the same environment. <br/> <br/>Having a mixed environment does increase complexity, maintenance tasks, and support costs. But, you can use HAADJ until those endpoints can be replaced or reset. Remember, Hybrid Azure AD joined shouldn't be your organization's end goal. |
| You want to be cloud-only, and remove dependency to on-premises | ✔️ Azure AD join <br/><br/> ❌ Hybrid Azure AD join<br/><br/> |

Search: HAADJ vs AADJ

https://docs.microsoft.com/en-us/answers/questions/33891/difference-between-azure-ad-registered-azure-ad-jo.html

## Follow the cloud native endpoints guidance

1. [Overview: What are cloud native endpoints?](cloud-native-endpoints-overview.md)
2. [Tutorial: Get started with cloud native Windows endpoints](cloud-native-windows-endpoints.md)
3. 🡺 **Concept: Azure AD joined vs. Hybrid Azure AD joined** (*You are here*)
4. [Concept: Cloud native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
5. [High level planning guide](cloud-native-endpoints-planning-guide.md)
6. [Known issues and important information](cloud-native-endpoints-known-issues.md)
