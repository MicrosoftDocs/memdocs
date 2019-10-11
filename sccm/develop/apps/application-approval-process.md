---
title: "Application approval process"
titleSuffix: "Configuration Manager"
ms.date: "10/15/2019"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e32671bd-3036-4c87-9371-f56b8d2eb57b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Application approval process

One of the important scenarios for application management is providing a controlled installation and uninstallation process for software that requires approval. To reduce the overall load on the Configuration Manager infrastructure and improve performance, the workflow doesn’t require creating individual collections to manage installations and uninstallations for each application.

## Scenario 1: Applications must be approved before they're installed

The IT administrator at Contoso uses Software Center to make software available to the users. These applications must be approved before they're installed. The admin deploys an application to all users and configures it to require approval.

The user browses the list of applications in Software Center but can’t install the application until the request is approved. The user submits the request from Software Center and specifies the reason for the request. If the option, **Approve application requests for users per device** is enabled, the user has to request approval from every device where they want to install the application. The admin then approves or denies the request for each of the user's devices where requests were made.

> [!Note]  
> Configuration Manager doesn't enable this feature by default. Before using it, enable the optional feature **Approve application requests for users per device**. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).


Software Center requires the user to submit the request for the application from their device. The user sees this in Software Center:

:::image type="content" source="media/user-requests-approval-software-center.png" alt-text="User requests application that needs approval from Software Center":::

The user specifies why they want the application and submits the approval request:

:::image type="content" source="media/user-request-submitted-software-center.png" alt-text="User notified that their approval request was submitted in Software Center":::

Once the admin approves the request, the user can install the application on their device. If the user takes no action, the application is automatically installed for the user during non-business hours.

:::image type="content" source="media/users-request-approved-software-center.png" alt-text="User installing approved application from Software Center":::

## Scenario 2: Integrate an application approval system 

The Northwind Traders has an existing application approval system, and the admin wants to integrate the approval system with Configuration Manager.

The admin deploys an application to all users and configures it to require approval. Then, the admin enables the Software Center client setting to **Hide unapproved applications in Software Center**.

:::image type="content" source="media/admin-hides-unapproved-applications.png" alt-text="Hide unapproved applications Software Center option":::

With this option, the user doesn’t see the application in Software Center until the application request is approved for installation on the device. When approval is granted via the organization’s approval system, the orchestration system can make an approved request for the user and their device in Configuration Manager. The orchestration systems used the `CreateApprovedRequest` WMI method in Configuration Manager. This method then uses the existing Configuration Manager application deployment mechanism. It doesn’t modify collection memberships, and it takes effect immediately. The application is now available to the user in Software Center.

The admin can also configure the automation to automatically install the application on the user’s device. No other users will see the application as available in Software Center until the approval is granted. This solution provides per-user and per-device control of the software without the need to create separate collections.

The WMI method `CreateApprovedRequest` in the `SMS_UserApplicationRequest` class has the following input parameters:

### Required parameters

- `ClientGUID` - Unique identifier of the client
- `Username` - Unique username of the user
- `ApplicationID` - Model name of the application

The ApplicationID is the ModelName property of the SMS_Application instance. This value is the unique ID of the application without the version. For example, `ScopeId_21A9ED3B-D8C6-49DC-87A6-01F296182F14/Application_40243740-01f2-48db-abf0-c95259986d94`. 

### Optional parameters

- `Comments` - Comments for the approved request to be displayed in the Software Center. By default, it specifies an empty string.
- `AutoInstall` - Install the application immediately after the request is approved. By default, this parameter is true.

The following code sample is a Windows PowerShell script that shows how to invoke the WMI method for a specific user, machine, and application:

```powershell
$machinename = $args[0]
$username = $args[1]
$appid = $args[2]
$autoInstall = $args[3]
$comments = $args[4]

$scObj=Get-WmiObject -Namespace root\sms -Query 'select SiteCode from sms_providerlocation'
$sitecode = $scObj.SiteCode
$namespace ="root\sms\site_" + $sitecode
$machine = Get-WmiObject -Namespace $namespace -Query "SELECT * FROM SMS_R_SYSTEM WHERE Name = '$machinename'"
$clientGuid = $machine.SMSUniqueIdentifier
Invoke-WmiMethod -Path "SMS_UserApplicationRequest" -Namespace $namespace -Name CreateApprovedRequest -ArgumentList @($appid, $autoInstall, $clientGuid, $comments, $username)
```

