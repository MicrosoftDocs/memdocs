---
title: Integrate Samsung Knox E-FOTA with Microsoft Intune
description: Learn how to integrate Samsung Knox E-FOTA with Microsoft Intune to register Samsung devices, configure firmware updates, and monitor campaigns.
ms.date: 08/24/2026
ms.topic: how-to
ms.reviewer: grwilso
ai-usage: ai-generated
ms.custom: msecd-doc-authoring-1017
---

# Samsung Knox E-FOTA integration with Microsoft Intune

Samsung Knox E-FOTA (Firmware Over-the-Air) lets IT administrators remotely deploy firmware updates to corporate-owned Samsung devices. Administrators can select firmware versions and schedule downloads and installations to reduce device downtime. After registration, firmware deployments don't require user interaction.

The Microsoft Intune integration brings Knox E-FOTA capabilities into the admin center. Before you begin, review the device, network, licensing, role, tenant, and cloud prerequisites. With this integration, you can:

- Launch, manage, and monitor firmware update campaigns for Samsung devices from the admin center.
- Lock devices to a specific operating system (OS) version or selected firmware.
- Schedule download and install windows to minimize device downtime.

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> Samsung Knox E-FOTA updates are supported on Android Enterprise devices enrolled in Intune. This support includes the following enrollment types:
> - Android Enterprise corporate-owned dedicated (COSU)
> - Android Enterprise corporate-owned fully managed (COBO)
> - Android Enterprise corporate-owned with a work profile (COPE)
>
> For information about which devices are supported by Samsung Knox, see [Devices Secured by Knox].
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [network-connectivity](../../includes/requirements/network-connectivity.md)]

:::column-end:::
:::column span="3":::
> For information about service ports and endpoints used by Samsung Knox, see [Samsung Knox firewall exceptions].
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]

:::column-end:::
:::column span="3":::

> You need a Samsung Knox E-FOTA license to use the service. For more information, see [Samsung Knox E-FOTA].
>
> You also need at least a Microsoft 365 E3 plan to use the service.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::

> The required permissions depend on the task.
>
> ---
>
> To **set up the Samsung connector**, sign in with an account assigned the [Intune Administrator] role.
>
> You also need a *Samsung Knox administrator* account to connect Intune to Samsung Knox E-FOTA. For more information, see [Manage admins].
>
> If your organization uses [Microsoft Entra Privileged Identity Management (PIM)], activate the Intune Administrator role only when you configure the connector.
>
> ---
>
> To configure devices and manage Samsung Knox E-FOTA deployments, use an account with at least the following permissions:
> - [Android FOTA] (to register devices with Samsung Knox E-FOTA and manage their firmware updates)
> - [Mobile apps] (to deploy the required apps to the devices)
> - [Device configurations] (to configure the devices by using an OEM configuration template)

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [tenant-configuration](../../includes/requirements/tenant-configuration.md)]

:::column-end:::
:::column span="3":::
> You must configure Managed Google Play for your tenant. For setup instructions, see [Set up Managed Google Play](../../device-enrollment/android/connect-managed-google-play.md).
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [cloud](../../includes/requirements/cloud.md)]
:::column-end:::
:::column span="3":::

> Samsung Knox E-FOTA updates are supported in the public cloud.
:::column-end:::
:::row-end:::

## Process overview

The process for using Samsung Knox E-FOTA through Intune is as follows:

