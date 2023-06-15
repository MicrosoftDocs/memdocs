---
title: How to bulk-enroll devices
titleSuffix: Configuration Manager
description: Bulk-enroll devices in an automated way with on-premises mobile device management (MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# How to bulk-enroll devices with on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Bulk enrollment in Configuration Manager on-premises mobile device management (MDM) is an automated method to enroll devices. The other method is user enrollment, which requires users to enter their credentials to enroll the device. Bulk enrollment uses an enrollment package to authenticate the device during enrollment. The package is a .ppkg file, which can also contain certificate and Wi-Fi profiles to support enrollment.

## <a name="bkmk_createCert"></a> Create a certificate profile

Include a certificate profile to automatically install a trusted root certificate on the device. This root certificate is required for trusted communication between the devices and the site system roles needed for on-premises MDM.

When you prepare the site for on-premises MDM, you export the trusted root certificate. Use this certificate in the enrollment package's certificate profile. For more information on how to get the trusted root certificate, see [Export the trusted root certificate](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).

Use the exported certificate to create a certificate profile. For more information, see [How to create certificate profiles](../../protect/deploy-use/create-certificate-profiles.md).

## <a name="CreateWifi"></a> Create a Wi-Fi profile

Another component of the bulk enrollment package is a Wi-Fi profile. This profile can make sure that the device has the network connectivity to support enrollment.

For more information on how to create a Wi-Fi profile in Configuration Manager, see [How to create Wi-Fi profiles](../../protect/deploy-use/create-wifi-profiles.md).

### Wi-Fi profile limitations

When you create a Wi-Fi profile for on-premises MDM bulk enrollment, review the following limitations.

#### Wi-Fi security configurations for on-premises MDM

The current branch of Configuration Manager only supports the following Wi-Fi security configurations for on-premises MDM:

- Security types: **WPA2 Enterprise** or **WPA2 Personal**

- Encryption types: **AES** or **TKIP**

- EAP types: **Smart Card or other certificate** or **PEAP**

#### Proxy server

Although Configuration Manager has a setting for proxy server information in the Wi-Fi profile, it doesn't configure the proxy when the device enrolls. If you need to set up a proxy server on bulk-enrolled devices:

- Deploy the settings using configuration items once devices enroll.

- Create a second package using the Windows Image and Configuration Designer (ICD), then deploy it along with the bulk enrollment package.

## <a name="bkmk_createEnroll"></a> Create an enrollment profile

The enrollment profile allows you to specify settings required for device enrollment. These settings include a [certificate profile](#bkmk_createCert) and a [Wi-Fi profile](#CreateWifi).

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **All Corporate-owned Devices**, expand **Windows**, and select the **Enrollment Profiles** node.

1. In the ribbon, select **Create Enrollment Profile**.

1. On the **General** page of the Create Enrollment Profile wizard, specify the following information:

    - **Name**: A unique name to identify the profile

    - **Description**: An optional field to further describe the profile

    - **Management Authority**: Only select **On-Premises**

1. On the **Site assignment** page, select the **Management site code** with a device management point.

1. On the **Select Enrollment Proxy Point** page, select **Intranet Only**, and then select one or more enrollment proxy points. Device will use these servers to start the enrollment process.

1. On the **Select Trusted Root Certificate** page, select the certificate profile that contains the trusted root certificate.

1. On the **Wi-Fi profiles** page, select the Wi-Fi profile that contains the necessary network settings for devices to connect.

    > [!TIP]
    > If you aren't using a Wi-Fi profile for your enrollment package, skip this step.

1. Complete the wizard.

## <a name="bkmk_createPpkg"></a> Create an enrollment package

The enrollment package (ppkg) is the file that you use to bulk-enroll devices for on-premises MDM. Create this file with Configuration Manager. While you can create similar types of packages with Windows ICD, only packages that you create in Configuration Manager can be used to enroll devices for on-premises MDM. A package that you create with Windows ICD can only provide the user principal name (UPN) needed for enrollment, it can't start the actual enrollment process.

The process to create the enrollment package requires the Windows Assessment and Deployment Toolkit (ADK) for Windows 10. On the computer running the Configuration Manager console, install the latest version of the Windows ADK. Select the **Imaging and Configuration Designer (ICD)** feature and any dependencies. (This version doesn't need to match the version used for OS deployment by the Configuration Manager site.) For more information, see [Download the Windows ADK for Windows 10](/windows-hardware/get-started/adk-install).

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **All Corporate-owned Devices**, expand **Windows**, and select the **Enrollment Profiles** node.

1. Select an existing enrollment profile. In the ribbon, select **Export**.

1. In the Export Enrollment Package window, specify the following information:

    - **Validity Period (days)**: By default, Configuration Manager sets the enrollment package to expire in two weeks (14 days). You can't use the package for device enrollment after the validity period expires. Enter an integer between 1 and 30.

    - **Package File**: Specify a local or network file path and name for the .ppkg file.

    - **Encrypt Package**: Enable this option to password-protect the package. After you export the package, Configuration Manager displays the generated password. Copy and save the password in a secure location. You can't use the exported enrollment package without the password.

        > [!IMPORTANT]
        > Configuration Manager doesn't save the password, and you can't customize or change it. Once you close the window that displays the password, there's no way to retrieve the password.

1. Select **Export**. Configuration Manager uses the Windows ADK to create the enrollment package.

Configuration Manager keeps track of valid enrollment packages. In the console, expand the **Enrollment Profile** node and select **Exported Packages**.

> [!TIP]
> If you remove an enrollment package from the Configuration Manager console, you can't use it to enroll devices. Use this method to manage enrollment packages that you don't want others to use for bulk enrollment.

## <a name="bkmk_getPpkg"></a> Bulk-enroll a device

You can use a package to enroll devices before or after the device's out-of-box experience (OOBE) process. The enrollment package can also be included as part of an original equipment manufacturer (OEM) provisioning package.

To use the package for bulk enrollment, you need to physically deliver it to the device. There are various methods depending on your needs, for example:

- Copy from the file system

- Attach to an email

- Copy across a near field communication (NFC) connection

- Copy from a memory card

- Scan a barcode

- Copy from a tethered device

- Include in an OEM provisioning package

### Enroll a device with bulk enrollment package

1. On a device, open the .ppkg file. Run as administrator if necessary.

1. Windows asks if the package is from a trusted source, select **Yes**.

The enrollment process starts.

## <a name="bkmk_verifyEnroll"></a> Verify enrollment

### Verify bulk enrollment on the device

1. On the device, open **Settings**.

1. Select **Accounts**, and select **Access work or school**. When enrollment is successful, you see an account under **CompanyApps**.

1. Select the account, and then select **Sync**. This action starts management with Configuration Manager.

### Verify enrollment in the console

Use the Configuration Manager console to verify that devices are enrolled successfully. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select **Devices**. Browse or search for the enrolled device in the list of devices.