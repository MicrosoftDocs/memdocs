---
# required metadata

title: Device query for multiple devices in Microsoft Intune
description: Learn how device query for multiple devices allows you to gain comprehensive insights about all your devices using Kusto Query Language (KQL).
keywords: 
ms.author: smbhardwaj
author: smritib17 
manager: dougeby
ms.date: 02/10/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Abby Starr 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier2
- M365-identity-device-management
---

# Device Query for Multiple Devices

Device query for multiple devices allows you to gain comprehensive insights about your entire fleet of devices using Kusto Query Language (KQL) to query across collected inventory data for your devices.

## Prerequisites

- To use Device query in your tenant, you must have a license that includes Microsoft Intune Advanced Analytics. Advanced Analytics features are available with:

  - The Intune Advanced Analytics add-on
  - Microsoft Intune Suite

-  For a user to use Device query, you must assign the Managed Devices – Query and Organization – Read permissions to them.

- Devices must be Intune managed and corporate owned.

- Device query for multiple devices only works on devices that are already collecting device inventory data.

## Supported platforms

Device query for multiple devices is currently only supported on devices running Windows 10 and later.

## How to use device query for multiple devices

To use Device query for multiple devices, navigate to the **Devices** pane and select **Device query**. Then, input a query in the query box using the supported properties and supported operators and select **Run** to execute the query. Results are displayed in the **Results** tab area.