1. [Set up the Samsung connector](#set-up-the-samsung-connector).
1. [Deploy the required apps to the devices](#deploy-the-required-apps-to-the-devices).
1. [Configure the devices by using an OEM configuration template](#configure-the-devices-by-using-an-oem-configuration-template).
1. [Sync devices with Samsung](#sync-devices-with-samsung).
1. [Complete device registration](#complete-device-registration).

After the devices are registered with Samsung, you can create an E-FOTA deployment to manage firmware updates for the devices.

### :::image type="icon" source="media/setup-samsung-knox/connector.svg" border="false":::&nbsp;Set up the Samsung connector

In the Microsoft Intune admin center, link Intune and Samsung Knox E-FOTA by creating a connector. The connector allows Intune to communicate with Samsung Knox E-FOTA and manage firmware updates for eligible Samsung devices.

1. Sign in to the [Microsoft Intune admin center].
1. Select **[Tenant administration]** > **[Connectors and tokens]** > **[Firmware over-the-air update]**.
1. Select **Samsung**.
1. Select **Connect**, and then select **Connect** again to confirm. The Samsung Knox E-FOTA portal opens. Sign in with a Samsung Knox administrator account and authorize the connection.
1. After the connection is established, you're redirected to the Intune admin center. The connector is listed as **Connected**.

> [!NOTE]
> If you use EMM group sync in Knox E-FOTA, connecting your Knox account to Intune doesn't retain the existing group sync configuration. In the Knox Admin Portal, connect Microsoft Intune again and select the device groups to sync. For instructions, see [Add device groups from Microsoft Intune].

### :::image type="icon" source="media/setup-samsung-knox/app.svg" border="false":::&nbsp;Deploy the required apps to the devices

Samsung Knox requires the following apps on each device to enroll it in the E-FOTA service:

- **Knox E-FOTA** (`com.samsung.android.knox.efota`)
- **Knox Service Plugin** (`com.samsung.android.knox.kpu`)

Add both apps to your tenant through Managed Google Play. Assign the apps as **Required** to the security groups that contain the Samsung devices you want to register. Intune then deploys the apps to those devices.

For more information, see [Add and assign Managed Google Play apps to Android Enterprise devices](../../app-management/deployment/add-managed-google-play.md).

### :::image type="icon" source="media/setup-samsung-knox/configure.svg" border="false":::&nbsp;Configure the devices by using an OEM configuration template

To manage firmware updates through the E-FOTA service, configure the devices by using an OEM configuration template.

1. Sign in to the [Microsoft Intune admin center].
1. Select **Devices** > **Configuration**.
1. Under **Policies**, select **Create**.
1. In **Create profile**, use the following settings and select **Create**:
   - **Platform**: Android Enterprise
   - **Profile type**: Templates
   - **Template name**: OEMConfig
1. Under **Configuration settings**, select:
   - **Enable device policy controls**: true
   - **Enable firmware controls**: true
   - **Enable E-FOTA client installation & launch**: true
1. Assign the device configuration to the same security group that contains the devices you registered with Samsung.
1. Select **Next**.

### :::image type="icon" source="media/setup-samsung-knox/registration.svg" border="false":::&nbsp;Sync devices with Samsung

To manage firmware updates for Samsung devices with Intune, register the devices with Samsung Knox E-FOTA. Assign the security groups that contain these devices to the Samsung connector.

To register the devices with Samsung:

1. Sign in to the [Microsoft Intune admin center].
1. Select **[Tenant administration]** > **[Connectors and tokens]** > **[Firmware over-the-air update]**.
1. Select **Samsung** to open the Samsung Knox E-FOTA connector setup.
1. Select **Add groups**, and then select the security groups that contain the Samsung devices to manage by using E-FOTA.
1. Select **Register**.
1. The devices are uploaded to Samsung. Use the Samsung Knox administrator account to view them in the Knox Admin Portal.

### :::image type="icon" source="media/setup-samsung-knox/registration-complete.svg" border="false":::&nbsp;Complete device registration

On each targeted Samsung device, open the **Knox E-FOTA** app. A device user must accept the terms and conditions to complete registration with Samsung Knox E-FOTA.

## Create an E-FOTA update campaign

After you register the devices with Samsung Knox E-FOTA, you can create a deployment to manage the firmware updates for the devices you registered. Samsung Knox E-FOTA deployments are also called *campaigns*.

1. Sign in to the [Microsoft Intune admin center].
1. Select **Devices** > **Android** > **Manage updates** > **Android FOTA deployments**.
1. Select **Create**.
1. In the **Create deployment - Basics** pane, select the device model, sales code, CSC, and firmware version.
1. In the **Create deployment - Settings** pane, configure the **deployment schedule**, **installation schedule**, and **device condition**.
1. Assign the deployment to the group of devices you registered with Samsung.
1. On the **Monitor** tab, review the campaign summary and status. From the summary, you can edit, cancel, or delete the campaign and open the campaign report. Status data from Samsung refreshes every hour.

You can also review the campaign in the Knox Admin Portal. After you assign the campaign, verify its status on a targeted Samsung device in the Knox E-FOTA app.

## Device registration status report

You can view the device registration status for devices registered with Samsung Knox E-FOTA in the Intune admin center. The report refreshes every hour with device status from Samsung.

To view the device registration status report:

1. Sign in to the [Microsoft Intune admin center].
1. Select **[Tenant administration]** > **[Connectors and tokens]** > **[Firmware over-the-air update]**.
1. Select **Samsung**.
1. Select the **Monitor** tab to view the device registration status report.
1. To view the list of devices registered with Samsung, select **View devices**. The device registration status report shows the following information for each device:
   - **Device name**
   - **Registration status**
   - **Status detail**
   - **Last status update (UTC)**

## Disconnect the Samsung connector

To disconnect the Samsung connector, follow these steps:

1. Sign in to the [Microsoft Intune admin center].
1. Select **[Tenant administration]** > **[Connectors and tokens]** > **[Firmware over-the-air update]**.
1. Select **Samsung**.
1. Select **Disconnect** and confirm the disconnection. This action disconnects your Intune tenant from Samsung Knox E-FOTA.

<a name='related-content'></a>

## Next step

- [Samsung Knox E-FOTA documentation](https://docs.samsungknox.com/admin/knox-efota/)

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431
[Tenant administration]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/TenantAdminMenu/~/tenantStatus
[Connectors and tokens]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/TenantAdminMenu/~/connectorsAndTokens
[Firmware over-the-air update]: https://go.microsoft.com/fwlink/?linkid=2109431#view/Microsoft_Intune_DeviceSettings/TenantAdminConnectorsMenu/~/fotaUpdate
[Intune Administrator]: /entra/identity/role-based-access-control/permissions-reference#intune-administrator
[Microsoft Entra Privileged Identity Management (PIM)]: /entra/id-governance/privileged-identity-management/pim-configure

[Android FOTA]: /intune/fundamentals/role-based-access-control/create-custom-role#android-fota
[Device configurations]: /intune/fundamentals/role-based-access-control/create-custom-role#device-configurations
[Mobile apps]: /intune/fundamentals/role-based-access-control/create-custom-role#mobile-apps

<!-- Samsung Knox links -->
[Devices Secured by Knox]: https://www.samsungknox.com/knox-platform/supported-devices
[Samsung Knox E-FOTA]: https://docs.samsungknox.com/admin/knox-efota/
[Samsung Knox firewall exceptions]: https://docs.samsungknox.com/admin/knox-admin-portal/get-started/samsung-knox-firewall-exceptions/#knox-e-fota
[Add device groups from Microsoft Intune]: https://docs.samsungknox.com/admin/knox-efota/emm-integration/microsoft-intune/add-device-groups-from-microsoft-intune/
[Manage admins]: https://docs.samsungknox.com/admin/knox-admin-portal/how-to-guides/admins-and-roles/manage-admins/
