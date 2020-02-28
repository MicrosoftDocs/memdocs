---
# required metadata

title: Remove SCEP or PKCS certificates in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Administrators can use the wipe or retire action to remove certificates from Microsoft Intune. There are some scenarios where the certificates are automatically removed, such as unenrolling a device or removing a compliance policy. There are some scenarios where certificates automatically remain on the device, such as when the Intune license is lost or removed. See the different ways for Android, Android Enterprise, iOS, macOS, and Windows devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: lacranda
---

# Remove SCEP and PKCS certificates in Microsoft Intune

In Microsoft Intune, you can use Simple Certificate Enrollment Protocol (SCEP) and Public Key Cryptography Standards (PKCS) certificate profiles to add certificates to devices.

These certificates can be removed when you [wipe](../remote-actions/devices-wipe.md#wipe) or [retire](../remote-actions/devices-wipe.md#retire) the device. There are also scenarios where certificates are automatically removed, and scenarios where certificates stay on the device. This article lists some common scenarios, and the impact on PKCS and SCEP certificates.

> [!NOTE]
> To remove and revoke certificates for a user who's being removed from on-premises Active Directory or Azure Active Directory (Azure AD), follow these steps in order:
>
> 1. Wipe or retire the user's device.
> 2. Remove the user from on-premises Active Directory or Azure AD.

## Manually deleted certificates

Manual deletion of a certificate is a scenario that applies across platforms and certificates provisioned by SCEP or PKCS certificate profiles. For example, a user might delete a certificate from a device, when the device remains targeted by a certificate policy.

In this scenario, after the certificate is deleted, the next time the device checks in with Intune it's found to be out of compliance as it is missing the expected certificate. Intune then issues a new certificate to restore the device to compliance. No additional action is needed to restore the certificate.

## Windows devices

### SCEP certificates

A SCEP certificate is revoked *and* removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.
- The device is removed from an Azure AD group.
- A certificate profile is removed from the group assignment.

A SCEP certificate is revoked when:

- An administrator changes or updates the SCEP profile.

A root certificate is removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

SCEP certificates *stay* on the device (certificates aren't revoked or removed) when:

- A user loses the Intune license.
- An administrator withdraws the Intune license.
- An administrator removes the user or group from Azure AD.

### PKCS certificates

A PKCS certificate is revoked *and* removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

A root certificate is removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

PKCS certificates *stay* on the device (certificates aren't revoked or removed) when:

- A user loses the Intune license.
- An administrator withdraws the Intune license.
- An administrator removes the user or group from Azure AD.
- An administrator changes or updates the PKCS profile.
- A certificate profile is removed from the group assignment.


## iOS devices

### SCEP certificates

A SCEP certificate is revoked *and* removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.
- The device is removed from the Azure AD group.
- A certificate profile is removed from the group assignment.

A SCEP certificate is revoked when:

- An administrator changes or updates the SCEP profile.

A root certificate is removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

SCEP certificates *stay* on the device (certificates aren't revoked or removed) when:

- A user loses the Intune license.
- An administrator withdraws the Intune license.
- An administrator removes the user or group from Azure AD.

### PKCS certificates

A PKCS certificate is revoked *and* removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

A PKCS certificate is removed when:

- A certificate profile is removed from the group assignment.

A root certificate is removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

PKCS certificates *stay* on the device (certificates aren't revoked or removed) when:

- A user loses the Intune license.
- An administrator withdraws the Intune license.
- An administrator removes the user or group from Azure AD.
- An administrator changes or updates the PKCS profile.

## Android KNOX devices

### SCEP certificates

A SCEP certificate is revoked *and* removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.

A SCEP certificate is revoked when:

- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.
- The device is removed from an Azure AD group.
- A certificate profile is removed from the group assignment.
- An administrator removes the user or group from Azure AD.
- An administrator changes or updates the SCEP profile.

A root certificate is removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

SCEP certificates *stay* on the device (certificates aren't revoked or removed) when:

- A user loses the Intune license.
- An administrator withdraws the Intune license.
- An administrator removes the user or group from Azure AD.

### PKCS certificates

A PKCS certificate is revoked *and* removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

A root certificate is removed when:

- A user unenrolls.
- An administrator runs the [wipe](../remote-actions/devices-wipe.md#wipe) action.
- An administrator runs the [retire](../remote-actions/devices-wipe.md#retire) action.

PKCS certificates *stay* on the device (certificates aren't revoked or removed) when:
- A user loses the Intune license.

- An administrator withdraws the Intune license.
- An administrator removes the user or group from Azure AD.
- An administrator changes or updates the PKCS profile.
- A certificate profile is removed from the group assignment.


> [!NOTE]
> Android for Work devices are not validated for the preceding scenarios.
> Android legacy devices (any non-Samsung, non-work profile devices) are not enabled for certificate removal.

## macOS certificates

### SCEP certificates

A SCEP certificate is revoked *and* removed when:

- A user unenrolls.
- An administrator runs a [retire](../remote-actions/devices-wipe.md#retire) action.
- The device is removed from an Azure AD group.
- A certificate profile is removed from the group assignment.

A SCEP certificate is revoked when:

- An administrator changes or updates the SCEP profile.

SCEP certificates *stay* on the device (certificates aren't revoked or removed) when:

- A user loses the Intune license.
- An administrator withdraws the Intune license.
- An administrator removes the user or group from Azure AD.

> [!NOTE]
> Using the [wipe](../remote-actions/devices-wipe.md#wipe) action to factory reset macOS devices is not supported.

### PKCS certificates

PKCS certificates aren't supported on macOS.

## Next steps

[Use certificates for authentication](certificates-configure.md)