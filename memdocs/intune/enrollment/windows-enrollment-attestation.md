---
# required metadata

title: Windows enrollment attestation | Microsoft Intune
titleSuffix:
description: Find out how the Device attestation status report can help you and learn to use the Attest device action to ensure your devices are secure and reliable.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/31/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: f94dbc2e-a855-487e-af6e-8d08fabe6c3d

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

# Windows enrollment attestation  

The goal of Windows enrollment attestation is to make devices more secure and trustworthy within the network they join. With this feature, you can check that Windows 10 and 11 devices meet strict security standards during enrollment, using Trusted Platform Module (TPM) technology to enhance their defense against threats. The Windows enrollment attestation feature also confirms and reports on the devices that enroll securely, ensuring the process is reliable.

Here’s how it benefits organizations:

**Improved security**: TPM attestation helps detect and address security weaknesses or compromised devices and lowers the chance of unauthorized access or security incidents.

**Meeting regulatory standards**: Windows attestation helps organizations prove they follow strict security measures during device enrollment, which is important for meeting industry regulations and compliance requirements.

The main goal is to establish a more secure and trusted environment for devices within the organizational infrastructure by using Windows attestation during the enrollment process.

## Requirements for Windows enrollment attestation

We recommend using the latest updates for a more successful attestation rate.

- Windows 10

  - 10.0.19045.3996+

- Windows 11

  - 10.0.22000.2713+
  - 10.0.22621.2792+
  - 10.0.22631.2792+

- Minimum TPM 2.0 on devices

- Physical devices are supported.

    > [!NOTE]
    > Virtual machines can't attest, including the following, even if they use vTPMs:
    >  - Hyper-V and Azure virtual machines  
    >  - Azure Virtual Desktop session hosts  
    >  - Windows 365 Cloud PCs  
    >  - Microsoft Dev Box  

- Attestation with TPM in this feature is during Intune device management enrollment, after the TPM attestation that occurs in Autopilot pre-provision and Shared device mode (SDM).

