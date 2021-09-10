---
title: Custom properties for devices
titleSuffix: Configuration Manager
description: Use the administration service to set custom property data on devices, for reporting or collections.
ms.date: 09/10/2021
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Custom properties for devices

*Applies to: Configuration Manager (current branch)*

<!--8939867-->

Many customers have other data that's external to Configuration Manager but useful for deployment targeting, collection building, and reporting. This data is typically non-technical in nature, not discoverable on the client, and comes from a single external source. For example, a central IT Infrastructure Library (ITIL) system or asset database, which has some of the following device attributes:

- Physical location
- Organizational priority
- Category
- Cost center
- Department

Starting in version 2107, you can [use the administration service](usage.md) to set this data on devices. The site stores the property's name and its value in the site database as the **Device Custom Properties** class. You can then use the custom properties in Configuration Manager for reporting or to create collections.

## Prerequisites

The account that makes the API calls requires the following permissions on a collection that contains the target device:

- To set properties: **Modify Resource**
- To view properties: **Read Resource**
- To remove properties: **Delete Resource**

## Set properties

To set properties on a device, use the **SetExtensionData** API. Make a POST call to the URI `https://<SMSProviderFQDN>/AdminService/v1.0/Device(<DeviceResourceID>)/AdminService.SetExtensionData` with a JSON body. The resource ID is an integer value, for example `16777345`.

This JSON example sets two name-value pairs for the device's asset tag and location:

```json
{
  "ExtensionData": {
    "AssetTag":"0580255",
    "Location":"Dublin"
  }
}
```

## View properties

Use the **GetExtensionData** API to view your custom properties.

To view properties on a _single_ device, make a GET call to the URI `https://<SMSProviderFQDN>/AdminService/v1.0/Device(<DeviceResourceID>)/AdminService.GetExtensionData`.

To view properties on _all_ devices, make a GET call to the URI `https://<SMSProviderFQDN>/AdminService/v1.0/Device/AdminService.GetExtensionData`. This call returns property values from devices to which you have read permission.

## Remove properties

To remove properties values from all devices, use the **DeleteExtensionData** API without a device ID. Include a device resource ID to only remove properties from a specific device. Make a POST call to the URI `https://<SMSProviderFQDN>/AdminService/v1.0/Device/AdminService.DeleteExtensionData`.

## Create a collection

Use the following steps to create a collection with a query rule based on the custom properties:

1. In the Configuration Manager console, [Create a collection](../../core/clients/manage/collections/create-collections.md).

1. On the Membership Rules page, in the **Add Rule** list, select **Query rule**.

1. In the Query Rule Properties window, specify a **Name** for the query. Then select **Edit Query Statement**.

1. In the Query Statement Properties window, switch to the **Criteria** tab. Then select the golden asterisk (`*`) to add new criteria.

1. In the Criterion Properties window, **Select** the following values:

    - Attribute class: **Device Custom Properties**
    - Attribute: **PropertyName**

1. Select an **Operator** and then specify the name of the property as the **Value**.

    At this point, the Criterion Properties window should look similar to the following image:

    :::image type="content" source="media/8939867-property-name.png" alt-text="Criterion Properties window for Device Custom Properties PropertyName.":::

    Select **OK** to save the criterion.

1. Repeat the steps to add a criterion for the **PropertyValue** attribute.

    At this point, the collection Query Statement Properties window should look similar to the following image:

    :::image type="content" source="media/8939867-query-statement-properties.png" alt-text="Query Statement Properties window with both Device Custom Properties criteria.":::

1. Select **OK** to close all property windows. Then complete the wizard to create the collection.

### Example WQL statement

You can also use the following sample query. In the query statement properties window, select **Show Query Language** to paste the query statement.

```sql
select SMS_R_SYSTEM.ResourceID,SMS_R_SYSTEM.ResourceType,SMS_R_SYSTEM.Name,SMS_R_SYSTEM.SMSUniqueIdentifier,SMS_R_SYSTEM.ResourceDomainORWorkgroup,SMS_R_SYSTEM.Client 
from SMS_R_System inner join SMS_G_System_ExtensionData on SMS_G_System_ExtensionData.ResourceId = SMS_R_System.ResourceId 
where SMS_G_System_ExtensionData.PropertyName = "AssetTag" and SMS_G_System_ExtensionData.PropertyValue = "0580255"
```

> [!NOTE]
> Incremental collection updates don't work with custom properties WQL statements.<!--10901844-->

## Next steps

[How to use the administration service](usage.md)

[Create a collection](../../core/clients/manage/collections/create-collections.md)
