---
# required metadata

title: eSIM configuration of a download server
description: Learn about configuration of an eSIM Download Server from Microsoft Intune.  
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 05/08/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---
# Configure eSIM download server using Microsoft Intune
 
The identity of a cellular-enabled device, such as a Windows Connected PC, has traditionally been encapsulated in a device called SIM (Subscriber Identity Module), and packaged as a discrete SIM card. Management of SIM cards for a fleet of devices can be costly and time-consuming. Therefore, Windows 10 and Windows 11 support eSIM (embedded Subscriber Identity Module) technology as a digital alternative to discrete SIM cards.
Windows 11 provides more capabilities for the deployment and management of eSIM content using Mobile Device Management (MDM) such as Microsoft Intune.

## About eSIM technology

eSIM technology has created a worldwide ecosystem of cellular devices and mobile operators based upon a common specification from the GSM Association (GSMA). The adoption of eSIM technology has been growing due to its incorporation in popular smart phones. Windows has supported eSIM for PCs since 2017.

eSIM decouples the secure execution environment of the plastic SIM card from the SIM credentials it contains. The secure container is called an eUICC (embedded Universal Integrated Circuit Card). In the same way that each physical SIM card has a unique identity, each eUICC has a unique identity called eUICC Identifier (EID).

The credentials and associated other configuration that uniquely identify a cellular subscription are contained in a digital (software) package called an eSIM Profile. Multiple eSIM Profiles may be installed into an eUICC. One of the installed eSIM Profiles is enabled (and the rest are disabled). The combination of the enabled eSIM Profile and its eUICC container behaves exactly like a traditional SIM card.

## At-Scale Configuration of eSIM PCs

eSIM digitizes the delivery of SIMs to devices such as PCs, eliminating the need to obtain and deploy physical SIM cards. The [Mobile Plans](/windows-hardware/drivers/mobilebroadband/mobile-plans) application in Windows further reduces friction by providing a user-friendly interface for a user to interact with a chosen mobile operator and coordinate the download and installation of the corresponding eSIM profile.

The Mobile Plans application is well suited to the needs of consumers and businesses with a few PCs. However, it requires user interaction on each device that is provisioned, an effort and cost that may become significant at large scale. To support larger-scale managed environments (such as an enterprise or an educational organization), Windows provides eSIM provisioning through mobile device management (MDM) such as Microsoft Intune.

When an enterprise provisions an eSIM through an MDM such as Microsoft Intune, it also configures the eSIM deployment along with other enterprise settings and policies. When the MDM server is enrolled to the end user's work or school account, it pushes the configuration to the PC throughout its lifecycle. After the PC is configured with the eSIM information, it downloads the eSIM profile from the mobile operator's download server (SM-DP+).

Within Windows, the [eUICCs Configuration Service Provider (CSP)](/windows/client-management/mdm/euiccs-csp) handles eSIM configuration. In addition, the enterprise can also configure some eSIM policies through the CSP and each PC obtains its eSIM profile from the CSP.

## Prerequisites

In addition to a Windows 11 Connected PC (eSIM-capable PC) managed through Microsoft Intune, you need the following information:

A mobile operator who can provide eSIM profiles to a set of known devices based upon their EIDs. This, in turn, requires some way through which an enterprise (or school) should be able to provide the EIDs of their PCs to the operator as part of their contract with the mobile operator.

- One option is for the enterprise to obtain the EIDs of their PCs from PC packaging and send it to the operator directly.

- Alternatively, for bulk device purchases, the EIDs of their PCs could come in a manifest file created by the device OEM or a reseller/distributor and delivered to the enterprise with the devices or directly to the mobile operator.

After the mobile operator knows the EIDs of the customer's PCs, the mobile operator will set up eSIM profiles for each PC on its download server (SM-DP+). The enterprise needs to know the fully qualified domain name (FQDN) of the download server (SM-DP+). For example, smdp.example.com. However, it doesn't need individual activation codes. Every PC connects to the same server. When each PC contacts the download server (SM-DP+), the download server (SM-DP+) authenticates the PC by its EID and provides it with the eSIM profile that is specific to that device.

## Process flow

:::image type="content" source="./media/esim-device-configuration/device-settings-cellular-profiles.png" alt-text="Process flow.":::

The overall process flow is as follows:

1. To set up a managed eSIM deployment, the enterprise customer must have a contract with a mobile operator and obtain information from the operator about its eSIM download server (SM-DP+). The enterprise then configures the policies and settings to be applied to all of their eSIM-capable Connected PCs, including the fully qualified domain name of the operator's SM-DP+.

    > [!NOTE]
    > The MDM administrator creates the eSIM configuration profile pointing to the download server (SM-DP+) provided by the mobile operator and assigns the profile to the required group(s).

2. As described earlier, the enterprise or its supplier (PC manufacturer or distributor) provides the EIDs of the Connected PCs to the operator. For each EID, the operator creates an eSIM profile on its download server (SM-DP+) for that device.
After the initial configuration is complete, the following process unfolds for each PC:

3. The end user unboxes the PC, powers it on, and goes through the initial Windows **out of box experience**. As part of this process, the end user connects the PC to a Wi-Fi network, and signs into their **work or school** account.

4. After the user has authenticated to the enterprise's (or school's) Azure Active Directory, the work or school account is set up on the device. As part of this process, the PC is enrolled to MDM, which then provisions it as configured by the enterprise (in step 1). This configuration includes the FQDN of the operator's download server (SM-DP+).

5. After configuration is complete, the PC connects to the download server (SM-DP+) according to the standard eSIM download protocol. As part of this process, the download server (SM-DP+) receives and authenticates the EID of the PC. The download server (SM-DP+) looks up the eSIM profile for that EID (created in step 2) and downloads that eSIM profile to the PC.

6. The PC installs and enables the eSIM profile. Windows recognizes the mobile operator and configures the cellular settings such as access point name (APNs), and the PC is now connected over cellular.

> [!NOTE]
> The process flow described focuses on the initial device setup experience. However, eSIM provisioning can also be done anytime throughout the lifecycle of the device for managed devices.

## Intune configuration of an eSIM download server

The Intune configuration of a mobile operator's eSIM download server is done via a Configuration Profile assigned to a Group.

This feature applies to:

- Windows 11

To deploy eSIM to your devices using Intune, the following are needed:

- **eSIM capable devices**, such as the [Surface Pro 9 with 5G](https://www.microsoft.com/surface/business/surface-pro-9): See [if your device supports eSIM](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data).
- **Windows 11** (version 22H2 (Build 22621) or higher) that is enrolled and MDM managed by Intune
- **eSIM Download Server (SM-DP+ or SM-DS) fully qualified domain name (FQDN)** provided by your mobile operator. Contact your mobile operator for details.

## eSIM capable devices

If you're unsure that your devices support eSIM, then contact your device manufacturer. On Windows devices, you can confirm eSIM supportability. For more information, see [Use an eSIM to get a cellular data connection on your Windows client device](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data).

After your mobile operator confirms that you need to create eSIM profiles on the download server (SM-DP+), go to Microsoft Intune and create a profile for the EIDs tied to the eSIM-capable Windows devices that you want to enable with eSIM.

## Create an Azure AD device group

Create a Device group that includes the eSIM capable devices. [Add groups](../fundamentals/groups-add.md) lists the steps.

> [!NOTE]
> We recommend creating a static Azure AD device group that includes your eSIM devices. Using a group confirms you target only eSIM devices.

## Create a profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create Profile**.

3. For the **Platform** field, select **Windows 10 and later**.

4. For the **Profile type** field, select **Settings catalog**.

5. Select **Create** and follow the wizard to complete the steps.

6. In the **Basic** tab, enter the **Name** and **Description** of the profile, and select **Next**.

7. In the **Configuration Settings** tab, select **+ Add** settings and search for *eSIM* in the Settings Picker. After you select eSIM, you can select the settings that you want to make available on your policy.

- In the **Download Servers** area:

  - **Auto Enable**: It indicates whether the discovered profile must be automatically enabled after installation. The default value of the dropdown list is *Enable*. Select **Auto Enable** if the eSIM profile should be automatically enabled (independently of any other eSIM profiles stored in eUICC).

  - **Server Name**: It's the fully qualified domain name of the SM-DP+ server that is used for profile discovery. DO NOT INCLUDE *https://*.

  - **Display Local UI**: Determines whether eSIM settings can be viewed and changed in the Settings app on the eSIM capable devices that are being provisioned. True if available, false otherwise. If **Display Local UI** is set to Disabled, **Auto Enable** must be checked.

  - Enter the Server Name, select the desired settings, and then select **Next**.

8. In the **Scope tags** tab, add the required tags, and select **Next**.

9. In the **Assignments** tab, select the user or device group(s) to assign your profile. For more information on assigning the profile to a user or device group, go to [Assign device profiles](device-profile-assign.md#user-groups-vs-device-groups) in Microsoft Intune.
Also, before creating the profile, you need to have your group(s) set up. For more information, go to Add groups to organize users and devices.

10. In the **Review + create** tab, review all the details and select **Create**.

## Best practices & troubleshooting

- Create a device Azure AD group that only includes the targeted eSIM devices.

- If the policy is deployed to a non-eSIM capable device, the **Assignment Status** displays an Error.

- The current implementation only supports a single Server Name. Even if more Server Names are added, only the first one is used.

- If the **Local UI** isn't disabled as part of the Configuration Profile, you can change the active profile, stop using, or remove any of the eSIM profiles stored in the device.

- As with other settings in Intune, when the deployment status shows as *successful* it simply means that the setting is now applied, but the eSIM isn't activated.

- There's no way to remove the eSIM profile using Intune. The profile must be manually removed from the device.

- There's no way to distinguish between an eSIM and a non-eSIM device in Microsoft Intune.

- EIDs can't be collected via Intune and aren't exposed programmatically. Some OEM/resellers have the capability of providing this information.

## Next steps

[Configure device profiles](device-profiles.md)
