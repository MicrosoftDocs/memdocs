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

For Windows 365 to function in the Government Community Cloud (GCC) environment, customers must link their Azure AD (Commercial) tenant with their Azure AD (Government) tenant. This enables Intune running in Azure Commercial to manage Cloud PCs running in Azure Government regions, including the options of using custom images and connecting to your own networks.   

Use the following procedures to setup Windows 365 in the Government Community Cloud (GCC).

> [!NOTE]
> These instructions are specifically for GCC.  The instructions on this page do not apply to GCC High.

## Before you begin
- You must have an Azure Commercial AND an Azure Government subscription.
- You will be required to enter the credentials of a user that has
    - *Owner* role in your Azure Commercial subscription, AND
    - *Global Administrator* role in your Azure AD (Commercial) tenant which ends in onmicrosoft.com.
- You (or another person) will be required to enter the credentials of a user that has
    - *Owner* role in your Azure Government subscription, AND
    - *Global Administrator* role in your Azure AD (Government) tenant which ends in onmicrosoft.us.
- You must have Windows PowerShell version 5.1.
    - PowerShell 5.1 is [preinstalled](/powershell/scripting/windows-powershell/install/installing-windows-powershell) on Windows 10/11 and Windows Server 2016 or later.
    - Other PowerShell versions may result in errors when performing the tenant mapping.

## Azure Commercial side

The Azure Commercial subscription includes a tenant (which ends in onmicrosoft.com) and the following:

- Windows 365 Government subscription.
- Enterprise Mobility + Security (EMS)/Microsoft Endpoint Manager subscription.
- Azure Active Directory information such as Users and Groups.

## Azure Government side

The Azure Government subscription includes a tenant (which ends in onmicrosoft.us) and the following if you wish to:

**Use Custom Images**
- [Add a custom image](/windows-365/enterprise/add-device-images)

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

To connect the two tenants, the **AAD Tenant Mapping.ps1** PowerShell script must be run. This script will give admins either or both of the following abilities:

- Upload custom images for use with Windows 365 Government Cloud PCs.
- Define Azure Network Connections so that the Windows 365 Government Cloud PCs can access on-premises or Microsoft-hosted resources.

1. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
2. Navigate to the **Windows 365 GCC** folder > **AAD Tenant Mapping** > select **AAD Tenant Mapping.ps1** > **Raw** > save the raw file to a location on your computer as a .ps1 file.
3. Open Windows PowerShell 5.1 (x64) as Administrator and run the PowerShell script. It will download missing modules if needed.
    >[!NOTE]
    >If the script was previously run successfully, you'll see the error **HttpStatusCode Conflict**. This warning can be ignored to execute the script functions Add and Get.
4. In PowerShell 5.1, type **A** to add tenant mapping.
5. A web browser prompt will open.  Enter your **Azure Commercial** credentials (e.g. GlobalAdmin@contoso.onmicrosoft.com). The window will then close after successful authentication. 
6. Another web browser prompt will open, you will be asked for your **Azure Commercial** credentials again, after that another prompt will ask you to grant permissions.  Check the box **Consent on behalf of your organization** and then click on the **Accept** button. The windows will then close.
7. A web browser prompt will open. Enter your **Azure Government** credentials (e.g. GlobalAdmin@fabrikam.onmicrosoft.us). The window will then close after successful authentication.
8. Another web browser prompt will open, you will be asked for your **Azure Government** credentials again, after that another prompt will ask you to grant permissions.  Check the box **Consent on behalf of your organization** and then click on the **Accept** button. The windows will then close.
8. After the mapping completes, you will see **Added tenant mapping successfully!**

## Common tenant mapping issues

If the mapping fails, try the following suggestions:

- **Wait at least 10 minutes and try again.** Permission changes must propagate before the mapping can complete.

- **Confirm there isn't an existing tenant mapping.** Only a 1:1 mapping of the Commercial:Government tenant is supported. Run the *AAD Tenant Mapping.ps1** script again and select the **Get** option.  Contact support by filing a support ticket in the Microsoft Intune admin center (intune.microsoft.com) > Tenant Administration > Help and support > Windows 365 via with the error details.

## Set permissions to upload custom images

If you're going to use Gallery images to provision Cloud PCs using the Microsoft-hosted network, no further configurations are required.

Extra steps are needed to upload custom images on the Microsoft-hosted network. In this case, follow these steps before uploading your custom image:

1. Make sure you've already run the TenantMapping.ps script above to connect the Government cloud and Commercial cloud.
2. Make sure you have both commercial and government credentials.
3. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
4. Navigate to the **Windows 365 GCC/Grant Service Principal Roles in Tenant** folder > select **Grant W365 SP Roles in Tenant.ps1** > **Raw** > save the raw file to a location on your computer as a .ps1 file.
5. Run the PowerShell script.
6. For Azure AD join infrastructures, you don't need to enable permissions for creating ANC just to upload custom images. Therefore, at the prompt, type **1** to enable custom image uploads.
7. For hybrid Azure AD join infrastructures, creating ANCs is a requirement for uploading custom images. Therefore, at the prompt, type **3**.

## Set permissions to connect to on-premises resources

When provisioning Windows 365 Cloud PCs without the Microsoft-hosted network, you must define an [Azure Network Connection](azure-network-connections.md) (ANC) that the Cloud PCs will use to connect with other resources, including your on-premises infrastructure. To grant permissions for admins to create ANCs in the Government cloud, follow these steps:

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
4. Navigate to the **Windows 365 GCC/Grant Service Principal Roles in Tenant** folder > select **Grant W365 SP Roles in Tenant.ps1** > **Raw** > save the raw file to a location on your computer as a .ps1 file.
5. Open Windows PowerShell 5.1 and run the PowerShell script. First step is to sign in to your Azure Government cloud tenant.
6. At the prompt, type one of the following options:
    - **2** to grant permissions to create ANCs.
    - **3** to grant permissions to create ANCs and upload custom images.
7. The script lists the subscriptions available for the Azure Government cloud tenant. Select the subscription that you want to grant permissions to.
8. The resource groups for that subscription are listed. Select the group that you want to use.
9. Select your vNet.
10. The script grants the permissions and lists what was configured.



## Next steps

[Learn more about Windows 365 Government](introduction-windows-365-government.md)
