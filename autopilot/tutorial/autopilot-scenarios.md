---
title: Windows Autopilot scenarios
description: Describes the different Autopilot scenarios.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/19/2024
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
  - essentials-get-started
ms.subservice: itpro-autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot scenarios

Due to different environments, different configurations, and different needs, Windows Autopilot offers several different scenarios. The following table summarizes the scenarios that are available in Windows Autopilot:

| **Scenario** | **Purpose** | **Description** |
| --- | --- | --- |
| **Windows Autopilot user-driven mode** | Device for a single user | User runs deployment |
| **Windows Autopilot for pre-provisioned** | Device for a single user | Deployment is split between IT admin/OEM/reseller and user |
| **Windows Autopilot self-deploying mode** | Kiosk device or device for multiple users | Deployment is completely automated |
| **Windows Autopilot for existing devices** | Prepare device where Windows OS needs to be reinstalled for a Windows Autopilot deployment | Utilizes Microsoft Configuration Manager to install a fresh Windows OS on an existing device before running a Windows Autopilot deployment |
| **Windows Autopilot Reset** | Resets an existing device back to the factory default installation of Windows | Utilizes the existing installation of Windows on a device to rebuild Windows and restore it back to the factory installation of Windows |

> [!NOTE]
>
> This tutorial is for **Windows Autopilot**. For the **Windows Autopilot device preparation** tutorial, see [Windows Autopilot device preparation scenarios](../device-preparation/tutorial/scenarios.md).

## Scenario capabilities

The following table compares the different capabilities for each Autopilot scenario:

| Scenario | **User-driven** | **Pre-provisioned** | **Self-deploying** | **Existing devices** | **Reset** |
| --- | --- | --- | --- | --- | --- |
| **Supports Microsoft Entra join** | Yes | Yes | Yes | Yes | Yes |
| **Supports Microsoft Entra hybrid join** | Yes | Yes | No | Yes | No |
| **Deployment requires interaction by user** | Yes | Yes | No | NA | Local reset |
| **Deployment requires interaction by IT admin/OEM/reseller** | No | Yes | No | Yes | Remote reset |
| **Supports assigning user to device** | Yes | Yes | No | NA | NA |
| **Minimizes time user interacts with deployment** | No | Yes | Yes | NA | NA |
| **User authenticates** | Yes | User flow | No | NA | Local reset |
| **TPM authenticates** | No | Technician flow | Yes | NA | NA |
| **Needs to be registered as Autopilot device before deployment** | Yes | Yes | Yes | No | Yes |

> [!NOTE]
>
> The **Windows Autopilot for existing devices** scenario is a method to completely reinstall Windows on a device in preparation to run a Windows Autopilot deployment. However the Windows Autopilot for existing devices scenario itself isn't technically an Autopilot deployment. After the Windows Autopilot for existing devices process completes, it automatically runs an Autopilot scenario.
>
> The above table lists what the Windows Autopilot for existing devices scenario can potentially support. However, a given Windows Autopilot scenario might not always be supported once the **Windows Autopilot for existing devices** scenario completes.

## Scenario pros and cons

The following table describes the pros and cons of each Windows Autopilot scenario during the deployment process.

