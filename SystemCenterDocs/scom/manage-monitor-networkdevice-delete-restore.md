---
title: How to Delete or Restore a Network Device in Operations Manager
description: This article describes how to delete or restore a network devices monitored by Operations Manager.   
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 01/25/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 85dae573-5813-4fd1-b81a-6a05f6e1cb7f
---

# How to delete or restore a network device in Operations Manager

After System Center 2016 - Operations Manager has discovered and is monitoring a network device, you might want to stop monitoring the device because it is being replaced or because there is no business value in monitoring that particular device or for any other reason. To stop monitoring a device, you can use maintenance mode or you can delete the network device from the discovery rule. You can also restore a deleted device that was discovered by a recursive discovery rule.  
  
To delete a device that is the starting point for recursive discovery, you must first delete the discovery rule or remove the device from the discovery rule.  
  
> [!NOTE]  
> You can identify the discovery rule associated with a discovered network device by right-clicking the device in **Network Devices** or **Network Devices Pending Management** and then clicking **Discovery Rule Properties**.  
  
If you delete a device that was discovered by a recursive discovery rule, it will be added to the exclude list of the rule. If you want to have that device discovered and monitored again, you must remove the device from the **Exclude Filters** page of the rule's properties and run the discovery again.  
  
## To delete a network device discovered by explicit discovery  
  
1.  In the Operations console, select the **Administration** workspace.  
  
2.  Click **Network Devices**, right-click the device that you want to delete, and then click **Delete**.  
  
    > [!NOTE]  
    > You can select multiple devices to delete.  
  
## To delete a network device specified in a recursive discovery rule  
  
1.  In the Operations console, select the **Administration** workspace.  
  
2.  Open **Properties** for the discovery rule and remove the device on the **Devices** page.  
  
## To delete a network device discovered by recursive discovery  
  
1.  In the Operations console, select the **Administration** workspace.  
  
2.  Click **Network Devices** in **Network Management**.  
  
3.  In the **Network Devices** pane, right-click a device that was discovered by recursive discovery, and then select **Delete**.  
  
4.  You will be prompted with a message asking you to confirm that you want to stop monitoring the selected network device. Click **Yes**.  
  
5.  Click **Discovery Rules**.  
  
6.  Right-click the recursive discovery rule, and then select **Properties**.  
  
7.  Click **Exclude Filters**.  
  
8.  Verify that an exclude filter has been created for the deleted device. This may take a few minutes to occur.  
  
### To restore a network device that was deleted from recursive discovery  
  
1.  In the Operations console, select the **Administration** workspace.  
  
2.  Click **Discovery Rules**.  
  
3.  Right-click the recursive discovery rule, and then select **Properties**.  
  
4.  Click **Exclude Filters**.  
  
5.  Click the network device and then click **Remove**.  
  
6.  Click **Summary**, and then click **Save** to save and close the discovery rule.  
  
7.  With the discovery rule selected, click **Run** in the **Actions** pane to rerun the discovery rule.  
  
    Note the status of the rule as it runs and wait until it shows a blank status.  
  
8.  Verify that the device is rediscovered. This may take a few minutes to a few hours depending on the number of devices in the environment. You can view the status of the discovery rule to determine when it has completed.  
  
## Next steps

- To understand how to configure what to monitor and alert with your network devices, see [How to configure monitoring of network devices](manage-monitor-networkdevice-configure-monitoring.md).  

- To view information about the network devices you are monitoring, see [Viewing Network Devices and Data in Operations Manager](manage-monitor-networkdevice-viewing-data.md).  

