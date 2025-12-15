---
author: scbree
ms.topic: include
ms.date: 07/31/2025
ms.author: scbree
---
1. Click *Try it* to open Graph Explorer.
1. Once Graph Explorer is open, select the :::image type="icon" source="../media/icons/user.svg"::: user icon in the top right to sign-in and sign in with your Intune administrator organizational account.
1. Click **Run query** to create the policy in your tenant.
   > [!TIP]
   > If it's the first time using Graph Explorer, you may need to authorize the application to access your tenant or to modify the existing permissions. This graph call requires *DeviceManagementConfiguration.ReadWrite.All* permissions. You can grant the required permissions by selecting **modify permissions** and then selecting **Consent**.

1. The policy is created in your tenant and can be edited to meet your requirements before assigning to groups.

> [!NOTE]
> As of July 31 2025, Microsoft Graph replaced use of the *DeviceManagementConfiguration.ReadWrite.All* permission with *DeviceManagementScripts.ReadWrite.All* for the following API calls:
> - ~/deviceManagement/deviceShellScripts
> - ~/deviceManagement/deviceHealthScripts
> - ~/deviceManagement/deviceComplianceScripts
> - ~/deviceManagement/deviceCustomAttributeShellScripts
> - ~/deviceManagement/deviceManagementScripts 

