---
# required metadata

title: Join your cloud-native endpoints to Azure AD
titleSuffix: Microsoft Intune
description: When moving to or using cloud-native endpoints, use Azure AD joined endpoints. When your endpoints are joined to Azure AD, you can use Windows Autopilot to provision or get devices ready for organization use. Learn more about the benefits to IT admins and end-users.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 07/13/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: 
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
  - intune-scenario
---

# Azure AD joined vs. Hybrid Azure AD joined in cloud-native endpoints

> [!TIP]
> [!INCLUDE [cloud-native-endpoints-definitions](../../includes/cloud-native-endpoints-definitions.md)]

Many critical and valuable services, including [Conditional Access](/azure/active-directory/conditional-access/overview) and [Azure AD single sign-on](/azure/active-directory/manage-apps/what-is-single-sign-on), require endpoints to have a cloud identity. For organization owned Windows endpoints, a cloud identity is created when the device is Azure AD joined or Hybrid Azure AD joined.

When moving to cloud-native endpoints, you need to understand the differences between Azure AD joined and hybrid Azure AD joined devices:

- **Azure AD joined** (AADJ): Devices are joined to an Azure Active Directory (Azure AD). They're not joined to on-premises AD.

  For more specific information, go to [Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join) (opens another Microsoft website).

- **Hybrid Azure AD joined** (HAADJ): Devices are registered in Azure AD and joined to an on-premises AD domain.

  For more specific information, go to [Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (opens another Microsoft website).

This feature applies to:

- Windows cloud-native endpoints

This article describes some of the differences between Azure AD joined and hybrid Azure AD joined devices. For an overview of cloud-native endpoints, and their benefits, go to [What are cloud-native endpoints](cloud-native-endpoints-overview.md).

## Azure AD joined

When an endpoint, like a Windows 10/11 device is Azure AD joined, it establishes a trust with Azure AD, and has an identity (`device-id`) in Azure AD. The endpoint is managed and controlled by the organization.

The endpoint is joined to Azure AD. It's not joined to an on-premises AD domain.

To join Windows endpoints to Azure AD, you have some options:

- **Use [Windows Autopilot](/autopilot/index)**. Windows Autopilot guides users through the Windows Out of Box Experience (OOBE). When users enter their work or school account, the endpoint joins Azure AD.

  All devices registered with Windows Autopilot are automatically considered organization owned devices. Windows Autopilot is one of the most adopted approaches to get organization devices joined to Azure AD and managed by IT.  

- **Use Windows Out of Box Experience (OOBE)**. When users enter their work or school account on the device, the endpoint automatically joins Azure AD.

- **Use the Settings app**. On the device, end users open the Settings app (**Accounts** > **Access work or school** > **Connect**), and use their work or school account.

- **Use a Window Provisioning Package**. For more information, go to:

  - [Provisioning packages for Windows](/windows/configuration/provisioning-packages/provisioning-packages)
  - [Bulk join a Windows device to Azure AD and Microsoft Intune using a provisioning package - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/intune-customer-success/bulk-join-a-windows-device-to-azure-ad-and-microsoft-endpoint/ba-p/2381400) blog post

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

[Hybrid Azure AD joined devices](/azure/active-directory/devices/concept-azure-ad-join-hybrid) are joined to your on-premises AD domain and are registered with Azure AD. These devices **require** a network line-of-sight to your on-premises domain controllers (DCs) for initial sign-in and for device management.

If the devices can't connect to the DC, then users might be prevented from signing in, and may not receive policy updates.

Many organizations with existing domain joined devices want the benefits and features of Azure AD and endpoint management. If your devices can't be fully cloud-native yet, then you can register these existing devices with Azure AD. When you register existing devices in Azure AD, a [device identity](/azure/active-directory/devices/overview) is created, and your devices are hybrid Azure AD joined. They're not considered cloud-native endpoints.

If your organization is ready and wants to be cloud-native, then [Azure AD joined](#azure-ad-joined) (in this article) is the correct choice. Existing devices need to be reset. For more specific information and guidance, go to the [High level planning guide](cloud-native-endpoints-planning-guide.md).

### Hybrid Azure AD joined resources

For information on how to register your existing domain joined devices to Azure AD, go to [Configure hybrid Azure AD join](/azure/active-directory/devices/howto-hybrid-azure-ad-join). [Configure hybrid Azure AD join](/azure/active-directory/devices/howto-hybrid-azure-ad-join) includes information for managed domains and federated domains.

## Which option is right for your organization

The right option depends on your environment, your endpoints, and your organization goals. When making this decision, consider the future and long term impact.

Consider the following scenarios:

| Scenario | AADJ or HAADJ |
| --- | --- |
| You're provisioning new Windows endpoints | ✔️ Azure AD join (AADJ) <br/><br/> If you have new, refurbished, or refreshed Windows devices that you're provisioning and enrolling, then Azure AD join is recommended. Windows 10/11 has modern features built in to the OS, including modern management, modern authentication, and more. AADJ should be your default option for new and reset endpoints.<br/><br/>❌ Hybrid Azure AD join (HAADJ) <br/><br/> You can use HAADJ for new endpoints, but it's typically not recommended. When joined using HAADJ, you might not get to use the modern features built into Windows 10/11.  |
| You have existing, previously provisioned Windows endpoints that are hybrid Azure AD or AD joined | ✔️ Hybrid Azure AD join (HAADJ) <br/> <br/>If you have existing endpoints that are joined to an on-premises AD domain (including hybrid Azure AD joined), then hybrid Azure AD join is recommended. Devices get a cloud identity and can use cloud services that require a cloud identity. For end users with existing endpoints, this option has minimal impact. <br/><br/>❌ Azure AD join (AADJ) <br/><br/> Existing devices joined to an on-premises AD domain (including hybrid Azure AD joined) must be reset to become Azure AD joined. If they can't be reset, then there's no supported Microsoft path to Azure AD join them. |

### Common questions, answers, and scenarios

This section answers common questions about Azure AD joined and hybrid Azure AD joined devices.

#### Should hybrid Azure AD joined (HAADJ) be a long term or end goal state for devices?

No, HAADJ shouldn't be long term nor the end goal for any organization.

When you're not restricted or limited (technical, political, or regulatory reasons), your organization should be moving or planning on moving to Azure AD joined (AADJ) for your Windows endpoints.

#### What strategy should an organization adopt to move existing HAADJ devices to AADJ?

The strategy depends on many factors, many that are specific to your organization.

In general, Microsoft recommends waiting for a complementary event. For example, you can move to AADJ during a hardware refresh, OS upgrade, or device troubleshooting scenario when there's a new (or reset) instance of Windows. Using this approach, you minimize user disruption and streamline the conversion process to AADJ. Remember, there's no Microsoft supported process or path to convert an existing device from HAADJ to AADJ without a Windows reset.

You can proactively reset existing devices to move to AADJ. This approach can be more disruptive to users and requires more planning & testing. But you can use this approach if you have a few devices or if you have a strong business case to move to AADJ.

#### There's a blocker that prevents my organization from moving to AADJ

It's possible there are blockers and challenges outside of Microsoft's control that can prevent your organization from fully moving to AADJ. There may also be unknown blockers that are specific to your organization and its configuration or expectations. These blockers can be technical or happen for other, nontechnical reasons.

Remember, moving to AADJ isn't an all or nothing proposition. Moving devices to AADJ takes time, even with or without blockers or inhibitors.

If you identify a potential blocker that's preventing you from using AADJ, then determine the scope, impact, and solution. The [High level planning guide to move to cloud-native endpoints](cloud-native-endpoints-planning-guide.md) can help.

#### Can AADJ and HAADJ endpoints coexist in the same environment?

Yes, AADJ and HAADJ endpoints can coexist in the same environment. They aren't mutually exclusive.

Having a mixed environment does increase complexity, maintenance, and support costs. But you can use HAADJ until those endpoints are replaced or reset. Remember, HAADJ shouldn't be your organization's end goal for Windows endpoint state.

#### Can users on AADJ systems access on-premises resources?

Yes, users on AADJ systems can access on-premises resources.

AADJ endpoints can access on-premises resources, and can use single sign-on (SSO). For more specific information, go to [Cloud-native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md).

#### What device join states can Intune manage?

Microsoft Intune, which is a 100% cloud solution, can manage Windows client devices that are AADJ or HAADJ. Intune has many built-in features and settings that can manage settings, control device features, help secure your endpoints, and more.

The [High level planning guide to move to cloud-native endpoints: Intune features you should know](cloud-native-endpoints-planning-guide.md#intune-features-you-should-know) lists some of these features. [What is Intune](../../intune/fundamentals/what-is-intune.md) is also a good resource.

On HAADJ endpoints, you can use on-premises group policies objects (GPO) or Intune to control policy settings. It's possible to also use a combination of GPO and Intune, but this combination adds administrative overhead and complexity. If you enable [co-management](../../configmgr/comanage/overview.md) (Intune (cloud) + Configuration Manager (on-premises)), then you can use some Azure AD features, such as conditional access.

For some guidance, go to [Deployment guide: Setup or move to Microsoft Intune](../../intune/fundamentals/deployment-guide-intune-setup.md).

#### What device join states are required for device compliance and/or conditional access?

Both HAADJ and AADJ endpoints support [compliance policies](../../intune/protect/device-compliance-get-started.md) and [conditional access](../../intune/protect/conditional-access.md) when managed by Intune or co-managed by Intune and Configuration Manager.

#### Are there limitations for HAADJ?

Yes, there are limitations for HAADJ.

These limitations are generally the same with on-premises only domain joined devices. Specifically, HAADJ endpoints require a line-of-sight to the on-premises AD domain controller for initial sign-in and to change passwords. If the domain is down or is unavailable, then users could be blocked from signing in to their endpoints. If your organization is moving away from having an on-premises domain, then you must also move away from HAADJ for your devices.

If you use [passwordless authentication](/azure/active-directory/authentication/concept-authentication-passwordless), then users need internet access and a line of sight to the domain controllers (DCs). To authenticate, HAADJ endpoints can use kerberos and NTLM.

#### Is HAADJ considered cloud-native?

No, HAADJ isn't considered cloud-native.

The cloud solution is to AADJ your endpoints. The endpoints and their identities are created and stored in Azure AD. Intune manages the endpoints with settings and policies. These services work with other cloud services, including Microsoft 365, Microsoft Defender XDR, and more.

## Follow the cloud-native endpoints guidance

1. [Overview: What are cloud-native endpoints?](cloud-native-endpoints-overview.md)
2. [Tutorial: Get started with cloud-native Windows endpoints](cloud-native-windows-endpoints.md)
3. 🡺 **Concept: Azure AD joined vs. Hybrid Azure AD joined** (*You are here*)
4. [Concept: Cloud-native endpoints and on-premises resources](cloud-native-endpoints-on-premises.md)
5. [High level planning guide](cloud-native-endpoints-planning-guide.md)
6. [Known issues and important information](cloud-native-endpoints-known-issues.md)
