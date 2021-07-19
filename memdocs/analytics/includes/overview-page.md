---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 06/30/2020

---
<!--Don't apply H2 in this include file since they are context driven by article. Used in scores.md, enroll-configmgr.md and enroll-intune.md files -->

- The **Endpoint analytics score** is a 50/50 weighted average of the [**Recommended software**](../recommended-software.md) and [**Startup performance scores**](../startup-performance.md). We'll be expanding the set of subscores over time.

- You can compare your current score to other scores by setting a baseline.
  - There's a built-in baseline for **All organizations (median)** to see how you compare to a typical enterprise. You can create new baselines based on your current metrics so you can track progress or view regressions over time. For more information, see [baseline settings](../settings.md#bkmk_baselines).
   - Baseline markers are shown for your overall score and subscores. If any of the scores have regressed by more than the configurable threshold from the selected baseline, the score is displayed in red and the top-level score is flagged as needing attention.
  - A status of **insufficient data** means you don't have enough devices reporting to provide a meaningful score. We currently require at least five devices.

- **Insights and recommendations** is a prioritized list to improve your score. This list is filtered to the subnode's context when you navigate to **Best practices** or **Recommended software**.

[![Endpoint analytics overview page](../media/overview-page.png)](../media/overview-page.png#lightbox)
