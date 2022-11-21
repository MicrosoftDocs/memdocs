---
# required metadata
title: Set up tenants for Windows 365 Government
titleSuffix:
description: Learn how to set up tenants for Windows 365 Government.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/10/2022
ms.topic: overview
ms.service: windows-365
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

> [!NOTE]
> You do not need an Azure (Commercial or Government) subscription to use Windows 365.

The instructions on this page are only if you must use either or both:
- **Custom images**. Windows 365 provides optimized images; Intune can be used for further customization of [common settings](/mem/intune/configuration/settings-catalog-common-features) and [application deployment](/mem/intune/apps/apps-windows-10-app-deploy). If you must use your existing custom image, for more information, see [add a custom image](./add-device-images.md).
- **Azure Network Connections (ANC)**. ANC lets you provision Cloud PCs that are attached to a virtual network that you manage. For more information, see [create an Azure network connection](/windows-365/enterprise/create-azure-network-connection).

For Windows 365 to function in the Government Community Cloud (GCC) environment, customers must link their Azure Commercial tenant with their Azure Government tenant. This linkage lets Intune running in Azure Commercial to manage Cloud PCs running in Azure Government regions, including the options of using custom images and connecting to your own networks.     

Use the following procedures to set up Windows 365 in the Government Community Cloud (GCC).

> [!NOTE]
> These instructions are specifically for GCC.  The instructions on this page do not apply to GCC High.

## Before you begin
For both tenant mapping and granting permissions for custom images and/or connecting to your own networks, you'll need:

- An Azure Commercial subscription.
- An Azure Government subscription.
- Credentials of a user that has:
    - *Owner* role in your Azure Commercial subscription, AND
    - *Global Administrator* role in your Azure Commercial tenant (ending in onmicrosoft.com).
- Credentials of a user that has:
    - *Owner* role in your Azure Government subscription, AND
    - *Global Administrator* role in your Azure Government tenant (ending in onmicrosoft.us).
