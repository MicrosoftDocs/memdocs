---
title: Avoid policy conflicts
description: Learn how to avoid policy conflicts when creating and deploying new policies.
ms.date: 7/11/2024
ms.topic: tutorial
ms.author: scbree
author: scottbreenmsft
ms.service: microsoft-intune
ms.subservice: education
---

# Avoiding policy conflicts

✅ Ensure policies apply effectively to devices

Devices and users targeted with the same setting from different policies cause conflicts. When conflicts occur, Intune generates an error and doesn't apply either setting. As a result, it's important to avoid or resolve conflicts to ensure the correct configuration is applied. Use the steps in this document when creating new policies to avoid or resolve policy conflicts.

> [!NOTE]
> If you only use Intune for Education to manage your devices, you can easily update the settings or apps that you have deployed to existing groups or create new groups to apply new policies or apps. You don't need to do anything extra to prevent conflicts if the members of the new groups are different from the members of the existing groups.

## 1. Determine which users or devices need the new policy

Review the existing Microsoft Entra ID groups and determine if they're applicable for the new policy. Otherwise, create a new group and add users or devices.

## 2. Identify and review potentials sources of conflict

The key to avoiding policy conflicts is to understand if existing policies targeted at the same set of users or devices contain the same settings. If a new policy has settings that overlap with existing ones for the same users or devices, either exclude those users or devices from the old policies or remove the overlapping settings.

You can exclude groups of devices or users using the "exclude group" option or by excluding devices using [filters](/mem/intune-service/fundamentals/filters).

> [!TIP]
> For more information about grouping and targeting, see [Plan Education device grouping and targeting](plan-grouping.md).

### Default policies for Education tenants

When Intune licenses are added to an Education tenant for the first time, a set of default policies are created. These policies can be viewed in the Configuration policies list in the Intune admin center. They should be reviewed for overlapping settings to determine if exclusions are required when targeting the same set of users or devices. By default, these policies are targeted to *All Devices*.

Default policy names:

- **Devices** – **Windows** – **Configuration**
  - Default Policies for EDU
  - Default Admx policy for EDU
  - Edition Upgrade
  - Shared PC Policy
- **Devices** – **Windows** – **Windows 10 and later updates** – **Update rings**
  - Windows Update Policy

> [!NOTE]
> If you're using Intune for Education, you can see and change these settings by navigating to **Groups** and then selecting the group **All Devices** or **All Users** – **Settings**. Select **Windows device settings** or **iOS device settings**.

### Policies created in the Intune for Education console

When you configure settings in Intune for Education, corresponding policies are created in the Intune service that can be viewed and edited from the Intune admin console. Configuration profiles created by Intune for Education have a recognizable naming template that always starts with the name of the group followed by a suffix based on the template type. The *\<GROUP NAME>* part of each name represents the group that was selected in Intune for Education when the settings were configured.

This list provides examples of configuration profiles created by Intune for Education. They should be reviewed for overlapping settings to determine if exclusions are required when targeting the same set of users or devices.

- **Devices** – **Windows** – **Configuration**
  - *\<GROUP NAME>* Windows10General
  - *\<GROUP NAME>* GroupPolicyConfiguration
  - *\<GROUP NAME>* Windows10EndpointProtection
  - *\<GROUP NAME>* Windows10CustomDenyAdministrativeApps
  - *\<GROUP NAME>* Windows10CustomDenyStore
  - *\<GROUP NAME>* Windows10SharedPC
  - *\<GROUP NAME>* Windows10EnterpriseModernAppManagement
  - *\<GROUP NAME>* ConfigurationPolicy
- **Devices** – **Windows** – **Enrollment** – **Windows Autopilot/Deployment Profiles**
  - *\<GROUP NAME>* Windows10AutopilotProfile
- **Devices** – **Windows** – **Windows 10 and later updates** – **Update rings**
  - *\<GROUP NAME>* Windows10UpdatesForBusiness
- **Devices** – **Windows** – **Windows 10 and later updates** – **Feature Updates**
  - *\<GROUP NAME>* WindowsFeatureUpdates
- **Endpoint security** – **Account protection**
  - *\<GROUP NAME>*_LocalUsersAndGroupsConfig_EDU

## 3. Assign the policy to target group

Once all the potential sources of conflict are reviewed and any exclusions are configured, you can assign the new policy to the user or device groups. Assign the policy using "Included groups" and optionally use assignment filters.

## 4. Monitoring for policy conflicts

### [:::image type="icon" source="../../../media/icons/intune.svg"::: Intune](#tab/intune)

You can check for potential policy conflicts by going to **Devices** – **Monitor** – **Configuration policy assignment failure**. Find the new policy and review any conflicts in the report. The report can also be exported to CSV.

### [:::image type="icon" source="../../../media/icons/intune.svg"::: Intune for Education](#tab/intune-for-education)

You can check for potential policy conflicts by going to **Reports** – **Settings error**.

---

If a conflict is found, remove the overlapping settings from the new policy or exclude the targeted users or devices from existing policies.
