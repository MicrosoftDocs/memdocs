---
# required metadata

title: Restrict USB devices using administrative templates in Microsoft Intune
description: Use Administrative templates in Microsoft Intune to restrict USB devices, including thumb drives, flash drives, USB cameras, and more. Use other settings to allow specific USB devices on Windows 10/11 devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/10/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano, kufang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Restrict USB devices and allow specific USB devices using Administrative Templates in Microsoft Intune

Many organizations want to block specific types of USB devices, such as USB flash drives or cameras. You may also want to allow specific USB devices, such as a keyboard or mouse.

You can use Administrative Templates (ADMX) templates to configure these settings in a policy, and then deploy this policy to your Windows devices. For more information on Administrative Templates, and what they are, see [Use Windows 10/11 templates to configure group policy settings in Microsoft Intune](administrative-templates-windows.md).

This article shows you how to create an ADMX policy with USB settings, and use a log file to troubleshoot devices that shouldn't be blocked.

Applies to:

- Windows 11
- Windows 10

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Templates** > **Administrative Templates**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. For example, enter **Restrict USB devices**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, configure the following settings:

    - **Prevent installation of devices not described by other policy settings**: Select **Enabled** > **OK**:

      :::image type="content" source="media/administrative-templates-restrict-usb/prevent-installation-of-devices-not-described-setting.png" alt-text="In Intune, set the Prevent installation of devices not described by other policy settings setting to Enabled.":::

    - **Allow installation of devices using drivers that match these device setup classes**: Select **Enabled**. Then, add the [class GUID of the device classes](/windows-hardware/drivers/install/system-defined-device-setup-classes-available-to-vendors) you want to allow.

      In the following example, the **Keyboard**, **Mouse**, and **Multimedia** classes are allowed:

      :::image type="content" source="media/administrative-templates-restrict-usb/allow-installation-of-devices-using-drivers-setting.png" alt-text="Screenshot that shows how to set the Allow installation of devices using drivers that match these device setup classes setting in Intune and how to add your class GUIDs.":::

      Select **OK**.

    - **Allow installation of devices that match any of these Device IDs**: Select **Enabled**. Then, add the device/hardware IDs for devices you want to allow:

       :::image type="content" source="media/administrative-templates-restrict-usb/allow-installation-of-devices-that-match-setting.png" alt-text="Screenshot that shows how to set the Allow installation of devices that match any of these Device IDs setting in Intune and how to add your hardware IDs.":::

      To get the device/hardware ID, you can use Device Manager, find the device, and look at the properties. For the specific steps, see [find the hardware ID on a Windows device](/windows-hardware/drivers/install/hardware-ids).

      There's also some helpful device ID information at       [Microsoft Defender for Endpoint Device Control Device Installation: Deploying and managing policy via Intune](/microsoft-365/security/defender-endpoint/mde-device-control-device-installation#deploying-and-managing-policy-via-intune).

      Select **OK**.

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the device groups that will receive the profile. Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved and the profile is assigned.

## Verify on Windows devices

After the device configuration profile is deployed to your targeted devices, you can confirm that it works correctly.

If a USB device is blocked from installing, then you see a message similar to the following message:

`The installation of this device is forbidden by system policy. Contact your system administrator.`

In the following example, the iPad is blocked because its device ID isn't in the allowed device ID list:

:::image type="content" source="media/administrative-templates-restrict-usb/device-status.png" alt-text="Device blocked by group policy.":::

## A device is blocked but should be allowed

Some USB devices have multiple GUIDs, and it's common to miss some GUIDs in your policy settings. As a result, a USB device that's allowed in your settings, might be blocked on the device.

In the following example, in the **Allow installation of devices using drivers that match these device setup classes** setting, the Multimedia class GUID is entered, and the camera is blocked:

:::image type="content" source="media/administrative-templates-restrict-usb/camera-blocked.png" alt-text="Windows can't find your camera message on a Windows device.":::

:::image type="content" source="media/administrative-templates-restrict-usb/cam-blocked.png" alt-text="The camera is blocked by group policy message on a Windows device.":::

**Resolution**:

To find the GUID of your device, use the following steps:

