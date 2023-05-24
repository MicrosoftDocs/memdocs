---
# required metadata
title: Set up tenants for Windows 365 Government
titleSuffix:
description: Learn how to set up tenants for Windows 365 Government.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/31/2023
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
ms.collection:
- M365-identity-device-management
- tier2
---

# Set up tenants for Windows 365 Government

> [!NOTE]
> You don't need an Azure Government subscription to use Windows 365 Government.

The fastest way to use Windows 365 is to use AADJ, gallery images and the Microsoft Hosted Network option. The instructions on this page are only if you must use either or both:

- **Custom images**. Windows 365 provides optimized gallery images, including images with Microsoft 365 apps preinstalled(/windows-365/enterprise/device-images). After the gallery image is deployed, Intune can be used for further customization of [common settings](/mem/intune/configuration/settings-catalog-common-features) and [application deployment](/mem/intune/apps/apps-windows-10-app-deploy). If you must use your existing custom image, for more information, see [add a custom image](./add-device-images.md).
- **Azure Network Connections (ANC)**. ANC lets you provision Cloud PCs that are attached to a virtual network that you manage. For more information, see [create an Azure network connection](./create-azure-network-connection.md).

For Government Community Cloud (GCC) customers only, the instructions below lets Intune running in Azure Commercial to manage Cloud PCs running in Azure Government regions.

> [!NOTE]
> These instructions are specifically for GCC.  The instructions on this page don't apply to GCC High.

## Before you begin
For both tenant mapping and granting permissions for custom images and/or connecting to your own networks, you need:

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
    - The following installed. The script downloads the following missing items if it isn't present.
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
> While the GCC users' Cloud PCs are hosted and secured in the Azure Government cloud, the endpoints for admins and end users are in the commercial Azure domain. Users will login to the Cloud PCs using credentials synched with Azure Commercial AAD.

## Azure AD options

If you want to use Azure AD join or hybrid Azure AD join, consider these preparations:

**Azure AD joined Cloud PCs**: If you want to use an Azure AD join infrastructure and your own network, you need a tenant and Azure subscription in the Azure Government cloud. The tenant in the Azure commercial .com domain must be mapped to the tenant in the Azure Government .us domain.

**Hybrid Azure AD joined Cloud PCs**: If you want to use a hybrid Azure AD join infrastructure, you must configure your commercial (.com) tenant and your government (.us) tenants before creating your Azure Virtual Networks.

## Get started with the Windows 365 GCC Setup Tool

Follow these steps to configure tenant mapping using the Windows 365 GCC Setup Tool.

1. Launch the GCCSetupTool.exe.
2. On the **Let's get you started** page, select **Next**.
3. Sign in with your Azure Commercial account. This account must have Global Administrator permissions.
4. Confirm that you want to continue with your commercial account > **Next**.
5. Sign in with your Azure Government account > **Next** > type your credentials.
6. Confirm that you want to continue with your government account > **Next**.
7. On the **Select feature to enable screen**, make sure **Custom Images** is selected.
8. Select **Azure network connections** and then select the **Subscription**, **Virtual network**, and **Subnet** that you want to configure. Select **Next**.

    > [!NOTE]
    > ANC includes the permissions for custom images.

9. On the **Review settings** page, review the selections you made and select **Grant**.
10. After setup is complete, you can close the tool.

### Troubleshooting

If you have issues running the Windows 365 GCC Setup Tool:

