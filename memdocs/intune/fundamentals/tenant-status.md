---
# required metadata

title: About the Microsoft Intune tenant status page
titleSuffix: Microsoft Intune
description: The Intune tenant status page displays details about your tenant and the status of connectors you've configured, and messages intended for tenants and about the Intune service health. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/20/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: crisk
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---
# View details about your Tenant on the Intune tenant status page

The Microsoft Intune tenant status page is a centralized hub where you can view important details about your tenant. Details include:

- Your tenant name and location
- Service release versions
- Licensed users and enrolled devices

You can also view the status of the Intune connectors you've configured, and health messages for the Intune service and general messages for Tenants.

> [!TIP]
> A tenant is an instance of Azure Active Directory (Azure AD). Your subscription to Intune is hosted by an Azure AD Tenant. For more information, see [Set up a tenant](/azure/active-directory/develop/quickstart-create-new-tenant) in the Azure AD documentation.

To view the dashboard, sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Tenant administration**, and then select **Tenant Status**.

The page is divided into three tabs:

## Tenant details
Tenant details provide at-a-glance information about your tenant. View details like your tenant name and location, your MDM Authority, and your tenants service release number. The service release number is a link that opens [What's new in Intune](../fundamentals/whats-new.md). In *What's new*, you can read about the latest features and updates to the Intune service.  

On this tab, you'll also find basic information about your available licenses and how many are assigned to users. Licenses for devices aren't shown.

## Connector status
Connector status is a one-stop location to review the status of all available connectors for Intune.  

Connectors are:  
- **Connections you configure to external services**. For example, the *Apple Volume Purchase Program* service or the *Windows Autopilot* service.  Status for this type of connector is based on the last successful synchronization time.
- **Certificates or credentials that are required to connect to an external unmanaged service**, like *Apple Push Notification Services* (APNS) certificates. Status for this type of connector is based on the expiry timestamp of the certificate or credential.  

When you open the *Connector status* tab, any unhealthy connectors display at the top of the list. Next are connectors with warnings, and then the list of healthy connectors. Connectors you haven't yet configured appear last as *Not Enabled*.

When there's more than a single connector of any one type, the status is a summary for all of those same connectors. The least healthy status of any single connector is used as the health for the group.  

> [!IMPORTANT]
> Some connectors can report a status of *Healthy* or *Connected* but might not be functioning correctly. If you encounter issues with a specific connector, review the any applicable connector logs or open a case with [support](../../get-support.md) to investigate further.

**Connector status:**

- **Unhealthy:**
  - The certificate or credential has expired
  - The last synchronization was three or more days ago
- **Warning:**
  - The certificate or credential will expire within seven days
  - The last synchronization was more than one day ago
- **Healthy:**
  - The certificate or credential won't expire within the next seven days
  - The last synchronization was less than one day ago  

When you select a connector from the list, the portal presents the portal page that is relevant to that connector. From the connectors page, you can view the status for previously configured connectors. You can also select options to add or create a new connector of that type.

For example, if you select the **VPP Expiry Date** connector, the **iOS Volume-Purchased Program Tokens** page opens. On this page you can view more details about that connector, create a new configuration, or edit and fix issues with an existing one.

## Service health and message center  

The Service health and message center page are where you can view details about the Intune *Service health*, *Issues in your environment that require action*, and *Message center* posts that can provide information about updates and planned changes.

You can only set up your communication preferences for Intune Message center through the Microsoft 365 admin center. To do so, sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/) and go to **Health** > **Service health**. Select **Customize**, and then open the **Email** tab. On the *Email* tab, select the checkbox for **Send me email notifications about service health**, and then configure the additional preferences to meet your requirements.
### Service health

View details for active incidents and advisories in the Microsoft Endpoint Manager admin center. Only incidents that affect your tenant are shown. This information is also available in on the Service health page of the [Microsoft 365 admin center](https://admin.microsoft.com).

When you select an incident, the incident details are presented directly in the Tenant Status page. To view past advisories and incidents, select **See past Incidents/Advisories**. The Microsoft 365 admin center opens and you can then view advisories and incidents from the last 30 days for your tenant.  

To view information for *Service health*, your account must have the **Global Administrator** or **Service support administrator** role in Azure Active Directory or the Microsoft 365 admin center. To assign these permissions, sign in to the [Microsoft 365 admin center](https://admin.microsoft.com) with Global Administrator permissions. Select **Users > Active Users**, and then select the account that requires access. Select **Edit** for Roles, select *Service support administrator* or *Global Administrator*, and then **Save** your edit to assign the permissions.  

### Issues in your environment that require action  
The **Issues in your environment that require action** section displays messages that are sent to alert tenant administrators about issues that might require action to resolve.

To view information for *Issues in your environment that require action*, your account must have the **Global Administrator** or **Service support administrator** role in Azure Active Directory or the Microsoft 365 admin center. To assign these permissions, sign in to the [Microsoft 365 admin center](https://admin.microsoft.com) with Global Administrator permissions. Select **Users > Active Users**, and then select the account that requires access. Select **Edit** for Roles, select *Service support administrator* or *Global Administrator*, and then **Save** your edit to assign the permissions.  

### Intune Message center  
View informational communications from the Intune service team without having to navigate to the Office Message Center. Communications include messages about changes that have recently happened to the Intune service, or that are on the way for your tenant.  

By default, the 10 most recent and active messages display. To view older messages, select **See past Messages** to open the *Message center* in the Microsoft 365 admin center.  

To view information for Intune News, your account must have the **Global Administrator** or **Service support administrator** role in Azure Active Directory, or the **Message Center reader** role in the Microsoft 365 admin center.  To assign this permission, sign in to the [Microsoft 365 admin center](https://admin.microsoft.com) with administrator permissions. Select **Users > Active Users**, and then select the account that requires access. Select **Edit** for *Roles*, select *Teams Communications Administrator*, and then **Save** your edit to assign the permissions.  

## Next steps

- [Walkthrough Intune in Microsoft Endpoint Manager](../fundamentals/tutorial-walkthrough-endpoint-manager.md)
- [Get support for Intune](../../get-support.md)