1. On the device, open the `%windir%\inf\setupapi.dev.log` file.
2. In the file:

    1. Search for **Restricted installation of devices not described by policy**. 
    2. In this section, find the `Class GUID of device changed to: {GUID}` text. This `{GUID}` needs added to your policy.

        In the following example, you see the `Class GUID of device changed to: {36fc9e60-c465-11cf-8056-444553540000}` text:

        ```log
        >>>  [Device Install (Hardware initiated) - USB\VID_046D&PID_C534\5&bd89ed7&0&2]
        >>>  Section start 2020/01/20 17:26:03.547
       dvi: {Build Driver List} 17:26:03.597
       …
       dvi: {Build Driver List - exit(0x00000000)} 17:26:03.645
       dvi: {DIF_SELECTBESTCOMPATDRV} 17:26:03.647
       dvi:      Default installer: Enter 17:26:03.647
       dvi:           {Select Best Driver}
       dvi:                Class GUID of device changed to: {36fc9e60-c465-11cf-8056-444553540000}.
       dvi:                Selected Driver:
       dvi:                     Description - USB Composite Device
       dvi:                     InfFile     - c:\windows\system32\driverstore\filerepository\usb.inf_amd64_9646056539e4be37\usb.inf
       dvi:                     Section     - Composite.Dev
       dvi:           {Select Best Driver - exit(0x00000000)}
       dvi:      Default installer: Exit
       dvi: {DIF_SELECTBESTCOMPATDRV - exit(0x00000000)} 17:26:03.664
       dvi: {Core Device Install} 17:26:03.666
       dvi:      {Install Device - USB\VID_046D&PID_C534\5&BD89ED7&0&2} 17:26:03.667
       dvi:           Device Status: 0x01806400, Problem: 0x1 (0xc0000361)
       dvi:           Parent device: USB\ROOT_HUB30\4&278ca476&0&0
        !!! pol:           The device is explicitly restricted by the following policy settings:
        !!! pol:           [-] Restricted installation of devices not described by policy
        !!! pol:      {Device installation policy check [USB\VID_046D&PID_C534\5&BD89ED7&0&2] exit(0xe0000248)}
        !!! dvi:      Installation of device is blocked by policy!
        !   dvi:      Queueing up error report for device install failure.
       dvi: {Install Device - exit(0xe0000248)} 17:26:03.692
       dvi: {Core Device Install - exit(0xe0000248)} 17:26:03.694
        <<<  Section end 2020/01/20 17:26:03.697
        <<<  [Exit status: FAILURE(0xe0000248)]
        ```

3. In the device configuration profile, go to the **Allow installation of devices using drivers that match these device setup classes** setting, and add the class GUID from the log file.
4. If the issue continues, repeat these steps to add the other class GUIDs until the device is successfully installed.

    In our example, the following class GUIDs are added to the device profile:

    - USB Bus devices (hubs and host controllers): `{36fc9e60-c465-11cf-8056-444553540000}`
    - Human Interface Devices (HID): `{745a17a0-74d3-11d0-b6fe-00a0c90f57da}`
    - Camera devices: `{ca3e7ab9-b4c3-4ae6-8251-579ef933890f}`
    - Imaging devices: `{6bdd1fc6-810f-11d0-bec7-08002be2092f}`

## Common class GUIDs to allow USB devices

- **Keyboard and mouse**: Add the following GUIDs to the device profile:

  - Keyboard: `{4d36e96b-e325-11ce-bfc1-08002be10318}`
  - Mouse: `{4d36e96f-e325-11ce-bfc1-08002be10318}`

- **Cameras, headphones and microphones**: Add the following GUIDs to the device profile:

  - USB Bus devices (hubs and host controllers): `{36fc9e60-c465-11cf-8056-444553540000}`
  - Human Interface Devices (HID): `{745a17a0-74d3-11d0-b6fe-00a0c90f57da}`
  - Multimedia devices: `{4d36e96c-e325-11ce-bfc1-08002be10318}`
  - Camera devices: `{ca3e7ab9-b4c3-4ae6-8251-579ef933890f}`
  - Imaging devices: `{6bdd1fc6-810f-11d0-bec7-08002be2092f}`
  - System devices: `{4D36E97D-E325-11CE-BFC1-08002BE10318}`
  - Biometric devices: `{53d29ef7-377c-4d14-864b-eb3a85769359}`
  - Generic software devices: `{62f9c741-b25a-46ce-b54c-9bccce08b6f2}`

- **3.5 mm headphones**: Add the following GUIDs to the device profile:

  - Multimedia devices: `{4d36e96c-e325-11ce-bfc1-08002be10318}`
  - Audio endpoint: `{c166523c-fe0c-4a94-a586-f1a80cfbbf3e}`

> [!NOTE]
> The actual GUIDs may be different for your specific devices.

## Next steps

[Learn more about ADMX templates in Microsoft Intune](administrative-templates-windows.md)
