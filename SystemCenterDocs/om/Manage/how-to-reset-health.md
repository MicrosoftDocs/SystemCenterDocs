---
title: How to Reset Health
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c36ccb4-0957-4879-9627-7603afcd7df0
author:mgoedtel
manager:cfreemanwa
---

# How to Reset Health

Some monitors can set state to critical \(red\), warning \(yellow\), and healthy \(green\). Other monitors are only able to change state to critical or warning and cannot detect that state has returned to healthy. In that situation, the monitor must be reset manually. Administrators can check whether a monitor is type **Manual Reset** in the **Authoring** workspace.  
  
> [!NOTE]  
> Only reset health for a monitor when you are sure that all issues have been resolved.  
  
### To reset health for a monitor  
  
1.  In the **Monitoring** workspace of the Operations console, right\-click an alert, point to **Open**, and then click **Health Explorer**.  
  
2.  In **Health Explorer**, select a monitor, and on the toolbar, click **Reset Health**.  
  
    > [!NOTE]  
    > You may also notice **Recalculate Health** on the toolbar. This function reexamines the health state of a monitor or monitors; however, it only works with monitors that implement **On Demand Detection**. Most monitors do not implement **On Demand Detection**.  
  
    The following message displays: **Resetting the health of a monitor may take several minutes and will not be reflected in the Health Explorer immediately. The health state of some monitors cannot be reset and will not be updated as a result of this request. Do you wish to continue?**  
  
3.  If you are sure that you want to reset the monitor, click **Yes**.  
  
4.  Return to the Monitoring workspace, right\-click the alert, point to **Set Resolution State**, and click **Closed**.  
  
## See Also  
[How Heartbeats Work in Operations Manager](How-Heartbeats-Work.md)  