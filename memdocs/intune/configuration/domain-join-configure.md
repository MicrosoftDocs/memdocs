---
# required metadata

title: Domain join profile settings for Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Create a domain join device configuration profile for hybrid Azure AD joined devices. Use this profile to deploy on-premises Active Directory domain information to devices provisioned with Windows Autopilot and Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

## Configuration Domain Join settings for hybrid Azure AD joined devices in Microsoft Intune

Many environments use on-premises Active Directory (AD). You can join your AD domain-joined devices to Azure AD. These devices are called hybrid Azure AD joined devices. Using Windows Autopilot, you can [enroll hybrid Azure AD joined](../enrollment/windows-autopilot-hybrid.md) devices in Intune. To enroll, you also need a **Domain Join** configuration profile.

A **Domain Join** configuration profile includes on-premises Active Directory domain information. When devices are provisioning (and typically offline), this profile deploys the AD domain details so devices know which on-premises domain to join. If you don't create a domain join profile, these devices might fail to deploy.

This feature applies to:

- Windows 10 and newer
- Hybrid Azure AD joined devices
- Hybrid deployment with Autopilot + Intune

This article shows you how to create a domain join profile for a hybrid Autopilot deployment. You can also see all available settings.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Windows 10: Domain join profile that includes on-premises domain information to enroll hybrid AD joined devices with Windows Autopilot**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.
    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Domain Join (preview)**.

4. Select **Settings**. Enter the following properties:

    - **Computer name prefix**: Enter a prefix for the device name. Computer names are 15 characters long. After the prefix, the remaining 15 characters are randomly generated.
    - **Domain name**: Enter the Fully Qualified Domain Name (FQDN) the devices are to join. For example, enter `americas.corp.contoso.com.`
    - **Organizational unit** (optional): Enter the full path ([distinguished name](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) to the organizational unit (OU) the computer accounts are to be created. For example, enter `"CN=Users,DC=Contoso,DC=com"`. If you don't enter a value, a well-known computer object container is used.

      For more information and advice on this setting, see [Deploy hybrid Azure AD-joined devices](../enrollment/windows-autopilot-hybrid.md).

5. When you're done, select **OK** > **Create** to save your changes.

The profile is created and shown on the profiles list. It's also ready for you to [deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).

## Next steps

After the profile is created, it's ready to be assigned. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

[Deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](../enrollment/windows-autopilot-hybrid.md).
