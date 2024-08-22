---
title: Windows Autopilot motherboard replacement
description: Understand how Windows Autopilot deployments function when the motherboard is replaced on a device.
ms.service: windows-client
ms.subservice: itpro-autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: how-to
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot motherboard replacement scenario guidance

This document offers guidance for Windows Autopilot device repair scenarios that Microsoft partners can use in motherboard replacement situations, and other servicing scenarios.

Repairing Autopilot enrolled devices is complex, as it tries to balance OEM requirements with Windows Autopilot requirements. Specifically, OEM requirements include strict uniqueness across motherboards, MAC addresses, etc. Windows Autopilot requires strict uniqueness at the hardware hash level for each device to enable successful registration. The hardware hash doesn't always accommodate all the OEM hardware component requirements. These requirements are sometimes at odds, which can cause issues with some repair scenarios. The hardware hash is also known as the hardware ID.

If a motherboard is replaced on an Autopilot registered device, then the following process is recommended:

1. [Deregister the device from Windows Autopilot](#deregister-the-autopilot-device-from-the-autopilot-program).

1. [Replace the motherboard](#replace-the-motherboard).

1. [Capture the new device ID (4K HH)](#capture-a-new-autopilot-device-id-4k-hh-from-the-device).

1. [Reregister the device](#reregister-the-repaired-device-using-the-new-device-id) with Windows Autopilot.

1. [Reset the device](#reset-the-device).

1. [Return the device](#return-the-repaired-device-to-the-customer).

Each of these steps is described in the following sections.

## Deregister the Autopilot device from the Autopilot program

Before the device arrives at the repair facility, the entity that registered the device must deregister it.

- If the **IT Admin** registered the device, they likely did so via Intune, [Microsoft 365 admin center](https://admin.microsoft.com/), or a legacy portal such as Microsoft Store for Business (MSfB). If so, they should deregister the device from Intune or the [Microsoft 365 admin center](https://admin.microsoft.com/) because devices registered in Intune don't show up in Microsoft Partner Center (MPC).

- If the **OEM or CSP partner** registered the device, they likely did so via the Microsoft Partner Center (MPC). In that case, they should deregister the device from MPC, which also removes it from the customer IT Admin's Intune account.

The below steps describe what an IT Admin would go through to deregister a device from Intune and the steps an OEM or CSP would go through to deregister a device from MPC.

To avoid problems, an OEM or CSP should register Autopilot devices whenever possible. If the customer registers the devices, OEMs or CSPs can't deregister them if, for example, a customer leasing a device goes out of business before deregistering it themselves.

If a customer grants an OEM permission to register devices on their behalf using the automated consent process, an OEM can use the API to deregister devices they didn't register themselves. This deregistration only removes those devices from the Autopilot program. It doesn't unenroll them from Intune or disjoin them from Microsoft Entra ID. Only the customer can unenroll the device from Intune or disjoin the device from Microsoft Entra ID.

## Deregister a device

[!INCLUDE [Deregister an Autopilot device](includes/deregister-autopilot-device.md)]

Because the repair facility doesn't have the user's sign-in credentials, they have to reimage the device as part of the repair process. The customer should do three things before sending the device to the facility:

1. Copy all important data off the device.
1. Let the repair facility know which version of Windows they should reinstall after the repair.
1. If applicable, let the repair facility know which version of Office they should reinstall after the repair.

## Replace the motherboard

Technicians replace the motherboard or other hardware on the broken device. A replacement Digital Product Key (DPK) is injected.

Repair and key replacement processes vary between facilities. Sometimes repair facilities receive motherboard spare parts from OEMs that have replacement DPKs already injected, but sometimes not. Sometimes repair facilities receive fully functional BIOS tools from OEMs, but sometimes not. The quality of the data in the BIOS after a motherboard replacement varies. To ensure the repaired device are still Autopilot capable following its repair, check to make sure the new post-repair BIOS can successfully gather and populate the following information at a minimum:

- DiskSerialNumber.
- SmbiosSystemSerialNumber.
- SmbiosSystemManufacturer.
- SmbiosSystemProductName.
- SmbiosUuid.
- TPM EKPub.
- MacAddress.
- ProductKeyID.
- OSType.

For simplicity, and because processes vary between repair facilities, additional steps often used in a motherboard replacement are excluded, such as:

- Verify that the device is still functional.
- Disable or suspend BitLocker.
- Repair the Boot Configuration Data (BCD).
- Repair and verify the network driver operation.

## Capture a new Autopilot device ID (4K HH) from the device

Repair technicians must sign in to the repaired device to capture the new device ID. If the repair technician doesn't have access to the customer's sign-in credentials, they have to reimage the device to gain access:

1. The repair technician creates a [WinPE bootable USB drive](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#create-a-bootable-windows-pe-winpe-partition).

1. The repair technician boots the device to WinPE.

1. The repair technician [applies a new Windows image to the device](/windows-hardware/manufacture/desktop/work-with-windows-images).

    Ideally, the same Windows version that was originally on the device should be reimaged onto the device. Some coordination is required between the repair facility and customer to capture this information at the time the device arrives for repair. Such coordination might include the customer sending the repair facility a customized image (.ppk file) via a USB stick, for example.

1. The repair technician boots the device into the new Windows image.

1. Once on the desktop, the repair technician captures the new device ID (4K HH) off the device using either the OA3 Tool or the PowerShell script.

Those repair facilities with access to the OA3 Tool (which is part of the ADK) can use the tool to capture the 4K Hardware Hash (4K HH).

Instead, the [WindowsAutopilotInfo PowerShell script](https://www.powershellgallery.com/packages/Get-WindowsAutopilotInfo) can be used to capture the 4K HH.

> [!NOTE]
>
> Other methods in addition to Windows PowerShell are also available to capture the hardware hash. For more information, see [Collect the hardware hash](add-devices.md#collect-the-hardware-hash).

To use the **WindowsAutopilotInfo** PowerShell script, follow these steps:

1. Install the script from the [PowerShell Gallery](https://www.powershellgallery.com/packages/Get-WindowsAutopilotInfo) or from the command line.

1. Navigate to the script directory and run it on the device when the device is either in Full OS or Audit Mode. See the following example.

   ```powershell
   md c:\HWID
   Set-Location c:\HWID
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
   Install-Script -Name Get-WindowsAutopilotInfo -Force
   Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
   ```

   - If prompted to install the **NuGet** package, select **Yes**.
   - If after installing the script an error occurs reporting that `Get-WindowsAutopilotInfo.ps1` isn't found, verify that `C:\Program Files\WindowsPowerShell\Scripts` is present in the `PATH` variable.
   - If the `Install-Script` cmdlet fails, verify that the default PowerShell repository is registered with the following command:

    ```powershell
    Get-PSRepository
    ```

    If the default PowerShell repository isn't registered, register it with the following command:

    ```powershell
    Register-PSRepository -Default -Verbose
    ```

   > [!NOTE]
   >
   > The `Get-WindowsAutopilotInfo` script was updated in July of 2023 to use the Microsoft Graph PowerShell modules instead of the deprecated AzureAD Graph PowerShell modules. Make sure to use the latest version of the script. The Microsoft Graph PowerShell modules might require approval of additional permissions in Microsoft Entra ID when they're first used. For more information, see [AzureAD](/powershell/module/azuread/) and [Important: Azure AD Graph Retirement and PowerShell Module Deprecation](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270).

The script creates a `.csv` file that contains the device information, including the complete 4K HH. Save this file so that it can be accessed later. The service facility uses this 4K HH to reregister device as described in the following sections. Be sure to use the `-OutputFile` parameter when saving the file, which ensures that file formatting is correct. Don't attempt to pipe the command output to a file manually.

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

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Navigate to **Devices** > **Device onboarding** | **Enrollment** > **Windows Autopilot** | **Devices**.

1. Select the **Import** option in the toolbar at the top to upload a CSV file containing the device ID of the device to be reregistered. The device ID was the 4K HH captured by the PowerShell script or OA3 tool described in the section [Capture a new Autopilot device ID (4K HH) from the device](#capture-a-new-autopilot-device-id-4k-hh-from-the-device).

### Reregister from the Microsoft Partner Center (MPC)

To reregister an Autopilot device from the Microsoft Partner Center MPC, an OEM or CSP would:

1. Sign in to the Microsoft Partner Center (MPC).

1. Navigate to the **Customer** > **Devices** page.

1. Select **Add devices** to upload the CSV file.

When a repaired device is reregistering through MPC, the uploaded CSV file must contain the 4K HH for the device, and not just the PKID or Tuple (SerialNumber + OEMName + ModelName). If only the PKID or Tuple was used, the Autopilot service would be unable to find a match in the Autopilot database. No match would be found because no 4K HH info was previously submitted for this essentially "new" device and the upload fails, likely returning a **ZtdDeviceNotFound** error. For this reason, only upload the 4K HH. Don't upload the Tuple or PKID.

When including the 4K HH in the CSV file, the PKID or Tuple don't also need to be included. Those columns might be left blank, as shown in the following example:

:::image type="content" source="images/hh.png" alt-text="Screenshot of a CSV file in Excel with a hash value in the Hardware Hash column.":::

## Reset the device

The repair facility must reset the image back to a pre-OOBE state before returning it to the customer. This reset is needed because the device was required to be in Full OS or Audit Mode to capture the 4K HH. One way to reset the image is by using the built-in reset feature in Windows.

To use the reset feature in Windows on a device:

**Windows 10**:

1. Go to **Settings** > **Update & Security** > **Recovery**.

1. Select **Get started**.

1. In the **Reset this PC** window:

   1. Under **Choose an option**, select **Remove everything**.

   1. Under **How would you like to reinstall Windows?**, select either option.

   1. Under **Additional settings**, select **Next**.

   1. Under **Ready to reset this PC**, select the **Reset** button.

**Windows 11**:

1. Go to **Settings** > **System** > **Recovery**.

1. Under **Recovery options**, select the **Reset PC** button next to **Reset this PC**.

1. In the **Reset this PC** window:

   1. Under **Choose an option**, select **Remove everything**.

   1. Under **How would you like to reinstall Windows?**, select either option.

   1. Under **Additional settings**, select **Next**.

   1. Under **Ready to reset this PC**, select the **Reset** button.

However, the repair facility most likely doesn't have access to Windows because they lack the user credentials to sign in. In this case, they need to use other means to reimage the device, such as the Deployment Image Servicing and Management (DISM) tool:

- [OEM Deployment of Windows 11 desktop editions](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-desktop-editions).
- [OEM Deployment of Windows 10 for desktop editions](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-desktop-editions?view=windows-10&preserve-view=true).

## Return the repaired device to the customer

The repaired device can now be returned to the customer. The device is auto-enrolled into the Autopilot program on first boot-up during OOBE.

> [!IMPORTANT]
>
> If the repair facility **didn't** reimage the device, they could be sending it back in a potentially broken state. For example, there's no way to log into the device because it's dissociated from the only known user account.

 A device can be **registered** for Autopilot before being powered-on. However, the device isn't actually **deployed** to Autopilot until it goes through OOBE. Therefore, resetting the device back to a pre-OOBE state is a required step.

## Fix pending and Attention required

If the profiles status of a device shows **Fix pending**, Autopilot is in the process of attempting to register the device. If the profile status of a device shows **Fix pending** for an extended period of time and doesn't switch to **Assigned**, or if the profile status of the device switches to **Attention required**, then:

1. Manually deregister the device using the steps in the [Deregister a device](#deregister-a-device) section.
1. Reregister the device.

For more information, see [Why is the Windows Autopilot profile not applied after a hardware change occurred on a device?](troubleshooting-faq.yml#why-is-the-windows-autopilot-profile-not-applied-after-a-hardware-change-occurred-on-a-device-).

## Specific repair scenarios

This section covers the most common repair scenarios, and their impact on Autopilot enablement.

> [!NOTE]
>
> - The scenarios were tested using Intune only. No other MDMs were tested.
> - In most test scenarios, the repaired and reregistered device needed to go through OOBE again for Autopilot to be enabled.
> - Motherboard replacement scenarios often result in lost data. Repair centers or customers should be reminded to back up data before repair.
> - When a repair facility can't write device info into the BIOS of the repaired device, new processes need to be created to successfully enable Autopilot.
> - Repaired device should have the Product Key (DPK) pre-injected in the BIOS before capturing the new 4K HH (device ID).

For the **Supported** column in the following table:

- **Yes**: the device can be reenabled for Autopilot.
- **No**: the device can't be reenabled for Autopilot.

| Scenario | Supported | Microsoft Recommendation |
| --- | --- | --- |
| **Motherboard Replacement in general** | Yes | The recommended course of action for motherboard replacement scenarios is: <br> 1. Autopilot device is deregistered from the Autopilot program. <br> 2. The motherboard is replaced. <br> 3. The device is reimaged (with BIOS info and DPK reinjected). <sup>1</sup> <br> 4. A new Autopilot device ID (4K HH) is captured off the device. <br> 5. The repaired device is reregistered for the Autopilot program using the new device ID. <br> 6. The repaired device is reset to boot to OOBE. <br> 7. The repaired device is shipped back to the customer. <br><br> <sup>1</sup> It's not necessary to reimage the device if the repair technician has access to the customer's sign-in credentials. It's technically possible to successfully re-enable motherboard replacement and Autopilot without keys or certain BIOS info (serial #, model name, etc.) However, doing so is only recommended for testing/educational purposes. |
| **Motherboard replacement when motherboard has a TPM chip enabled and only one onboard network card that also gets replaced** | Yes  | 1. Deregister damaged device. <br> 2. Replace motherboard. <br> 3. To gain access, reimage device or sign-in using customer's credentials. <br> 4. Write device info into BIOS. <br> 5. Capture new 4K HH. <br> 6. Reregister repaired device. <br> 7. Reset device back to OOBE. <br> 8. Go through Autopilot OOBE (customer). <br> 9. Autopilot successfully enabled. |
| **Motherboard replacement when motherboard has an enabled TPM chip enabled and a second network interface that isn't replaced along with the motherboard** | No | This scenario breaks the Autopilot experience. The resulting Device ID won't be stable until after TPM attestation is complete. Even then registration might give incorrect results because of ambiguity with MAC Address resolution. Therefore, this scenario isn't recommended. |
| **Motherboard replacement where the NIC card, HDD, and WLAN all remain the same after the repair** | Yes | 1. Deregister damaged device. <br> 2. Replace motherboard with a new Replacement Digital Product Key (RDPK) preinjected in BIOS. <br> 3. To gain access, reimage device or sign-in using customer's credentials. <br> 4. Write old device info into BIOS (same s/n, model, etc.) <sup>2</sup> <br> 5. Capture new 4K HH. <br> 6. Reregister repaired device. <br> 7. Reset device back to OOBE. <br> 8. Go through Autopilot OOBE (customer). <br> 9. Autopilot successfully enabled. <br><br> <sup>2</sup> For this and later scenarios, rewriting old device info wouldn't include the TPM 2.0 endorsement key, as the associated private key is locked to the TPM device. |
| **Motherboard replacement where the NIC card remains the same, but the HDD and WLAN are replaced** | Yes | 1. Deregister damaged device. <br> 2. Replace motherboard (with new RDPK preinjected in BIOS). <br> 3. Insert new HDD and WLAN. <br> 4. Write old device info into BIOS (same s/n, model, etc.) <br> 5. Capture new 4K HH. <br> 6. Reregister repaired device. <br> 7. Reset device back to OOBE. <br> 8. Go through Autopilot OOBE (customer). <br> 9. Autopilot successfully enabled. |
| **Motherboard replacement where the NIC card and WLAN remains the same, but the HDD is replaced** | Yes | 1. Deregister damaged device. <br> 2. Replace motherboard (with new RDPK preinjected in BIOS). <br> 3. Insert new HDD. <br> 4. Write old device info into BIOS (same s/n, model, etc.) <br> 5. Capture new 4K HH. <br> 6. Reregister repaired device. <br> 7. Reset device back to OOBE. <br> 8. Go through Autopilot OOBE (customer). <br> 9. Autopilot successfully enabled. |
| **Motherboard replacement where only the motherboard is replaced. All other parts remain same. The new motherboard was taken from a previously used device that has never been enabled for Autopilot.** | Yes | 1. Deregister damaged device. <br> 2. Replace motherboard (with new RDPK preinjected in BIOS). <br> 3. To gain access, reimage device or sign-in using customer's credentials. <br> 4. Write old device info into BIOS (same s/n, model, etc.) <br> 5. Capture new 4K HH. <br> 6. Reregister repaired device. <br> 7. Reset device back to OOBE. <br> 8. Go through Autopilot OOBE (customer). <br> 9. Autopilot successfully enabled. |
| **Motherboard replacement where only the motherboard is replaced. All other parts remain same. The new motherboard was taken from a previously used device that has been Autopilot-enabled before.** | Yes | 1. Deregister old device which motherboard is taken from. <br> 2. Deregister damaged device that needs to be repaired. <br> 3. Replace motherboard in repair device with motherboard from other Autopilot device (with new RDPK preinjected in BIOS). <br> 4. To gain access, reimage device or sign-in using customer's credentials. <br> 5. Write old device info into BIOS (same s/n, model, etc.) <br> 6. Capture new 4K HH. <br> 7. Reregister repaired device. <br> 8. Reset device back to OOBE. <br> 9. Go through Autopilot OOBE (customer). <br> 10. Autopilot successfully enabled. <br><br> The repaired device can also be used successfully as a normal, non-Autopilot device. |
| **BIOS info excluded from motherboard replacement device** | No | Repair facility doesn't have BIOS tool to write device info into BIOS after Motherboard replacement. <br><br> 1. Deregister damaged device. <br> 2. Replace motherboard (BIOS does NOT contain device info). <br> 3. Reimage and write DPK into image. <br> 4. Capture new 4K HH. <br> 5. Reregister repaired device. <br> 6. Create Autopilot profile for device. <br> 7. Go through Autopilot OOBE (customer). <br> 8. Autopilot FAILS to recognize repaired device. |
| **Motherboard replacement when there's no TPM** | Yes | Enabling Autopilot devices without a TPM isn't recommended. However, it's possible to enable an Autopilot device that doesn't have a TPM via user-driven mode. Pre-provision and self-deploying modes aren't supported without a TPM. When using user-driven mode: <br><br> 1. Deregister damaged device. <br> 2. Replace motherboard. <br> 3. To gain access, reimage device or sign-in using customer's credentials. <br> 4. Write old device info into BIOS (same s/n, model, etc.) <br> 5. Capture new 4K HH. <br> 6. Reregister repaired device. <br> 7. Reset device back to OOBE. <br> 8. Go through Autopilot OOBE (customer). <br> 9. Autopilot successfully enabled. |
| **New DPK written into image on repaired Autopilot device with a new motherboard** | Yes | Repair facility replaces normal motherboard on damaged device. motherboard doesn't contain any DPK in the BIOS. Repair facility writes DPK into image after motherboard replacement. <br><br> 1. Deregister damaged device. <br> 2. Replace motherboard - BIOS does NOT contain DPK info. <br> 3. To gain access, reimage device or sign-in using customer's credentials. <br> 4. Write device info into BIOS (same s/n, model, etc.) <br> 5. Capture new 4K HH. <br> 6. Reset or reimage device to pre-OOBE and write DPK into image. <br> 7. Reregister repaired device. <br> 8. Go through Autopilot OOBE. <br> 9. Autopilot successfully enabled. |
| **New Repair Product Key (RDPK)** | Yes | Using a motherboard with a new RDPK preinjected results in a successful Autopilot refurbishment scenario. <br><br> 1. Deregister damaged device. <br> 2. Replace motherboard (with new RDPK preinjected in BIOS). <br> 3. Reimage or rest image to pre-OOBE. <br> 4. Write device info into BIOS. <br> 5. Capture new 4K HH. <br> 6. Reregister repaired device. <br> 7. Reimage or reset image to pre-OOBE. <br> 8. Go through Autopilot OOBE. <br> 9. Autopilot successfully enabled. |
| **No Repair Product Key (RDPK) injected** | No | This scenario violates Microsoft policy and breaks the Windows Autopilot experience. |
| **Reimage damaged Autopilot device that wasn't deregistered before repair** | Yes, but the device is still associated with previous tenant ID, so should only be returned to same customer. | 1. Reimage damaged device. <br> 2. Write DPK into image. <br> 3. Go through Autopilot OOBE. <br> 4. Autopilot successfully enabled to same tenant ID as before. |
| **Disk replacement from a non-Autopilot device to an Autopilot device** | Yes | 1. Don't deregister damaged device before repair. <br> 2. Replace HDD on damaged device. <br> 3. Reimage or reset image back to OOBE. <br> 4. Go through Autopilot OOBE (customer). <br> 5. Autopilot successfully enabled (repaired device recognized as its previous self). |
| **Disk replacement from one Autopilot device to another Autopilot device** | Maybe | If the device from which the HDD is taken was itself previously deregistered from Autopilot, then that HDD can be used in a repair device. The newly repaired device won't have the proper Autopilot experience if the HDD wasn't previously deregistered from Autopilot before being used in the repaired device. <br><br> Assuming the used HDD was previously deregistered (before being used in this repair): <br> <br> 1. Deregister damaged device. <br> 2. Replace HDD on damaged device using an HDD from another deregistered Autopilot device. <br> 3. Reimage or rest the repaired device back to a pre-OOBE state. <br> 4. Go through Autopilot OOBE (customer). <br> 5. Autopilot successfully enabled. |
| **Non-OEM add-in network card replacement** | No | Any scenario where a network card is used other than the OEM on-board NIC breaks the Autopilot experience. These scenarios include the following scenarios: <br><br> • From a non-Autopilot device to an Autopilot device. <br> • From one Autopilot device to another Autopilot device. <br> • From an Autopilot device to a non-Autopilot device. <br><br> These scenarios aren't recommended. |
| **Memory replacement** | Yes | Replacing the memory on a damaged device doesn't negatively affect the Autopilot experience on the device. No deregistration/reregistration is needed. The repair technician simply needs to replace the memory. |
| **GPU replacement** | Yes | Replacing one or more GPUs on a damaged device doesn't negatively affect the Autopilot experience on that device. No deregistration/reregistration is needed. The repair technician simply needs to replace the GPU. |

> [!IMPORTANT]
>
> When parts are scavenged from another Autopilot device, Microsoft recommends to unregister the scavenged device from Autopilot, scavenge it, and then **never register the scavenged device again for Autopilot**. Reusing parts in this way might cause two active devices to end up with the same ID with no possibility of distinguishing between the two.

The following parts can be replaced without compromising Autopilot enablement or requiring special additional repair steps:

- Memory (RAM or ROM).
- Power Supply.
- Video Card.
- Card Reader.
- Sound card.
- Expansion card.
- Microphone.
- Webcam.
- Fan.
- Heat sink.
- CMOS battery.

Other repair scenarios not yet tested and verified include:

- Daughterboard replacement.
- CPU replacement.
- Wifi replacement.
- Ethernet replacement.

## FAQ

| Question | Answer |
| --- | --- |
| What to do if another customer's welcome page is displayed? | If another customer's welcome page is displayed on a replacement device or refurbished motherboard, a case needs to be raised to Microsoft to fix the device ownership. A case can be opened through the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting the Help and Support option outlined [here](/mem/get-support). If there isn't access to Microsoft Intune, a case can be submitted through Microsoft Store for Business by selecting **Manage** > **Support** and selecting **Technical Support**. A case can also be submitted through the Microsoft Volume Licensing Center agreement. Instructions on how to submit a case  are outlined at [Microsoft Software Assurance - Support Incident Submission](https://support.microsoft.com/topic/microsoft-software-assurance-support-incident-submission-74a9a148-9a75-ecc8-4420-14191e634d65). Title all cases **Autopilot Deregistration Request** to streamline requests. |
| We have a tool that programs product information into the BIOS after the motherboard replacement. Do we still need to submit a CBR report for the device to be Autopilot-capable? | No. Not if the in-house tool writes the minimum necessary information into the BIOS that the Autopilot program looks for to identify the device, as described earlier in this document. |
| What if only some components are replaced rather than the full motherboard? | It's true that some limited repairs don't prevent the Autopilot algorithm from successfully matching the post-repair device with the pre-repair device. However, Microsoft recommends to always go through the motherboard replacement steps described in the previous sections to ensure success. |
| How does a repair technician gain access to a broken device if they don't have the customer's sign-in credentials? | The technician has to reimage the device and use their own credentials during the repair process. |

## Related content

- [Device guidelines](autopilot-device-guidelines.md).