- List of applicable Configuration Service Providers (CSPs) for Windows attestation:

  - [Windows InitiateRecovery CSP](/windows/client-management/mdm/dmclient-csp#deviceproviderprovideridrecoveryinitiaterecovery)
  - [Windows RecoveryStatus CSP](/windows/client-management/mdm/dmclient-csp#deviceproviderprovideridrecoveryrecoverystatus)
  - [Windows MDMClientCertAttestation CSP](/windows/client-management/mdm/devicestatus-csp#certattestationmdmclientcertattestation)

## How Windows enrollment attestation works

:::image type="content" alt-text="High-level architecture diagram on how we harden the Windows device using TPM at enrollment" source="./media/windows-enroll-attestation/windows-enroll-attest.png":::

## Device attestation status report

The report shows information about the device, its TPM, and whether the device successfully attested on enrollment. If a device doesn’t attest, the report explains why in the **Status details** section. Use this report to see the full list of devices and check which ones successfully attested on enrollment.

To access this report:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Reports** > **Device attestation status (preview)** under the **Device Management** section.
3. Filter by **Attestation status** or **Ownership type** and select **Generate report**.

    :::image type="content" alt-text="Screenshot of Device attestation report" source="./media/windows-enroll-attestation/device-attest-report.png":::

After the report is generated, The top-level details that you see include:

- Device name

- Device ID

- UPN

- **Device attestation status**

- **Status detail**

- OS

- OS version

- Ownership

- Last check-in

- Enrollment date

- TPM version

- TPM manufacturer

- Model

By selecting an entry, you can find more detailed information about the device. You can also select an entry using the left-hand **Select** column and re-attest using the [Attest device action](#attest-device-action) at the top of the report.

The following table lists status details and their descriptions:

| Status detail | Description |
| --- | --- |
| Entra key can't be attested    | Entra team didn't store the ENTRA certificate's key in TPM. If device is enrolled with AP ODJ, then this Status Detail is temporary.                                                         |
| Attestation is in process       | Device is still working on attestation when Intune queries for its latest status.                                                 |
| TPM isn't trusted              | Device contains a TPM that isn't trusted and therefore can't be attested.                                                           |
| TPM isn't available            | Device doesn't have TPM 2.0 or TPM can't be attested due to firmware needing update. For more information on how to update firmware, see [Resources](#resources)                                          |
| TPM isn't ready                | TPM isn't ready to be used by this device. User needs to reset TPM ownership. For more information on how to reset TPM ownership, see [Resources](#resources)                                                    |
| Client request is rejected      | Client's attestation request didn't reach MDM server or server rejected the request.                                             |
| AIK certificate wasn't provided| AIK certificate is missing on the device. Could be due to network issue. If temporary, attestation would retry successfully once device receives AIK cert.  |
| Client didn't provide all required parameters | Both AIK certificate and AIK public key are missing.                                                                                     |
| MDM key is already in TPM       | Device indicates that the MDM key is already stored in TPM. But Intune is unable to attest it because AIK certificate or AIK public key is missing, or ENTRA key can't be attested. |
| Feature isn't supported        | This status shows for devices that aren't yet attestable. Examples include Hyper-V and Azure virtual machines, Azure Virtual Desktop session hosts, Windows 365 Cloud PCs, Microsoft Dev Box.                     |
| Entra token doesn't match device identity | ENTRA token for enrollment doesn't match the ENTRA key presented in the enrollment request. You can fix this issue by upgrading to the latest Windows build and by retrying attestation.                                          |
| Entra token is missing device identity | ENTRA token for enrollment is missing ENTRA device identity.                                                               |

> [!NOTE]
> For more information, see the [Resources](#resources) section.

## Attest device action

If you see devices in the report that have *Not started* TPM attestation, you can select a few of those devices at a time and TPM attest them using the new device action **Attest device** at the top of the report. This device action should take less than a few minutes to attest the device and is reflected in the report when you *Refresh*.  

To attest some *Not Started* devices:

1. Use the drop-down filters at top of report to filter to *Not Started* attestation status.

2. Select **Generate again**. From there, select a few devices and then select **Attest device** action at the top of the report.

3. Attestation can take up to 15 min depending on activity of device and number of devices selected. Refresh after some time to see the updated status of the selected devices.

> [!NOTE]
> You can only select up to 100 devices at a time for device action and wait at least 1 minute between triggering **Attest device** action.

If devices are failing attestation, depending on the value in the **Status detail** column, you can retry attestation using the **Attest device** action.
If any of the following **Status details** appear, we recommend re-attempting the **Attest device** action.

- AIK certificate wasn't provided by client

- Attestation is in process

- MDM key is already in TPM

- TPM isn't ready

- Authentication failed

- Client didn't provide all required parameters needed for attestation

- Entra token does not match device identity

### Permissions for device action

To use the **Attest device** device action, you require a role based permission known as Remote tasks: **Indicates mobile device management (MDM) attestation if device is capable for it**. Set the Permission to **yes** to enable the action. With the permission set to **Yes**, IT admins can initiate **Attest device** action.

## Resources

> [!IMPORTANT]
> Troubleshooting TPM usually requires a Wipe and Reset action, which can result in data loss. Ensure that you have backups in place before carrying out any TPM troubleshooting steps.

- [TPM recommendations - Windows Security | Microsoft Learn](/windows/security/hardware-security/tpm/tpm-recommendations)

- [Intune reports](../fundamentals/reports.md#device-enrollment-reports)

- [How to update Firmware](https://support.microsoft.com/windows/update-your-security-processor-tpm-firmware-94205cbc-a492-8d79-cc55-1ecd6b0a8022)

- [Troubleshoot the TPM - Windows Security | How to reset TPM ownership](/windows/security/hardware-security/tpm/initialize-and-configure-ownership-of-the-tpm)

Additional links:

- [TrustedPlatformModule](/powershell/module/trustedplatformmodule/?view=windowsserver2022-ps&viewFallbackFrom=win10-ps&preserve-view=true)

- [Enable TPM 2.0 on your PC](https://support.microsoft.com/en-gb/windows/enable-tpm-2-0-on-your-pc-1fd5a332-360d-4f46-a1e7-ae6b0c90645c)