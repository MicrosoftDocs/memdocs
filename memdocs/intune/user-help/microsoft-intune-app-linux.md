---
# required metadata

title: Get the Microsoft Intune app for Linux | Microsoft Docs
description: Describes how to install, update, and remove the Microsoft Intune app for Linux. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: ilwu
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---  

# Get the Microsoft Intune app for Linux   

This article describes how to install, update, and remove the Microsoft Intune app for Linux on a personal device.  

The Microsoft Intune app package is available at [https://packages.microsoft.com/](https://packages.microsoft.com/). For more information about how to use, install, and configure Linux software packages for Microsoft products, see [Linux Software Repository for Microsoft Products](/windows-server/administration/linux-package-repository-for-microsoft-software).  

## Requirements  
The Microsoft Intune app is supported with the following operating systems:  

 - Ubuntu Desktop 22.04 or 20.04 LTS (physical or Hyper-V machine with x86/64 CPUs)  
 - RedHat Enterprise Linux 8  
 - RedHat Enterprise Linux 9    

## Install Microsoft Intune app for Ubuntu Desktop
Run the following commands in a command line to manually install the Intune app and its dependencies on your device.  

1. Install Curl. 

    ```bash
    sudo apt install curl gpg
    ```

2. Install the Microsoft package signing key.  

   For Ubuntu 20.04:  

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
    sudo install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/
    sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/ubuntu/20.04/prod focal main" > /etc/apt/sources.list.d/microsoft-ubuntu-focal-prod.list'
    sudo rm microsoft.gpg
    ```
    
    For Ubuntu 22.04:  

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
    sudo install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/ 
    sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/ubuntu/22.04/prod jammy main" > /etc/apt/sources.list.d/microsoft-ubuntu-jammy-prod.list' 
    sudo rm microsoft.gpg
    ```

3. Install the Microsoft Intune app. 

    ```bash
    sudo apt update
    sudo apt install intune-portal
    ``` 

## Update Microsoft Intune app for Ubuntu Desktop 
The Microsoft Intune app automatically updates when updates become available in Software Updater.  Run the following commands to update the Microsoft Intune app manually.    

1. Update the package repo and metadata, which includes `intune-portal`, `msft-broker`, and `msft edge`.   

    ```bash
    sudo apt update
    ```
 
2. Upgrade the packages and clean up dependencies.  

    ```bash
    sudo apt-get dist-upgrade
    ```

## Uninstall Microsoft Intune app for Ubuntu Desktop  
Run the following commands to uninstall the Microsoft Intune app and remove local registration data on devices running Ubuntu Desktop.  

1. Remove the Microsoft Intune app from your system.  

    ```bash
    sudo apt remove intune-portal
    ```

2. Remove the local registration data.  

    ```bash
    sudo apt purge intune-portal
    ```  
    This command removes the local configuration data that contains your device registration.  

## Install Microsoft Intune app for RedHat Enterprise Linux  

1. Add the Microsoft repository.  

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   sudo dnf config-manager --add-repo https://packages.microsoft.com/yumrepos/microsoft-rhel9.0-prod
   ```

2. Install the Microsoft Intune app.  

   ```bash
   sudo dnf install intune-portal
   ```

## Update Microsoft Intune app for RedHat Enterprise Linux  
Run one of the following commands to update the Intune app.  

**Option 1**:  

   ```bash
   sudo dnf update
   ```

**Option 2**: 
   ```bash
   sudo dnf update intune-portal
   ```

## Uninstall Microsoft Intune app for RedHat Enterprise Linux  

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