1. In the same folder where the GCCSetupTool.exe is run, navigate to the **Log** folder and review the `GCCAdminTool.log` file.
2. If you continue to have issues, [contact support](/mem/get-support#contact-support).

### Subsequent use of the GCC Setup Tool

The Windows 365 GCC Setup Tool can be run again after the initial setup. You might want to use it again if you want to use ANC or expand the use of ANC to other networks. You can also use the following script to set up permissions for more ANCs.

#### If you have a Cloud Shell account that requires an Azure Storage account

1. Copy the following script.

```powershell
Azure PowerShellCopy  
Open Cloudshell  
connect-azaccount -usedeviceauthentication  
curl https://raw.githubusercontent.com/microsoft/Windows365-PSScripts/main/Windows%20365%20GCC/Grant%20Service%20Principal%20Roles%20in%20Tenant/Grant%20W365%20SP%20Roles%20In%20Tenant.ps1 -o GrantW365SProles.ps1 & ./GrantW365SProles.ps1
```

2. Paste the script into your Azure Government subscription's Cloud Shell session and run it.

#### If you don't have a Cloud Shell account that requires an Azure Storage account

1. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
2. Navigate to the **Windows 365 GCC** > **Grant Service Principal Roles in Tenant** folder.
3. Select **Grant W365 SP Roles in Tenant.ps1** > **Raw** > save the raw file to a location on your computer as a .ps1 file.  
4. Open Windows PowerShell 5.1 (x64) as an Administrator > run the PowerShell script.
5. Continue with the following section **Follow script instructions**.  

#### Follow script instructions

1. After running the script, at the prompt, select option **2**. This option sets up permissions for the ANC.
2. From the list of Azure Government subscriptions, select the subscription that you want to grant permissions to.
3. From the list of resource groups, select the resource group that you want to use.
4. Select your vNET.
5. The script grants permissions and lists what was configured.

## Map the commercial and government tenants

To connect the two tenants, the **AAD Tenant Mapping.ps1** PowerShell script must be run. This script is a prerequisite to give admins either or both of the following abilities:

- Upload custom images for use with Windows 365 Government Cloud PCs.
- Define Azure Network Connections so that the Windows 365 Government Cloud PCs can access on-premises or Microsoft-hosted resources.

1. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
2. Navigate to the **Windows 365 GCC** folder > **AAD Tenant Mapping** > select **AAD Tenant Mapping.ps1** > **Raw** > save the raw file to a location on your computer as a .ps1 file.
3. Open Windows PowerShell 5.1 (x64) as Administrator and run the PowerShell script. It downloads missing modules if needed.
    >[!NOTE]
    >If the script was previously run successfully, you'll see the error **HttpStatusCode Conflict**. This warning can be ignored to execute the script functions Add and Get.
4. In PowerShell 5.1, type **A** to add tenant mapping.
5. A web browser prompt opens.  Enter your **Azure Commercial** credentials (for example, GlobalAdmin@contoso.onmicrosoft.com). The window closes after successful authentication. 
6. A second web browser prompt opens, you're asked for your **Azure Commercial** credentials again, after that another prompt asks you to grant permissions.  Check the box **Consent on behalf of your organization** and then click on the **Accept** button. The window will then close.
7. A third browser prompt opens. Enter your **Azure Government** credentials (for example, GlobalAdmin@fabrikam.onmicrosoft.us). The window closes after successful authentication.
8. A fourth web browser prompt opens, you're asked for your **Azure Government** credentials again, after that another prompt asks you to grant permissions.  Check the box **Consent on behalf of your organization** and then click on the **Accept** button. The window will then close.
8. After the mapping completes, you'll see **Added tenant mapping successfully!**

## Common tenant mapping issues

If the mapping fails, try the following suggestions:

- **Wait at least 10 minutes and try again.** Permission changes must propagate before the mapping can complete.

- **Confirm there isn't an existing tenant mapping.** Only a 1:1 mapping of the Commercial and Government tenants is supported. Run the **AAD Tenant Mapping.ps1** script again and select the **Get** option.  Contact support by filing a support ticket in the Microsoft Intune admin center (intune.microsoft.com) > Tenant Administration > Help and support > Windows 365 via with the error details.

## Set permissions to upload custom images and/or connect to on-premises resources

If you're going to use Gallery images to provision Cloud PCs using the Microsoft-hosted network, no further configurations are required.  Stop here.

If you're going to upload custom images on the Microsoft-hosted network, keep reading.

When provisioning Windows 365 Cloud PCs without the Microsoft-hosted network, you must define an [Azure Network Connection](azure-network-connections.md) (ANC) that the Cloud PCs will use to connect with other resources, including your on-premises infrastructure. To set up the ANC, you need the existing values for the Azure Government:
    - Subscription ID.
    - Resource Group.
    - Virtual Network.

> [!NOTE]
> Tenant mapping must be successful before you proceed.

Copy the following script, then paste the command into your Azure Government subscription's CloudShell session for execution.  Next, go to the section **Script instructions**.

```azurepowershell-interactive
connect-azaccount -usedeviceauthentication
curl https://raw.githubusercontent.com/microsoft/Windows365-PSScripts/main/Windows%20365%20GCC/Grant%20Service%20Principal%20Roles%20in%20Tenant/Grant%20W365%20SP%20Roles%20In%20Tenant.ps1 -o GrantW365SProles.ps1 & ./GrantW365SProles.ps1
```

OR use the following instructions if you don't have a CloudShell account that requires an Azure Storage account.

1. Go to the [Windows 365 PowerShell GitHub repository](https://github.com/microsoft/Windows365-PSScripts).
2. Navigate to the **Windows 365 GCC** folder > **Grant Service Principal Roles in Tenant** folder > select **Grant W365 SP Roles in Tenant.ps1** > **Raw** > save the raw file to a location on your computer as a .ps1 file.
3. Open Windows PowerShell 5.1 (x64) as Administrator and run the PowerShell script and then go to the section **Script instructions**.

**Script instructions:**

1. At the prompt, type one of the following options to grant permissions:
    - **1** to only upload custom images. For Azure AD join infrastructures, you don't need to create an ANC just to upload custom images.
    - **2** to only create ANCs.
    - **3** to create ANCs and upload custom images. For hybrid Azure AD join infrastructures, creating an ANC is a requirement for uploading custom images.
        - The script lists the Azure Government subscriptions you have access to. Select the subscription that you want to grant permissions to.
        - The resource groups for that subscription are then listed. Select the group that you want to use.
        - Select your vNet.
2. The script grants the permissions and lists what was configured.


## Next steps

[Learn more about Windows 365 Government](introduction-windows-365-government.md).