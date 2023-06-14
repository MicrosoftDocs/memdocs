---
# required metadata

title: Get the Microsoft Intune app for Linux | Microsoft Docs
description: Describes how to install, update, and remove the Microsoft Intune app for Linux. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/17/2022
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
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

This article describes how to install, update, and remove the Microsoft Intune app for Linux on a  personal device.  

The Microsoft Intune app package is available at [https://packages.microsoft.com/](https://packages.microsoft.com/). For more information about how to use, install, and configure Linux software packages for Microsoft products, see [Linux Software Repository for Microsoft Products](/windows-server/administration/linux-package-repository-for-microsoft-software).  

## Install Intune app  
Run the following commands in a command line to manually install the Intune app and its dependencies on your device.  

1. Install Curl.  
    `$ sudo apt install curl gpg` 

2. Install the Microsoft package signing key.  

   For Ubuntu 20.04:  
    `$ curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg`  
 
    `$ sudo install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/` 

    `$ sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/ubuntu/20.04/prod focal main" > /etc/apt/sources.list.d/microsoft-ubuntu-focal-prod.list'` 

    `sudo rm microsoft.gpg` 
    
    For Ubuntu 22.04:  
     `$ curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg`  
     
     `$ sudo install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/`  
     
     `$ sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/ubuntu/22.04/prod jammy main" > /etc/apt/sources.list.d/microsoft-ubuntu-jammy-prod.list'`  
     
     `sudo rm microsoft.gpg`  

3. Install the Microsoft Intune app.  

    `$ sudo apt update` 

    `$ sudo apt install intune-portal` 

4. Reboot your device.   

## Update Intune app 
The Microsoft Intune app automatically updates when updates become available in Software Updater.   

Run these commands to update the Microsoft Intune app manually:    

1. Update the package repo and metadata, which includes intune-portal, msft-broker, and msft edge.  
    `$ sudo apt update` 
 
2. Upgrade the packages and clean up dependencies.   
    `$ sudo apt-get dist-upgrade`  

## Uninstall Intune app 

1. Remove the Intune app from your system.   
    `$ sudo apt remove intune-portal` 

2. Remove the local registration data. This command removes the local configuration data that contains your device registration.     
    `$ sudo apt purge intune-portal` 

 
