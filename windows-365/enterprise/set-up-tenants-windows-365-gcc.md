---
# required metadata
title: Set up tenants for Windows 365 Government
titleSuffix:
description: Learn how to set up tenants for Windows 365 Government.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/3/2022
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Set up tenants for Windows 365 Government

For Windows 365 to function in the Government Community Cloud (GCC) environment, customers must prepare one commercial Azure domain (.com) tenant with an onmicrosoft.com address. If you want to use configuration options described in this article, you must also prepare one Azure Government domain (.us) tenant with an onmicosoft.us address.

## Commercial Azure tenant (.com)

The commercial Azure tenant includes:

- Windows 365 subscription.
- Enterprise Mobility + Security (EMS)/Microsoft Endpoint Manager subscription.
- Azure Active Directory (Azure AD) information such as Users and Groups.

## Azure goverment tenant (.us)

The Azure Government tenant includes Microsoft Azure subscription and associated services, such as:

- Azure Virtual Network (vNet).
- Azure ExpressRoute connections.
- Other Azure Resources, including Cloud PC resources.

>[!NOTE]
> While the GCC users' Cloud PCs are hosted and secured in the Azure Government cloud, the admin and end user experience is similar to the commercial business uer experience. This is because the endpoints for admins and end users are in the commercial Azure domain.

## Azure AD options

If you want to use Azure AD join or hybrid Azure AD join, consider these preparations:

**Azure AD joined Cloud PCs**: If the you want to use an Azure AD join infrastructure and your own network, you'll need a tenant and Azure subscription in the Azure Government cloud. The tenant in the Azure commercial .com domain must be mapped to the tenant in the Azure Government .us domain.

**Hybrid Azure AD joined Cloud PCs**: If you want to use a hybrid Azure AD join infrastructure, you'll need to configure your commercial (.com) tenant and your government (.us) tenants before creating your Azure Virtual Networks.

## Map the commercial and government tenants
For the two tenants to be connected and have the ability for a user with an identity in the Azure Commercial cloud to access their Windows 365 Cloud PCs provisioned in the Azure Government,  the Tenant Mapping PowerShell script will need to be run.  The mapping also enables administrators using their Azure Commercial identity to provision and manage the Windows 365 Cloud PCs in the Azure Government cloud.

1. Find the following information. It will be used later in these steps.
    - [Commercial Azure tenant ID](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).
    - Commercial Azure Global administrator user name and password.
    - [Azure Government tenant ID](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).
  - Azure Government Global administrator credentials user name and password.
2. Make sure you have Windows PowerShell version 5.1. Other versions may result in errors when running the script.
3. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
4. Navigate to the **Windows 365 GCC** folder > right-click **TenantMapping.ps1** > **Save link as** > save the file to a location on your computer.
5. Open Windows PowerShell 5.1 and run the PowerShell script.
    >[!NOTE]
    >If the script was previously run successfully, you'll see the error **HttpStatusCode Conflict**. This warning can be ignored to execute the script functions Add and Get.
6. In PowerShell 5.1, type **I** to initiate tenant mapping.
7.	After the Initialization completes, type **A** at the prompt. When prompted, type the following information:
    - Your Commercial tenant ID, which can be found here: https://portal.azure.com/.
    - Your Azure Government tenant ID, which can be found here: https://portal.azure.us/.
8. When prompted, press Enter to open a web browser and enter your user name and password for your commercial tenant (GlobalAdmin@xxxxx.onmicrosoft.com).
9.	When prompted, press Enter to open a web browser and enter your credentials for your Azure government tenant (GlobalAdmin@yyyyy.onmicrosoft.us).
10. After the mapping completes, you'll see **Added tenant mapping successfully!**

## Azure AD join custom image management

If you're going to use Gallery images to provision Cloud PCs using the Microsoft Hosted Network (MHN), no further configurations are required.

However, extra steps are needed to upload custom images on the Microsoft Hosted Network for Azure AD join-only Cloud PC. In this case, follow these steps before uploading your Custom Image.

You will need Commercial and Gov credentials and line of sight to both tenants to execute the script.

1. Make sure you have both commercial and government credentials.
2. Make sure you have line of sight to both tenants.
3. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
4. Navigate to the **Windows 365 GCC** folder > right click **GrantSPRolesInTenant.ps1** > **Save link as** > save the file to a location on your computer.
5. Run the PowerShell script.
6. At the prompt, type **1** to enable custom image uploads.

## Set permissions for networking and custom image management

When provisioning Windows 365 Cloud PCs without the Microsoft Hosted Network (MHN), you must define an Azure Network Connection (ANC) resource that the Cloud PCs will use to connect with other resources, including your on-prem infrastructure.  This will allow GCC customers to use their own network.  There is also an option to enable customers to use custom images when the Windows 365 Cloud PCs are provisioned.

1. Gather the following information. It will be used later in these steps.
    - Commercial Azure tenant ID.
    - Commercial Azure Global administrator username and password.
    - Azure Government tenant ID.
    - Azure Government Global administrator credentials username and password.
    - Subscription in the Azure Government tenant.
    - Resource Group in the Azure Government tenant.
    - Virtual Network in the Azure Government tenant.
2. Make sure you have Windows PowerShell version 5.1. Other versions may result in errors when running the script.
3. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
4. Navigate to the **Windows 365 GCC** folder > right-click **GrantSPRolesInTenant.ps1** > **Save link as** > save the file to a location on your computer.
5. Open Windows PowerShell 5.1 and run the PowerShell script. First step is to login to your Azure Government cloud tenant.
6. At the prompt, type one of the following options:
    - **2** to grant permissions to create Azure Network Connections (ANC).
    - **3** to grant permissions to create ANCs and upload custom images.
7. The script lists the subscriptions available for the Azure Government cloud tenant. Select the subscription that you want to use.
8. The resource groups for that subscription are listed. Select the group that you want to use.
9. Select your vNet.
10. The script grants the permissions and lists what was configured.
