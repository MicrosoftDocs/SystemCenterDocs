---
title: How to Change Credentials for the System Center Management Configuration service and System Center Data Access service
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d15a2b53-7911-4558-a302-c92212ff124e
---
# How to Change Credentials for the System Center Management Configuration service and System Center Data Access service
During the installation of [!INCLUDE[om12long](Token/om12long_md.md)], you are prompted for credentials for the System Center Configuration service and System Center Data Access service. If you want to change the password for the credentials that you provided or use a different set of credentials, use the following procedure.

> [!NOTE]
> The same credentials must be used for both services.

### To change credentials or password for the System Center Configuration service and System Center Data Access service

1.  On the computer hosting the management server, on the Windows desktop, click **Start**, and then click **Run**.

2.  In the **Run** dialog box, type **services.msc**, and then click **OK**.

3.  In the list of services, right\-click **System Center Data Access Service**, and then click **Properties**.

4.  In the **System Center Data Access Properties** dialog box, click the **Log On** tab.

5.  Enter new credentials or change the password of the existing credentials, and then click **OK**.

6.  In the list of services, right\-click **System Center Management Configuration**, and then click **Properties**.

7.  In the **System Center Management Configuration Properties** dialog box, click the **Log On** tab.

8.  Enter new credentials or change the password of the existing credentials, and then click **OK**.

9. Stop and restart both the **System Center Data Access** service and **System Center Management Configuration** service.

## See Also
[Making Changes to an Operations Manager for System Center 2012 Environment](assetId:///22675bc3-1668-44c7-bc40-484e06a01946)
[How to Change the Credentials for the Action Account](assetId:///df996b1d-ffc4-4840-b34b-a287ce4dd041)


