---
title: Device Query for Multiple Devices in Advanced Analytics
description: Use device query for multiple devices in Microsoft Intune to run Kusto Query Language (KQL) queries, analyze device inventory, and gain cross-platform insights.
ms.date: 01/23/2026
ms.topic: how-to
---

# Device query for multiple devices

[!INCLUDE [intune-add-on-note](../intune-service/includes/intune-add-on-note.md)]

Device query for multiple devices allows you to gain comprehensive insights about your entire fleet of devices using Kusto Query Language (KQL) to query across collected inventory data for your devices.

## Before you begin

> [!div class="checklist"]
> - Confirm that your environment meets all [prerequisites](index.md#prerequisites).

Additional prerequisites for device query for multiple devices:

:::row:::
:::column span="1":::
[!INCLUDE [platform](../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> Device query for multiple devices supports:
> - Windows
> - Android
>   - Android Enterprise corporate owned dedicated devices (COSU)
>   - Android Enterprise corporate owned fully managed (COBO)
>   - Android Enterprise corporate owned work profile (COPE)
> - Apple
>   - iOS/iPadOS
>   - macOS
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> Device query for multiple devices supports devices that are:
>
> - Managed by Intune and marked as corporate owned
> - Windows devices must have a [properties catalog policy](../intune-service/configuration/properties-catalog.md) deployed to them to collect inventory data.\
>   For iOS/iPadOS, Android, and macOS, data is automatically collected and a separate properties catalog policy doesn't need to be deployed.
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> To use device query for multiple devices, use an account with at least one of the following roles:
> - [Help Desk Operator][INT-R1]
> - [Custom role][INT-RC] that includes:
>   - The permission **Managed Devices/Query**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

:::column-end:::
:::row-end:::

## Use device query for multiple devices

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Device query**.
1. Input a query in the query box using the supported properties and supported operators.
1. Select **Run** to execute the query.
1. Results are displayed in the **Results** tab area.
   - To run part of a query or a single query when multiple queries are in the window, highlight the query you want to run and select **Run**. Only the highlighted query runs.

You can expand the view on the left side to see all the properties that can be queried. Select any one to populate into your query. You can select and drag the edges of both the left side and the query window to make any adjustments.

After running a query, select **Export** to save results to a .CSV file. You have the option to export all columns in the query result or just the columns you select. You can export up to 50,000 results to a file.

For more information on Kusto Query Language, see [Learn more about Kusto Query Language](/azure/data-explorer/kusto/query/).

> [!TIP]
> Use Copilot in Intune to generate KQL queries for device query using natural language requests. To learn more, see [Query with Copilot in device query](../intune-service/copilot/copilot-intune-overview.md#-use-copilot-to-create-kql-queries-to-get-device-details).

<<<<<<< HEAD
## Manage device queries for multiple devices

You can save, share, and reuse queries with other Intune admins.

### Save a device query

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Device query**.
1. Once the query is complete, select **Save as new**.
1. In the **Save Query** pane, enter a name and description, and then select a query type:
   - **Personal query**: Visible only to you and available for future reuse.
   - **Shared query**: Available to other Intune admins.
1. Select **Save**.

The saved query appears under the **Saved Queries** tab. When you open **Device query**, you can select a saved personal or shared query from this tab.

> [!NOTE]
> Only the creator of a shared query can modify or delete it. If the creator's account is deleted, the query is marked for deletion and other admins must save a copy to retain it.

### Modify a saved query

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Device query**.
1. Select the **Saved Queries** tab.
1. Select a query from the personal queries list or shared queries list.
1. Make your changes, and then select one of the following:
   - **Save**: Saves changes to the existing query (available only for personal queries).
   - **Save as new**: Saves the query as a new query.

### Change a personal query to a shared query

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Device query**.
1. Select the **Saved Queries** tab.
1. Find the personal query that you want to share, and then select **…** > **Edit**.
1. From the **Query type** dropdown, select **Shared query**.
1. Select **Save**.

> [!NOTE]
> Only the creator of a shared query can modify or delete it. If the creator's account is deleted, the query is marked for deletion and other admins must save a copy to retain it.

### Delete a personal device query

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Device query**.
1. Select the **Saved Queries** tab.
1. Find the personal query that you want to delete, and then select **…** > **Edit**.
1. In the query pane, select **Delete**.
1. Select **Delete** to confirm.

=======
>>>>>>> cf374b8ce15add66b0b1b317d91f2f395dbfee9b
## Sample queries

To help you get started, some sample queries are provided in this section. To access the sample queries, expand the **example queries** section under the Getting started page, and select the one you want to add to the query window. The following section shows the list of sample queries.

### Top processors by Core Count

This query shows the top five CPUs by core count.

```kusto
Cpu
| project Device, ProcessorId, Model, Architecture, CpuStatus, ProcessorType, CoreCount, LogicalProcessorCount, Manufacturer, AddressWidth
| order by CoreCount asc
| take 5
```

### Devices with unprotected disks

This query lists devices with unencrypted disks.

```kusto
EncryptableVolume
| where ProtectionStatus != "PROTECTED"
| join LogicalDrive on Device
```

### Arm64 devices

This query lists all devices with an ARM64 processor.

```kusto
Cpu
| where Architecture == "ARM64"
```

### Device count by processor architecture

This query provides a summary of devices by CPU architecture.

```kusto
Cpu
| summarize DeviceCount = count() by Architecture
```

### Top devices by battery capacity

This query lists the top 10 devices by fully charged battery capacity.

```kusto
Battery
| project Device, InstanceName, Manufacturer, Model, SerialNumber, CycleCount,
          DesignedCapacity,
          FullChargedCapacity,
          FullChargedCapacityPercent = (FullChargedCapacity * 100) / DesignedCapacity
| top 10 by FullChargedCapacityPercent asc
```

### Devices memory information

This query lists devices with physical and virtual memory in GB.

```kusto
MemoryInfo
| project Device,
          PhysicalMemoryGB = PhysicalMemoryTotalBytes/(1000*1000*1000),
          VirtualMemoryGB = VirtualMemoryTotalBytes/(1000*1000*1000)
| order by PhysicalMemoryGB asc
```

### Device count by OS version

This query provides a summary of devices by OS version.

```kusto
OsVersion| summarize DevicesCount = count() by OsVersion
```

### Devices Bios Information

This query lists devices based on BIOS manufacturer.

```kusto
BiosInfo| where Manufacturer contains "Microsoft"
```

### TPM disabled devices

This query lists devices that have TPM disabled.

```kusto
Tpm | where Enabled != true
```

## Supported operators

Device query supports only a subset of the operators supported in the Kusto Query Language (KQL). The following operators are currently supported:

### Table operators

Table operators can be used to filter, summarize, and transform data streams. The following operators are supported:

| Table operator | Description |
| --- | --- |
| `count` | Returns a table with a single record containing the number of records. |
| `distinct` | Produces a table with distinct combinations of the provided columns from the input table. |
| `join` | Merges rows from two tables to form a new table based on matching values in the specified columns. The following join types are supported:<br>- `innerunique` (default)<br>- `inner`<br>- `leftouter`<br>- `rightouter`<br>- `fullouter`<br>- `leftsemi`<br>- `rightsemi`<br>- `leftanti`<br>- `rightanti`<br><br>Join statements support an optional `on` clause. In device query scenarios, you typically use `on Device` when joining tables that contain a `Device` entity. Common syntax for `join` is: `LeftTable | join [hints] (RightTable) on Conditions`.<br><br> **Important:** Joins that use `on Device.DeviceID` are no longer supported. Queries that currently specify `on Device.DeviceId` should switch to using `on Device`, or omit the `on` clause when joining on the `Device` entity.<br><br>For more information, see [Join operator](/kusto/query/join-operator). |
| `order by` | Sorts the rows of the input table by one or more columns. |
| `project` | Selects columns to include, rename, or drop, and inserts new computed columns. |
| `take` | Returns up to the specified number of rows. |
| `top` | Returns the first N records sorted by the specified columns. |
| `where` | Filters a table to the subset of rows that satisfy a predicate. |
| `summarize` | Produces a table that aggregates the contents of the input table. |

> [!NOTE]
> `Device` is an entity-type and can't be used directly in operators that require scalar values (such as `distinct`, `summarize`, and `order by`). For these operators, use a specific scalar property of the device (for example, `Device.SerialNumber` or `Device.OSVersion`).

### Scalar operators

Scalar operators can be used to perform operations on individual values. The following operators are supported:

| Operators | Description | Example |
| --- | --- | --- |
| `==` | Equal | `1 == 1`, `'aBc' == 'AbC'` |
| `!=` | Not Equal | `1 != 2`, `'abc' != 'abcd'` |
| `<` | Less | `1 < 2`, `'abc' < 'DEF'` |
| `>` | Greater | `2 > 1`, `'xyz' > 'XYZ'` |
| `<=` | Less or Equal | `1 <= 2`, `'abc' <= 'abc'` |
| `>=` | Greater or Equal | `2 >= 1`, `'abc' >= 'ABC'` |
| `+` | Add | `2 + 1`, `now() + 1d` |
| `-` | Subtract | `2 - 1`, `now() - 1h` |
| `*` | Multiply | `2 * 2` |
| `/` | Divide | `2 / 1` |
| `%` | Modulo | `2 % 1` |
| `like` | LHS contains a match for RHS | `'abc' like '%B%'` |
| `contains` | RHS occurs as a subsequence of LHS | `'abc' contains 'b'` |
| `!contains` | RHS doesn't occur in LHS | `'team' !contains 'i'` |
| `startswith` | RHS is an initial subsequence of LHS | `'team' startswith 'tea'` |
| `!startswith` | RHS isn't an initial subsequence of LHS | `'abc' !startswith 'bc'` |
| `endswith` | RHS is a closing subsequence of LHS | `'abc' endswith 'bc'` |
| `!endswith` | RHS isn't a closing subsequence of LHS | `'abc' !endswith 'a'` |
| `and` | True if and only if RHS and LHS are true | `(1 == 1) and (2 == 2)` |
| `or` | True if and only if RHS or LHS is true | `(1 == 1) or (1 == 2)` |

### Aggregation functions

Aggregation functions can be used to summarize data. The following functions are supported:

| Function | Description |
| --- | --- |
| `avg()` | Returns the average of the values across the group |
| `count()` | Returns a count of the records per summarization group |
| `countif()` | Returns a count of rows for which Predicate evaluates to true |
| `dcount()` | Returns the number of distinct values in the group |
| `max()` | Returns the maximum value across the group |
| `maxif()` | Returns the maximum value across the group for which Predicate evaluates to true |
| `min()` | Returns the minimum value across the group |
| `minif()` | Returns the minimum value across the group for which Predicate evaluates to true |
| `percentile()` | Returns an estimate for the specified nearest-rank percentile of the population defined by Expr |
| `sum()` | Returns the sum of the values across the group |
| `sumif()` | Returns a sum of Expr for which Predicate evaluates to true |

### Scalar functions

Scalar functions can be used to perform operations on individual values. The following functions are supported:

| Function | Description |
| --- | --- |
| `ago()` | Subtracts the given timespan from the current UTC clock time. |
| `bin()` | Rounds values down to a number of datetime multiple of a given bin size. |
| `case()` | Evaluates a list of predicates and returns the first result expression whose predicate is satisfied. |
| `datetime_add()` | Calculates a new datetime from a specified datepart multiplied by a specified amount, added to a specified datetime. Negative values for the amount parameter aren't supported. |
| `datetime_diff()` | Calculates the difference between two datetime values. |
| `iif()` | Evaluates the first argument and returns the value of either the second or third arguments depending on whether the predicate evaluated to true (second) or false (third). |
| `indexof()` | Reports the zero-based index of the first occurrence of a specified string within the input string. |
| `isnotnull()` | Evaluates its sole argument and returns a Boolean value indicating if the argument evaluates to a non-null value. |
| `isnull()` | Evaluates its sole argument and returns a Boolean value indicating if the argument evaluates to a null value. |
| `now()` | Returns the current UTC clock time. |
| `strcat()` | Concatenates between 1 and 64 arguments. |
| `strlen()` | Returns the length, in characters, of the input string. |
| `substring()` | Extracts a substring from a source string starting from some index to the end of the string. |
| `tostring()` | Converts input to a string representation. |

## Supported properties

Device query supports the following entities. To learn more about what properties are supported for each entity, see [Intune Data Platform Schema](data-platform-schema.md).

- `Apple Auto Setup Admin Accounts`
- `Apple Device States`
- `Apple Update Settings`
- `Battery`
- `Bios Info`
- `Bluetooth`
- `Cellular`
- `CPU`
- `Device Storage`
- `Disk Drive`
- `Encryptable Volume`
- `Logical Drive`
- `Memory Info`
- `Network Adapter`
- `Os Version`
- `Shared iPad`
- `Sim Info`
- `System Enclosure`
- `SystemInfo`
- `Time`
- `Tpm`
- `Video Controller`
- `Windows Qfe`

### Device entity

Device query for multiple devices supports a linked entity. The Device entity can be used with all other supported entities. The device entity supports the following properties:

| Property | Type | Description |
|--|--|--|
| `DeviceId` | String | A unique ID generated by Intune as part of device enrollment. |
| `EntraDeviceId` | String | Unique ID generated by Microsoft Entra as part of Microsoft Entra registration or join. |
| `ManagementName` | String | An easily recognizable device name used only in the Intune admin center. Changing this name doesn't change the device name or the name in the Company Portal. |
| `DeviceName` | String | Name of the device |
| `SerialNumber` | String | Serial number of the device |
| `Manufacturer` | String | Manufacturer of the device |
| `Model` | String | Model of the device |
| `OSDescription` | String | Full description of the operating system edition |
| `OSVersion` | String | The version of the operating system on the device |
| `EnrollmentProfileName` | String | Name of the enrollment profile assigned to the device. Default value is an empty string indicating no enrollment profile was assigned to the device. |
| `EnrolledDateTime` | Datetime | The date and time that the device was enrolled in Intune. |
| `CertExpirationDateTime` | Datetime | Reports device management certificate expiration date. |
| `EnrolledByUserId` | String | Unique identifier for the user that enrolled the device |
| `PrimaryUserId` | String | Unique identifier for the user associated with the device. |
| `LastLoggedOnUserId` | String | Unique identifier for the user who last logged on to the device. |
| `InCompliancePeriodUntilDateTime` | Datetime | The DateTime when device compliance grace period expires |
| `DeviceCategoryId` | String | Device category display name. Default is an empty string. |
| `LastSeenDateTime` | String | The date and time that the device last connected to Intune. |
| `Ownership` | String | Ownership of the device. |


The `Device` entity allows you to reference device information associated with each resulting row without needing to explicitly join to a device table.

By default, query results include a `Device` entity column that provides device context for each row. Operators such as `project`, `summarize`, or `distinct` can change which columns are returned.

`Device` represents the device associated with the resulting row and can be referenced directly as an entity-type column. When displayed in query results, the `Device` entity is shown using a friendly identifier, such as the device name, to make it easier to identify devices.

You can reference properties of the `Device` entity in queries using `Device.[Property]`.

The following query returns all `DiskDrive` information for devices with a specific serial number:

```kusto
DiskDrive
| where Device.SerialNumber == "123"
```


The following query projects the `Device` entity and the `Manufacturer` property from the `DiskDrive` entity:

```kusto

DiskDrive
| project Device, Manufacturer

```

By default, query results include a `Device` entity that represents the device associated with each row. The `Device` entity is an entity-type column and does not implicitly resolve to a specific scalar property.
When sorting or filtering results, explicitly reference the device property you want to use. For example, this query orders results by device name:

```kusto

MemoryInfo
| order by Device.DeviceName

```

Similarly, to filter by device name, reference the `DeviceName` property directly:

```kusto

Cpu
| where Device.DeviceName == "Desktop123"

```

## Known limitations


- Using entity-type columns such as `Device` in aggregation functions can show a red underline in the editor because aggregation functions require scalar values. To avoid this, reference a specific scalar property of the entity. For example:

  ```kusto
  Cpu
  | summarize max(CpuUsage) by Device.Manufacturer
  ```

- Queries that use the `join` operator with `$left` and `$right` parameters may show a red underline in the editor. However, the query can still run and return results as expected.
- A single query can contain a maximum of three `join` operators. Queries with more joins fail.
- A maximum of ~50,000 records are returned for a query.
- A maximum of 10 queries can be submitted per minute. Additional queries within the same minute fail.
- A maximum of 1,000 queries can be submitted per month.
- Negative values for the `amount` parameter of the `datetime_add()` function aren't supported.
- Referencing a variable that was generated by an aggregation function without explicitly naming it can cause a query to fail. Explicitly naming the variable allows the query to succeed. For example:
  - The query `Device | summarize dcount(DeviceId) | order by dcount_DeviceId` fails.
  - The query `Device | summarize DCountDeviceIdRename = dcount(DeviceId) | order by DCountDeviceIdRename` succeeds.

<!--links-->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role
[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
