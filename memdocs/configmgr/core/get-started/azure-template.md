---
title: Create a lab in Azure
titleSuffix: Configuration Manager
description: Automate the creation of a Configuration Manager technical preview lab or current branch evaluation lab using Azure templates
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Create a Configuration Manager lab in Azure

*Applies to: Configuration Manager (technical preview branch)*

<!--3556017-->

This guide describes how to build a Configuration Manager lab environment in Microsoft Azure. It uses Azure templates to simplify and automate the creation of a lab using Azure resources. Two Azure templates are provided: 

- Configuration Manager technical preview Azure template installs the latest version of the Configuration Manager technical preview branch.
- Configuration Manager current branch Azure template installs the evaluation of the latest version of Configuration Manager current branch. 

For more information, see [Configuration Manager on Azure](../understand/configuration-manager-on-azure.md).



## Prerequisites

This process requires an Azure subscription in which you can create the following objects: 
- Two Standard_B2s virtual machines for Domain Contoller and MP & DP roles.
- One Standard_B2ms virtual machine for Primary Site Server and SQL database server.
- Standard_LRS storage account

> [!Tip]  
> See the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to help determine potential costs.  



## Process

1. Go to the [Configuration Manager technical preview template](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) or [Configuration Manager current branch template](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

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

Azure validates the settings, and then begins the deployment. Check the status of the deployment in the Azure portal. 

> [!NOTE]
> The process can take 2-4 hours. Even when the Azure portal shows successful deployment, configuration scripts continue to run. Don't restart the VMs during the process.

To see the status of the configuration scripts, connect to the `<prefix>PS1` server, and view the following file: `%windir%\TEMP\ProvisionScript\PS1.json`. If it shows all steps as complete, the process is done.

To connect to the VMs, first get from the Azure portal the public IP addresses for each VM. When you connect to the VM, the domain name is `contoso.com`. Use the credentials that you specified in the deployment template. For more information, see [How to connect and log on to an Azure virtual machine running Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## Azure VM info

All Three VMs have the following specifications:
- 150 GB of disk space
- Both a public and private IP address. The public IPs are in a network security group that only allows remote desktop connections on TCP port 3389. 

The prefix that you specified in the deployment template is the VM name prefix. For example, if you set "contoso" as the prefix, then the domain controller machine name is `contosoDC`.


### `<prefix>DC01`

- Active Directory domain controller
- Standard_B2s, which has two CPU and 4 GB of memory
- Windows Server 2019 Datacenter edition

#### Windows features and roles
- Active Directory Domain Services (ADDS)
- .NET
- Remote Differential Compression (RDC)


### `<prefix>PS01`

- Standard_B2ms, which has two CPU and 8 GB of memory
- Windows Server 2016 Datacenter edition
- SQL Server
- Windows 10 ADK with Windows PE 
- Configuration Manager primary site

#### Windows features and roles
- .NET
- Remote Differential Compression (RDC) 
- Internet Information Service (IIS)


### `<prefix>DPMP01`

- Standard_B2s, which has two CPU and 4 GB of memory
- Windows Server 2019 Datacenter edition
- Distribution point
- Management point

#### Windows features and roles
- .NET
- Remote Differential Compression (RDC) 
- Internet Information Service (IIS)
- Background intelligent transfer service (BITS)

### `<prefix>CL01`

- Only for Configuration Manager current branch evaluation template
- Windows 10
- Configuration Manager client
