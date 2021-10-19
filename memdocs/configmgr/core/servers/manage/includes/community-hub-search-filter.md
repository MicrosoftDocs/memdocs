---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 03/02/2021
ms.localizationpriority: medium
---
<!--This file is shared by the community-hub and community-hub-extensions.md files for 8516139. H2s/H3s are driven by the article-->

|Filter name|Example search| Uses a `like` filter|
---|---|
| **Type**|`type:report`| Yes|
|**Curated**| `curated:false`| No|
|**User**| `user:<GitHubUserName>`| No|
|**Organization**| `org:<GitHubOrganizationName>`| No|
|**Name**| `name:test_report`| Yes|
|**Description**| `desc:description`| Yes|

When filtering Community hub items in search:
- The filtering on some items is done using `like` so you don't need to know the exact name of an item you are trying to find. For instance, using `type:task` would return task sequences.
- You can't use the same filter twice in a search. For instance, using `type:report` and `type:extension` would only return reports since the second filter gets ignored.
- Search filtering respects the hierarchy setting for displaying [Community hub content categories](../community-hub.md#bkmk_category).
  - If your hierarchy is set to **Display Microsoft and curated community content**, then `curated:false` is ignored.
  - If your hierarchy is set to **Display Microsoft content**, then the `curated:` filter is ignored.