---
title: Windows Autopilot customer consent
description: Learn how a cloud service provider (CSP) partner or an OEM can get customer authorization to register Windows Autopilot devices on the customer's behalf.
ms.subservice: autopilot
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/28/2024
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: reference
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---


# Windows Autopilot customer consent

This article describes how a cloud service provider (CSP) partner (direct bill, indirect provider, or indirect reseller) or an OEM can get customer authorization to register Windows Autopilot devices on the customer's behalf.

## CSP authorization

CSP partners can get customer authorization to register Windows Autopilot devices on the customer's behalf per the following restrictions:

| **Method** | **Description** |
|--------|-------------|
| **Direct CSP** | Gets direct authorization from the customer to register devices. |
| **Indirect CSP Provider** | Gets implicit permission to register devices through the relationship their CSP Reseller partner has with the customer. Indirect CSP Providers register devices through Microsoft Partner Center. |
| **Indirect CSP Reseller** | Gets direct authorization from the customer to register devices. At the same time, their indirect CSP Provider partner also gets authorization, which means that either the Indirect Provider or the Indirect Reseller can register devices for the customer. However, the Indirect CSP Reseller must register devices through the Microsoft Partner Center UI (manually uploading CSV file). The Indirect CSP Provider can register devices using the Microsoft Partner Center APIs. |

### Steps

For a CSP to register Windows Autopilot devices for a customer, the customer must first grant that CSP partner permission using the following process:

1. CSP sends link to customer requesting authorization/consent to register/manage devices on their behalf. To do so:

    1. CSP logs into Microsoft Partner Center.

    1. Select **Dashboard** on the top menu.

    1. Select **Customer** on the side menu.

    1. Select the **Request a reseller relationship** link:

        :::image type="content" source="images/csp1.png" alt-text="Request a reseller relationship.":::

    1. Select the checkbox indicating if delegated admin rights are desired:

        :::image type="content" source="images/csp2.png" alt-text="Delegated rights.":::

        > [!NOTE]
        >
        > Depending on the partner, they might request Delegated Admin Permissions (DAP) when requesting this consent. If possible, it's better to use the newer DAP-free process (shown in this document). If not, their DAP status can be easily removed from the [Microsoft 365 admin center](https://admin.microsoft.com/). For more information, see [Obtain permissions to manage a customer's service or subscription](/partner-center/customers_revoke_admin_privileges).

    1. Send the template in the previous step to the customer via email.

1. Customer with Microsoft Admin Center global administrator privileges selects the link in email. The link takes them to the following [Microsoft 365 admin center](https://admin.microsoft.com/) page:

    :::image type="content" source="images/csp3a.png" alt-text="Screenshot of Accept agreement and authorize partner page - delegated admin rights.":::

    The above image is what the customer sees if they requested delegated admin rights (DAP). The page says what Admin roles are being requested. If the customer didn't request delegated admin rights, they would see the following page:

    :::image type="content" source="images/csp3b.png" alt-text="Screenshot of Accept agreement and authorize partner page.":::

    > [!NOTE]
    >
    > A user without global administrator privileges who selects the link sees a message similar to the following message:

    :::image type="content" source="images/csp4.png" alt-text="Screenshot of permission page.":::

1. Customer selects the **Yes** checkbox, followed by the **Accept** button. Authorization happens instantaneously.

1. To check that the authorization request is complete, the CSP can check the **Customers** list in their Microsoft Partner Center account. If the customer is in the list, the request is complete. For example:

    :::image type="content" source="images/csp5.png" alt-text="Customers.":::

<!-- MAXADO-9048730 -->

> [!IMPORTANT]
>
> Microsoft recommends using roles with the fewest permissions. Using lower permissioned accounts helps improve security for an organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when an existing role can't be used.

## OEM authorization

OEM authorization is only available for those OEMs who are eligible to use OEM Direct API for Windows Autopilot registration and deregistration.

OEMs who are eligible of using Direct API solution have a unique link to provide to their respective customers, which the OEM can request from Microsoft via the **msoemops support** alias. Contact the organization's account manager to obtain this support alias.

1. OEM emails link to their customer.

1. Customer signs into the [Microsoft 365 admin center](https://admin.microsoft.com/) using a cloud-native account (for example, [domain].onmicrosoft.com) with global administrator privileges.

1. Customer selects the link in the email, which takes them directly to the following page:

    :::image type="content" source="images/csp6.png" alt-text="Screenshot of Accept partner invitation page.":::

    > [!NOTE]
    >
    > A user without global admin privileges who selects the link sees a message similar to the following message:

    :::image type="content" source="images/csp7.png" alt-text="Screenshot of MSfB permission required page.":::

1. Customer selects the **Yes** checkbox, followed by the **Accept** button, and they're done. Authorization happens instantaneously.

    > [!NOTE]
    >
    > Once this process is completed, it isn't currently possible for an administrator to remove an OEM. To remove an OEM or revoke their permissions, send a request to <msoemops@microsoft.com>

1. The OEM can use the Validate Device Submission Data API to verify the consent is completed.

    > [!NOTE]
    >
    > This API is discussed in the latest version of the [API Whitepaper, p. 14ff](https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx). This link is only accessible by Microsoft Device Partners. As discussed in this article, it's a best practice recommendation for OEM partners to run the API check to confirm customer consent is received before attempting to register devices. This check can help avoid errors in the registration process.

    > [!NOTE]
    >
    > During the OEM authorization registration process, no delegated admin permissions are granted to the OEM.

## Summary

At this stage of the process, Microsoft is no longer involved. The consent exchange happens directly between the OEM and the customer. It all also happens instantaneously - as quickly as buttons are selected.
