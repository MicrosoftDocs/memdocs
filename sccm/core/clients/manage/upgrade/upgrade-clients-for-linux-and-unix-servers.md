---
itle: "Upgrade clients | Linux UNIX "
description: "Upgrade a client on a Linux or UNIX server in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to upgrade clients for Linux and UNIX servers in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can upgrade the version of the client for Linux and UNIX on a computer to a newer client version without first uninstalling the current client. To do so, install the new client installation package on the computer while using the **-keepdb** command line property. When the client for Linux and UNIX installs, it overwrites existing client data with the new client files. However, the **-keepdb** command line property directs the install process to retain the clients unique identifier (GUID), local database of information, and certificate store. This information is then used by the new client installation.  

 For example, you have a RHEL5 x64 computer that runs the client from the original release of the Configuration Manager client for Linux and UNIX. To upgrade this client to the client version from cumulative update 1, you manually run the **install** script to install the applicable client package from cumulative update 1, with the addition of the **-keepdb** command line switch. The command line you use resembles the following: **./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar**  

## How to use a Software Deployment to Upgrade the Client on Linux and UNIX Servers  
 You can use a software deployment to upgrade the client for Linux and UNIX to a new client version. However, the System Center Configuration Manager client cannot directly run the installation script to install the new client because the installation of a new client must first uninstall the current client. This would end the Configuration Manager client process that runs the installation script before the installation of the new client begins. To successfully use a software deployment to install the new client, you must schedule the installation to start at a future time and to be run by the operating system's built-in scheduling capabilities.  

 To accomplish this, use a software deployment to first copy the files for the new client installation package to the client computer, and then deploy and run a script to schedule the client installation process. The script uses the operating system's built-in **at** command to delay its start. Then, when the script runs, its operation is managed by the client operating system and not the Configuration Manager client on the computer. This allows the command line called by the script to first uninstall the Configuration Manager client and then install the new client, completing the process of upgrade of the client on the Linux or UNIX computer. After the upgrade completes, the upgraded client remains managed by Configuration Manager.  

 Use the following procedure to help you configure a software deployment to upgrade the client for Linux and UNIX. The following steps and examples upgrade a RHEL5 x64 computer that runs the initial release of the client to the cumulative update 1 client version.  

#### To use a software deployment to upgrade the client on Linux and UNIX servers  

1.  Copy the new client installation package file to the computer that runs the Configuration Manager client that you plan to upgrade.  

     For example, you might place the client installation package and install script for cumulative update 1 in the following location on the client computer: **/tmp/PATCH**  

2.  Create a script to manage the upgrade of the Configuration Manager client, and then place a copy of the script in the same folder on the client computer as the client installation files from step 1.  

     The script does not require a specific name, but must contain command lines sufficient to use the client installation files from a local folder on the client computer, and to install the client installation package by using the **-keepdb** command line property. You use the **-keepdb** command line property to maintain the unique identifier of the current client for use by the new client you are installing.  

     For example, you create a script named **upgrade.sh** that contains the following lines, and then copy it to the **/tmp/PATCH** folder on the client computer:  

    ```  
    #!/bin/sh  
    #  
    /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

    ```  

3.  Use software deployment to have each client use the computers built-in **at** command to run the **upgrade.sh** script with a short delay before the script runs.  

     For example, use the following command line to run the script: **at -f /tmp/upgrade.sh -m now + 5 minutes**  

 After the client successfully schedules the **upgrade.sh** script to run, the client submits a status message indicating the software deployment completed successfully. However, the actual client installation is then managed by the computer, after the delay. After the client upgrade completes, validate the install by reviewing the **/var/opt/microsoft/scxcm.log** file on the client computer. Additionally, you can confirm that the client is installed and communicating with the site by viewing details for the client in the **Devices** node of the **Assets and Compliance** workspace in the Configuration Manager console.  
