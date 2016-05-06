---
title: Adding an Azure subscription in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6805c8cf-d768-4680-9990-2b8c895f31ec
---
# Adding an Azure subscription in VMM
Withthe Add Azure Subscription feature, administrators of [!INCLUDE[vmm12sp1_long]./Token/vmm12sp1_long_md.md)] can add Microsoft Azure subscriptions to VMM and perform basic actions on Azure instances in those subscriptions. For each Azure subscription you add, you can use a console to see all role instances in all Deployment Groups in that subscription.

## What you can do with this feature
If you already manage your on\-premise virtual machines in VMM, you can use this feature to perform some very basic actions on Azure instances without leaving the VMM console. You can:

-   Add and Remove one or more Azure subscriptions by using the VMM console.

-   See a list view with details and status of all role instances in all Deployments in that subscription.

-   Manually refresh the list of instances.

-   Perform basic actions on the instances:

    -   Start

    -   Stop

    -   Shutdown

    -   Restart

    -   Connect via RDP

Later sections provide more details about these actions.

## What you can't do with this feature
This feature is not intended to provide feature parity with the Microsoft Azure Management Portal. The functionality of this feature is a small subset of the features at [https://manage.windowsazure.com](https://manage.windowsazure.com), but you can view your instances and do other basic actions, to simplify everyday tasks and help make management easier.

You cannot:

-   Manage your Azure subscription

-   Deploy instances to Azure

-   Migrate on\-premise virtual machines to Azure

-   Manage Azure Storage

-   Manage Azure Networks

-   See the Dashboard Summary view

-   See the Performance Monitoring Summary

## <a name="BKMK_requirements"></a>System and Environment Requirements
The following is a list of system and environment requirements that are needed in order to be able to install and evaluate this feature.

|Item|Requirements|
|--------|----------------|
|Internet connectivity|The console computer where this feature will be installed must have connectivity to the Internet in order to connect to the Azure Subscription.|
|Azure Subscription|You will need to have an Azure Subscription in order to be able to add it to the VMM console. If you want to evaluate the Azure instance actions functionality, you will need to have one or more Azure instances deployed in that subscription.|
|Service Administrator|To perform this action, you must be at least a **Service Administrator** for the Microsoft Azure Subscription being added. This provides access to the Management Certificate information required to complete this operation.|
|Management Certificate in Azure|The Microsoft Azure Subscription must have a **Management Certificate** associated with it in order to allow VMM to use the service management API in Microsoft Azure. For information about how to configure this, see [Create and Upload a Management Certificate for Azure](http://msdn.microsoft.com/library/azure/gg551722.aspx). Make note of your subscription ID and the certificate thumbprint, because you will need it during configuration.<br /><br />Microsoft Azure requires certificates to be x509 v3 compliant.|
|Management Certificate in the local certificate Store|The Management Certificate that is associated with the Azure Subscription must be present in the local certificate store on the computer that the wizard is being run on. The certificate needs to be present in the **Current User \\ Personal** store of the computer running the VMM console.|

## Using the Add Azure Subscription Feature

### Review the ribbon
In the VMM console, open the **VMs and Services** workspace, and look on the ribbon for the **Azure** group, where **Add Subscription** appears.

![/Image/VMM-R2-UR6-AddAzureSub01.jpg)

**Figure 1: The Azure "Add Subscription" button in the VMM console**

### Configure certificates
Before you try to add a subscription, it's a good idea to check a few things, such as your certificates, to make sure you're ready. You might want to review [System and Environment Requirements](./Adding-an-Azure-subscription-in-VMM.md#BKMK_requirements), earlier in this document. Also, the following procedure provides details about how to review requirements.

##### To review requirements before you add a subscription

1.  Confirm that you're a Service Administrator on the Subscription that you plan to add.

2.  If you already know that you have a Management Certificate associated with your Azure Subscription for Service Management, skip to step 5. Otherwise, start by checking for a certificate:

    1.  Go to [https://manage.windowsazure.com](https://manage.windowsazure.com) and log in with your account.

    2.  Click the Settings link ![/Image/VMM-R2-UR6-AddAzureSub02.jpg) to access your subscription information.

    3.  On the Settings pages, click the MANAGEMENT CERTIFICATES link on the Settings page. If you see a certificate here, make note of the certificate thumbprint, because you will need this later. Then skip to step 5.

3.  If you need to add a certificate to your Azure Subscription, decide whether you can use an existing certificate or whether you need to create a new one. If you need to create a new one, create one by following the steps in [Create a Service Certificate for Azure](http://msdn.microsoft.com/library/azure/gg432987.aspx).

4.  Upload your certificate to Windows Azure:

    1.  In the Azure Portal, in **Settings** > **Management Certificates**, click the **Upload** button. You’ll be prompted for your .cer file \(certificate file\).

        For instructions on importing and exporting certificates and private keys, see [To import a certificate](http://social.technet.microsoft.com/wiki/contents/articles/2167.how-to-use-the-certificates-console.aspx#To_import_certificates) and [To export a certificate](http://social.technet.microsoft.com/wiki/contents/articles/2167.how-to-use-the-certificates-console.aspx#To_export_certificates) in "How to Use the Certificates Console."

    2.  Confirm that the uploaded certificate appears in the list of Management Certificates. Make note of the certificate thumbprint, as you will need this later when you run the **Add Azure Subscription Wizard**.

5.  Import the Management Certificate to the Certificate Store on the computer you’ll be running the VMM console on.

    Make sure you import the certificate to the **Current User \\ Personal** certificate store on the local computer.

    For instructions, see [To import a certificate](http://social.technet.microsoft.com/wiki/contents/articles/2167.how-to-use-the-certificates-console.aspx#To_import_certificates) in "How to Use the Certificates Console."

### <a name="BKMK_wizard"></a>Add Azure Subscription Wizard
If you don't already have your Subscription ID and the thumbprint of the certificate, make sure you gather that information now. You can find both of these pieces of information at the **Azure Management Portal** on the **Settings** > **Management Certificates** page.

![/Image/VMM-R2-UR6-AddAzureSub03.jpg)

**Figure 2: Service Management Certificate Details on the Azure Management Portal**

To start the **Add Azure Subscription Wizard**, in VMM, click the Azure **Add Subscription** button. The wizard is a single page dialog box:

![/Image/VMM-R2-UR6-AddAzureSub04.jpg)

**Figure 3: Add Azure Subscription Wizard**

> [!NOTE]
> Certificates and subscription setting information is stored in the Registry under HKEY\_CURRENT\_USER and is per login specific. This means that subscriptions that are added are visible on a per\-machine, per\-login basis. If users log in to VMM Server using a shared account \(not a recommended best practice by VMM\), and the subscription is added under that account, then the subscription will be exposed to all users. Alternately, Azure subscriptions that are added by one Admin user are not automatically visible to all other VMM Admins. In this case, the process will need to be repeated for all VMM Admins that require access to the Azure Subscription.

### View an Azure subscription
Once you have successfully added the subscription, if you look in the VMM console with the **VMs and Services** workspace open, and you look in the navigation tree under the **Azure Subscriptions** node, you should see the subscription.

![/Image/VMM-R2-UR6-AddAzureSub05.jpg)

**Figure 4: Newly added Azure Subscription**

Selecting the subscription node will display the following context\-sensitive actions in the VMM ribbon:

![/Image/VMM-R2-UR6-AddAzureSub06.jpg)

**Figure 5: Azure Subscription actions in the VMM console ribbon**

|Action\/Button|What it does|
|------------------|----------------|
|Add Subscription|Opens the wizard described in [Add Azure Subscription Wizard](./Adding-an-Azure-subscription-in-VMM.md#BKMK_wizard), earlier in this document. New subscriptions are added to the top level Azure Subscriptions node, rather than underneath the currently selected node.|
|Remove Subscription|Removes the currently selected Azure Subscription. You will be prompted for confirmation.|
|Refresh Virtual Machines|Refreshes the list of virtual machines in the Azure Virtual Machines view.|

### Azure Virtual Machines List View
The **Azure Virtual Machines** view displays a list of the Role Instances in all Deployments in all Resource Groups for the selected Azure Subscription.

![/Image/VMM-R2-UR6-AddAzureSub07.jpg)

**Figure 6: Azure Virtual Machines list view**

### Azure Virtual Machine Details Pane
When an Azure instance is selected in the list, if you look below the list grid view, you can see the **Azure Virtual Machines** details pane. Additional useful information is displayed, such as **DNS name** and the **OS** installed on the instance.

![/Image/VMM-R2-UR6-AddAzureSub08.jpg)

**Figure 7: Virtual machine details pane**

### Virtual Machine Actions
When an individual virtual machine is selected from the list, a set of VM action buttons will appear in the ribbon. The following actions are available:

|Action|Description|
|----------|---------------|
|Start|Starts an instance that is in the stopped state.|
|Stop|Stops a running instance but does not de\-allocate it.|
|Shut Down|Requests a graceful shutdown of a running instance and de\-allocates it.|
|Restart|Requests a restart of a running instance.|
|Connect via RDP|Initiates a remote desktop session to the Host Name \(DNS Name\) of the instance.|

![/Image/VMM-R2-UR6-AddAzureSub09.jpg)

**Figure 8: Virtual Machines Actions**

## See Also
[Creating and deploying virtual machines in VMM](./Creating-and-deploying-virtual-machines-in-VMM.md)
[Creating Virtual Machine Role Templates by using VMM and Windows Azure Pack](./Creating-Virtual-Machine-Role-Templates-by-using-VMM-and-Windows-Azure-Pack.md)



