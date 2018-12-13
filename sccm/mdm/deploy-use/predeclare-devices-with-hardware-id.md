---
title: "Predeclare devices with IMEI or iOS serial numbers"
titleSuffix: "Configuration Manager"
description: "Predeclare corporate-owned devices with their IMEI or iOS serial number."
ms.date: 09/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Predeclare devices with IMEI or iOS serial numbers

*Applies to: System Center Configuration Manager (Current Branch)*

You can identify corporate-owned devices by importing their international station mobile equipment identity (IMEI) numbers or iOS serial numbers. You can upload a comma-separated values (.csv) file containing device IMEI numbers or you can manually enter device information.  Imported information will set **Ownership** of the devices that enroll as **Corporate** in lists of devices. An Intune license is still required for each user that accesses the service.  

When you upload serial numbers for company-owned iOS devices, they must be paired with a corporate enrollment profile. Devices must then be enrolled using either Apple’s device enrollment program (DEP) or Apple Configurator to have them appear as company-owned.

>[!NOTE]
>Android devices, excluding Samsung Knox Standard devices, must have a phone number assigned to them to predeclare and enroll as a company-owned device with an IMEI number.

## How to predeclare corporate-owned devices

1. In the Configuration Manager console, go to **Assets and Compliance** > **Overview** > **All Corporate-owned devices** > **Predeclared devices**.

2. Click **Create Predeclared Devices**. The Create Predeclared Devices wizard opens.

3. Choose how you want to add device information:

    -  **Upload a CSV file containing IMEI or serial numbers and details**

       For this option, click **Browse** to specify the .csv file containing information to predeclare corporate-owned devices. The .csv file must be formatted correctly. For more information, see [Format for uploading .csv files](#format-for-uploading-csv-files).

    -  **Manually add IMEI or serial numbers and details**

       To manually enter information, type the IMEI number or iOS serial number and details for the devices. Correct any error or warnings before continuing.

   Click **Next**.

4. If you uploaded a .csv file, review the results of the file import. If a device number was previously imported, Configuration Manager displays those devices and the replacement **Details**. Select the devices whose details you want to overwrite. Device details can only be modified by reimporting the device identification or serial number.

   If you chose to manually enter number, complete the form for the devices you want to predeclare.

   Click **Next** to continue.

5. If your list includes iOS serial numbers, select the **Enrollment Profile to Assign** from the list of available profiles, and then click **Next**.

6. Click **Next** to review the details, and then click **Next** again to upload the data.

7. Click **Close** to finish.

## Format for uploading .csv files

The .csv file you use to identify devices by IMEI or iOS serial number must have the following format, excluding the top row which is provided for guidance only. Each row must contain an ID number, either an IMEI number or an iOS serial number. For iOS devices, you can include both. IMEI numbers can be used for Android, iOS, and Windows devices. This table contains sample data:

| IMEI #  | iOS Serial #  | OS | Details |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Company-owned Windows device|
|   | A1B2C3D4E5C6 | IOS | 	Company-owned iOS device|
| 223456789012345 | E6D5C4B3A210 |   IOS | 	Another iOS device|
| 323456789012345 |        |   IOS | 	A third iOS device|
| 123456789012346 |         |   ANDROID | 	Company-owned Android device|

Do not include a header row in your .csv file. The following example shows the same sample data in CSV format:

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

The columns in the .csv file accept the following values:

| Column 1 | Column 2 | Column 3 | Column 4 |
|---|---|---|---|
|IMEI number without spaces | iOS serial number | IOS, WINDOWS, or ANDROID | Optional device details (1024 character limit) |
