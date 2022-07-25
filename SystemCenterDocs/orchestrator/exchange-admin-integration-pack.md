---
title: Exchange Admin Integration Pack for Orchestrator in System Center
description: This article provides information about exchange Integration packs and how to deploy it.
ms.custom: na
ms.date: 007/25/2022
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3d807dc8-013d-45da-9647-825ab64aba2a
author: jyothisuri
ms.author: jsuri
manager: carmonm
---

# Exchange Admin Integration Pack for Orchestrator in System Center

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

Integration packs are add-ons for System Center - Orchestrator, a component of System Center. Integration packs help to optimize IT operations across heterogeneous environments. They enable you to design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and other third-party products.

The Integration Pack for Exchange Admin helps to facilitate the automation of Exchange administration tasks, such as mailbox management, for on-premise, remote, or cloud-based environments in Microsoft Exchange and Microsoft 365.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information about Orchestrator-related privacy, see the [System Center Orchestrator Privacy Statement](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## System requirements

Before you implement the Integration Pack for Exchange Admin, the following listed software must be installed. For more information about installing and configuring Orchestrator and the Exchange Admin Integration Pack, refer to the respective product documentation.

::: moniker range="<=sc-orch-2019"
-   System Center 2016 integration packs require System Center 2016 - Orchestrator
-   System Center 2019 integration packs require System Center 2019 - Orchestrator
-   Microsoft .NET Framework 3.5 Service Pack 1
-   Microsoft Exchange 2010 Service Pack 2 or Microsoft Exchange 2012 or Microsoft Exchange Online/Microsoft 365
-   Microsoft Exchange Management Shell
-   Microsoft PowerShell 2.0
-   Microsoft WinRM 2.0
::: moniker-end

::: moniker range="sc-orch-2022"
-   System Center 2022 integration packs require System Center 2022 - Orchestrator
-   Microsoft .NET Framework 3.5 Service Pack 1
-   Microsoft Exchange 2010 Service Pack 2 or Microsoft Exchange 2012 or Microsoft Exchange Online/Microsoft 365
-   Microsoft Exchange Management Shell
-   Microsoft PowerShell 2.0
-   Microsoft WinRM 2.0
-   Exchange Online PowerShell V2 Module (EXO V2) for Exchange Online
::: moniker-end

## Downloading the Integration Pack

::: moniker range="<=sc-orch-2019"
- To download the Exchange Admin Integration Pack for Orchestrator 2016, see the [Microsoft Download Center for 2016](https://www.microsoft.com/download/details.aspx?id=54098).

- To download the Exchange Admin Integration Pack for Orchestrator 2019, see the [Microsoft Download Center for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all).
::: moniker-end

::: moniker range="sc-orch-2022"

- To download the Exchange Admin Integration Pack for Orchestrator 2022, see the [Microsoft Download Center for 2022](https://www.microsoft.com/download/details.aspx?id=104335).

::: moniker-end

## Register and Deploy the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How to add an Integration Pack](how-to-add-an-integration-pack.md).

## Configure the Exchange Admin Integration Pack connections

A connection establishes a reusable link between the Orchestrator and an Exchange server. You can specify as many connections as you require to create links to multiple servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

#### [Exchange on-premises](#Exchange/on-prem)

### Set up an Exchange Configuration connection

1. In the **Orchestrator Runbook Designer**, select **Options** > **Exchange Admin**. The **Exchange Admin** dialog appears.
2. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.
3. In the **Name** box, enter a name for the connection. This can be the name of the **Exchange** server or a descriptive name to differentiate the type of connection.
4. Select the **(...)** button and select **Exchange Configuration**.
5. Select the **(...)** button for **Exchange Environment** and select **On-Premise**. 
6. In the **Exchange Server Host** box, enter the name or IP address of the Exchange server. To use a computer name, you can type the *NetBIOS* name or the *fully qualified domain name (FQDN)*.
7. In the **Exchange Server Port** box, enter the port that is used to communicate with the Exchange server. If you use SSL, be sure to select the appropriate port.
8. In the **Exchange PowerShell Application** box, enter the application name segment of the connection URI.
9.  In the **Exchange User Name** and **Exchange User Password** boxes, enter the credentials that Orchestrator will use to log on to the Exchange environment. The configured user must have the appropriate Exchange permissions.
10.  Configure the **Exchange Environment** as necessary for connecting to an On-Premise installation or to Office.
11. Set the **Use SSL** property to **True** to have all communication between the runbook server and the Exchange server encrypted over HTTPS.
12. If you use SSL, 
    - The **Skip CA Check** property specifies whether the client does not validate that the server certificate is signed by a trusted certification authority (CA).
    - The **Skip CN Check** property specifies that the certificate common name (CN) of the server does not need to match the hostname of the server.
    - The **Skip Revocation Check** property specifies whether the revocation status of the server certificate will not be checked for validity.
13. Select **OK** and add additional connections if applicable.
14. Select **Finish**.

#### [Exchange Online](#Exchange/online)

Configure IP with Exchange Online.

Exchange Admin 2022 supports only [App-only](/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps) based modern authentication to Exchange Online. 
To setup app-only authentication, follow the steps mentioned [here](/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps#set-up-app-only-authentication). 

1. In the **Orchestrator Runbook Designer**, select **Options** > **Exchange Admin**. The **Exchange Admin** dialog appears.
2. In the **Name** box, enter a name for the connection. This can be the name of the **Exchange** server or a descriptive name to differentiate the type of connection.
3. Click the **(...)** button and select **Exchange Configuration**.
4. Click the **(...)** button for **Exchange Environment** box and select **Online**. Below are the four parameters that are mandatory: 
   - **CertificateFilePath**
   - **CertificatePassword**
   - **ApplicationId**
   - **EXOOrganization**. 
The other parameters can be kept blank. 
5. For **CertificateFilePath**, provide the path to where *pfx* file is stored locally. The *pfx* file should be generated from the certificate file while setting up App-only authentication. 
   >[!Note]
   >Path provided should be case sensitive. 
6. For **CertificatePassword**, provide the password with which the *pfx* file was generated. 
7. For **ApplicationId**, provide your Azure App ID generated above. 
8. For **EXOOrganization**, provide details in the format <organization name>**.onmicrosoft.com** 
   :::image type="exchange admin" source="media/exchange-admin-integration-pack/exchange-admin.png" alt-text="Screenshot showing exchange admin prerequisite configuration screen.":::
   
---

## Configure Windows PowerShell and WinRM for the Exchange Admin Integration Pack

#### [Exchange on-premises](#Exchange/on-prem)

### Configure 64-bit PowerShell to run scripts

On the computer where Orchestrator runbooks are executed, ensure that 64-bit PowerShell scripts can be run:

1.  Start **Windows PowerShell** command line.
2.  To determine whether PowerShell 64-bit scripts can be executed, run the following command:

    ```PowerShell
        Get-ExecutionPolicy
    ```

3.  If **Execution Policy** is **Restricted**, you must change it to **RemoteSigned**. Run the following command:

    ```PowerShell
        Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

### Configure remote PowerShell rights for the Exchange user

The configured user must be granted remote PowerShell rights on the Exchange server.

1.  On the Exchange server, start the **Exchange Management Shell**.
2.  To determine whether the user has remote PowerShell rights, run the following command and check the value in the **RemotePowerShellEnabled** field:

  ```PowerShell
        Get-User <UserName>
  ```

3.  To grant the user remote PowerShell rights, run the following command:

  ```PowerShell
        Set-User <UserName> -RemotePowerShellEnabled $true
  ```

### Configure Windows PowerShell to allow Basic Authentication on the Exchange server

1.  On the Exchange server, make sure that PowerShell Basic Authentication is enabled:
2.  Start **Internet Information Services (IIS) Manager**.
3.  Navigate to the **PowerShell** site.
4.  Open the **Authentication** settings.
5.  Ensure **Basic Authentication** is enabled.

### Configure WinRM for HTTP unencrypted communication

On the machine where Orchestrator runbooks are executed, configure WinRM trusted hosts and to allow unencrypted traffic:

1.  Open the **Local Group Policy** user interface: Windows Start Button &gt; Run &gt; gpedit.msc.
2.  Navigate to **Local Computer Policy** &gt; **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Windows Remote Management (WinRM)** &gt; **WinRM Client**.
3.  Ensure that **Allow unencrypted traffic** is enabled.
4.  Add the targeted computer that runs Exchange Server to the **Trusted Hosts** list.

On the Exchange server, ensure that PowerShell does not require SSL:

1.  Start **Internet Information Services (IIS) Manager**.
2.  Navigate to the **PowerShell** site.
3.  Open **SSL Settings**.
4.  Ensure that the **Require SSL** checkbox is not selected.

#### [Exchange Online](#Exchange/online)

Due to the [deprecation](https://techcommunity.microsoft.com/t5/exchange-team-blog/basic-authentication-deprecation-in-exchange-online-may-2022/ba-p/3301866) of Basic Auth in Exchange Online, Exchange Admin 2022 Integration Pack for System-Center now uses [Exchange Online PowerShell	V2 Module (EXO V2)](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps) to connect to Exchange Server. For detailed information on EXO V2 Module, see
 - [Prerequisites](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps#prerequisites-for-the-exo-v2-module)
 - [Installation instructions](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps#install-the-exo-v2-module) and
 - [Troubleshooting installation issues](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps#troubleshoot-installing-the-exo-v2-module)

---

