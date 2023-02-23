---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 02/23/2023
ms.localizationpriority: medium
---

Before a device can use Autopilot, it must be registered as an Autopilot device. Registering a devices as an Autopilot device can be thought of as importing the device into Autopilot so that Autopilot can be used on the device. It does not mean that the device has ever used the Autopilot service. It just makes the Autopilot service available to the device.

Also note that a device registered in Autopilot doesn't mean the device is enrolled in Intune. A device may be registered as an Autopilot device but may not exist in Intune. It's not until an Autopilot registered device goes through the Autopilot process for the first time that it becomes enrolled in Intune. After the Autopilot device undergoes the Autopilot process and enrolls in Intune, the Autopilot device subsequently appears as a device in both Azure AD and Intune.

> [!TIP]
>
> For Configuration Manager admins, an Autopilot device before undergoing the Autopilot process for the first time can be thought of as the equivalent of an Unknown Computer.

There are several methods to register a device as an Autopilot device in Intune:

- Manually registering devices into Intune as an Autopilot device via the hardware hash. The hardware hash of a device can be collected via one of the following methods:

  - [Configuration Manager](/mem/configmgr/comanage/how-to-prepare-Win10#windows-autopilot)
  - [PowerShell script](/mem/autopilot/add-devices#powershell)
  - [Diagnostics page hash export](/mem/autopilot/add-devices#diagnostics-page-hash-export)
  - [Desktop hash export](/mem/autopilot/add-devices#desktop-hash-export)
  
  The above methods of obtaining the hardware hash of a device are well documented. The corresponding documentation can be viewed by selecting the appropriate link listed above.

- Automatically registering device via:
  - An [OEM](/mem/autopilot/oem-registration), including [Microsoft Surface](/surface/surface-autopilot-registration-support) devices
  - A [partner](/mem/autopilot/partner-registration)

  Registering a device via an OEM or partner is also well documented. The corresponding documentation can be viewed by selecting the appropriate link listed above.

For most organizations, using an OEM or partner to register devices as Autopilot devices is the preferred, most common, and most secure method. However for smaller organizations, for testing/lab scenarios, and for emergency scenarios, manually registering devices as Autopilot devices via the hardware hash is also used.

> [!IMPORTANT]
>
> Assuming that a device isn't currently enrolled Intune, remember that registering a device in Autopilot doesn't make it an Intune enrolled device. That device won't enroll into Intune until Autopilot runs on the device for the first time.

### Importing the hardware hash CSV file for devices into Intune

Several of the above methods on obtaining the hardware hash when manually registering devices as Autopilot devices will produce a CSV file that contains the hardware hash of the device. This CSV file with the hardware hash needs to be imported into Intune to register the device as an Autopilot device.

After the CSV files has been created, it can be imported into Intune via the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **By platform: Windows**.

3. Select **Windows enrollment** > **Windows Autopilot Deployment Program: Devices**.

4. In the **Windows Autopilot devices** screen, select **Import**.

5. In the **Add Windows Autopilot devices** pane, under **Specify the path to the list you want to import.**, select the blue select a file folder.

6. Browse to the CSV file obtained using one of the above methods to obtain the hardware hash of a device.

7. After selecting the CSV file, verify that the correct CSV file is selected under **Specify the path to the list you want to import.**, and then select **Import**. Importing can take several minutes.

8. After the import is complete, in the **Windows Autopilot devices** screen, select **Sync**.

   A message will display saying that the sync is in progress. The sync process might take a few minutes to complete, depending on how many devices are being synchronized.

    > [!NOTE]
    >
    > If another sync is attempted within 10 minutes after initiating a sync, an error will be displayed. Syncs can only occur once every 10 minutes. To attempt a sync again, wait at least 10 minutes before trying again.

9. Select **Refresh** to refresh the view. The newly imported devices should display within a few minutes. If the devices aren't yet displayed, wait a few minutes and then select **Refresh** again.

For more information on registering devices as Autopilot devices, see the following articles:

- [Manually register devices with Windows Autopilot](/mem/autopilot/add-devices)
- [Windows Autopilot customer consent](/mem/autopilot/registration-auth)
