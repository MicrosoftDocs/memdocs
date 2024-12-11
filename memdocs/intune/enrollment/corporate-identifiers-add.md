---
# required metadata

title: Add corporate identifiers to Intune
description: Add corporate identifiers (enrollment method, IMEI, and serial numbers) to Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/08/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 566ed16d-8030-42ee-bac9-5f8252a83012

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Identify devices as corporate-owned  

*Applies to: Android, iOS/iPadOS, Windows 10, Windows 11*  

Ensure that corporate devices are marked as *corporate-owned* as soon as they enroll by adding their corporate identifiers ahead of time in the Microsoft Intune admin center. The benefit of managing corporate devices is that they enable more device management capabilities than personal devices. For example, Microsoft Intune can collect full phone number and app inventory from a corporate device, but can only collect partial phone number and app inventory for personal devices. To add corporate identifiers to Microsoft Intune, you can upload a file of corporate identifiers in the admin center or enter each identifier separately.

It isn't necessary to add corporate identifiers for all deployments. During enrollment, Intune automatically assigns corporate-owned status to devices that join to Microsoft Entra via:  

- [Device enrollment manager](device-enrollment-manager-enroll.md) account (all platforms)
- An Apple device enrollment program such as [Apple School Manager](apple-school-manager-set-up-ios.md), Apple Business Manager, or [Apple Configurator](apple-configurator-enroll-ios.md) (iOS/iPadOS only)  
- [Windows Autopilot](/autopilot/windows-autopilot)
- Co-management with Microsoft Intune and group policy (GPO)  
- Azure Virtual Desktop  
- Automatic mobile device management (MDM) enrollment via provisioning package  
- [Knox Mobile Enrollment](android-samsung-knox-mobile-enroll.md)
- Android Enterprise management: 
  - [Coporate-owned devices with work profile](./android-corporate-owned-work-profile-enroll.md)  
  - [Fully managed devices](./android-fully-managed-enroll.md)  
  - [Dedicated devices](./android-kiosk-enroll.md).
- Android Open Source Project (AOSP) management:
  - [Corporate-owned user-associated devices](./android-aosp-corporate-owned-user-associated-enroll.md)
  - [Corporate-owned userless devices](./android-aosp-corporate-owned-userless-enroll.md)  
  - [Google Zero Touch](android-dedicated-devices-fully-managed-enroll.md#enroll-by-using-google-zero-touch)  

Microsoft Intune marks devices that register with Microsoft Entra as personal.

## Role-based access control  

To add corporate identifiers in Microsoft Intune, you must be assigned one of these roles:  

- Policy and Profile Manager, a Microsoft Intune built-in role  
- [Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator), a Microsoft Entra built-in role    

These roles can *read*, *delete*, *create*, and *update* corporate device identifiers.    

|Permission| Description |
|---------------|------------|
|Read | View the IMEI or serial numbers used as corporate device identifiers. | 
|Delete | Delete IMEI or serial numbers used as corporate device identifiers. |
|Create | Create new corporate device identifiers or import a CSV file containing a list of corporate device identifiers. |
|Update | Change IMEI or serial numbers used as corporate device identifiers. |  

You can also create a custom Intune role for people managing corporate identifiers and assign corporate device identifier permissions. For more information about built-in roles and custom roles, see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).  

## Supported corporate identifiers  

 Before you begin, determine the type of corporate identifiers you want to add. You can add one type of corporate identifier per CSV file. Devices that enroll without corporate identifiers are marked as *personal*. Intune supports the following identifiers:

- IMEI
- Serial number  
- Serial number, manufacturer, and model (Windows only)  

### Support by platform 

The following table shows the identifiers supported for each platform. When a device with a matching identifier enrolls, Intune marks it as *corporate*.  

