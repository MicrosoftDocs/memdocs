---
title: Get the Microsoft Intune app for Linux
description: Describes how to install, update, and remove the Microsoft Intune app for Linux.
ms.date: 03/31/2026
ms.reviewer: arnab
---

# Get the Microsoft Intune app for Linux

This article describes how to install, update, and remove the Microsoft Intune app for Linux on a personal device.

The Microsoft Intune app package is available at [https://packages.microsoft.com/](https://packages.microsoft.com/). For more information about how to use, install, and configure Linux software packages for Microsoft products, see [Linux Software Repository for Microsoft Products](/windows-server/administration/linux-package-repository-for-microsoft-software).

## Requirements

The Microsoft Intune app is supported with the following operating systems:

 - Ubuntu Desktop, version 22.04 LTS or 24.04 LTS (physical or Hyper-V machine with x86/64 CPUs)
 - RedHat Enterprise Linux 9
 - RedHat Enterprise Linux 10

## Install Microsoft Intune app for Ubuntu Desktop
A sample script to install the Microsoft Intune app and its dependencies on your device is available on [GitHub](https://go.microsoft.com/fwlink/?linkid=2358529). Review the instructions carefully before installing.  

### Uninstall app for Ubuntu Desktop
Run the following commands to uninstall the Microsoft Intune app and remove local registration data from devices running Ubuntu Desktop.

1. Remove the Intune app from your system.

    ```bash
    sudo apt remove intune-portal
    ```

2. Remove the local registration data. This command removes the local configuration data that contains your device registration.

    ```bash
    sudo apt purge intune-portal
    ```
## Install Microsoft Intune app for RedHat Enterprise Linux
A sample script to install the Microsoft Intune app and its dependencies on your device is available on [GitHub](https://go.microsoft.com/fwlink/?linkid=2358529). Review the instructions carefully before deploying.  

### Uninstall app for RedHat Enterprise Linux

Run the following commands to uninstall the Microsoft Intune app and remove local registration data on devices running RedHat Enterprise Linux.

1. Remove the Intune portal package.

   ```bash
   sudo dnf remove intune-portal
   ```

2. Remove local registration data.

   ```bash
   sudo rm -rf /var/opt/microsoft/mdatp
   sudo rm -rf /etc/opt/microsoft/mdatp
   sudo rm -rf /opt/microsoft/mdatp
   ```
