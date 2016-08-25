---
title: "Predeclare devices with IMEI or iOS serial numbers"
ms.custom: na
ms.date: 2016-07-22
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
---
# Predeclare devices with IMEI or iOS serial numbers
You can identify corporate-owned devices by importing their international station mobile equipment identity (IMEI) numbers or iOS serial numbers. You can upload a comma-separated values (.csv) file containing device IMEI numbers or you can manually enter device information.  Imported information will set **Ownership** of the devices that enroll as “**Corporate**” in lists of devices. An Intune license is still required for each user that accesses the service.  

## Predeclare corporate-owned devices with IMEI or iOS serial number

1.	In the Configuration Manager console navigate Assets and Compliance > Overview > All Corporate-owned devices > Predeclared devices > and then click Add Predeclared devices. The Predeclared Devices wizard opens.
2.	Specify how you want to add device information:
     -	Upload a .csv file containing IMEI numbers and details
     -	Manually add IMEI numbers and details. To manually enter information, type the IMEI number or iOS serial number and details for the devices.
    
      For uploaded files, Browse to the .csv file containing information to predeclare corporate-owned devices. The file must have the following format, excluding the top row which provided for guidance only. Each row must contain either an IMEI number or iOS serial number. Only the serial numbers of iOS devices can be predeclared; use IMEI number for other device platforms. This table contains sample data: 
      | IMEI #  | iOS Serial #  | OS | Details |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | Company-owned Windows device|
      |       | A1B2C3D4E5C6 |   iOS | 	Company-owned iOS device|
      | 223456789012345 | E6D5C4B3A210 |   iOS | 	Another iOS device|
      | 323456789012345 |        |   iOS | 	A third iOS device|
      | 123456789012346 |         |   Android | 	Company-owned Android device|
      
    Do not include a header row in your .csv file. The example above includes a header for clarification only.
    
    **The columns accept the following values:**    
      -	Column 1: IMEI number without spaces
      -	Column 2: iOS serial number
      -	Column 3: Operating system of the device:
         - IOS – All iOS devices
         - WINDOWS – Includes Windows Phone, Window 10 Mobile, and Windows PCs
         - ANDROID – All Android devices
      -	Column 4: Details (optional) – Additional device information that appears in the Configuration Manager console. 1024 character limit.
    
    Click **Next**.
    
3. Review the results of the file import. If a device number was preciously imported, Configuration Manager displays those devices and the replacement **Details**. Select the devices whose details you want to overwrite. Device details can only be modified by reimporting the device identification or serial number. Click **Next** to continue or **Back** to preserve updated details, and then complete the wizard.

4. If your import includes iOS serial numbers, you must assign those devices to an enrollment profile. Select the **Enrollment Profile to Assign** from the list of available profiles, and then click **Next**.

5. Click **Next** to view the Summary and then complete the wizard.

