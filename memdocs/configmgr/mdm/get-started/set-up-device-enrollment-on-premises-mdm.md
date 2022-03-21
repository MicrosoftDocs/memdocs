---
title: Set up enrollment for on-premises MDM
titleSuffix: Configuration Manager
description: Grant users permission to enroll their devices for on-premises mobile device management (MDM) in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Set up device enrollment for on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

The final step to set up on-premises mobile device management (MDM) is to enable users to enroll their devices. Use Configuration Manager client settings to grant users permission to enroll devices in on-premises MDM.

## <a name="bkmk_createProf"></a> Create an enrollment profile

To push the settings required to allow users to enroll mobile devices, add a new enrollment profile to the default client settings. This profile then applies to all users in the Configuration Manager site.

> [!NOTE]
> This process uses the **Default Client Settings**, which will automatically apply to all devices and users. Alternatively, you can create custom client settings, and then deploy to collections of your choice. This alternative method requires at least two custom client settings, one for *device* settings and one for *user* settings. For more information, see [How to configure client settings](../../core/clients/deploy/configure-client-settings.md).

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node. Open **Default Client Settings** and select the **Enrollment** group.

1. Under Device Settings, specify the **Polling interval for modern devices (minutes)**. By default this interval is 60 minutes.

1. Under User Settings, enable the option to **Allow users to enroll modern devices**.

1. For the **Modern device enrollment profile**, select **Set Profile**. In the Enrollment Profile window, select **Create**.

1. In the Create Enrollment Profile window, specify the following information:

    - A unique and descriptive **Name** for the enrollment profile.

    - An optional **Description** to provide additional information about the profile.

    - Choose the **Management site code** that contains the device management point. Select **OK** to save and close.

## <a name="bkmk_addClient"></a> Configure additional client settings

There are additional client settings to configure devices after they've enrolled. For more general information, see [How to configure client settings](../../core/clients/deploy/configure-client-settings.md).

Configuration Manager supports the following client settings for on-premises MDM:

- **Client policy**: These settings specify the frequency for downloading client policy to the device. You can also enable settings for user policy. For more information, see [About client settings - Client Policy](../../core/clients/deploy/about-client-settings.md#client-policy).

- **Software deployment**: Set the interval for evaluating software deployments. For more information, see [About client settings - Software Deployment](../../core/clients/deploy/about-client-settings.md#software-deployment).

    > [!NOTE]
    > For on-premises MDM, software deployment settings can only be used as default client settings.

## <a name="bkmk_enableUsers"></a> Discover users

For users to receive the client settings with the enrollment profile for on-premises MDM, the site discovers their user account in Active Directory. To make sure everyone that needs the enrollment profile gets it, run discovery for Active Directory users. For more information, see [Active Directory User Discovery](../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

## <a name="bkmk_storeCert"></a> Install the trusted root certificate

Domain-joined devices get the trust root certificate for trusted communication with the servers hosting the site system roles. Active Directory Certificate Services automatically distributes the trusted root certificate. Non-domain joined computers and mobile devices need this certificate installed via other means to allow enrollment.

> [!NOTE]
> If the web server certificates are issued by a public certificate authority, most devices already trusted these CAs. If your design includes use of one of these public CAs, you don't need to do this step.

After you [export the trusted root certificate](set-up-certificates-on-premises-mdm.md#bkmk_exportCert), you need to install it on devices that will need it to enroll. For example, devices that aren't joined to the domain and can't get it automatically from Active Directory. The process that you use will depend upon the following factors:

- Specific device types and technical capabilities
- OS version
- Your business, security, and user experience requirements

The following list includes some example methods to deliver and install the trusted root certificate on devices:

- File share

- Email attachment

- Memory card

- Tethered device

- Cloud storage (such as OneDrive)

- Near field communication (NFC) connection

- Barcode scanner

- Out of box experience (OOBE) provisioning package

### Manually install the trusted root certificate in Windows

1. On the device to be enrolled, browse in File Explorer to the trusted root certificate file (.cer), and **Open** it.

1. In the Certificate window, select **Install Certificate**.

1. In the Certificate Import Wizard, select **Local Machine**, and then select **Next** to continue as administrator.

1. On the Certificate Store page, select **Place all certificates in the following store**, and then select **Browse**.

1. In the Select Certificate Store window, select **Trusted Root Certification Authorities**, and select **OK**.

1. Complete and wizard.

## Next step

> [!div class="nextstepaction"]
> [Enroll devices](../deploy-use/enroll-devices-on-premises-mdm.md)
