---
title: Third-party device compliance partners support in Microsoft Intune
description: Use a third-party device compliance partner as a source of compliance data for devices you manage with Intune.
ms.date: 02/27/2026
ms.topic: overview
ms.reviewer: ilwu-microsoft
ms.collection:
- M365-identity-device-management
- compliance
- sub-device-compliance
---

# Support third-party device compliance partners in Intune

Microsoft Intune supports integration with several third-party device compliance partners. When you use a [third-party device compliance partner](#supported-device-compliance-partners), the partner adds the compliance state data it collects to Microsoft Entra ID. You can use device compliance data from the partner alongside the compliance results you collect with Intune. Together, these signals power [Conditional Access policies](./overview.md#integrate-with-conditional-access) that help to protect your organization and data.  

By default, Intune is the mobile device management (MDM) authority for your devices. When you add a compliance partner to Microsoft Entra ID and Intune, that partner becomes the MDM authority for devices assigned to it through a Microsoft Entra user group.  

To enable user data from device compliance partners, complete the following tasks:

1. **Configure Intune to work with the device compliance partner**, and then configure groups of users whose devices are managed by that compliance partner.

1. **Configure your compliance partner to send data to Intune**.

1. **Enroll your devices to your device compliance partner**.

With these tasks complete, the device compliance partner sends device state details to Intune. Intune adds this information to Microsoft Entra ID. For example, devices in a noncompliant state have a *not compliant* status added to their device record in Microsoft Entra ID.

## Supported device compliance partners

The following compliance partners are supported as generally available:

- 42Gears SureMDM
- 7P
- Addigy
- BlackBerry UEM
- Citrix Workspace device compliance
- CLOMO MDM
- Fleet
- IBM MaaS360
- Jamf Pro
- Kandji
- Ivanti Neurons for MDM
- Ivanti EPMM
- mobiconnect
- Mosyle Fuse
- Mosyle Onek12
- Omnissa Workspace ONE UEM
- Scalefusion
- SOTI MobiControl

> [!NOTE]
> If you offer an MDM product and want to onboard as a device compliance partner, fill out the form: [Intune partner compliance onboarding](https://aka.ms/IntunePartnerComplianceOnboarding).

## Requirements

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

> - Microsoft Intune subscription with access to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
> - Intune licenses assigned to device users.

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::

> - Android
> - iOS/iPadOS
> - macOS
>
> Not all partners support all platforms. Check your partner's documentation for supported platforms.

:::column-end:::
:::row-end:::

You also need:

- A subscription to the device compliance partner.
- Check your compliance partner's documentation for prerequisites.  

## Configure Intune to work with a device compliance partner

Enable support for a device compliance partner to use compliance state data from that partner with your Conditional Access policies.

### Add a compliance partner to Intune

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Go to **Tenant Administration** > **Connectors and Tokens** > **Partner Compliance management** > **Add Compliance Partner**.

   :::image type="content" alt-text="Add a device compliance partner" source="./media/third-party-partners/add-compliance-partner.png" lightbox="./media/third-party-partners/add-compliance-partner.png":::

1. On **Basics**, expand the **Compliance partner** dropdown and select the partner you want to add.

   - To use Omnissa Workspace ONE UEM as the compliance partner for iOS or Android platforms, select **Omnissa Workspace ONE UEM**.

   Next, select the dropdown for **Platform**, and select the platform.

   You can use only one partner per platform, even if you add multiple compliance partners to Microsoft Entra ID.  

1. On **Assignments**, select the user groups that contain devices managed by this partner. With this assignment, you change the MDM authority for applicable devices to use this partner. Users who have devices managed by the partner must also be assigned a license for Intune.

1. On **Review + create**, review your selections, and then select **Create** to complete this configuration.

Your configuration now appears on the **Partner compliance management** page.

### Modify the configuration for a compliance partner

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Go to **Tenant Administration** > **Connectors and Tokens** > **Partner Compliance management**, and then select the partner configuration you want to modify. Configurations appear by platform type.

1. On the partner configuration **Overview** page, select **Properties** to edit the assignments.

1. On the **Properties** page, select **Edit** to change the assigned groups.

1. Select **Review + save** and then **Save** to save your edits.

1. *This step only applies when you use Omnissa Workspace ONE*:

   From within the Workspace ONE UEM console, you must manually synchronize the changes you saved in the Microsoft Intune admin center. Until you manually sync changes, Workspace ONE UEM isn't aware of configuration changes, and users in newly assigned groups don't successfully report compliance. 

   To manually sync from Azure Services:
   1. Sign in to your Omnissa Workspace ONE UEM console.
   1. Go to **Settings** > **System** > **Enterprise Integration** > **Directory Services**.
   1. For *Sync Azure Services*, select **SYNC**.

      Azure services synchronize all changes made after the initial configuration or the last manual synchronization to UEM.   

## Configure your compliance partner to work with Intune

To enable a device compliance partner to work with Intune, you must complete configurations specific to that partner. For information on this task, see the documentation for the applicable partner:

- [42Gears SureMDM](https://docs.42gears.com/suremdm/docs/SureMDM/ConditionalAccessintheSureMDMCon.html)
- [Citrix Endpoint Management integration with Microsoft Endpoint Manager](https://docs.citrix.com/en-us/citrix-endpoint-management/integration-with-mem.html)
- [CLOMO MDM](https://support.clomo.com/?page_id=61477)
- [Fleet](https://fleetdm.com/guides/entra-conditional-access-integration)
- [Kandji Device Compliance](https://support.kandji.io/support/solutions/articles/72000630314)
- [mobiconnect](https://help.mobi-connect.net/function/function_category/c0119/?func_os=ios-ipados)
- [Omnissa Workspace ONE UEM](https://docs.omnissa.com/bundle/WorkspaceONE-UEM-Managing-DevicesVSaaS/page/ConditionalAccessMicrosoftEntraID.html)
- [Scalefusion](https://help.scalefusion.com/docs/microsoft-intune-partner-compliance)


## Enroll your devices to your device compliance partner

See your device compliance partner's documentation to enroll devices. After devices enroll and submit compliance data to the partner, that compliance data is forwarded to Intune and added to Microsoft Entra ID.

## Monitor devices managed by third-party device compliance partners

After you configure a third-party compliance partner and enroll devices, the partner forwards compliance data to Intune. You can then view device details in the Microsoft Entra admin center.

Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) and go to **Devices** > [**All devices**](https://entra.microsoft.com/#view/Microsoft_AAD_Devices/DevicesMenuBlade/~/Devices).

## Best practices for migrating devices from third-party MDM to Intune MDM

When you migrate devices from third-party MDM providers to a full Intune stack, follow these cleanup steps:

1. Initiate a retirement action from the third-party MDM service before enrolling the device with Intune MDM. This retirement action notifies Intune to perform the necessary cleanup tasks in its third-party integration services.
> [!NOTE]
> Removing the third-party MDM profile locally on a device doesn't sufficiently trigger the Intune cleanup tasks.

1. Confirm that devices retired from the third-party MDM appear in Microsoft Entra ID with **None** listed in the **MDM** column. At this point, your devices can now be enrolled with Intune MDM.

1. After all devices migrate to Intune through steps 1 and 2, disable the Intune connection in your third-party MDM provider's admin console. If that isn't an option, you can also disable the connection console in the Microsoft Intune admin center.
   1. Go to **Tenant administration** > **Connectors and tokens** > **Device compliance partner**.
   1. Select the device compliance partner you want to disable.
   1. Toggle the connection to **Off**.

> [!NOTE]
> If devices don't complete the cleanup tasks and still appear enrolled in Intune, Intune applies its own compliance policies and ignores third‑party policies.  

## Next steps

Use your partner's documentation to create compliance policies for devices.

- [Addigy](https://support.addigy.com/hc/en-us/articles/12346305032211)
- [Blackberry UEM](https://docs.blackberry.com/en/id-comm-collab/blackberry-workspaces/blackberry-workspaces-plug-in-for-blackberry-uem/4_10/compatibility-matrix/imm1460398825659/ioz1460399956336)
- [Citrix Endpoint Management - Integrate with Microsoft Entra Conditional Access](https://docs.citrix.com/en-us/citrix-endpoint-management/prepare-to-enroll-devices-and-deliver-resources.html#integrate-with-azure-ad-conditional-access)
- [Ivanti Neurons for MDM](https://forums.ivanti.com/s/article/MobileIron-Cloud-Azure-Device-Compliance-for-iOS-and-Android)
