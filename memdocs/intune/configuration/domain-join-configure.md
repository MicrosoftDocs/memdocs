---
# required metadata

title: Domain join profile settings for Windows 10/11 in Microsoft Intune
description: Create a domain join device configuration profile for hybrid Azure AD joined devices. Use this profile to deploy on-premises Active Directory domain information to devices provisioned with Windows Autopilot and Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/18/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Configuration Domain Join settings for hybrid Azure AD joined devices in Microsoft Intune

Many environments use on-premises Active Directory (AD). When AD domain-joined devices are also joined to Azure AD, they're called hybrid Azure AD joined devices. Using Windows Autopilot, you can [enroll hybrid Azure AD joined devices](../../autopilot/windows-autopilot-hybrid.md) in Intune. To enroll, you also need a **Domain Join** configuration profile.

A **Domain Join** configuration profile includes on-premises Active Directory domain information. When devices are provisioning (and typically offline), this profile deploys the AD domain details so devices know which on-premises domain to join. If you don't create a domain join profile, these devices might fail to deploy.

This feature applies to:

- Windows 11
- Windows 10
- Hybrid Azure AD joined devices
- Hybrid deployment with Autopilot + Intune

This article shows you how to create a domain join profile for a hybrid Autopilot deployment. You can also see the available settings.

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile**: Select **Templates** > **Domain Join**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Windows 10/11: Windows Autopilot domain join**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended. For example, enter **Windows 10/11: Domain join profile that includes on-premises domain information to enroll hybrid AD joined devices with Windows Autopilot**.

6. Select **Next**.
7. In **Configuration settings**, enter the following properties:

    - **Computer name prefix**: Enter a prefix for the device name. Computer names are 15 characters long. After the prefix, the remaining 15 characters are randomly generated.
    - **Domain name**: Enter the Fully Qualified Domain Name (FQDN) the devices are to join. For example, enter `americas.corp.contoso.com.`
    - **Organizational unit** (optional): Enter the full path ([distinguished name](/windows/win32/ad/object-names-and-identities#distinguished-name)) to the organizational unit (OU) the computer accounts are to be created. For example, enter `OU=Mine,DC=Contoso,DC=com`. Don't enter quotation marks. To use the well-known computer object container (CN=Computers, DC=Contoso, DC=Com), leave this property blank.

      For more information and advice on this setting, see [Deploy hybrid Azure AD-joined devices](../../autopilot/windows-autopilot-hybrid.md).

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the device groups that will receive your profile. For more information about assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    If you need to join devices to different domains or OUs, create different device groups.

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

It's now ready for you to [deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

## Next steps

After the profile is [assigned](device-profile-assign.md), [monitor its status](device-profile-monitor.md).

[Deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).
