---
title: How to Reset Health
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
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
  
