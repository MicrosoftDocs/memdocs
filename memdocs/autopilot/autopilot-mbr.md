---
title: Windows Autopilot motherboard replacement
description: Understand how Windows Autopilot deployments function when you replace the motherboard on a device.
ms.prod: windows-client
ms.technology: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/24/2022
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: how-to
---

# Windows Autopilot motherboard replacement scenario guidance

*Applies to:*

- Windows 11
- Windows 10

This document offers guidance for Windows Autopilot device repair scenarios that Microsoft partners can use in motherboard replacement (MBR) situations, and other servicing scenarios.

Repairing Autopilot enrolled devices is complex, as it tries to balance OEM requirements with Windows Autopilot requirements. Specifically, OEM requirements include strict uniqueness across motherboards, MAC addresses, and so on. Windows Autopilot requires strict uniqueness at the hardware hash level for each device to enable successful registration. The hardware hash doesn't always accommodate all the OEM hardware component requirements. So these requirements are sometimes at odds, causing issues with some repair scenarios. The hardware hash is also known as the hardware ID.

If a motherboard is replaced on an Autopilot registered device with the following versions of Windows:

- Windows 11 22H2 (all versions)
- Windows 11 21H2 with [KB5015882](https://support.microsoft.com/topic/july-21-2022-kb5015882-os-build-22000-832-preview-473e1d95-06a0-4f40-9554-cdc7cca85584) or newer installed
- Windows 10 22H2 (all versions)
- Windows 10 21H2 with [KB5017383](https://support.microsoft.com/topic/september-20-2022-kb5017383-os-build-22000-1042-preview-62753265-68e9-45d2-adcb-f996bf3ad393) or newer installed

and the device goes back to the same tenant without an OS reset, Autopilot attempts to register the new hardware components. In Intune, the profile status for the device shows **Fix pending** as Autopilot attempts to register the new hardware components. If the new hardware components are successfully registered, the device status goes back to the assigned Autopilot profile. If the device can't be successfully registered, the profile status for the device shows **Attention required**. 

If the OEM resets the OS, the device needs to be re-registered.

If the following conditions are true:

- The OS version is older than the ones in the above list
- A motherboard is replaced on an Autopilot registered device

then the following process is recommended:

1. If the device isn't going back to the original tenant, [deregister it from Windows Autopilot](#deregister-the-autopilot-device-from-the-autopilot-program). If it's going back to the same tenant, you don't need to deregister it.
2. [Replace the motherboard](#replace-the-motherboard).
3. If the device needs to be re-registered because of a reimage or will be used in a new tenant, [capture a new device ID (4K HH)](#capture-a-new-autopilot-device-id-4k-hh-from-the-device).
4. [Reregister the device](#reregister-the-repaired-device-using-the-new-device-id) with Windows Autopilot.
5. [Reset the device](#reset-the-device).
6. [Return the device](#return-the-repaired-device-to-the-customer).

Each of these steps is described in the following sections.

## Deregister the Autopilot device from the Autopilot program

Before the device arrives at the repair facility, the entity that registered the device must deregister it.

- If the **IT Admin** registered the device, they likely did so via Intune, Microsoft 365 admin center, or a legacy portal such as Microsoft Store for Business (MSfB). If so, they should deregister the device from Intune or Microsoft 365 admin center because devices registered in Intune don't show up in Microsoft Partner Center (MPC).

- If the **OEM or CSP partner** registered the device, they likely did so via the Microsoft Partner Center (MPC). In that case, they should deregister the device from MPC, which also removes it from the customer IT Admin's Intune account.

Below we describe the steps an IT Admin would go through to deregister a device from Intune, and the steps an OEM or CSP would go through to deregister a device from MPC.

To avoid problems, an OEM or CSP should register Autopilot devices whenever possible. If the customer registers the devices, OEMs or CSPs can't deregister them if, for example, a customer leasing a device goes out of business before deregistering it themselves.

If a customer grants an OEM permission to register devices on their behalf using the automated consent process, an OEM can use the API to deregister devices they didn't register themselves. This deregistration only removes those devices from the Autopilot program. It doesn't unenroll them from Intune or disjoin them from Azure AD. Only the customer can unenroll the device from Intune or disjoin the device from Azure AD.

## Deregister a device

[!INCLUDE [Deregister an Autopilot device](includes/deregister-autopilot-device.md)]

Because the repair facility doesn't have the user's sign-in credentials, they have to reimage the device as part of the repair process. The customer should do three things before sending the device to the facility:

1. Copy all important data off the device.
2. Let the repair facility know which version of Windows they should reinstall after the repair.
3. If applicable, let the repair facility know which version of Office they should reinstall after the repair.

## Replace the motherboard

Technicians replace the motherboard or other hardware on the broken device. A replacement Digital Product Key (DPK) is injected.

Repair and key replacement processes vary between facilities. Sometimes repair facilities receive motherboard spare parts from OEMs that have replacement DPKs already injected, but sometimes not. Sometimes repair facilities receive fully functional BIOS tools from OEMs, but sometimes not. The quality of the data in the BIOS after an MBR varies. To ensure the repaired device are still Autopilot capable following its repair, check to make sure the new post-repair BIOS can successfully gather and populate the following information at a minimum:

- DiskSerialNumber
- SmbiosSystemSerialNumber
- SmbiosSystemManufacturer
- SmbiosSystemProductName
- SmbiosUuid
- TPM EKPub
- MacAddress
- ProductKeyID
- OSType

For simplicity, and because processes vary between repair facilities, we've excluded many of the additional steps often used in an MBR, such as:

- Verify that the device is still functional
- Disable or suspend BitLocker
- Repair the Boot Configuration Data (BCD)
- Repair and verify the network driver operation

## Capture a new Autopilot device ID (4K HH) from the device

Repair technicians must sign in to the repaired device to capture the new device ID. If the repair technician doesn't have access to the customer's sign-in credentials, they have to reimage the device to gain access:

1. The repair technician creates a [WinPE bootable USB drive](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#create-a-bootable-windows-pe-winpe-partition).

2. The repair technician boots the device to WinPE.

3. The repair technician [applies a new Windows image to the device](/windows-hardware/manufacture/desktop/work-with-windows-images).

    Ideally, the same Windows version that was originally on the device should be reimaged onto the device. Some coordination is required between the repair facility and customer to capture this information at the time the device arrives for repair. Such coordination might include the customer sending the repair facility a customized image (.ppk file) via a USB stick, for example.

4. The repair technician boots the device into the new Windows image.

5. Once on the desktop, the repair technician captures the new device ID (4K HH) off the device using either the OA3 Tool or the PowerShell script.

Those repair facilities with access to the OA3 Tool (which is part of the ADK) can use the tool to capture the 4K Hardware Hash (4K HH).

Instead, the [WindowsAutopilotInfo PowerShell script](https://www.powershellgallery.com/packages/Get-WindowsAutopilotInfo) can be used to capture the 4K HH.

> [!NOTE]
> Other methods in addition to Windows PowerShell are also available to capture the hardware hash. For more information, see [Collect the hardware hash](add-devices.md#collect-the-hardware-hash).

To use the **WindowsAutopilotInfo** PowerShell script, follow these steps:

1. Install the script from the [PowerShell Gallery](https://www.powershellgallery.com/packages/Get-WindowsAutopilotInfo) or from the command line.

2. Navigate to the script directory and run it on the device when the device is either in Full OS or Audit Mode. See the following example.

   ```powershell
   md c:\HWID
   Set-Location c:\HWID
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
   Install-Script -Name Get-WindowsAutopilotInfo -Force
   Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
   ```

   - If you're prompted to install the **NuGet** package, choose **Yes**.
   - If after installing the script you get an error that `Get-WindowsAutopilotInfo.ps1` isn't found, verify that `C:\Program Files\WindowsPowerShell\Scripts` is present in your `PATH` variable.
   - If the `Install-Script` cmdlet fails, verify that you have the default PowerShell repository registered (**Get-PSRepository**) or register the default repository with the following command:

    ```powershell
    Register-PSRepository -Default -Verbose
    ```

The script creates a `.csv` file that contains the device information, including the complete 4K HH. Save this file so that you can access it later. The service facility uses this 4K HH to reregister device as described in the following sections. Be sure to use the `-OutputFile` parameter when saving the file, which ensures that file formatting is correct. Don't attempt to pipe the command output to a file manually.

> [!NOTE]
>
> If the repair facility can't run the OA3 tool or PowerShell script to capture the new 4K HH, then the OEM or CSP partners must do it for them. Without some entity capturing the new 4K HH, there's no way to reregister this device as an Autopilot device.

## Reregister the repaired device using the new device ID

If an OEM can't reregister the device, there are two options:

- The repair facility or CSP can reregister the device using MPC.
- The customer IT Admin should reregister the device via Intune (or MSfB).

Both ways of reregistering a device are shown in the following sections.

### Reregister from Intune

To reregister an Autopilot device from Intune, an IT Admin would:

1. Sign in to Intune.
2. Navigate to **Device enrollment** > **Windows enrollment** > **Devices** > **Import**.
3. Select the **Import** button to upload a csv file containing the device ID of the device to be reregistered. The device ID was the 4K HH captured by the PowerShell script or OA3 tool described in the section [Capture a new Autopilot device ID (4K HH) from the device](#capture-a-new-autopilot-device-id-4k-hh-from-the-device).

### Reregister from the Microsoft Partner Center (MPC)

To reregister an Autopilot device from the Microsoft Partner Center MPC, an OEM or CSP would:

1. Sign in to the Microsoft Partner Center (MPC).
2. Navigate to the **Customer** > **Devices** page.
3. Select **Add devices** to upload the csv file.

![Screenshot of Add devices button](images/device2.png)<br>
![Screenshot of Add devices page](images/device3.png)

When a repaired device is reregistering through MPC, the uploaded csv file must contain the 4K HH for the device, and not just the PKID or Tuple (SerialNumber + OEMName + ModelName). If only the PKID or Tuple was used, the Autopilot service would be unable to find a match in the Autopilot database. No match would be found because no 4K HH info was previously submitted for this essentially "new" device and the upload fails, likely returning a **ZtdDeviceNotFound** error. For this reason, only upload the 4K HH, not the Tuple or PKID.

When including the 4K HH in the csv file, you don't also need to include the PKID or Tuple. Those columns may be left blank, as shown in the following example:

![hash](images/hh.png)

## Reset the device

The repair facility must reset the image back to a pre-OOBE state before returning it to the customer. This reset is needed because the device was required to be in Full OS or Audit Mode to capture the 4K HH. One way to reset the image is by using the built-in reset feature in Windows, as follows:

On the device:

1. Go to **Settings** > **Update & Security** > **Recovery**.
2. Select **Get started**.
3. Under **Reset this PC**, select **Remove everything and Just remove my files.
4. Select **Reset**.

![Screenshot of rest this PC](images/reset.png)

However, it's likely the repair facility doesn't have access to Windows because they lack the user credentials to sign in. In this case they need to use other means to reimage the device, such as the [Deployment Image Servicing and Management tool](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#use-a-deployment-script-to-apply-your-image).

## Return the repaired device to the customer

The repaired device can now be returned to the customer. The device will be auto-enrolled into the Autopilot program on first boot-up during OOBE.

> [!IMPORTANT]
>
> If the repair facility did NOT reimage the device, they could be sending it back in a potentially broken state. For example, there's no way to log into the device because it's been dissociated from the only known user account. So, they should tell the organization that they need to fix the registration and OS themselves.
> A device can be "registered" for Autopilot before being powered-on. But the device isn't actually "deployed" to Autopilot until it goes through OOBE. Therefore, resetting the device back to a pre-OOBE state is a required step.

## Specific repair scenarios

This section covers the most common repair scenarios, and their impact on Autopilot enablement.

> [!NOTE]
>
> - The scenarios were tested using Intune only. No other MDMs were tested.
> - In most test scenarios, the repaired and reregistered device needed to go through OOBE again for Autopilot to be enabled.
> - Motherboard replacement scenarios often result in lost data. Repair centers or customers should be reminded to back up data before repair.
> - When a repair facility can't write device info into the BIOS of the repaired device, new processes need to be created to successfully enable Autopilot.
> - Repaired device should have the Product Key (DPK) preinjected in the BIOS before capturing the new 4K HH (device ID)

In the following table:

- Supported = **Yes**: the device can be reenabled for Autopilot
- Supported = **No**: the device can't be reenabled for Autopilot

<table>
<th>Scenario<th>Supported<th>Microsoft Recommendation
<tr><td>Motherboard Replacement (MBR) in general<td>Yes<td>The recommended course of action for MBR scenarios is:

1. Autopilot device is deregistered from the Autopilot program
2. The motherboard is replaced
3. The device is reimaged (with BIOS info and DPK reinjected)
4. A new Autopilot device ID (4K HH) is captured off the device
5. The repaired device is reregistered for the Autopilot program using the new device ID
6. The repaired device is reset to boot to OOBE
7. The repaired device is shipped back to the customer

> [!NOTE]
>
> For item 3, it's not necessary to reimage the device if the repair technician has access to the customer's sign-in credentials. It's technically possible to successfully re-enable MBR and Autopilot without keys or certain BIOS info (like serial #, model name, and so on). But doing so is only recommended for testing/educational purposes.

<tr><td>MBR when motherboard has a TPM chip (enabled) and only one onboard network card (that also gets replaced)<td>Yes<td>

1. Deregister damaged device
2. Replace motherboard
3. Reimage device (to gain access), unless you have access to customers' sign-in credentials
4. Write device info into BIOS
5. Capture new 4K HH
6. Reregister repaired device
7. Reset device back to OOBE
8. Go through Autopilot OOBE (customer)
9. Autopilot successfully enabled

<tr><td>MBR when motherboard has a TPM chip (enabled) and a second network card (or network interface) that isn't replaced along with the motherboard<td>No<td>This scenario breaks the Autopilot experience. The resulting Device ID won't be stable until after TPM attestation has completed. Even then registration may give incorrect results because of ambiguity with MAC Address resolution. Therefore, we don't recommend this scenario.


<tr><td>MBR where the NIC card, HDD, and WLAN all remain the same after the repair<td>Yes<td>

1. Deregister damaged device
2. Replace motherboard with a new Replacement Digital Product Key (RDPK) preinjected in BIOS
3. Reimage device (to gain access), unless you have access to customers' sign-in credentials
4. Write old device info into BIOS (same s/n, model, and so on)*
5. Capture new 4K HH
6. Reregister repaired device
7. Reset device back to OOBE
8. Go through Autopilot OOBE (customer)
9. Autopilot successfully enabled

*For this and later scenarios, rewriting old device info wouldn't include the TPM 2.0 endorsement key, as the associated private key is locked to the TPM device

<tr><td>MBR where the NIC card remains the same, but the HDD and WLAN are replaced<td>Yes<td>

1. Deregister damaged device
2. Replace motherboard (with new RDPK preinjected in BIOS)
3. Insert new HDD and WLAN
4. Write old device info into BIOS (same s/n, model, and so on)
5. Capture new 4K HH
6. Reregister repaired device
7. Reset device back to OOBE
8. Go through Autopilot OOBE (customer)
9. Autopilot successfully enabled

<tr><td>MBR where the NIC card and WLAN remains the same, but the HDD is replaced<td>Yes<td>

1. Deregister damaged device
2. Replace motherboard (with new RDPK preinjected in BIOS)
3. Insert new HDD
4. Write old device info into BIOS (same s/n, model, and so on)
5. Capture new 4K HH
6. Reregister repaired device
7. Reset device back to OOBE
8. Go through Autopilot OOBE (customer)
9. Autopilot successfully enabled

<tr><td>MBR where only the MB is replaced (all other parts remain same). The new MB was taken from a previously used device that has never been enabled for Autopilot.<td>Yes<td>

1. Deregister damaged device
2. Replace motherboard (with new RDPK preinjected in BIOS)
3. Reimage device (to gain access), unless you have access to customers' sign-in credentials
4. Write old device info into BIOS (same s/n, model, and so on)
5. Capture new 4K HH
6. Reregister repaired device
7. Reset device back to OOBE
8. Go through Autopilot OOBE (customer)
9. Autopilot successfully enabled

<tr><td>MBR where only the MB is replaced (all other parts remain same). The new MB was taken from a previously used device that **has** been Autopilot-enabled before.<td>Yes<td>

1. Deregister old device from which MB will be taken
2. Deregister damaged device (that you want to repair)
3. Replace motherboard in repair device with MB from other Autopilot device (with new RDPK preinjected in BIOS)
4. Reimage device (to gain access), unless you have access to customers' sign-in credentials
5. Write old device info into BIOS (same s/n, model, and so on)
6. Capture new 4K HH
7. Reregister repaired device
8. Reset device back to OOBE
9. Go through Autopilot OOBE (customer)
10. Autopilot successfully enabled

The repaired device can also be used successfully as a normal, non-Autopilot device.

<tr><td>BIOS info excluded from MBR device<td>No<td>Repair facility doesn't have BIOS tool to write device info into BIOS after MBR.

1. Deregister damaged device
2. Replace motherboard (BIOS does NOT contain device info)
3. Reimage and write DPK into image
4. Capture new 4K HH
5. Reregister repaired device
6. Create Autopilot profile for device
7. Go through Autopilot OOBE (customer)
8. Autopilot FAILS to recognize repaired device

<tr><td>MBR when there's no TPM chip<td>Yes<td>We don't recommend enabling Autopilot devices without a TPM chip (which is recommended for BitLocker encryption). However, it's possible to enable an Autopilot device in "standard user" mode (but NOT Self-deploying mode) that doesn't have a TPM chip. In this case, you would:

1. Deregister damaged device
2. Replace motherboard
3. Reimage device (to gain access), unless you have access to customers' sign-in credentials
4. Write old device info into BIOS (same s/n, model, and so on)
5. Capture new 4K HH
6. Reregister repaired device
7. Reset device back to OOBE
8. Go through Autopilot OOBE (customer)
9. Autopilot successfully enabled

<tr><td>New DPK written into image on repaired Autopilot device with a new MB<td>Yes<td>Repair facility replaces normal MB on damaged device. MB doesn't contain any DPK in the BIOS. Repair facility writes DPK into image after MBR. 

1. Deregister damaged device
2. Replace motherboard - BIOS does NOT contain DPK info
3. Reimage device (to gain access), unless you have access to customers' sign-in credentials
4. Write device info into BIOS (same s/n, model, and so on)
5. Capture new 4K HH
6. Reset or reimage device to pre-OOBE and write DPK into image
7. Reregister repaired device
8. Go through Autopilot OOBE
9. Autopilot successfully enabled

<tr><td>New Repair Product Key (RDPK)<td>Yes<td>Using a motherboard with a new RDPK preinjected results in a successful Autopilot refurbishment scenario. 

1. Deregister damaged device
2. Replace motherboard (with new RDPK preinjected in BIOS)
3. Reimage or rest image to pre-OOBE
4. Write device info into BIOS 
5. Capture new 4K HH
6. Reregister repaired device
7. Reimage or reset image to pre-OOBE
8. Go through Autopilot OOBE
9. Autopilot successfully enabled

<tr><td>No Repair Product Key (RDPK) injected<td>No<td>This scenario violates Microsoft policy and breaks the Windows Autopilot experience.
<tr><td>Reimage damaged Autopilot device that wasn't deregistered before repair<td>Yes, but the device is still associated with previous tenant ID, so should only be returned to same customer<td>

1. Reimage damaged device
2. Write DPK into image
3. Go through Autopilot OOBE
4. Autopilot successfully enabled (to previous tenant ID)

<tr><td>Disk replacement from a non-Autopilot device to an Autopilot device<td>Yes<td>

1. don't deregister damaged device before repair
2. Replace HDD on damaged device
3. Reimage or reset image back to OOBE
4. Go through Autopilot OOBE (customer)
5. Autopilot successfully enabled (repaired device recognized as its previous self)

<tr><td>Disk replacement from one Autopilot device to another Autopilot device<td>Maybe<td>If the device from which the HDD is taken was itself previously deregistered from Autopilot, then that HDD can be used in a repair device. The newly repaired device won't have the proper Autopilot experience if the HDD wasn't previously deregistered from Autopilot before being used in the repaired device.

Assuming the used HDD was previously deregistered (before being used in this repair):

1. Deregister damaged device
2. Replace HDD on damaged device using an HDD from another deregistered Autopilot device
3. Reimage or rest the repaired device back to a pre-OOBE state
4. Go through Autopilot OOBE (customer)
5. Autopilot successfully enabled

<tr><td>Non-Microsoft network card replacement <td>No<td>Any scenario where a third party non-onboard network card is replaced breaks the Autopilot experience. These scenarios include the following scenarios:

- From a non-Autopilot device to an Autopilot device.
- From one Autopilot device to another Autopilot device.
- From an Autopilot device to a non-Autopilot device.

We don't recommend any of these scenarios.

<tr><td>Memory replacement<td>Yes<td>Replacing the memory on a damaged device doesn't negatively affect the Autopilot experience on that device. No de/reregistration is needed. The repair technician simply needs to replace the memory.
<tr><td>GPU replacement<td>Yes<td>Replacing the GPU(s) on a damaged device doesn't negatively affect the Autopilot experience on that device. No de/reregistration is needed. The repair technician simply needs to replace the GPU.
</table>

>When scavenging parts from another Autopilot device, we recommend unregistering the scavenged device from Autopilot, scavenging it, and then NEVER REGISTERING THE SCAVENGED DEVICE (AGAIN) FOR AUTOPILOT, because reusing parts this way may cause two active devices to end up with the same ID, with no possibility of distinguishing between the two.

The following parts may be replaced without compromising Autopilot enablement or requiring special additional repair steps:

- Memory (RAM or ROM)
- Power Supply
- Video Card
- Card Reader
- Sound card
- Expansion card
- Microphone
- Webcam
- Fan
- Heat sink
- CMOS battery

Other repair scenarios not yet tested and verified include:

- Daughterboard replacement
- CPU replacement
- Wifi replacement
- Ethernet replacement

## FAQ

| Question | Answer |
| --- | --- |
| What to do if you see another customer's welcome page? | If you continue seeing another customer's welcome page on a replacement device or refurbished motherboard, a ticket needs to be raised to Microsoft to fix the device ownership. You can open a ticket through the Microsoft Intune admin center by selecting the Help and Support option outlined [here](../get-support.md). If you don't have access to Microsoft Endpoint Manager, you can submit a ticket through Microsoft Store for Business by selecting Manage > Support and selecting Technical Support. You can also submit a ticket through your Microsoft Volume Licensing Center agreement, instructions outlined [here](https://support.microsoft.com/topic/microsoft-software-assurance-support-incident-submission-74a9a148-9a75-ecc8-4420-14191e634d65). Title all tickets **Autopilot Deregistration Request** to streamline requests. |
| We have a tool that programs product information into the BIOS after the MBR. Do we still need to submit a CBR report for the device to be Autopilot-capable? | No. Not if the in-house tool writes the minimum necessary information into the BIOS that the Autopilot program looks for to identify the device, as described earlier in this document. |
| What if only some components are replaced rather than the full motherboard? | It's true that some limited repairs don't prevent the Autopilot algorithm from successfully matching the post-repair device with the pre-repair device. Even so, it's best to ensure 100% success by going through the MBR steps described in the previous sections even for devices that only needed limited repairs. |
| How does a repair technician gain access to a broken device if they don't have the customer's sign-in credentials? | The technician has to reimage the device and use their own credentials during the repair process. |

## Related articles

[Device guidelines](autopilot-device-guidelines.md)<br>
