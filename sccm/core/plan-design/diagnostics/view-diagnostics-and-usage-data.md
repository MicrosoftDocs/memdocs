---
title: "How to view diagnostics and usage data for System Center Configuration Manager"
ms.custom: na
ms.date: 2016-05-25
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: 8
author: Brenduns
translation.priority.ht:
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to view diagnostics and usage data for System Center Configuration Manager
You can view diagnostic and usage data from your System Center Configuration Manager hierarchy to confirm that no sensitive or identifiable information is included. Telemetry data is summarized and stored in the **TEL_TelemetryResults** table of the site database and is formatted to be programmatically usable and efficient. While the following options give you a view of the exact data sent to Microsoft, it is not intended to be used for other purposes, like data analysis.  

The following SQL command can be used to view the contents of this table, and shows the exact data that is sent (you can also export this data to a text file):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Prior to installing version 1602, the table that stores telemetry data is **TelemetryResults**.  

When the service connection point is in offline mode, you can use the service connection tool to export the current diagnostics and usage data into a common-separated values (CSV) file. Run the service connection tool on the service connection point with the **-Export** parameter.  

##  <a name="bkmk_hashes"></a> One-way hashes  
Some of the data consists of strings of random alphanumeric characters. Configuration Manager uses one-way hashes using the SHA-256 algorithm to ensure we do not collect potentially sensitive data while leaving it in a state where it can still be used for correlation and comparison purposes. For example, instead of collecting the names of tables in the site database, a one-way hash is captured for each table name. This ensures that any custom table names created by you or third-party product add-ons are not visible. We can then do the same one-way hash of the SQL table names that ship by default in the product, and compare to determine the deviation of your database schema against the product default. This is then used to improve updates that require changes to the SQL schema.  

When viewing the raw data, a common hashed value will appear in each row of data. This is the hierarchy ID. This hashed value is used to ensure the data is correlated with the same hierarchy without identifying the customer or source.  

#### To see how the one-way hash works  

1.  Obtain your hierarchy ID by running the following SQL statement in SQL Management Studio against the Configuration Manager database: **select [dbo].[fnGetHierarchyID](\)**  

2.  Next, use the following Windows PowerShell script to perform the one-way hash of the GUID obtained from the database. You can then compare this against the hierarchy ID in the raw data to see how we obscure this data.  

    ```  
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

## See Also  
 [Diagnostics and usage data for System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)   
 [How diagnostics and usage data is used for System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)   
 [Levels of diagnostic usage data collection for System Center Configuration Manager](../../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection.md)   
 [How diagnostics and usage data is collected by System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)