The following command line is an example to run this sample script:

```powershell
.\CreateApprovedRequest.ps1 "MachineName" "Domain\User" "ScopeId_2E4DAE44-C9A0-4694-8B7A-474424C080D4/Application_88808a3a-86e4-4820-be59-aa7d61cb8c33 "true" "Application has been approved"
```

The admin can still see the approved requests in the Configuration Manager console from **Software Library** > **Application Management** > **Approval Requests**.

:::image type="content" source="media/approval-requests-console.png" alt-text="Application requests node in the Configuration Manager console":::

### Limitations

The current version of this application approval WMI method has the following limitations:

1. The `CreateApprovedRequest` method can be called only once for a unique machine ID, application ID, and username combination. It returns an error if the method is called with the same parameters more than once. The details about this error are in `SMSProv.log`.
1. To enable the automatic install of the application, deploy the application to a collection of users or user groups before calling the WMI method. If you create the deployment after calling the WMI method, the application is made available to the user for install and won’t be automatically installed.

## Scenario 3: Revoke application approval

If the admin revokes the approval, or the application is no longer in use, uninstall the application.

The admin revokes the approval of the application using the Configuration Manager console, a PowerShell script, or WMI. Even if the application was already approved, the admin can use the Deny option. Revoking the approval prevents the user from installing the application on their device. The same action also causes uninstallation of the application on the user's device if the application was previously installed.

Learn more about the [Deny-CMApprovalRequest](https://docs.microsoft.com/powershell/module/configurationmanager/Deny-CMApprovalRequest) cmdlet.

### Prerequisites

1. Set the [Select these new settings to specify company information](/sccm/core/clients/deploy/about-client-settings#software-center) client setting to **Yes**.
1. Enable the optional feature **Approve application requests for users per device**. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).


## Scenario 4: Machine-based pre-approved requests

 You can use the `CreateApprovedRequest` API to create a pre-approved request for a device with no user required. This allows you to install and uninstall applications in real time.  Currently this functionality is only available in the SDK. For machine-based pre-approved requests to work, you must also enable the optional feature **Approve application requests for users per device**. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

Administrators can create a machine-available deployment that requires approval using the [New-CMApplicationDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmapplicationdeployment) cmdlet. Here’s an example:

```powershell
New-CMApplicationDeployment -CollectionName “All Systems” -Name “Test app” -DeployAction Install -DeployPurpose Available -ApprovalRequired $true -DistributionPointName 'DistributionPoint.domain.com" -DistributeContent
```

A deployment created with the `requires approval` flag set to `true` stays on the server and can be used with larger collections. The user-request flow isn't yet available for machine-targeted deployments that require approval. So, the application isn’t visible in Software Center until you create a pre-approved request to the individual device.

The following Windows PowerShell sample script shows how to invoke the WMI method for a machine and application to create a pre-approved request:

```powershell
$machinename = $args[0]
$appid = $args[1]
$autoInstall = $args[2]
$comments = $args[3]

$scObj=Get-WmiObject -Namespace root\sms -Query 'select SiteCode from sms_providerlocation'
$sitecode = $scObj.SiteCode
$namespace ="root\sms\site_" + $sitecode
$machine = Get-WmiObject -Namespace $namespace -Query "SELECT * FROM SMS_R_SYSTEM WHERE Name = '$machinename'"
$clientGuid = $machine.SMSUniqueIdentifier
Invoke-WmiMethod -Path "SMS_ApplicationRequest" -Namespace $namespace -Name CreateApprovedRequest -ArgumentList @($appid, $autoInstall, $clientGuid, $comments)
```

The following command line is an example to run this sample script:

```powershell
.\CreateApprovedRequestForMachine.ps1 "MachineName.domain.com" "ScopeId_2E4DAE44-C9A0-4694-8B7A-474424C080D4/Application_88808a3a-86e4-4820-be59-aa7d61cb8c33 "true" "Application has been approved"
```

Setting the `autoInstall` parameter to `false` has no effect in Configuration Manger for machine-based pre-approved request. As soon as the pre-approved request is created on the site, the device will attempt to install the application. You can deny the approval request to remove the application from the device.
