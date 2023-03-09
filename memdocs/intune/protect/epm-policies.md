---
title: Configure policies to manage Endpoint Privilege Management with Microsoft Intune
description: Configure policies that define how Endpoint Privilege Management functions in your tenant, and behaviors when elevating files to run in administrative context.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mattcall
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
---

# Configure policies for Endpoint Privilege Management

Configuration of policies for Endpoint Privilege Management includes the following objects:

- Windows elevation settings policy
- Windows elevation rules policy
- Reusable settings groups, which are optional configurations for your elevation rules.

## Windows elevation settings policy

Deploy a Windows elevation settings policy to users or devices to configure the following on devices:

- Enable Endpoint Privilege Management on the device.
- Set default rules for elevation requests for any file that’s not managed by an Endpoint Privilege Management elevation rule policy on that device.
- Configure what information elevation requests and activity are reported back to Intune.

To create the policy:

## Windows elevation rules policy

Deploy a Windows elevation rules policy to users or devices to deploy one or more rules for files that are managed for elevation by Endpoint Privilege Management. Each rule you add to this policy:

- Identifies a file tor which you manage elevation requests.
- Can include a certificate to help validate that file’s integrity before it’s run. You can also add a reusable group that contains a certificate that you then use with one or more rules or policies.
- Specifies if the elevation  type of the file as automatic (silently) or requiring user confirmation. With user confirmation, you can add additional user actions that must be completed before the file is run.
In addition to this policy, a device must also be assigned a Windows elevation settings policy that enables Endpoint Privilege Management.

To create the policy:

## Reusable settings groups

Endpoint Privilege Management uses reusable settings groups to manage the certificates that validate the files you manage with Endpoint Privilege Management elevation rules. Like all reusable settings groups for Intune, changes to a reusable group are automatically passed to the policies that reference the group.  For Endpoint Privilege Management, this means if you must update the certificate you use for file validation, you would only need to update it in the reusable settings group a single time to have that updated certificate applied to all your elevation rules that use that group.

To create the reusable settings group for Endpoint Privilege Management:

1. Sign  in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Reusable settings (preview)** tab >  and then select **Add**.

2. On **Basics**, enter the following properties:
   - **Name**: Enter a descriptive name for the reusable group. Name groups so you can easily identify each later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. In **Configuration settings**, select the folder icon for *Certificate file*, and browse to a **.CER** file to add it to this reusable group. The *Base 64 value* field fills in based on the certificate selected.

4. In **Review + create**, review your settings and select **Add**. When you select *Add*, your configuration is saved, and group is then shown in the reusable settings group list for Endpoint Privilege Management.


## Next steps
[Use reports for Endpoint Privilege Management](../protect/epm-reports.md)