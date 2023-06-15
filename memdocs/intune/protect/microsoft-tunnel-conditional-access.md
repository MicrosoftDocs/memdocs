---
title: Use Microsoft Tunnel VPN gateway with Conditional Access policies
description: Configure your Azure tenant to support using Conditional Access policies to grant access to the Intune Microsoft Tunnel VPN gateway solution.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/31/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use Conditional Access with Microsoft Tunnel in Intune

If your Microsoft Intune environment uses both Azure Active Directory (AD) and Conditional Access, you can use Conditional Access policies to gate device access to your Microsoft Tunnel VPN gateway.

To support integration of Conditional Access and Microsoft Tunnel, you’ll use Azure AD PowerShell to enable your tenant to support Microsoft Tunnel. After enabling your tenant to support Microsoft Tunnel, you can then create Conditional Access policies that apply to the Microsoft Tunnel app.

## Provision your tenant

Before you can configure Conditional Access policies for the tunnel, you must enable your tenant to support Microsoft Tunnel for Conditional Access. Use the Azure Active Directory PowerShell module and run a PowerShell script to modify your tenant to add **Microsoft Tunnel Gateway** as a cloud app.  After the tunnel is added as a cloud app, you can select it as part of a Conditional Access policy.

1. [Download and install](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0&preserve-view=true) the **AzureAD PowerShell module**.

2. Download the PowerShell script named **mst-ca-provisioning.ps1** from aka.ms/mst-ca-provisioning.

3. Using credentials that have the Azure Role permissions [equivalent to **Global Administrator**](/azure/active-directory/roles/permissions-reference#global-administrator), run the script from any location in your environment, to provision your tenant.

   The script modifies your tenant by creating a service principal with the following details:

   - App ID: 3678c9e9-9681-447a-974d-d19f668fcd88
   - Name: Microsoft Tunnel Gateway

   The addition of this service principal is required so you can select the tunnel cloud app while configuring Conditional Access policies. It's also possible to use Graph to add the service principal information to your tenant.

4. After the script completes, you can use your normal process to create Conditional Access policies.

## Conditional Access to limit access to Microsoft Tunnel

If you'll use Conditional Access policy to limit user access, we recommend configuring this policy after you provision your tenant to support the Microsoft Tunnel Gateway cloud app, but before you install the Tunnel Gateway.

1. Sign in to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Endpoint Security** > **Conditional access** > **New policy**.

2. Specify a name for this policy.

3. To configure user and group access, below *Assignments*, select **Users and groups**.

   1. Select **Include** > **All users**.
   2. Next, select **Exclude** and configure the groups you want to *grant access to*, and then save the user and Group configuration.

4. Under **Cloud apps or actions** > **Select apps**, select the **Microsoft Tunnel Gateway app**.

5. Below *Access controls*, select **Grant**, select **Block access**, and then save the configuration.

6. Set **Enable policy** to **On**.

7. Select **Create**.

For more information about creating policies for Conditional Access, see [Create a device-based Conditional Access policy](../protect/create-conditional-access-intune.md).

## Next steps

[Monitor Microsoft Tunnel](microsoft-tunnel-monitor.md)
