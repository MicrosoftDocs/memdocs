---
title: View diagnostics data
titleSuffix: Configuration Manager
description: View diagnostic and usage data to confirm that your Configuration Manager hierarchy contains no sensitive information.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# How to view diagnostics and usage data for Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can view diagnostic and usage data from your Configuration Manager hierarchy to confirm that it includes no sensitive or identifiable information. The site summarizes and stores its diagnostic data in the **TEL_TelemetryResults** table of the site database. It formats the data to be programmatically usable and efficient.

The information in this article gives you a view of the exact data sent to Microsoft. It's not intended to be used for other purposes, like data analysis.  

## View data in database

Use the following SQL command to view the contents of this table and show the exact data that's sent:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## Export the data

When the service connection point is in offline mode, use the service connection tool to export the current data to a comma-separated values (CSV) file. Run the service connection tool on the service connection point with the **-Export** parameter.

For more information, see [Use the service connection tool](/sccm/core/servers/manage/use-the-service-connection-tool).

## <a name="bkmk_hashes"></a> One-way hashes

Some data consists of strings of random alphanumeric characters. Configuration Manager uses the SHA-256 algorithm to create one-way hashes. This process makes sure that Microsoft doesn't collect potentially sensitive data. The hashed data can still be used for correlation and comparison purposes.

For example, instead of collecting the names of tables in the site database, it captures the one-way hash for each table name. This behavior makes sure that any custom table names aren't visible. Microsoft then does the same one-way hash process of the default SQL table names. Comparing the results of the two queries determines the deviation of your database schema from the product default. This information is then used to improve updates that require changes to the SQL schema.  

When you view the raw data, a common hashed value appears in each row of data. This hash is the hierarchy ID. It's used to correlate data with the same hierarchy without identifying the customer or source.

### How the one-way hash works

1. Get your hierarchy ID by running the following SQL query in SQL Management Studio against the Configuration Manager database:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Use the following Windows PowerShell script to do the one-way hash of your hierarchy ID.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Compare the script output against the GUID in the raw data. This process shows how the data is obscured.
