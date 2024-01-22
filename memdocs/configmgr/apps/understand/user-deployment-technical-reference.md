---
title: App deployment to users technical reference
titleSuffix: Configuration Manager
description: Troubleshooting application deployments to users technical reference for Configuration Manager.
ms.date: 11/04/2019
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: troubleshooting
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Application Deployment Policy for Users

*Applies to: Configuration Manager (current branch)*

When an application is deployed to a User collection, the policy for the deployment is created for Required deployments only. For Available deployments, the policy is created when the user attempts to install the application from the Software Center. This article will explain the deployment process for Required as well as Available deployments.

> [!TIP]
> All the information necessary to review the client logs can be obtained by running the SQL query referenced in the [Before you begin](app-deployment-technical-reference.md#before-you-begin) section.

## Required Deployments

The policy for a required application deployment to a User collection is targeted to all the users in the collection when the deployment is created. Client-side processing for these deployments is similar to a required deployment to a Device collection. Deployment activation occurs at the defined Available Time, and enforcement occurs at the defined Deadline time. For more information, see [Application Deployment to Device Collections](device-deployment-technical-reference.md).

## Available Deployments

Applications that are deployed to a user collection as Available behave differently. This behavior change allows the Administrator to make applications available to the users without causing resource contention for policy. When a user launches the Software Center, a list of applications that are available for the user is queried from the Management Point in real time. This request is made to the `CMUserService_WindowsAuth` virtual directory on the Management Point and can be seen in the **SCClient_[UserName].log** on the client.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

When the Management Point receives this request, it queries the list of applications available to the user by executing `usp_GetApplicationPropertyValuesFiltered` stored procedure. This activity can be tracked in the **UserService.log** on the Management Point.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

Software Center receives the list and displays the applications that the user can install. When the user clicks on the application, additional information about the application is queried from the Management Point, which involves execution of stored procedures such as usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence, usp_GetDeploymentTypeForAnApp, etc.

The deployment is activated when the user selects the application and clicks on the **Install** button, and a DCM Agent Job is created to evaluate the application. If the application is applicable, another DCM Agent Job is created to download and enforce the application. This activity can be tracked in the **DCMAgent.log** on the client.

## Next Steps

- [Understanding application deployment client components](client-components-technical-reference.md)