| **Scenario** | **Pros** | **Cons** |
| --- | --- | --- |
| **User-driven** | • Requires no interaction from admin/OEM/reseller. <br> • Doesn't require [TPM attestation](/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation) so works on physical devices and VMs. | • Takes longer for user than the pre-provisioned scenario since user has to go through both device ESP and user ESP. |
| **Pre-provisioned** | • Faster for user since IT admin/OEM/reseller handles bulk of device ESP during the technician flow.  | • Requires interaction by IT admin/OEM/reseller. <br> • Requires [TPM attestation](/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation) during technician flow so only works on physical devices with supported TPM (doesn't work in VMs even with virtual TPM). |
| **Self-deploying** | • Requires no interaction from user or admin/OEM/reseller. | • Can't assign a user to the device. <br> • User ESP doesn't run during the Autopilot deployment since no user is assigned. <br> • Requires [TPM attestation](/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation) so only works on physical devices with supported TPM (doesn't work in VMs even with virtual TPM). <br> • Doesn't support Microsoft Entra hybrid join devices. |
| **Existing devices** | • Can use custom images. <br> • Can use ConfigMgr task sequences. <br> • Can reinstall a fresh copy of Windows in cases of severe corruption in Windows installation. <br> • Good scenario to upgrade a device from domain joined or Microsoft Entra hybrid join to Microsoft Entra join. | • Requires Microsoft Configuration Manager. <br> • Not an actual Autopilot deployment so doesn't work on its own - only works alongside one a supported Autopilot scenario. <br> •  Takes longer since device has to undergo both task sequence and Autopilot deployment. <br> • JSON file only supports user-driven Autopilot scenarios. <br> • Pre-provisioning and self-deploying Autopilot scenarios are only supported when the device is already an Autopilot device and there's an Autopilot profile assigned to the device. |
| **Reset** | • Easily allows resetting an existing broken or repurposed device to a business ready state. | • Doesn't work if there's severe corruption in Windows installation. <br> • Doesn't support Microsoft Entra hybrid join devices. |

## Microsoft Entra join and Microsoft Entra hybrid join vs. Autopilot scenarios

Microsoft Entra join and Microsoft Entra hybrid join aren't Autopilot scenarios, but instead [device identity](/azure/active-directory/devices/overview) options. All Autopilot scenarios support Microsoft Entra join, while only the **User-driven**, **Pre-provisioned**, and **Existing devices** scenarios support Microsoft Entra hybrid join. When deciding which Autopilot scenario to use, keep in mind the following factors:

- Device identities currently being used in the environment.
- Device identities being used going forward.
- Possible device identities being used in the future.

Microsoft recommends deploying new devices as cloud-native using Microsoft Entra join. Deploying new devices as Microsoft Entra hybrid join devices isn't recommended, including through Autopilot. Microsoft Entra join provides the best user experience. However, current environment configurations and restrictions might require the continued use of on-premises Active Directory. In scenarios where on-premises Active Directory is still needed, Microsoft Entra hybrid join can be used. However, consider moving new devices to Microsoft Entra join while keeping existing devices on Microsoft Entra hybrid join. Microsoft Entra hybrid join can also be seen as a way to transition from on-premises Active Directory to purely Microsoft Entra ID.

Also keep in mind that for the Autopilot deployments that support Microsoft Entra hybrid join, Microsoft Entra hybrid join requires connectivity to a domain controller. If the device undergoing an Autopilot deployment is a remote device and isn't able to connect to a domain controller either on-premises or via a VPN connection, then only Microsoft Entra join is an option.

<!-- Intune 12378279 -->

For more information on Microsoft Entra join versus Microsoft Entra hybrid join, see the following articles:

- [Microsoft Entra joined vs. Microsoft Entry hybrid joined in cloud-native endpoints](/mem/solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined).
- [What is a device identity?](/azure/active-directory/devices/overview).
- [Learn more about cloud-native endpoints](/mem/solutions/cloud-native-endpoints/cloud-native-endpoints-overview).
- [Tutorial: Set up and configure a cloud-native Windows endpoint with Microsoft Intune](/mem/solutions/cloud-native-endpoints/cloud-native-windows-endpoints).
- [How to: Plan your Microsoft Entra join implementation](/azure/active-directory/devices/device-join-plan).
- [A framework for Windows endpoint management transformation](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/a-framework-for-windows-endpoint-management-transformation/ba-p/2460684).
- [Understanding hybrid Azure AD and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201).
- [Success with remote Windows Autopilot and hybrid Azure Active Directory join](https://techcommunity.microsoft.com/t5/intune-customer-success/success-with-remote-windows-autopilot-and-hybrid-azure-active/ba-p/2749353).

## Which Autopilot scenario to use

Which Autopilot scenario should be used depends on various factors including the environment and the needs of the organization. The first thing to account for is which type of device identity (Microsoft Entra ID or hybrid Microsoft Entra ID) is currently being used in the environment. Which device identity is being used may restrict which Autopilot scenarios can be used in the environment.

The following guide makes general suggestions on which Autopilot scenario to use:

### User-driven

- Windows Autopilot user-driven supports both Microsoft Entra join and Microsoft Entra hybrid join.
- The device is intended to be used primarily by a single user.
- If the device needs to be shipped and delivered directly to the end-user without IT admin intervention.
- If the OEM or reseller is unable to perform the technician flow of the Windows Autopilot pre-provision scenario.
- If virtual machines (VMs) need to undergo the Windows Autopilot deployment process.

### Pre-provisioned

- Windows Autopilot for pre-provisioned supports both Microsoft Entra join and Microsoft Entra hybrid join.
- The device is intended to be used primarily by a single user.
- The deployment time that the end-user experiences needs to be minimized.
- Is an IT admin, an OEM, or a reseller able to handle the technician flow and the first half of the deployment. If an IT admin handles the technician flow, then the device may need to be first shipped to the IT admin to perform the technician flow, followed by the device shipped or delivered to the end-user.
- In Microsoft Entra hybrid join scenarios, if the OEM or reseller is performing the technician flow, their environment must have connectivity to a domain controller for the organization.
- Windows Autopilot for pre-provisioned uses [TPM attestation](/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation) for authentication during the technician flow so only devices that have a supported TPM are supported. For this reason, virtual machines (VMs) aren't supported even when the VM has a virtual TPM.

### Self-deploying mode

- Windows Autopilot self-deploying mode only supports Microsoft Entra join. It doesn't support Microsoft Entra hybrid join.
- The device is intended to be used as a kiosk device or by multiple users.
- If the device isn't going to be assigned to a user.
- The deployment needs to be automated as much as follow with no user interaction during the deployment process. For example, the end-user having to sign into Microsoft Entra ID during the deployment process.
- Windows Autopilot self-deploying mode uses [TPM attestation](/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation) for authentication during the technician flow so only devices that have a supported TPM are supported. For this reason, virtual machines (VMs) aren't supported even when the VM has a virtual TPM.

### Existing devices

- Windows Autopilot for existing devices isn't a Windows Autopilot deployment itself, but a method to prepare an existing device for an Autopilot deployment. As part of the Windows Autopilot for existing devices deployment, a JSON file is added to the device. The JSON file defines which Autopilot deployment to run once the Windows Autopilot for existing devices deployment completes.
- The device doesn't need to be a current Autopilot device.
- On existing devices that are already part of the environment. For example, when repurposing a device and the Windows OS need to be reinstalled.
- On existing devices where the Windows OS needs to be reinstalled. For example, the previous Windows OS installation is corrupted and needs to be reinstalled, or if the hard drive of the device is replaced.
- For converting devices from Microsoft Entra hybrid join to Microsoft Entra join.
- When custom images of Windows installations are desired.
- When task sequences are desired to run complex application deployments.

### Reset

- Windows Autopilot Reset isn't a Windows Autopilot deployment itself, but a method to reset an existing Autopilot device to a business ready state.
- The device needs to be registered as an Autopilot device.
- Windows Autopilot Reset only supports existing Microsoft Entra join devices. It doesn't support existing Microsoft Entra hybrid join devices.
- When the current Windows installation is in a stable non-corrupted state. If the Windows installation is in a corrupted state, use Windows Autopilot for existing devices instead.
- When the device needs to repurposed, for example to a new user.
- When the device needs to be reset to resolve ongoing problems on the device. Sometimes it's better and quicker to reset a device than to troubleshoot and fix on going problems on the device.

## Next steps: Scenario walkthroughs

The following list contains links to Autopilot scenario walkthroughs. The walkthroughs contain step by step instructions on how to configure each of the Autopilot scenarios:

1. Windows Autopilot user-driven mode:
   1. [Microsoft Entra join](user-driven/azure-ad-join-workflow.md).
   1. [Microsoft Entra hybrid join](user-driven/hybrid-azure-ad-join-workflow.md).
1. Windows Autopilot for pre-provisioned deployment:
   1. [Microsoft Entra join](pre-provisioning/azure-ad-join-workflow.md).
   1. [Microsoft Entra hybrid join](pre-provisioning/hybrid-azure-ad-join-workflow.md).
1. [Windows Autopilot self-deploying mode](self-deploying/self-deploying-workflow.md).
1. [Windows Autopilot for existing devices](existing-devices/existing-devices-workflow.md).
1. [Windows Autopilot Reset](reset/autopilot-reset-overview.md).

## Related content

For more information on Autopilot scenarios, see the following articles:

- [Windows Autopilot scenarios and capabilities](../windows-autopilot-scenarios.md).
- [Windows Autopilot deployment process](../deployment-process.md).

