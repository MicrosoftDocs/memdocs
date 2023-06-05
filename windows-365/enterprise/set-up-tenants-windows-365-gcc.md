---
# required metadata
title: Set up tenants for Windows 365 Government
titleSuffix:
description: Learn how to set up tenants for Windows 365 Government.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 06/08/2023
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

The fastest way to use Windows 365 is to use AADJ, gallery images and the Microsoft Hosted Network option. The instructions on this page are only if you must use either or both:

- **Custom images**. Windows 365 provides optimized gallery images, including [images with Microsoft 365 apps preinstalled](/windows-365/enterprise/device-images). After the gallery image is deployed, Intune can be used for further customization of [common settings](/mem/intune/configuration/settings-catalog-common-features) and [application deployment](/mem/intune/apps/apps-windows-10-app-deploy). If you must use your existing custom image, for more information, see [add a custom image](./add-device-images.md).
- **Azure Network Connections (ANC)**. ANCs let you provision Cloud PCs that are attached to a virtual network that you manage. Examples include:
    - Azure Virtual Network (VNet).
    - Azure VPN Gateway or a dedicated connection via ExpressRoute.
    - Other Azure Resources, including Cloud PC resources.
- For more information, see [create an Azure network connection](create-azure-network-connection.md).

For Government Community Cloud (GCC) customers only, the following instructions let Intune running in Azure Commercial to manage Cloud PCs running in Azure Government regions.

> [!NOTE]
> - You don't need an Azure Government subscription to use Windows 365 Government. These instructions are specifically for GCC, and only if Custom Images and/or Azure Network Connections are required.  The instructions on this page don't apply to GCC High.
> - For government customers that don't have an Azure Government subscription, or require integration with Azure Commercial, using consider Windows 365 Enterprise. Make sure this meets your compliance requirements. Window 365 Enterprise is FedRAMP compliant. See [Windows 365 Service Description](/office365/servicedescriptions/windows-365-service-description/windows-365-service-description)

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
- To meet [Licensing requirements](/windows-365/enterprise/requirements?tabs=government%2Cent#licensing-requirements).
- (If applicable) The following information to apply permissions to setup the Azure network connection. The virtual network and subnet must already exist.
    - Subscription ID.
    - Resource Group.
    - Virtual Network.
    - Subnet.

>[!NOTE]
> While the GCC users' Cloud PCs are hosted and secured in the Azure Government cloud, the endpoints for admins and end users are in the commercial Azure domain. Users will login to the Cloud PCs using credentials synched with Azure Commercial AAD.

## Azure AD options

If you want to use Azure AD join or hybrid Azure AD join, consider these preparations:

**Azure AD joined Cloud PCs**: If you want to use an Azure AD join infrastructure and your own network, you need a tenant and Azure subscription in the Azure Government cloud. The tenant in the Azure commercial .com domain must be mapped to the tenant in the Azure Government (.us) domain.

**Hybrid Azure AD joined Cloud PCs**: If you want to use a hybrid Azure AD join infrastructure, you must configure your commercial (.com) tenant and your government (.us) tenants before creating your Azure Virtual Networks.

## Get started with the Windows 365 GCC Setup Tool

Follow these steps to configure tenant mapping using the Windows 365 GCC Setup Tool.

1. Launch the GCCSetupTool.exe. This tool is available at https://aka.ms/gccsetuptool.
2. On the **Let's get you started** page, select **Next**.
3. Sign in with your Azure Commercial account. This account must have Global Administrator permissions.
4. Confirm that you want to continue with your commercial account > **Next**.
5. Sign in with your Azure Government account > **Next** > type your credentials.
6. Confirm that you want to continue with your government account > **Next**.
7. On the **Select feature to enable screen** make sure **Custom Images** is selected. This option is selected by default because there is no reason to run the Windows 365 GCC Setup Tool unless you need at least one of these features below.
    > [!NOTE]
    > ANC includes the permissions for custom images.
8. Select **Azure network connections** and then select the **Subscription**, **Virtual network**, and **Subnet** that you want to configure. Select **Next**.
9. On the **Review settings** page, review the selections you made and select **Grant**.
10. After setup is complete, you can close the tool.

### Troubleshooting

If you have issues running the Windows 365 GCC Setup Tool:

1. In the same folder where the GCCSetupTool.exe is run, navigate to the **Log** folder and review the `GCCAdminTool.log` file.
2. If you continue to have issues, [contact support](/mem/get-support#contact-support) and provide the GCCADminTool.log file.

### Subsequent use of the GCC Setup Tool

The Windows 365 GCC Setup Tool can be run again after the initial setup. You might want to use the GCC Setup Tool again if you:

- Didn't setup ANCs before, or
- Want to expand the use of ANCs to other networks.

#### Script alternative

As an alternative to using the GCC Setup Tool for setting up ANC, you can also use the following script to set up permissions for more ANCs.

> [!NOTE]
> Tenant mapping must be successful before you proceed with the script to set up ANCs.

```azurepowershell-interactive
connect-azaccount -usedeviceauthentication
curl https://raw.githubusercontent.com/microsoft/Windows365-PSScripts/main/Windows%20365%20GCC/Grant%20Service%20Principal%20Roles%20in%20Tenant/Grant%20W365%20SP%20Roles%20In%20Tenant.ps1 -o GrantW365SProles.ps1 & ./GrantW365SProles.ps1
```

1. If you don't have Cloud Shell set up (an Azure Storage account required), you have two options to run the script:
    - Select **Copy** on the script, and run the PowerShell script locally on your computer. 
    - Select **Open Cloudshell** > paste the script into your Azure Government subscription's Cloud Shell session > run the script.
2. After running the script, at the prompt, select option **2**. This option sets up permissions for the ANC.
3. From the list of Azure Government subscriptions, select the subscription that you want to grant permissions to.
4. From the list of resource groups, select the resource group that you want to use.
5. Select your vNET.
6. The script grants permissions and lists what was configured.

## Next steps

[Learn more about Windows 365 Government](introduction-windows-365-government.md).