> [!TIP]
> You can now use Copilot in Intune (public preview) to generate KQL queries for device query using natural language requests. To learn more, go to [Query with Copilot in device query](../intune-service/copilot/copilot-intune-overview.md#query-multiple-devices).

For more information on Kusto Query Language, see [Learn more about Kusto Query Language](/azure/data-explorer/kusto/query/).

## Supported operators

Device query supports only a subset of the operators supported in the Kusto Query Language (KQL). The following operators are currently supported:

### Table operators

Table operators can be used to filter, summarize, and transform data streams. The following operators are supported:

| **Table Operators** | **Description** |
| --- | --- |
| count | Returns a table with a single record containing the number of records. |
| distinct | Produces a table with the distinct combination of the provided columns of the input table. |
| join | Merge the rows of two tables to form a new table by matching row for the same device. Only the join type of innerunique is supported. Join statements support on syntax. Common syntax for join is LeftEntity \| join [hints] (RightEntity) on Conditions. For more info, see [Join](/kusto/query/join-operator) documentation.|
| order by | Sort the rows of the input table into order by one or more columns. |
| project | Select the columns to include, rename or drop, and insert new computed columns. |
| take | Return up to the specified number of rows. |
| top | Returns the first N records sorted by the specified columns. |
| where | Filter a table to the subset of rows that satisfy a predicate. |

> [!NOTE]
> Only the join type of [innerunique](/kusto/query/join-innerunique) is supported. If you join two entities that result in duplicate records, only the first record is returned.

### Scalar operators

Scalar operators can be used to perform operations on individual values. The following operators are supported:

| **Operators** | **Description** | **Example** |
| --- | --- | --- |
| == | Equal | 1 == 1, 'aBc' == 'AbC' |
| != | Not Equal | 1 != 2, 'abc' != 'abcd' |
| < | Less | 1 < 2, 'abc' < 'DEF' |
| > | Greater | 2 > 1, 'xyz' > 'XYZ' |
| <= | Less or Equal | 1 <= 2, 'abc' <= 'abc' |
| >= | Greater or Equal | 2 >= 1, 'abc' >= 'ABC' |
| + | Add | 2 + 1, now() + 1d |
| - | Subtract | 2 - 1, now() - 1h |
| * | Multiply | 2 * 2 |
| / | Divide | 2 / 1 |
| % | Modulo | 2 % 1 |
| like | LHS contains a match for RHS | 'abc' like '%B%' |
| !like | LHS doesn't contain a match for RHS | 'abc' !like '_d_' |
| contains | RHS occurs as a subsequence of LHS | 'abc' contains 'b' |
| !contains | RHS doesn't occur in LHS | 'team' !contains 'i' |
| startswith | RHS is an initial subsequence of LHS | 'team' startswith 'tea' |
| !startswith | RHS isn't an initial subsequence of LHS | 'abc' !startswith 'bc' |
| endswith | RHS is a closing subsequence of LHS | 'abc' endswith 'bc' |
| !endswith | RHS isn't a closing subsequence of LHS | 'abc' !endswith 'a' |
| and | True if and only if RHS and LHS are true | (1 == 1) and (2 == 2) |
| or | True if and only if RHS or LHS is true | (1 == 1) or (1 == 2) |

### Aggregation functions

Aggregation functions can be used to summarize data. The following functions are supported:

| **Function** | **Description** |
| --- | --- |
| avg() | Returns the average of the values across the group |
| count() | Returns a count of the records per summarization group |
| countif() | Returns a count of rows for which Predicate evaluates to true |
| dcount() | Returns the number of distinct values in the group |
| max() | Returns the maximum value across the group |
| maxif() | Returns the maximum value across the group for which Predicate evaluates to true |
| min() | Returns the minimum value across the group |
| minif() | Returns the minimum value across the group for which Predicate evaluates to true |
| percentile() | Returns an estimate for the specified nearest-rank percentile of the population defined by Expr |
| sum() | Returns the sum of the values across the group |
| sumif() | Returns a sum of Expr for which Predicate evaluates to true |

### Scalar functions

Scalar functions can be used to perform operations on individual values. The following functions are supported:

| **Function** | **Description** |
| --- | --- |
| ago() | Subtracts the given timespan from the current UTC clock time |
| bin() | Rounds values down to a number of datetime multiple of a given bin size |
| case() | Evaluates a list of predicates and returns the first result expression whose predicate is satisfied |
| datetime_add() | Calculates a new datetime from a specified datepart multiplied by a specified amount, added to a specified datetime |
| datetime_diff() | Calculates the difference between two datetime values |
| iif() | Evaluates the first argument and returns the value of either the second or third arguments depending on whether the predicate evaluated to true (second) or false (third) |
| indexof() | Reports the zero-based index of the first occurrence of a specified string within the input string |
| isnotnull() | Evaluates its sole argument and returns a Boolean value indicating if the argument evaluates to a non-null value |
| isnull() | Evaluates its sole argument and returns a Boolean value indicating if the argument evaluates to a null value |
| now() | Returns the current UTC clock time |
| strcat() | Concatenates between 1 and 64 arguments |
| strlen() | Returns the length, in characters, of the input string |
| substring() | Extracts a substring from a source string starting from some index to the end of the string |
| tostring() | Converts input to a string representation |

## Supported properties

Device query supports the following entities. To learn more about what properties are supported for each entity, see [Intune Data Platform Schema](data-platform-schema.md).

- Battery
- Bios Info
- Cpu
- Disk Drive
- Encryptable Volume
- Logical Drive
- Memory Info
- Network Adapter
- Os Version
- System Enclosure
- Time
- Tpm
- Video Controller
- Windows Qfe

### Device entity

Device query for multiple devices supports a linked entity which can be used with all other supported entities. The device entity supports the following properties:

| **Property** | **Type** | **Description** |
| --- | --- | --- |
| DeviceId | String | A unique ID generated by Intune as part of MDM enrollment. |
| EntraDeviceId | String | Unique ID generated by Microsoft Entra as part of Microsoft Entra registration or join. |
| ManagementName | String | An easily recognizable device name used only in the Intune admin center. Changing this name doesn't change the device name or the name in the Company Portal. |
| DeviceName | String | Name of the device |
| SerialNumber | String | Serial number of the device |
| Manufacturer | String | Manufacturer of the device |
| Model | String | Model of the device |
| OsDescription | String | Full description of the operating system edition |
| OsVersion | String | The version of the operating system on the device |
| EnrollmentProfileName | String | Name of the enrollment profile assigned to the device. Default value is an empty string indicating no enrollment profile was assigned to the device. |
| EnrolledDateTime | Datetime | The date and time that the device was enrolled in Intune. |
| CertExpirationDateTime | Datetime | Reports device management certificate expiration date. |
| EnrolledByUserId | String | Unique identifier for the user that enrolled the device |
| PrimaryUserId | String | Unique identifier for the user associated with the device. |
| LastLoggedOnUserId | String | Unique identifier for the user who last logged on to the device. |
| InCompliancePeriodUntilDateTime | Datetime | The DateTime when device compliance grace period expires |
| DeviceCategoryId | String | Device category display name. Default is an empty string. |
| LastSeenDateTime | String | The date and time that the device last connected to Intune. |
| Ownership | String | Ownership of the device. |

The device entity shows up in query results, unless specified not to (through something like a project that doesn't include the Device entity). The device entity and its properties can also be referenced in queries by referencing Device.[Insert property].

The following query returns all the DiskDrive information for all devices with serial number 123.:

```kusto
DiskDrive 
where Device.SerialNumber = 123
```

The following query projects the Device ID and Manufacturer properties of the entity DiskDrive:  

```kusto
DiskDrive | project Device.DeviceId, Manufacturer
```

Although the Device entity that is shown as the first column by default appears as device names using Device by itself in a query parses to Device.DeviceId.  

This query returns results ordered by the DeviceID, not by DeviceName.:

```kusto
MemoryInfo | order by Device
```

Similarly, this query returns no results unless the device ID is Desktop123. It doesn't query on device name:

```kusto
Cpu | where Device == “Desktop123”
```

Use the following example to query on device name:  

```kusto
Cpu | where Device.DeviceName == ‘Desktop123”
```

## Known limitations

- Using the Device entity in aggregation functions shows a red underline. However, the query can  still run and can return results as expected. For example, the following query shows a red underline under **Device** but still runs:

    ```kusto
    Cpu | summarize max(Device) by Manufacturer.
    ```

- When writing queries with a join operator, $left and $right parameters show a red underline under $left and $right. However, the query can still run and returns results as expected.  

- A single query can contain a maximum of 3 join operators. Queries with additional joins fail.

- A max of ~50,000 records are returned for a query.  

- A maximum of 10 queries can be submitted per minute. Additional queries will fail.

- A maximum of 1,000 queries can be submitted per month.
