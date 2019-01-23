---
title: Create a lab in Azure
titleSuffix: Configuration Manager
description: Automate the creation of a Configuration Manager technical preview lab using Azure templates
ms.date: 01/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create a Configuration Manager technical preview lab in Azure

*Applies to: System Center Configuration Manager (Technical Preview)*

<!--3556017-->

This guide describes how to build a Configuration Manager lab environment in Microsoft Azure. It uses Azure templates to simplify and automate the creation of a lab using Azure resources. This process installs the latest version of the Configuration Manager technical preview branch. 

For more information on Configuration Manager current branch, see [Configuration Manager on Azure](/sccm/core/understand/configuration-manager-on-azure).



## Prerequisites

This process requires an Azure subscription in which you can create the following objects: 
- Four Standard_D2s_v3 virtual machines
- Standard_LRS storage account

> [!Tip]  
> See the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to help determine potential costs.  



## Process

1. Go to the [Configuration Manager template](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/).  

2. Select **Deploy to Azure**, which opens the Azure portal.  

3. Complete the Azure quickstart template with the following information:

    - Basics  

        - **Subscription**: The name of the subscription in which to create the VMs  

        - **Resource group**: Select a resource group to use for these VMs  

        - **Location**: Select an Azure data center to host this lab environment  

    - Settings  

        - **Prefix**: The prefix name of the machines. For more information, see [Azure VM info](#azure-vm-info).  

        - **Admin Username**: The name of a user on the VMs with administrative rights. You use this user to sign in to the VMs.  

        - **Admin Password**: The password must meet the Azure complexity requirements. For more information, see [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > The following settings are required by Azure. Use the default values. Don't change these values.  
    > 
    > - **\_artifacts Location**: The location of the scripts for this template <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_artifacts Location Sas Token**: The sasToken is required to access the artifacts location  
    > 
    > - **Location**: The location for all resources

4. Read the terms and conditions. If you agree, select **I agree to the terms and conditions stated above**. Then select **Purchase** to continue. 

Azure validates the settings, and then begins the deployment. Check the status of the deployment in the Azure portal. The process can take 2-4 hours. Even when the Azure portal shows successful deployment, configuration scripts continue to run. Don't restart the VMs during the process.

To see the status of the configuration scripts, connect to the `<prefix>PS1` server, and view the following file: `%windir%\TEMP\ProvisionScript\PS1.json`. If it shows all steps as complete, the process is done.

To connect to the VMs, first get from the Azure portal the public IP addresses for each VM. When you connect to the VM, the domain name is `contoso.com`. Use the credentials that you specified in the deployment template. For more information, see [How to connect and log on to an Azure virtual machine running Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## Azure VM info

All four VMs have the following specifications:
- Standard_D2s_v3, which has two CPU cores and 8 GB of memory  
- Windows Server 2016 Datacenter edition
- 150 GB of disk space
- Both a public and private IP address. The public IPs are in a network security group that only allows remote desktop connections on TCP port 3389. 

The prefix that you specified in the deployment template is the VM name prefix. For example, if you set "contoso" as the prefix, then the domain controller machine name is `contosoDC`.


### `<prefix>DC`

Active Directory domain controller

#### Windows features and roles
- Active Directory Domain Services (ADDS)
- .NET
- Remote Differential Compression (RDC)


### `<prefix>PS1`

- SQL Server
- Windows 10 ADK with Windows PE 
- Configuration Manager primary site

#### Windows features and roles
- .NET
- Remote Differential Compression (RDC) 
- Internet Information Service (IIS)


### `<prefix>MPDP`

- Management point
- Distribution point

#### Windows features and roles
- .NET
- Remote Differential Compression (RDC) 
- Internet Information Service (IIS)
- Background intelligent transfer service (BITS)


### `<prefix>Other`

This VM can be used as a client, or to host other site roles.

#### Windows features and roles
- .NET
- Remote Differential Compression (RDC) 


