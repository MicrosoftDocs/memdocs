---
# required metadata

title: Device compliance partners in Microsoft Intune - Azure | Microsoft Docs
description: Use a third-party device compliance partner as a source of compliance data for devices you manage with Intune. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.reviewer: samyada

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Support third-party device compliance partners in Intune

Microsoft Intune can add compliance state data to Azure Active Directory (Azure AD) for the devices you manage with one or more third-party device compliance partners. With this configuration, compliance data from those devices can be used with your conditional access policies.

By default, Intune is set up to be the Mobile Device Management (MDM) authority for your devices. When you add a compliance partner to Azure AD and Intune, you're configuring that partner to be a source of Mobile Device Management (MDM) authority for the devices you assign to that partner through an Azure AD user group.

To enable use data from device compliance partners, complete the following tasks:

1. **Add the device compliance partner to Azure AD** to  establish that partner as a Mobile Device Management (MDM) authority for applicable devices.

2. **Configure Intune to work with the device compliance partner**, and then configure groups of users whose devices are managed by that compliance partner.

3. **Configure your compliance partner to send data to Intune**.

4. **Enroll your iOS or Android devices to that device compliance partner**.

With these tasks complete, the device compliance partner sends device state details to Intune. Intune then adds this information to Azure AD. For example, devices with a state of non-compliant have that status added to their device record in Azure AD.

The compliance state is then evaluated by conditional access policies, the same as compliance state data for devices managed by Intune.  By default, Intune is a registered compliance partner for iOS and Android. When you add additional partners, you can set the priority order to ensure the correct partner manages device to fit your business needs.

## Supported device compliance partners

- VMWare Workspace ONE (formerly AirWatch)

## Prerequisites

- A subscription to Microsoft Intune, and access to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

- A subscription to the device compliance partner.

- Review documentation for your compliance partner for supported device platforms and additional prerequisites.

## Add support in Azure AD for a device compliance partner

To enable support for devices that are managed by third-party device compliance partners, you must add that partner to *Mobility (MDM and MAM)* in Azure AD. By default, Intune is already registered for *Mobility (MDM and MAM)*.

### Add a device compliance partner to Azure AD

1. Sign in to the [Azure portal](https://aad.portal.azure.com/) and go to **Azure Active Directory** > **Mobility (MDM and MAM)** > **Add Application**. ([Open the *Mobility (MDM and MAM)* blade directly](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility).)

2. On the **Add an application** blade, select the tile for your device compliance partner, and then select **Add**.

   - For *Workspace ONE*, select **AirWatch by VMware**

3. On the *Mobility (MDM and MAM)* blade, select your compliance partner to open the **Configure** blade and configure the available options.  Options include the **MDM user scope**, **MDM terms of use URL**, and **MDM discovery URL**. When the user scope is set to **Some**, you select the Azure AD user groups that can enroll devices with this compliance partner.

   The devices that are targeted through the groups you select will use the partner as their MDM authority.

4. Select **Save** to complete the partner configuration in Azure AD. Next, you’ll add the compliance partner in Intune.

## Configure Intune to work with a device compliance partner

When Azure AD is configured to support a device compliance partner for *Mobility (MDM and MAM)*, you can configure Intune to also work with that partner. This configuration is required if you want to use compliance state data from that partner with your conditional access policies.

### Add a compliance partner to Intune

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Tenant Administration** > **Connectors and Tokens** > **Partner Compliance management** > **Add Compliance Partner**.

   > [!div class="mx-imgBorder"]
   > ![Add a device compliance partner](./media/device-compliance-partners/add-compliance-partner.png)

3. On the **Basics** page, expand the **Compliance partner** drop-down and select the partner you're adding. Next, select the drop-down for **Platform**, and select the platform.

   You're limited to a single partner per platform, even if you have added multiple compliance partners to Azure AD.

4. On **Assignments**, select the user groups that will have devices managed by this partner. With this assignment, you'll change the MDM authority for applicable devices to use this partner.

5. On the **Review + create** page, review your selections, and then select **Create** to complete this configuration.

Your configuration now appears on the Partner compliance management page.

### Modify the configuration for a compliance partner

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Tenant Administration** > **Connectors and Tokens** > **Partner Compliance management**, and then select the partner configuration you want to modify. Configurations are ordered by platform type.

3. On the partner configuration **Overview** page, select **Properties** to open the Properties page where you can edit the assignments.

4. On the **Properties** page, select **Edit** to open the Assignments view where you can change the groups that will use this configuration.

5. Select **Review + save** and then **Save** to save your edits.

## Configure your compliance partner to work with Intune

To enable a device compliance partner to work with Intune, you must complete configurations specific to that partner. For information on this task, see the documentation for the applicable partner:

- [VMware Workspace ONE](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## Enroll your iOS or Android devices to that device compliance partner

Refer to device compliance partners documentation for how to enroll devices with that partner. After devices enroll and submit compliance data to the partner, that compliance data is forwarded to Intune and added to Azure AD.

## Monitor devices managed by third-party device compliance partners

After you configure third-party device compliance partners and enroll devices with them, the partner will forward compliance details to Intune. After Intune receives that data,  you can view details about the devices in the Microsoft Endpoint Manager admin center.  

Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and go to **Endpoint security** > **All devices**.  Devices that are managed by a third-party partner MDM authority, display the name of that partner in the **Managed by** column. 

For more information about this view, see [Manage devices](../protect/endpoint-security-manage-devices).

## Next steps

- [Get started with device compliance policy](../protect/device-compliance-get-started.md)