- Administrative rights on a workstation or server with:
    - Windows PowerShell version 5.1. PowerShell 5.1 is [preinstalled](/powershell/scripting/windows-powershell/install/installing-windows-powershell) on Windows 10/11 and Windows Server 2016 or later. Other PowerShell versions may result in errors when performing the tenant mapping.
    - The following installed. The script will download the missing items below if it isn't present.
        - NuGet provider
        - [AzureAD](https://www.powershellgallery.com/packages/AzureAD/2.0.2.140)
        - [MSAL.PS](https://www.powershellgallery.com/packages/MSAL.PS/4.37.0.0)

## Azure Commercial requirements

The Azure Commercial subscription includes a tenant (which ends in onmicrosoft.com) and the following:

- Windows 365 Government subscription.
- Enterprise Mobility + Security (EMS)/Microsoft Endpoint Manager subscription.
- Azure Active Directory tenant with the Users and Groups accessing Windows 365.

## Azure Government requirements

The Azure Government subscription includes a tenant (which ends in onmicrosoft.us) and the following if you wish to:

**Use Custom Images**
- For more information, see [add a custom image](./add-device-images.md).

**Connect to resources via a private network connection**
- Azure Virtual Network (VNet).
- Azure VPN Gateway or a dedicated connection via ExpressRoute.
- Other Azure Resources, including Cloud PC resources.

>[!NOTE]
> While the GCC users' Cloud PCs are hosted and secured in the Azure Government cloud, the admin and end user experience is similar to the commercial business user experience. This is because the endpoints for admins and end users are in the commercial Azure domain.

## Azure AD options

If you want to use Azure AD join or hybrid Azure AD join, consider these preparations:

**Azure AD joined Cloud PCs**: If you want to use an Azure AD join infrastructure and your own network, you'll need a tenant and Azure subscription in the Azure Government cloud. The tenant in the Azure commercial .com domain must be mapped to the tenant in the Azure Government .us domain.

**Hybrid Azure AD joined Cloud PCs**: If you want to use a hybrid Azure AD join infrastructure, you'll need to configure your commercial (.com) tenant and your government (.us) tenants before creating your Azure Virtual Networks.


## Map the commercial and government tenants

To connect the two tenants, the **AAD Tenant Mapping.ps1** PowerShell script must be run. This script is a pre-requisite to give admins either or both of the following abilities:

- Upload custom images for use with Windows 365 Government Cloud PCs.
- Define Azure Network Connections so that the Windows 365 Government Cloud PCs can access on-premises or Microsoft-hosted resources.

1. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
2. Navigate to the **Windows 365 GCC** folder > **AAD Tenant Mapping** > select **AAD Tenant Mapping.ps1** > **Raw** > save the raw file to a location on your computer as a .ps1 file.
3. Open Windows PowerShell 5.1 (x64) as Administrator and run the PowerShell script. It will download missing modules if needed.
    >[!NOTE]
    >If the script was previously run successfully, you'll see the error **HttpStatusCode Conflict**. This warning can be ignored to execute the script functions Add and Get.
4. In PowerShell 5.1, type **A** to add tenant mapping.
5. A web browser prompt will open.  Enter your **Azure Commercial** credentials (for example, GlobalAdmin@contoso.onmicrosoft.com). The window will then close after successful authentication. 
6. A second web browser prompt will open, you'll be asked for your **Azure Commercial** credentials again, after that another prompt will ask you to grant permissions.  Check the box **Consent on behalf of your organization** and then click on the **Accept** button. The window will then close.
7. A third browser prompt will open. Enter your **Azure Government** credentials (for example, GlobalAdmin@fabrikam.onmicrosoft.us). The window will then close after successful authentication.
8. A fourth web browser prompt will open, you'll be asked for your **Azure Government** credentials again, after that another prompt will ask you to grant permissions.  Check the box **Consent on behalf of your organization** and then click on the **Accept** button. The window will then close.
8. After the mapping completes, you'll see **Added tenant mapping successfully!**

## Common tenant mapping issues

If the mapping fails, try the following suggestions:

- **Wait at least 10 minutes and try again.** Permission changes must propagate before the mapping can complete.

- **Confirm there isn't an existing tenant mapping.** Only a 1:1 mapping of the Commercial and Government tenants is supported. Run the **AAD Tenant Mapping.ps1** script again and select the **Get** option.  Contact support by filing a support ticket in the Microsoft Intune admin center (intune.microsoft.com) > Tenant Administration > Help and support > Windows 365 via with the error details.

## Set permissions to upload custom images and/or connect to on-premises resources

If you're going to use Gallery images to provision Cloud PCs using the Microsoft-hosted network, no further configurations are required.  Stop here.

If you're going to upload custom images on the Microsoft-hosted network, keep reading.

When provisioning Windows 365 Cloud PCs without the Microsoft-hosted network, you must define an [Azure Network Connection](azure-network-connections.md) (ANC) that the Cloud PCs will use to connect with other resources, including your on-premises infrastructure. To set up the ANC, you'll need the existing values for the Azure Government:
    - Subscription ID.
    - Resource Group.
    - Virtual Network.

> [!NOTE]
> Tenant mapping must be successful before you proceed.

Copy and paste the command below to execute in your Azure Government subscription's CloudShell and then go to the section **Script instructions** below.

```azurepowershell-interactive
curl https://raw.githubusercontent.com/microsoft/Windows365-PSScripts/main/Windows%20365%20GCC/Grant%20Service%20Principal%20Roles%20in%20Tenant/Grant%20W365%20SP%20Roles%20In%20Tenant.ps1 -o GrantW365SProles.ps1 & .\GrantW365SProles.ps1
```

OR use the instructions below if you do not have a CloudShell account which requires an Azure Storage account.

1. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
2. Navigate to the **Windows 365 GCC** folder > **Grant Service Principal Roles in Tenant** folder > select **Grant W365 SP Roles in Tenant.ps1** > **Raw** > save the raw file to a location on your computer as a .ps1 file.
3. Open Windows PowerShell 5.1 (x64) as Administrator and run the PowerShell script and then go to the section **Script instructions** below.

**Script instructions:**
You will be asked to enter the Azure subscription ID from a list of subscriptions you have access to, where the W365 app permissions will be granted.
1. At the prompt, type one of the following options to grant permissions:
    - **1** to only upload custom images. For Azure AD join infrastructures, you don't need to create an ANC just to upload custom images.
    - **2** to only create ANCs.
    - **3** to create ANCs and upload custom images. For hybrid Azure AD join infrastructures, creating an ANC is a requirement for uploading custom images.
        - The script lists the Azure Government subscriptions you have access to. Select the subscription that you want to grant permissions to.
        - The resource groups for that subscription are then listed. Select the group that you want to use.
        - Select your vNet.
2. The script will then grant the permissions and lists what was configured.


## Next steps

[Learn more about Windows 365 Government](introduction-windows-365-government.md)
