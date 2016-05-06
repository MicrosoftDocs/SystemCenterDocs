---
title: How to Delete or Restore a Network Device in Operations Manager_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d9f871f-438e-4fd2-8c0c-13d8ba1a4ac8
---
# How to Delete or Restore a Network Device in Operations Manager_1
After [!INCLUDE[om12long](Token/om12long_md.md)] has discovered and is monitoring a network device, you might want to stop monitoring the device because it is being replaced or because there is no business value in monitoring that particular device or for any other reason. To stop monitoring a device, you can use maintenance mode or you can delete the network device from the discovery rule. You can also restore a deleted device that was discovered by a recursive discovery rule.

To delete a device that is the starting point for recursive discovery, you must first delete the discovery rule or remove the device from the discovery rule.

> [!NOTE]
> You can identify the discovery rule associated with a discovered network device by right\-clicking the device in **Network Devices** or **Network Devices Pending Management** and then clicking **Discovery Rule Properties**.

If you delete a device that was discovered by a recursive discovery rule, it will be added to the exclude list of the rule. If you want to have that device discovered and monitored again, you must remove the device from the **Exclude Filters** page of the rule’s properties and run the discovery again.

### To delete a network device discovered by explicit discovery

1.  In the Operations console, select the **Administration** workspace.

2.  Click **Network Devices**, right\-click the device that you want to delete, and then click **Delete**.

    > [!NOTE]
    > You can select multiple devices to delete.

### To delete a network device specified in a recursive discovery rule

1.  In the Operations console, select the **Administration** workspace.

2.  Open **Properties** for the discovery rule and remove the device on the **Devices** page.

### To delete a network device discovered by recursive discovery

1.  In the Operations console, select the **Administration** workspace.

2.  Click **Network Devices** in **Network Management**.

3.  In the **Network Devices** pane, right\-click a device that was discovered by recursive discovery, and then select **Delete**.

4.  You will be prompted with a message asking you to confirm that you want to stop monitoring the selected network device. Click **Yes**.

5.  Click **Discovery Rules**.

6.  Right\-click the recursive discovery rule, and then select **Properties**.

7.  Click **Exclude Filters**.

8.  Verify that an exclude filter has been created for the deleted device. This may take a few minutes to occur.

### To restore a network device that was deleted from recursive discovery

1.  In the Operations console, select the **Administration** workspace.

2.  Click **Discovery Rules**.

3.  Right\-click the recursive discovery rule, and then select **Properties**.

4.  Click **Exclude Filters**.

5.  Click the network device and then click **Remove**.

6.  Click **Summary**, and then click **Save** to save and close the discovery rule.

7.  With the discovery rule selected, click **Run** in the **Actions** pane to rerun the discovery rule.

    Note the status of the rule as it runs and wait until it shows a blank status.

8.  Verify that the device is rediscovered. This may take a few minutes to a few hours depending on the number of devices in the environment. You can view the status of the discovery rule to determine when it has completed.

## See Also
[Monitoring Networks by Using Operations Manager](Monitoring-Networks-by-Using-Operations-Manager.md)
[How to Discover Network Devices in Operations Manager](How-to-Discover-Network-Devices-in-Operations-Manager.md)
[Network Device Discovery Settings](Network-Device-Discovery-Settings.md)
[Run As Accounts for Network Monitoring in Operations Manager](Run-As-Accounts-for-Network-Monitoring-in-Operations-Manager.md)
[Tuning Network Monitoring](Tuning-Network-Monitoring.md)
[Viewing Network Devices and Data in Operations Manager](Viewing-Network-Devices-and-Data-in-Operations-Manager.md)
[Security for Servers Performing Network Discovery](Security-for-Servers-Performing-Network-Discovery.md)
[Network Devices Supported for Discovery by Operations Manager](Network-Devices-Supported-for-Discovery-by-Operations-Manager.md)
[Reports for Network Monitoring in Operations Manager](Reports-for-Network-Monitoring-in-Operations-Manager.md)


