---
ms.assetid: 61b25aa7-b725-445b-8f4c-40ce213714c2
title: How to Configure Run As Accounts and Profiles for UNIX and Linux Access
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Configure Run As Accounts and Profiles for UNIX and Linux Access

>Applies To: System Center 2016 - Operations Manager

If you are the system administrator in charge of the monitoring of UNIX and Linux computers, you must create Run As accounts for agent maintenance operations, and for health and performance monitoring. These Run As accounts must then be associated with the Run As profiles defined in the UNIX and Linux management packs, so they can access the agents on UNIX and Linux computers. For an overview of the process, see [Planning Security Credentials for Accessing UNIX and Linux Computers](../plan/planning-security-credentials-for-accessing-unix-and-linux-computers.md).  
  
## Configuring Run As accounts  

The **UNIX\/Linux Run As Accounts Wizard** creates Run As accounts that can be of two Run As account types:  
  
-   A monitoring account  
  
-   An agent maintenance account.  
  
Use this wizard three or more times as needed so that you have the following Run As accounts:  
  
-   A monitoring Run As account for unprivileged monitoring.  
  
-   A monitoring Run As account for privileged monitoring.  
  
-   An agent maintenance Run As account for upgrading, uninstalling, and other agent maintenance operations.  
  
To run this wizard, you must have the following credentials information:  
  
-   Username and password for unprivileged access to the UNIX or Linux computer.  
  
-   Secure Shell \(SSH\) credentials for root\-level privileged access to the UNIX or Linux computer. This can be either a username and password, or a username and a key. A passphrase can be optionally provided with a key.  If you prefer not to provide credentials for a privileged account, you can use unprivileged credentials and have the credentials on the UNIX or Linux computer elevated.  
  
-   Username and password for privileged access to the UNIX or Linux computer.  If you prefer not to provide credentials for a privileged account, you can use unprivileged credentials and have the credentials on the UNIX or Linux computer elevated.  
  
    You can choose between su or sudo elevation. If the account is to be elevated using 'su', you will need the 'su' password.  
  
#### To create a Run As account  
  
1.  In the Operations console, click **Administration**.  
  
2.  In **Run As Configuration**, click **UNIX\/Linux Accounts**.  
  
3.  In the **Tasks** pane, click **Create Run As Account**.  
  
4.  On the **Account Type** page, choose a **Monitoring Account** or an **Agent Maintenance Account**.  
  
5.  On the **General Properties** page, provide a name and description for the account. The description is optional.  
  
6.  On the **Account Credentials** page, provide account credentials that can be used for the Run As account type that you selected.  
  
7.  On the **Distribution Security** page, select the **More Secure** or **Less Secure** option.  
  
8.  Click **Create**.  
  
Repeat as needed until all the needed Run As accounts are created.  
  
## Configuring Run As profiles  

Now that you have created the Run As accounts, you must add each Run As account to the applicable profile. There are three profiles to configure:  
  
-   UNIX\/Linux Action Account  
  
    Add a monitoring Run As account that has unprivileged credentials, to this profile.  
  
-   UNIX\/Linux Privileged Account  
  
    Add a monitoring Run As account that has privileged credentials or credentials to be elevated, to this profile.  
  
-   UNIX\/Linux Agent Maintenance Account  
  
    Add a monitoring Run As account that has privileged credentials or credentials to be elevated, to this profile.  
  
> [!NOTE]  
> There is no need to run the **Create Run As Profile Wizard** unless you have authored a new management pack that requires it.  
  
#### To add a Run As account to a profile  
  
1.  In the Operations console, click **Administration**.  
  
2.  In **Run As Configuration**, click **Profiles**.  
  
3.  In the list of profiles, right click and then select **Properties** on one of the following profiles:  
  
    -   UNIX\/Linux Action Account  
  
    -   UNIX\/Linux Privileged Account  
  
    -   UNIX\/Linux Agent Maintenance Account  
  
4.  In the **Run As Profile** wizard, click **Next** until you get to the **Run As Accounts** page.  
  
5.  On the **Run As Accounts** page, click **Add** to add a Run As account that you created. Select the class, group, or object that will be accessed using the credentials in the Run As account.  
  
6.  Click **Save**.  
  
Repeat as needed until all three profiles have been configured with one or more Run As accounts.  
  

  
