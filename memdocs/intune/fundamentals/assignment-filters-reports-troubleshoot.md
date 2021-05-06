---
# required metadata

title: Assignment filter reports and troubleshooting in Microsoft Intune - Azure | Microsoft Docs
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/03/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection: M365-identity-device-management
---

# Reporting and troubleshooting

When a device is evaluated against filters, the results are logged and surfaced in reports in the MEM admin center. 

## Reports

The following reports are currently available: 

- **Filter evaluation report for a single device**: In **Devices** > **All Devices** > [DeviceName] > **Filter evaluation (preview)** is a report that shows a row for every workload (policy or app) where a filter evaluation was performed. For each evaluated workload, you can select the Filters evaluated link which opens a detailed evaluation result context pane. On the context pane you can see the following information: 

- The filter(s) that were evaluated 

- The time the evaluation occurred 

- The evaluation results (Match/No match) and if the filter was operating in Include or Exclude mode. 

- The Filter name, description and rules 

- The properties presented to the evaluation engine during the evaluation process.

## Troubleshooting

