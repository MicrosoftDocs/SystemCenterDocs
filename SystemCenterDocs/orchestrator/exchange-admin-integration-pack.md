---
title: Exchange Admin Integration Pack for Orchestrator in System Center
description: This article provides information about exchange Integration packs and how to deploy it.
ms.date: 11/19/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 3d807dc8-013d-45da-9647-825ab64aba2a
author: jyothisuri
ms.author: jsuri
---

# Exchange Admin Integration Pack for Orchestrator in System Center

Integration packs are add-ons for System Center - Orchestrator, a component of System Center. Integration packs help to optimize IT operations across heterogeneous environments. They enable you to design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and other third-party products.

The Integration Pack for Exchange Admin helps to facilitate the automation of Exchange administration tasks, such as mailbox management, for on-premises, remote, or cloud-based environments in Microsoft Exchange and Microsoft 365.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more information about Orchestrator-related privacy, see the [System Center Orchestrator Privacy Statement](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## System requirements

Before you implement the Integration Pack for Exchange Admin, you must install the following software. For more information on how to install and configure Orchestrator and the Exchange Admin Integration Pack, see the respective product documentation.

::: moniker range="<=sc-orch-2019"
- System Center 2016 integration packs require System Center 2016 - Orchestrator
- System Center 2019 integration packs require System Center 2019 - Orchestrator
- Microsoft .NET Framework 4.7 or above
- Microsoft Exchange 2010 Service Pack 2 or Microsoft Exchange 2012 or Microsoft Exchange Online/Microsoft 365
- Microsoft Exchange Management Shell
- Microsoft PowerShell 2.0
- Microsoft WinRM 2.0

> [!IMPORTANT]
>
> 1. Exchange Admin Integration Pack (v10.19.16.0 or above) targets .NET Framework 4.5.2. Ensure
>    that .NET Framework Runtime v4.5.2 or later is installed on Runbook Designer and Runbook Server
>    machines. We recommend installing the latest available .NET framework version.
> 2. Create the following files with (identical) contents as shown below to update
>    `supportedRuntimeVersion` to v4:
>    - `%systemdrive%/Program Files (x86)/Microsoft System Center/Orchestrator/Runbook Designer/RunbookDesigner.exe.config`
>    - `%systemdrive%/Program Files (x86)/Microsoft System Center/Orchestrator/Runbook Designer/RunbookTester.exe.config`
>    - `%systemdrive%/Program Files (x86)/Microsoft System Center/Orchestrator/Runbook Server/PolicyModule.exe.config`
>
>    Contents:
>
>    ```xml
>    <?xml version="1.0" encoding="utf-8"?>
>    <configuration>
>      <startup useLegacyV2RuntimeActivationPolicy="true">
>        <supportedRuntime version="v4.0.30319"/>
>      </startup>
>      <system.xml.serialization>
>        <xmlSerializer tempFilesLocation="C:\ProgramData\Microsoft System Center 2012\Orchestrator\Activities\XmlSerializers\"/>
>      </system.xml.serialization>
>    </configuration>
>    ```

::: moniker-end

::: moniker range="sc-orch-2022"

# [Exchange on-premises](#tab/exchan-on-prem)

- System Center 2022 integration packs require System Center 2022 - Orchestrator
- Microsoft .NET Framework 4.0 or higher (.NET 4.7.2 recommended)
- Microsoft Exchange 2010 Service Pack 2 or Microsoft Exchange 2012 or Microsoft Exchange Online/Microsoft 365
- Microsoft Exchange Management Shell
- Microsoft PowerShell
- Microsoft WinRM 2.0

# [Exchange Online](#tab/exchan-online)

- System Center 2022 integration packs require System Center 2022 - Orchestrator
- Microsoft .NET Framework 4.0 or higher (.NET 4.7.2 recommended)
- Microsoft Exchange 2010 Service Pack 2 or Microsoft Exchange 2012 or Microsoft Exchange Online/- Microsoft 365
- Microsoft Exchange Management Shell
- Microsoft PowerShell
- Microsoft WinRM 2.0
- Exchange Online PowerShell V3 Module ([EXO V3](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps&preserve-view=true)); you must [upgrade from EXO V2 to EXO V3](https://techcommunity.microsoft.com/t5/exchange-team-blog/announcing-deprecation-of-remote-powershell-rps-protocol-in/ba-p/3695597) for this IP.

---

::: moniker-end

## Download the Integration Pack

::: moniker range="<=sc-orch-2019"
- To download the Exchange Admin Integration Pack for Orchestrator 2016, see the [Microsoft Download Center for 2016](https://www.microsoft.com/download/details.aspx?id=54098).

- To download the Exchange Admin Integration Pack for Orchestrator 2019, see the [Microsoft Download Center for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all).
::: moniker-end

::: moniker range="sc-orch-2022"

- To download the Exchange Admin Integration Pack for Orchestrator 2022, see the [Microsoft Download Center for 2022](https://www.microsoft.com/download/details.aspx?id=104335).

::: moniker-end

::: moniker range=">=sc-orch-2025"

Exchange Admin Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the Exchange Admin Integration Pack [here](https://www.microsoft.com/download/details.aspx?id=104335).

::: moniker-end

## Register and Deploy the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to runbook servers and Runbook Designers. For the procedures on installing integration packs, see [How to add an Integration Pack](how-to-add-an-integration-pack.md).

## Configure the Exchange Admin Integration Pack connections

A connection establishes a reusable link between the Orchestrator and an Exchange server. You can specify as many connections as you require to create links to multiple servers. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

# [Exchange on-premises](#tab/ex-on-prem)

### Set up an Exchange Configuration connection

1. In the **Orchestrator Runbook Designer**, select **Options** > **Exchange Admin**. The **Exchange Admin** dialog appears.
2. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.
3. In the **Name** box, enter a name for the connection. This can be the name of the **Exchange** server or a descriptive name to differentiate the type of connection.
4. Select the **(...)** button and select **Exchange Configuration**.
5. Select the **(...)** button for **Exchange Environment** and select **On-Premise**. 
6. In the **Exchange Server Host** box, enter the name or IP address of the Exchange server. To use a computer name, you can enter the *NetBIOS* name or the *fully qualified domain name (FQDN)*.
7. In the **Exchange Server Port** box, enter the port that is used to communicate with the Exchange server. If you use SSL, ensure to select the appropriate port.
8. In the **Exchange PowerShell Application** box, enter the application name segment of the connection URI.
9. In the **Exchange User Name** and **Exchange User Password** boxes, enter the credentials that Orchestrator will use to sign in to the Exchange environment. The configured user must have the appropriate Exchange permissions.
10. Configure the **Exchange Environment** as necessary for connecting to an on-premises installation or to Office.
11. Set the **Use SSL** property to **True** to have all communication between the runbook server and the Exchange server encrypted over HTTPS.
12. If you use SSL:
    - The **Skip CA Check** property specifies whether the client doesn't validate that the server certificate is signed by a trusted certification authority (CA).
    - The **Skip CN Check** property specifies that the certificate common name (CN) of the server doesn't need to match the hostname of the server.
    - The **Skip Revocation Check** property specifies whether the revocation status of the server certificate won't be checked for validity.
13. Select **OK** and add additional connections if applicable.
14. Select **Finish**.

# [Exchange Online](#tab/exch-online)

**Configure IP with Exchange Online:**

Exchange Admin 2022 supports [App-only](/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps&preserve-view=true) based modern (OAuth) authentication to Exchange Online.
For more information on setting up app-only authentication for Exchange Online to provision an Azure AD application in your tenant, see [setup app-only authentication](/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps#set-up-app-only-authentication&preserve-view=true). 

1. In the **Orchestrator Runbook Designer**, select **Options** > **Exchange Admin**. The **Exchange Admin** dialog appears.
2. In the **Name** box, enter a name for the connection. This can be the name of the **Exchange** server or a descriptive name to differentiate the type of connection.
3. Select the **(...)** button and select **Exchange Configuration**.
4. Select the **(...)** button for **Exchange Environment** box and select **Online**. While the other parameters are optional, below are the four mandatory parameters: 
   - **CertificateFilePath** - provide the path to store the `pfx` file locally. The `pfx` file was generated while setting up App-only authentication.
     >[!Note]
     >**CertificateFilePath** is case sensitive.
   - **CertificatePassword** - provide the password with which the `pfx` file was generated.
   - **ApplicationId** - provide your Azure App ID generated above.
   - **EXOOrganization** - provide details in the format `<organization name>.onmicrosoft.com`

   :::image type="exchange admin" source="media/exchange-admin-integration-pack/exchange-admin-inline.png" alt-text="Screenshot showing exchange admin prerequisite configuration screen." lightbox="media/exchange-admin-integration-pack/exchange-admin-expanded.png":::

---

## Configure Windows PowerShell and WinRM for the Exchange Admin Integration Pack

# [Exchange on-premises](#tab/exch-on-prem)

### Configure PowerShell to run scripts

On the computer where Orchestrator runbooks are executed, ensure that PowerShell scripts can be run:

1. Start the **Windows PowerShell** command line.
2. To determine whether PowerShell scripts can be executed, run the following command:

    ```PowerShell
        Get-ExecutionPolicy
    ```

3. If **Execution Policy** is **Restricted**, you must change it to **RemoteSigned**. Run the following command:

    ```PowerShell
        Set-ExecutionPolicy -ExecutionPolicy RemoteSigned
    ```

### Configure remote PowerShell rights for the Exchange user

The configured user must be granted remote PowerShell rights on the Exchange server.

1. On the Exchange server, start the **Exchange Management Shell**.
2. To determine whether the user has remote PowerShell rights, run the following command, and check the value in the **RemotePowerShellEnabled** field:

  ```PowerShell
        Get-User <UserName>
  ```

3. To grant the user remote PowerShell rights, run the following command:

  ```PowerShell
        Set-User <UserName> -RemotePowerShellEnabled $true
  ```

### Configure Windows PowerShell to allow Basic Authentication on the Exchange server

On the Exchange server, ensure that PowerShell Basic Authentication is enabled:

1. Start **Internet Information Services (IIS) Manager**.
2. Navigate to the **PowerShell** site.
3. Open the **Authentication** settings, and ensure **Basic Authentication** is enabled.

### Configure WinRM for HTTP unencrypted communication

On the machine where Orchestrator runbooks are executed, configure WinRM trusted hosts, and to allow unencrypted traffic:

1. Open the **Local Group Policy** user interface: Windows Start Button &gt; Run &gt; gpedit.msc.
2. Navigate to **Local Computer Policy** &gt; **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Windows Remote Management (WinRM)** &gt; **WinRM Client**.
3. Ensure that **Allow unencrypted traffic** is enabled.
4. Add the targeted computer that runs Exchange Server to the **Trusted Hosts** list.

On the Exchange server, ensure that PowerShell doesn't require SSL:

1. Start **Internet Information Services (IIS) Manager**.
2. Navigate to the **PowerShell** site.
3. Open **SSL Settings** and ensure that the **Require SSL** checkbox isn't selected.

# [Exchange Online](#tab/ex-online)

Due to the [deprecation](https://techcommunity.microsoft.com/t5/exchange-team-blog/announcing-deprecation-of-remote-powershell-rps-protocol-in/ba-p/3695597#:~:text=Starting%20today%2C%20RPS%20use%20through%20running%20New-PSSession%20cmdlet,module%20deprecation%20will%20be%20completed%20by%20July%202023.) of Basic Auth in Exchange Online, Exchange Admin 2022 Integration Pack for System-Center now uses [Exchange Online PowerShell V3 Module (EXO V3)](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps&preserve-view=true) to connect to Exchange Server. For detailed information on EXO V3 module, see:
 - [Prerequisites](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps#prerequisites-for-the-exo-v2-module&preserve-view=true)
 - [Installation instructions](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps#install-the-exo-v2-module&preserve-view=true)
 - [Troubleshooting installation issues](/powershell/exchange/exchange-online-powershell-v2?view=exchange-ps#troubleshoot-installing-the-exo-v2-module&preserve-view=true)

---
