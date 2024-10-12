---
# required metadata

title: Third-party device compliance partners support in Microsoft Intune
description: Use a third-party device compliance partner as a source of compliance data for devices you manage with Intune. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/25/2023
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.reviewer: tycast

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- compliance
- sub-device-compliance
---

# Support third-party device compliance partners in Intune

Several third-party device compliance partners have been evaluated as a supported partner solution that you can integrate with Microsoft Intune. When you use a [third-party device compliance partner](#supported-device-compliance-partners), the partner adds the compliance state data it collects to Microsoft Entra ID. You can then use the device compliance data from the partner along side the compliance results you collect with Intune to power your [conditional access policies](../protect/device-compliance-get-started.md#integrate-with-conditional-access) that help to protect your organization and data.

Third-party partners support one or more of the following platforms:

- Android
- iOS/iPadOS
- macOS

By default, Intune is set up to be the Mobile Device Management (MDM) authority for your devices. When you add a compliance partner to Microsoft Entra ID and Intune, you're configuring that partner to be a source of Mobile Device Management (MDM) authority for the devices you assign to that partner through a Microsoft Entra user group.

To enable user data from device compliance partners, complete the following tasks:

1. **Configure Intune to work with the device compliance partner**, and then configure groups of users whose devices are managed by that compliance partner.

2. **Configure your compliance partner to send data to Intune**.

3. **Enroll your devices to your device compliance partner**.

With these tasks complete, the device compliance partner sends device state details to Intune. Intune adds this information to Microsoft Entra ID. For example, devices in a noncompliant state have a *not compliant* status added to their device record in Microsoft Entra ID. 

## Supported device compliance partners

The following compliance partners are supported as generally available:

- 42Gears SureMDM
- 7P
- Addigy
- BlackBerry UEM
- Citrix Workspace device compliance
- IBM MaaS360
- Jamf Pro
- Kandji
- MobileIron Device Compliance Cloud
- MobileIron Device Compliance On-prem
- Mosyle Fuse
- Mosyle Onek12
- SOTI MobiControl
- VMware Workspace ONE UEM (formerly AirWatch)

> [!NOTE]
> If you offer an MDM product and would like to onboard as a device compliance partner, fill out this Form: [Intune partner compliance onboarding.](https://aka.ms/IntunePartnerComplianceOnboarding)

## Prerequisites

- A subscription to Microsoft Intune, and access to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

- Device users must be assigned a license for Intune.

- A subscription to the device compliance partner.

- Review documentation for your compliance partner for supported device platforms and that partners prerequisites.

## Configure Intune to work with a device compliance partner

Enable support for a device compliance partner to use compliance state data from that partner with your conditional access policies.

### Add a compliance partner to Intune

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Tenant Administration** > **Connectors and Tokens** > **Partner Compliance management** > **Add Compliance Partner**.

   :::image type="content" alt-text="Add a device compliance partner" source="./media/device-compliance-partners/add-compliance-partner.png" lightbox="./media/device-compliance-partners/add-compliance-partner.png":::

3. On the **Basics** page, expand the **Compliance partner** drop-down and select the partner you're adding.

   - To use VMware Workspace ONE as the compliance partner for iOS or Android platforms, select **VMware Workspace ONE mobile compliance**.

   Next, select the drop-down for **Platform**, and select the platform.

   You're limited to a single partner per platform, even if you have added multiple compliance partners to Microsoft Entra ID.

4. On **Assignments**, select the user groups that include devices that are managed by this partner. With this assignment, you change the MDM authority for applicable devices to use this partner. Users who have devices managed by the partner must also be assigned a license for Intune.

5. On the **Review + create** page, review your selections, and then select **Create** to complete this configuration.

Your configuration now appears on the Partner compliance management page.

### Modify the configuration for a compliance partner

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Go to **Tenant Administration** > **Connectors and Tokens** > **Partner Compliance management**, and then select the partner configuration you want to modify. Configurations are ordered by platform type.

3. On the partner configuration **Overview** page, select **Properties** to open the Properties page where you can edit the assignments.

4. On the **Properties** page, select **Edit** to open the Assignments view where you can change the groups that will use this configuration.

5. Select **Review + save** and then **Save** to save your edits.

6. *This step only applies when you use VMware Workspace ONE*:

   From within the Workspace ONE UEM console, you must manually synchronize the changes you saved in the Microsoft Intune admin center. Until you manually sync changes, Workspace ONE UEM isn’t aware of configuration changes, and users in new groups you’ve assigned won’t successfully report compliance.

   To manually sync from Azure Services:
   1. Sign in to your VMware Workspace ONE UEM console.
   2. Go to **Settings** > **System** > **Enterprise Integration** > **Directory Services**.
   3. For *Sync Azure Services*, select **SYNC**.

      All the changes you’ve made since the initial configuration or the last manual synchronization are synchronized from Azure Services to UEM.  

## Configure your compliance partner to work with Intune

To enable a device compliance partner to work with Intune, you must complete configurations specific to that partner. For information on this task, see the documentation for the applicable partner:

- [42Gears SureMDM](https://docs.42gears.com/suremdm/docs/SureMDM/ConditionalAccessintheSureMDMCon.html)
- [Citrix Endpoint Management integration with Microsoft Endpoint Manager](https://docs.citrix.com/en-us/citrix-endpoint-management/integration-with-mem.html)
- [Kandji Device Compliance](https://support.kandji.io/support/solutions/articles/72000630314)
- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/2102/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)

## Enroll your devices to your device compliance partner

Refer to the documentation from your device compliance partner for how to enroll devices with that partner. After devices enroll and submit compliance data to the partner, that compliance data is forwarded to Intune and added to Microsoft Entra ID.

## Monitor devices managed by third-party device compliance partners

After you configure third-party device compliance partners and enroll devices with them, the partner will forward compliance details to Intune. After Intune receives that data,  you can view details about the devices in the Azure portal.

Sign in to the Azure portal and go to **Microsoft Entra ID** > **Devices** > [**All devices**](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/).

## Next steps

Use the documentation from your third-party partner to create compliance policies for devices.

- [Addigy](https://support.addigy.com/hc/en-us/articles/12346305032211)
- [Blackberry UEM](https://docs.blackberry.com/en/id-comm-collab/blackberry-workspaces/blackberry-workspaces-plug-in-for-blackberry-uem/4_10/compatibility-matrix/imm1460398825659/ioz1460399956336)
- [Citrix Endpoint Management - Integrate with Microsoft Entra Conditional Access](https://docs.citrix.com/en-us/citrix-endpoint-management/prepare-to-enroll-devices-and-deliver-resources.html#integrate-with-azure-ad-conditional-access)
- [MobileIron Device Compliance Cloud](https://forums.ivanti.com/s/article/MobileIron-Cloud-Azure-Device-Compliance-for-iOS-and-Android)
- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/2102/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