| Platform | IMEI number | Serial number | Serial number, model, manufacturer |  
|---|---|---|---|
| Windows 11 | Not supported | Not supported | ✔️ <br></br> Supported with Windows 11, version 22H2 and later with [KB5035942 (OS Builds 22621.3374 and 22631.3374)](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df). | 
| Windows 10 | Not supported | Not supported | ✔️ <br></br> Supported with Windows 10, version 22H2 and later with [KB5039299 (OS Build 19045.4598)](https://support.microsoft.com/topic/june-25-2024-kb5039299-os-build-19045-4598-preview-d4e3e815-fdd8-465e-8144-42afa165efed). |
| iOS/iPadOS | ✔️ <br></br> Supported in some cases. For more information, see [Add Android, iOS corporate identifiers](#add-android-ios-corporate-identifiers). | ✔️ <br></br> We recommend using a serial number for iOS/iPadOS identification when possible.  |Not supported|
| macOS | Not supported | ✔️ |Not supported |
| Android device administrator | ✔️ <br></br> Supported with Android 9 and earlier. | ✔️ <br></br> Supported with Android 9 and earlier. |Not supported |
| Android Enterprise, personally owned work profile  | ✔️ <br></br> Supported with Android 11 and earlier. | ✔️ <br></br> Supported with Android 11 and earlier. |Not supported |  

<!-- When you upload serial numbers for corporate-owned iOS/iPadOS devices, they must be paired with a corporate enrollment profile. Devices must then be enrolled using either Apple's Automated Device Enrollment or Apple Configurator to have them appear as corporate-owned. -->  

## Step 1: Create CSV file
Create a list of corporate identifiers and save it as a CSV file. You can add up to 5,000 rows or 5 MB of data per file, whichever comes first. Don't add headers.

> [!IMPORTANT]
> Remember, only add one type of corporate identifier per CSV file.  

### Add Android, iOS corporate identifiers

To add corporate identifiers for Android and iOS/iPadOS platforms, list one IMEI or serial number per line as shown in the following example.

```
01234567890123,device details  
02234567890123,device details  
```

Remove all periods, if applicable, from the serial number before you add it to the file. You can add device details after each corporate identifier. Details are limited to 128 characters and are for administrative use only. They don't appear on the device.  

Android and iOS/iPadOS devices can have multiple IMEI numbers. Intune reads and records one IMEI per enrolled device. If you import an IMEI that's different from the one already in Intune, Intune will mark the device as personal. If you import multiple IMEI numbers for the same device, the identifiers that haven't been inventoried appear with an *unknown* enrollment status.

Android serial numbers aren't guaranteed to be unique or present. Check with your device supplier to find out if the serial number is a reliable device ID. Serial numbers reported by the device to Intune might not match the ID shown on the device in Android settings or Android device information. Verify the type of serial number reported by the device manufacturer.  

### Add Windows corporate identifiers  

> [!IMPORTANT]
> Windows corporate identifiers only apply at enrollment time. They don't determine ownership type in Intune after enrollment. Corporate identifiers are supported for devices running Windows 10 KB5039299 (with OS Build 19045.4598) and later. If you're enrolling Windows 10 devices with an earlier build, do not use the corporate identifier feature.

To add corporate identifiers for corporate devices running Windows 11, list the manufacturer, model, and serial number for each device as shown in the following example.  

```
Microsoft,surface 5,01234567890123   
Lenovo,thinkpad t14,02234567890123  
```

Remove all periods, if applicable, from the serial number before you add it to the file.  

After you add Windows corporate identifiers, Intune marks devices that match all three identifiers as corporate-owned, and marks all other enrolling devices in your tenant as personal. This means that anything you exclude from the Windows corporate identifiers is marked personal, but only at enrollment time. Existing Windows logic determines the final state in Intune. For more information, see the table in this section. To change the ownership type in Intune, you have to manually adjust it in the admin center.  

:::image type="content" source="./media/corporate-identifiers-add/device-enrollment-add-identifiers.png" alt-text="Screenshot of selecting and adding corporate identifiers.":::

The following table lists the type of ownership given to devices when they enroll without corporate identifiers and when they enroll with corporate identifiers. 

>[!TIP]
> As a reminder, corporate identifiers only change the device state at enrollment time. This means that after the device enrolls, the device state matches what you see in the **Without corporate identifiers** column in the table.  

|Windows enrollment types | Without corporate identifiers | With corporate identifiers |
|---|---|---|
| The device enrolls through [Windows Autopilot](/autopilot/enrollment-autopilot) | Corporate | Corporate |
| The device enrolls through GPO, or [automatic enrollment from Configuration Manager for co-management](/configmgr/comanage/quickstart-paths) | Corporate | Corporate|
| The device enrolls through a [bulk provisioning package](windows-bulk-enroll.md) | Corporate | Corporate |
| The enrolling user is using a [device enrollment manager account](device-enrollment-manager-enroll.md) | Corporate | Corporate |
| The device enrolls through Azure Virtual desktop (non-hybrid) | Corporate | Corporate |
| [Automatic MDM enrollment](windows-enroll.md) with [Microsoft Entra join during Windows setup](/azure/active-directory/device-management-azuread-joined-devices-frx) | Corporate, but will be blocked by personal enrollment restriction | Personal, unless defined by corporate identifiers |
| [Automatic MDM enrollment](windows-enroll.md) with [Microsoft Entra join from Windows Settings](/azure/active-directory/device-management-azuread-joined-devices-frx) | Corporate, but will be blocked by personal enrollment restriction | Personal, unless defined by corporate identifiers |
| [Automatic MDM enrollment](windows-enroll.md) with Microsoft Entra join or hybrid Entra join via [Windows Autopilot for existing devices](/autopilot/existing-devices) | Corporate, but will be blocked by personal enrollment restriction | Personal, unless defined by corporate identifiers |
| [Autopilot device preparation profile](/autopilot/device-preparation/tutorial/user-driven/entra-join-workflow#windows-autopilot-device-preparation-user-driven-microsoft-entra-join-process) | Corporate, but will be blocked by personal enrollment restriction | Personal, unless defined by corporate identifiers |
| [Automatic MDM enrollment](windows-enroll.md) with [Add Work Account from Windows Settings](/azure/active-directory/user-help/user-help-register-device-on-network) | Personal | Personal, unless defined by corporate identifiers |
| [MDM enrollment only](/windows/client-management/mdm/mdm-enrollment-of-windows-devices) option from Windows Settings | Personal | Personal, unless defined by corporate identifiers |
| [Enrollment using the Intune Company Portal app](../user-help/enroll-windows-10-device.md) | Personal | Personal, unless defined by corporate identifiers |
| Enrollment via a Microsoft 365 app, which occurs when users select the **Allow my organization to manage my device** option during app sign-in | Personal | Personal, unless defined by corporate identifiers |

Windows corporate identifiers can only change ownership type if someone adds them to Microsoft Intune. If you don't have corporate identifiers for Windows in Intune, or if you remove them, devices that are Microsoft Entra domain joined are marked as corporate-owned at enrollment time. This includes devices enrolled via [automatic MDM enrollment](windows-enroll.md#enable-windows-automatic-enrollment) with:

- [Microsoft Entra join during Windows setup](/azure/active-directory/device-management-azuread-joined-devices-frx).  

- [Microsoft Entra join from Windows settings](/azure/active-directory/user-help/user-help-join-device-on-network).

## Step 2: Add corporate identifiers in admin center

You can upload a CSV file of corporate identifiers, or manually enter the corporate identifiers in the Microsoft Intune admin center. Manual entry isn't available for Windows corporate identifiers.

### Upload CSV file  

Upload the CSV file you created in [Step 1: Create CSV file](#step-1-create-csv-file) to add corporate identifiers.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
1. Go to **Devices** > **Enrollment**.
1. Select the **Corporate device identifiers** tab.  
1. Choose **Add** > **Upload CSV file**.  
1. Select the identifier type. Your options:  
   - **IMEI**  
   - **Serial**
   - **Manufacturer, model, and serial number (Windows only)**  
1. Under **Import identifiers**, find and select the CSV file.  
1. Wait while Intune validates the CSV file. When the total device identifiers count appears onscreen, validation is complete.

   > [!TIP]
   > If your import fails, check that the CSV file meets formatting requirements.

1. Select **Add**, and then look for the success notification at the top of the admin center to confirm that the file is imported.  

   > [!NOTE]
   > A pop-up window prompting you to review duplicate identifiers appears if the CSV file contains corporate identifiers that are already in Intune but have different device details. To resolve the duplicates, select the identifiers that you want to overwrite in Intune. Then select **Ok** to add the identifiers. Intune only compares the first duplicate of each identifier.  

### Manually enter corporate identifiers  

*Applies to Android and iOS/iPadOS*  

Manually add corporate identifiers in the Microsoft Intune admin center.  

1. In the admin center, go to **Devices** > **Enrollment**.
1. Select the **Corporate device identifiers** tab.
1. Choose **Add** > **Enter manually**.  
1. Select the identifier type. Your options:  

   - **IMEI**  
   - **Serial**  

1. Enter the corporate identifier and details. When you're done entering identifiers, select **Add**.  
1. Select **Refresh** to reload your list. The corporate identifiers you added should now be visible.  

   > [!NOTE]
   > A pop-up window prompting you to review duplicate identifiers appears if your entries contain corporate identifiers that are already in Intune but have different device details. To resolve the duplicates, select the identifiers that you want to overwrite. Then select **Ok** to add the identifiers. Intune only compares the first duplicate of each identifier.  

### Check enrollment status  

Follow up on imported devices to ensure that they enroll in Intune. After you add corporate identifiers, you can see the status of the devices in the admin center:  

- **Enrolled**: The device completed enrollment.  
- **Not contacted**: The device hasn't made contact with the Microsoft Intune service. 
- **Not applicable**
- **Failed**: The device didn't complete enrollment.  

## Delete corporate identifiers

1. In the admin center, go to **Devices** > **Enrollment**.
1. Select the **Corporate device identifiers** tab.  
1. Select the device identifiers you want to delete, and choose **Delete**.
1. Confirm the deletion.  

Deleting a corporate identifier for an enrolled device does not change the device's ownership. 

## Change device ownership

To edit a device's identification after enrollment, change its ownership setting in the admin center. An ownership property appears for each device record in Microsoft Intune.  

1. Go to **Devices** > **All devices**.
1. Select a device.  
1. Choose **Properties**.  
1. For **Device ownership**,  select **Personal** or **Corporate**.  

   :::image type="content" source="./media/corporate-identifiers-add/device-properties.png" alt-text="Screenshot of the Managed device properties showing Device category and Device ownership options.":::

When you change a device's ownership type from *corporate* to *personal*, Intune deletes all app information previously collected from that device within seven days. If applicable, Intune also deletes the phone number on record. Intune still collects the inventory of apps installed by the IT admin on the device, and a partial phone number.

When you change the ownership of an iOS/iPad or Android device from *personal* to *corporate*, a push notification is sent through the Company Portal app to inform the device user of the change. To configure push notifications, go to **Tenant administration** > **Customization**. For more information, see [Company Portal - Configuration](../apps/company-portal-app.md#configuration).  

## Block personal devices

To prevent all personal devices from enrolling, configure an [enrollment platform restriction](create-device-platform-restrictions.md#create-a-device-platform-restriction) for personal devices.  

To confirm the reason for an enrollment failure, go to **Devices** > **Enrollment failures** and look in the table under **Failure reason**. In this case, the reason is **Enrollment restriction not met**. Select the reason to open failure details.

## Known issues and limitations  

- Windows corporate device identifiers only apply at enrollment time. This means that when a device with corporate identifiers enrolls using the *Add Work Account from Windows Settings* option, it is marked as corporate-owned only at enrollment time. Microsoft Intune treats it as a corporate device for the enrollment restriction evaluation, but then after that the device appears as a personal device in the admin center. See the table under [Add Windows corporate identifiers](#add-windows-corporate-identifiers) to help you determine the ownership type. Look to the **Without corporate identifiers** column to learn which devices remain corporate or personal in your tenant for the longterm. 
  
- Windows corporate device identifiers are only supported for devices running:  
  
  -  Windows 10 version 22H2 (OS build 19045.4598) or later.
    
  -  Windows 11 version 22H2 (OS build 22621.3374) or later.
    
  -  Windows 11 version 23H2 (OS build 22631.3374) or later.  
  
  Earlier versions can't render the model and manufacturer property. As a result, the property appears in the admin center as **Unknown**.  

- You can upload up to 10 CSV files for Windows corporate identifiers in the admin center. If you need to upload more data, we recommend using PowerShell or the Microsoft Intune Graph API to add corporate identifiers.  

- Windows currently doesn't support device details in CSV files.
  
- Apple user enrollment with Company Portal and account driven user enrollment corporate identifiers are not currently supported because the MDM does not get access to the device serial number, IMEI, and UDID.

## Resources

For details about International Mobile Equipment Identifiers, see [3GGPP TS 23.003](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=729).  

You can use the following script to get the device details required for Windows corporate identifiers:

 ```powershell
 (Get-WmiObject -Class Win32_ComputerSystem | ForEach-Object {$_.Manufacturer, $_.Model, (Get-WmiObject -Class Win32_BIOS).SerialNumber -join ',' })

 ```

To request the device details remotely, use the following script:  

```powershell
Get-CimInstance -ClassName Win32_ComputerSystem | ForEach-Object {$_.Manufacturer, $_.Model, (Get-CimInstance -ClassName Win32_BIOS).SerialNumber -join ','}

```  

 For more information about locating a serial number, see [Find Surface serial number](https://support.microsoft.com/surface/find-the-serial-number-on-your-microsoft-or-surface-device-6c0abc0c-2b45-247d-f959-70e504e55fa5).
