---
title: How to create and remove update exemptions for resources in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1ed9144-fcac-401b-bee8-179a12e76fac
---
# How to create and remove update exemptions for resources in VMM
The procedures in this topic explain how to create an update exemption that prevents an update from being installed on a server managed by [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], and how to remove the exemption so that the update can be installed in the next update remediation.

When an administrator creates an update exemption for a managed computer, the computer remains accountable to an assigned baseline while it is exempted from a particular update in the baseline.

The most common reason for creating an update exemption is that a specific update has placed a managed computer in an unhealthy state. The administrator uninstalls the update, which returns the computer to a healthy state, and wants to prevent the update from being reinstalled until the issues can be identified and resolved so that the update can be installed without placing the computer in an unhealthy state.

Because the update was removed out of band, the computer's update status in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] remains **Compliant** until the computer is again scanned for update compliance. The next scan will change the computer's status to **Non Compliant**. To prevent an accidental reinstallation of that update before the issues are resolved, and to provide a valid business justification, the administrator adds an update exemption to the baseline. After the issues are resolved on the computer, the administrator removes the exemption so that the update will be installed during the next update remediation.

### To create an update exemption for a resource

1.  Open the **Fabric** workspace.

2.  Display **Compliance** view of the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] fabric. To display **Compliance** view, on the **Home** tab, in the **Show** group, click **Compliance**.

3.  On the **Fabric** pane, expand **Servers**, navigate to the server that is to be exempted from the update, and click the server to select it.

    The results pane displays the update baselines that have been assigned to the server.

4.  In the results pane, expand the update baseline that contains the update from which you want to exempt the server. Then click the update to select it.

5.  On the **Home** tab, in the **Compliance** group, click **Compliance Properties**.

    The **Compliance Properties** dialog box opens.

6.  Select the update or updates to include in the exemption and then click **Create** to open the **Create Exemption** dialog box.

7.  In **Notes**, enter information about the reason, intended duration of the exemption, contact person, and so forth. For example, you might enter the following notes: "Exempt through 03\/15\/2015 to resolve issues with MyService.exe interactions."

8.  Click **Create**.

    In **Compliance Properties** dialog box, the status of the update or updates changes to **Exempt**. The update will not be applied to the resource during update remediations until the exemption is removed.

After you remove an update exemption from a resource, you should scan the resource for compliance and then perform update remediation to bring the resource back into a compliant state. The following procedure explains how to perform this process.

### To remove an update exemption from a resource

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Compliance**.

3.  On the **Fabric** pane, expand **Servers**, navigate to the server for which the exemption was created.

4.  In the results pane, expand the update baseline that contains the exemption, and then in the **Compliance** group, click **Compliance Properties**.

5.  In the **Compliance Properties** dialog box, select the exemption or exemptions to be removed and click **Delete** and then click **Yes** to confirm.

    After the exemption is removed, the status of the update changes to **Unknown**. You should perform a compliance scan on the resource to update the compliance status, and then perform update remediation to bring the resource into compliance.

6.  Click **OK** to close the **Compliance Properties** dialog box.

7.  To perform a compliance scan on a server, in the results pane, click the server to select it. Then, on the **Home** tab, in the **Compliance** group, click **Scan**.

    The statuses of the update, the update baseline, and the server change to **Non Compliant**.

8.  To return the server to a **Compliant** state, in the results pane, select the update, the update baseline, or the server that is in a **Non Compliant** state. Then, on the **Home** tab, in the **Compliance** group, click **Remediate**. For more information about performing an update remediation, see [Performing update remediation in VMM](../Topic/Performing-update-remediation-in-VMM.md).

## See Also
[Managing fabric updates in VMM](../Topic/Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

