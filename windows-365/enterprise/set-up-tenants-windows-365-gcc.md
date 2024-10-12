---
# required metadata
title: Set up tenants for Windows 365 Government
titleSuffix:
description: Learn how to set up tenants for Windows 365 Government.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/11/2023
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
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

For Government Community Cloud (GCC) customers only, the following instructions let Intune running in Azure to manage Cloud PCs running in Azure Government regions.

> [!NOTE]
> - You don't need an Azure Government subscription to use Windows 365 Government. These instructions are specifically for GCC, and only if Custom Images and/or Azure Network Connections are required.  The instructions on this page don't apply to GCC High.
> - For government customers that don't have an Azure Government subscription, or require integration with Azure, consider using Windows 365 Enterprise. Make sure this meets your compliance requirements. Windows 365 Enterprise is FedRAMP compliant. See [Windows 365 Service Description](/office365/servicedescriptions/windows-365-service-description/windows-365-service-description)

## Before you begin
For both tenant mapping and granting permissions for custom images and/or connecting to your own networks, you need:

- An Azure Government subscription.
- Credentials of a user that has:
    - *Global Administrator* role in your Azure tenant (ending in onmicrosoft.com).
- Credentials of a user that has:
    - *Owner* role in your Azure Government subscription, AND
    - *Global Administrator* role in your Azure Government tenant (ending in onmicrosoft.us).
- To meet [Licensing requirements](/windows-365/enterprise/requirements?tabs=government%2Cent#licensing-requirements).
- (If applicable) The following information to apply permissions to set up the Azure network connection. The virtual network and subnet must already exist.
    - Subscription ID.
    - Resource Group.
    - Virtual Network.
    - Subnet.

>[!NOTE]
> While the GCC users' Cloud PCs are hosted and secured in the Azure Government cloud, the endpoints for admins and end users are in the commercial Azure domain. Users will login to the Cloud PCs using credentials synched with Microsoft Entra ID.

<a name='azure-ad-options'></a>

## Microsoft Entra options

If you want to use Microsoft Entra join or Microsoft Entra hybrid join, consider these preparations:

**Microsoft Entra joined Cloud PCs**: If you want to use a Microsoft Entra join infrastructure and your own network, you need a tenant and Azure subscription in the Azure Government cloud. The tenant in the Azure .com domain must be mapped to the tenant in the Azure Government (.us) domain.

**Hybrid Microsoft Entra joined Cloud PCs**: If you want to use a Microsoft Entra hybrid join infrastructure, you must configure your commercial (.com) tenant and your government (.us) tenants before creating your Azure Virtual Networks.

## Preparing for Windows 365 GCC Setup Tool

For the Windows 365 GCC Setup Tool to complete tenant mapping, the Windows 365 Microsoft Entra application must be given permission to access your Azure Government AD tenant through a service principal. The service principal object defines what the app can do in the tenant, who can access the app, and what resources the app can access. Before running the Windows 365 GCC Setup Tool the first time, you must do the following:

1. If not already completed, install the Azure CLI on the computer where you will be creating the service principal. For more information, see [How to install the Azure CLI](/cli/azure/install-azure-cli).
2. Sign into your Azure Government AD tenant by using the Azure CLI steps defined in [Sign in with Azure CLI](/cli/azure/authenticate-azure-cli). Global Administrator permissions are required to create the service principal for Windows App.
3. For more information about working with service principals in Azure, see [Work with Azure service principal using the Azure CLI](/cli/azure/azure-cli-sp-tutorial-1). Grant the Windows 365 Microsoft Entra app permissions to your tenant by running the following PowerShell command: ```az ad sp create --id 0af06dc6-e4b5-4f28-818e-e78e62d137a5```.
4. After the command completes successfully, you should be able to view details about the service principal by running the following PowerShell command: ```az ad sp show --id 0af06dc6-e4b5-4f28-818e-e78e62d137a5```. You should see Windows App listed in the **All Applications** view in the Enterprise application blade in Azure portal.

The Windows App service principal can only access Azure resources necessary to configure custom image and Azure Network Connection (ANC) support in Windows 365. After it's created, the service principal can only be deleted when custom images, ANC objects and corresponding Cloud PCs using them have been deprovisioned. Otherwise, Cloud PC provisioning tasks may fail, and existing Cloud PCs may become inaccessible.

## Get started with the Windows 365 GCC Setup Tool

Follow these steps to configure tenant mapping using the Windows 365 GCC Setup Tool.

1. Launch the GCCSetupTool.exe. This tool is available at https://aka.ms/gccsetuptool.
2. On the **Let's get you started** page, select **Next**.
3. Sign in with your Azure account. This account must have Global Administrator permissions.
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

- Didn't set up ANCs before, or
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
