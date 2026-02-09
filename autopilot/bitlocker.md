---
title: Setting the BitLocker encryption algorithm for Windows Autopilot devices
description: Microsoft Intune provides a comprehensive set of configuration options to manage BitLocker on Windows devices.
ms.date: 04/02/2025
ms.collection:
  - M365-modern-desktop
ms.topic: how-to
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Setting the BitLocker encryption algorithm for Windows Autopilot devices

BitLocker [automatically encrypts](/windows-hardware/design/device-experiences/oem-bitlocker#bitlocker-automatic-device-encryption) internal drives during the out-of-box experience (OOBE) for devices that support [Modern Standby](/windows-hardware/design/device-experiences/modern-standby) or meet the [Hardware Security Testability Specification (HSTI)](/windows-hardware/test/hlk/testref/hardware-security-testability-specification). By default, BitLocker uses XTS-AES 128-bit used space only for automatic encryption.

With Windows Autopilot, BitLocker encryption settings can be configured to apply before automatic encryption starts. This configuration makes sure the default encryption algorithm or type isn't applied automatically. A device that receives these settings after encrypting automatically needs to be decrypted before changing the encryption algorithm.

## Encryption algorithm

BitLocker uses the specified BitLocker encryption algorithm when BitLocker is first enabled. During Windows Autopilot, BitLocker will be enabled after the device setup portion of the [enrollment status page](enrollment-status.md). The following encryption algorithms are available:

- AES-CBC 128-bit.
- AES-CBC 256-bit.
- XTS-AES 128-bit (default).
- XTS-AES 256-bit.

For more information about the recommended encryption algorithms to use, see [BitLocker Configuration Service Provider (CSP)](/windows/client-management/mdm/bitlocker-csp).

## Full disk or used space-only encryption

There are two types of encryption, full disk or used space-only. Configuration of [silent enablement](/mem/intune-service/protect/encrypt-devices#silently-enable-bitlocker-on-devices) and hardware support for modern standby automatically determines the type of encryption used. The type of encryption used can be enforced by configuring the [SystemDrivesEncryptionType](/windows/client-management/mdm/bitlocker-csp) setting. Like the encryption algorithm, BitLocker uses the encryption type when BitLocker is first enabled. For more information on the expected encryption type behavior, see [Manage BitLocker policy](/mem/intune-service/protect/encrypt-devices#full-disk-vs-used-space-only-encryption).

## Configure a BitLocker policy for Windows Autopilot devices

To make sure both the desired BitLocker encryption algorithm and the encryption are set before automatic encryption occurs for Windows Autopilot devices, follow these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Endpoint security** in the left hand pane.

1. In the **Endpoint security | Overview** screen, expand **Manage**, and then select **Disk encryption**.

1. In the **Endpoint security | Disk encryption** screen. Select **+ Create Policy**.

1. In the **Create a profile** page that opens:

   1. Under **Platform**, select **Windows**.

   1. Under **Profile**, select **BitLocker**.

   1. Select the **Create** button.

1. In the **Basics** page of the **Create Policy** screen, enter a **Name** and optional **Description**, and then select the **Next** button.

1. In the **Configuration settings** page, configure the various BitLocker settings as desired, including the **Encryption method and cipher** and **Encryption type** settings:

   - **Encryption method and cipher**

     1. Expand the **BitLocker Drive Encryption** section.

     1. For **Choose drive encryption method and cipher strength**, select **Enabled**.

     1. For each of the drive types (Fixed data drives, Operating system drive, Removable data drives), select the desired encryption method and cipher from the drop-down menu. The default for each type is **XTS-AES 128-bit**.

   - **Encryption type**

     1. Expand the **Operating System Drives** section.

     1. For **Enforce drive encryption type on operating system drives**, select **Enabled**.

     1. For **Select the drive encryption type**, select the desired encryption type, either **Full encryption** or **Used Space Only encryption**, from the drop-down menu. The default is **Allow user to choose**.

    Once all BitLocker settings are configured as desired, select the **Next** button.

1. In the **Scope tags** page, select the **Next** button.

    > [!NOTE]
    >
    > **Scope tags** are optional. If a custom scope tag needs to be specified, do so at this page. For more information about scope tags, see [Use role-based access control and scope tags for distributed IT](/mem/intune-service/fundamentals/scope-tags).

1. In the **Assignments** page, use the **Search by group name...** search box to find and add the Windows Autopilot device group. Once the  Windows Autopilot device group is added and is listed under **Group**, make sure **Target type** is set to **Include**, and then select the **Next** button. For more information about assigning a policy, see [Assign policies in Microsoft Intune](/mem/intune-service/configuration/device-profile-assign).

    > [!IMPORTANT]
    >
    > Make sure that the Windows Autopilot device group selected in this step is a device group and not a user group.

1. In the **Review + create** page, review the settings to verify they're configured as desired, and then select the **Save** button.

1. Configure and assign an [Enrollment Status page (ESP)](enrollment-status.md) for the Windows Autopilot device. If an ESP isn't enabled, the BitLocker policy doesn't apply before encryption starts. For more information, see one of the following articles:

   - [Windows Autopilot Enrollment Status Page](enrollment-status.md).
   - [User-driven Microsoft Entra join: Configure and assign the Enrollment Status Page (ESP)](tutorial/user-driven/azure-ad-join-esp.md).
   - [User-driven Microsoft Entra hybrid join: Configure and assign the Enrollment Status Page (ESP)](tutorial/user-driven/hybrid-azure-ad-join-esp.md).
   - [Pre-provision Microsoft Entra join: Configure and assign the Enrollment Status Page (ESP)](tutorial/pre-provisioning/azure-ad-join-esp.md).
   - [Pre-provision Microsoft Entra hybrid join: Configure and assign the Enrollment Status Page (ESP)](tutorial/pre-provisioning/hybrid-azure-ad-join-esp.md).
   - [Self-deploying mode: Configure and assign the Enrollment Status Page (ESP)](tutorial/self-deploying/self-deploying-esp.md).

## Related content

- [BitLocker overview](/windows/security/information-protection/bitlocker/bitlocker-overview).
- [Manage BitLocker policy for Windows devices with Intune](/mem/intune-service/protect/encrypt-devices).
