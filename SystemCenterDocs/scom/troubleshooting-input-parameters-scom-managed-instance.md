---
ms.assetid: 
title: Troubleshoot commonly encountered errors while validating input parameters
description: This article describes the errors that might occur while validating input parameters and how to resolve them.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 07/25/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Troubleshoot commonly encountered errors while validating input parameters

This article describes the errors that might occur while validating input parameters and how to resolve them.

If you encounter any issues while creating on-premises parameters, use [this script](https://go.microsoft.com/fwlink/?linkid=2221732) for assistance.

This script is designed to help troubleshoot and resolve issues related to on-premises parameter creation. Access the script and utilize its functionalities to address any difficulties you may encounter during the process.

Use the following guidelines for using the script:

1. Download the script and run it with the **-Help** option to get the parameters.
2. Sign in with domain credentials to a domain joined machine and then run the script with the specified parameters.
3. If any validation fails, take the corrective actions suggested by the script and re-run the script until it passes all validations.
4. Once all the validations are successful, select **Continue to create** and use the same parameters used in the script, for instance creation.

## Validation checks and details

| Validation| Description|
|----|----|
|Azure input validation checks| |
|Setting up pre-requisites on the test machine| 1. Install AD PowerShell module. </br>2. Install Group Policy PowerShell module.|
|Internet connectivity| Checks if outbound internet connectivity is available on the test servers.|
|SQL MI connectivity| Checks if the provided SQL MI is reachable from the network on which the test servers are created.|
|DNS Server connectivity| Checks if the provided DNS Server IP is reachable and resolved to a valid DNS Server.|
|Domain connectivity| Checks if the provided domain name is reachable and resolved to a valid domain.|
|Domain join validation| Checks if domain join succeeds using provided OU Path and domain credentials.|
|Static IP and LB FQDN association| Checks if a DNS record has been created for the provided static IP against the provided DNS name.|
|Computer group validations| Checks if the provided computer group is managed by the provided domain user, and the manager can update group membership.|
|gMSA account validations| Checks if the provided gMSA </br>- Is enabled. </br>- Has its DNS Host Name set to the provided DNS name of the LB. </br>- Has a SAM Account Name length of 15 characters or less. </br>- Has the right SPNs set. </br> The password can be retrieved by members of the provided computer group.
|Group policy validations| Checks if the domain (or the OU Path which hosts the management servers) is affected by any group policy which will alter the local Administrators group.|
|Post validation clean-up| Unjoin from the domain.|

## General guidelines for running validation script

During the onboarding process, a validation is conducted at the validation stage/tab. If all validations are successful, you can proceed to the final stage of creating SCOM Managed Instance. However, if any validations fail, you can't proceed with the creation.

In cases where multiple validations fail, the best approach is to address all the issues at once by manually running a validation script on a test machine.

Follow these steps for running the validation script:

1. Create a new test virtual machine (VM) in the same subnet selected for SCOM Managed Instance creation and sign in to the VM.

2. Download the validation script to the test VM and extract.  It  consists of two files:
      1. Validation.ps1
      2. Runvalidation.ps1

3. Open the *RunValidation.ps1* in PowerShell ISE, provide the applicable input values in settings dictionary and run the *RunValidation.ps1* by selecting F5. You can add break point in the specific check to understand the issues better.

4. The validation script displays all the validation checks and their respective errors, which will assist in resolving the validation issues. For fast resolution, run the script in PowerShell ISE with break point, which can speed up the debugging process.

If all the checks pass successfully, return to the onboarding page and commence the onboarding process again.

## Internet connectivity

### Issue: Outbound internet connectivity doesn't exist on the test servers

**Cause:** Occurs due to an incorrect DNS Server IP or an incorrect network configuration.

**Resolution:**

1. Check the DNS Server IP, and ensure that DNS Server is up and running.
2. Ensure that the VNet which is being used for SCOM Managed Instance creation has line-of-sight to the DNS Server.

### Issue: Unable to connect to the storage account to download SCOM Managed Instance product bits

**Cause:** Occurs due to a problem with your internet connectivity.

**Resolution:** Verify that the VNet being used for SCOM Managed Instance creation has outbound internet access by creating another virtual machine on the network.

### General troubleshooting steps for internet connectivity

1. Create a virtual machine in the subnet selected for SCOM Managed Instance creation and sign in to the VM.

2. To check the internet connectivity, run the following command:

      ```powershell
      Test-NetConnection www.microsoft.com -Port 80
      ```

      This command verifies the connectivity to *www.microsoft.com* on port 80. If this fails, it indicates an issue with outbound internet connectivity.

3. To verify the DNS settings, run the following command:

      ```powershell
      Get-DnsClientServerAddress
      ```

      This command retrieves the DNS server IP addresses configured on the machine. Ensure that the DNS settings are correct and accessible.

4. To check the network configuration, run the following command:

      ```powershell
      Get-NetIPConfiguration
      ```

      This command displays the network configuration details. Verify that the network settings are accurate and match your network environment.

5. To get the blob URL for any file in your storage account, download the file using the following command:

      ```powershell
      Invoke-WebRequest -Uri $decodedUrl -OutFile "$ScomServerDownloadPath\filename.ext"
      ```

      This command downloads the files from the provided blob URL to the specified path.

## SQL MI connectivity

### Issue: Outbound internet connectivity doesn't exist on the test servers

**Cause:** Occurs due to an incorrect DNS Server IP, or an incorrect network configuration.

**Resolution:**
      
1. Check the DNS Server IP and ensure that the DNS Server is up and running.
2. Ensure that the VNet which is being used for SCOM Managed Instance creation has line-of-sight to the DNS Server.

### Issue: Failed to connect to SQL MI from this instance

**Cause:** Occurs as the SQL MI VNet isn't delegated or isn't properly peered with the SCOM Managed Instance VNet.

**Resolution:**

1. Verify that the SQL MI is correctly configured.
2. Ensure that the VNet which is being used for SCOM Managed Instance creation has line-of-sight to the SQL MI, either by being in the same VNet or by VNet peering.

### General troubleshooting steps for SQL MI connectivity

1. Create a virtual machine in the subnet selected for SCOM Managed Instance creation and sign in to the VM.

2. To check the outbound internet connectivity, run the following command:

      ```powershell
      Test-NetConnection -ComputerName "www.microsoft.com" -Port 80
      ```

      This command verifies the outbound internet connectivity by attempting to establish a connection to *www.microsoft.com* on port 80. If the connection fails, it indicates a potential issue with the internet connectivity.

3. To verify the DNS settings and network configuration, ensure that the DNS server IP addresses are correctly configured and validate the network configuration settings on the machine where the validation is being performed.

4. To test the SQL MI connection, run the following command:

      ```powershell
      Test-NetConnection -ComputerName $sqlMiName -Port $sqlMiPort
      ```

      Replace `$sqlMiName` with the name of the SQL MI instance, and `$sqlMiPort` with the appropriate port number.

      This command tests the connection to the SQL MI instance. If the connection is successful, it indicates that the SQL MI is reachable.

## DNS Server connectivity

### Issue: DNS IP provided (\<DNS IP\>) is incorrect, or the DNS Server isn't reachable

**Resolution:** Check the DNS Server IP, and ensure that DNS Server is up and running.

### General trouble shooting for DNS server connectivity

1. Create a virtual machine in the subnet selected for SCOM Managed Instance creation and sign in to the VM.

2. To check the DNS resolution for the specified IP address, run the following command:

      ```powershell
      Resolve-DnsName -Name $ipAddress -IssueAction SilentlyContinue
      ```

      Replace `$ipAddress` with the IP address you want to validate.

      This command checks the DNS resolution for the provided IP address. If the command doesn't return any results or throws an error, it indicates a potential issue with DNS resolution.

3. To verify the network connectivity to the IP address, run the following command:

      ```powershell
      Test-NetConnection -ComputerName $ipAddress -Port 80
      ```

      Replace `$ipAddress` with the IP address you want to test.

      This command checks the network connectivity to the specified IP address on port 80. If the connection fails, it suggests a network connectivity issue.

## Domain connectivity

### Issue: Domain controller for domain \<domain name\> isn't reachable from this network, or port 9389 isn/t open on at least one domain controller

**Cause:** Occurs due to an issue with the provided DNS Server IP or your network configuration.
**Resolution:**
      
1. Check the DNS Server IP and ensure that DNS Server is up and running.
2. Check the domain name and ensure that at least one domain controller is up and running.
     >[!Note]
     >Port 9389 should be open on it , and Active Directory Web Services service should be running.
3. The domain controller meeting the above criteria should be within line-of-sight from the VNet being used for SCOM Managed Instance creation.

### General trouble shooting steps for domain connectivity

1. Create a virtual machine in the subnet selected for SCOM Managed Instance creation and sign in to the VM.
2. To check the domain controller reachability, run the following command:
      ```powershell
      Test-Connection -ComputerName $domainName -Count 1 -Quiet
      ```

      Replace `$domainName` with the name of the domain you want to test.

      This command tests if at least one domain controller for the specified domain is reachable. If the command returns **True**, it indicates successful reachability.

3. To verify DNS server settings:

      - Ensure that the DNS server settings on the machine running the validation are correctly configured.
      - Verify if the DNS server IP addresses are accurate and accessible.

4. To validate network configuration:

      - Verify the network configuration settings on the machine where the validation is being performed.
      - Ensure that the machine is connected to the correct network and has the necessary network settings to communicate with the domain controller.

5. To test the required port on the domain controller, run the following command:

      ```powershell
      Test-NetConnection -ComputerName $domainName -Port $portToCheck
      ```

      Replace `$domainName` with the name of the domain you want to test, and `$portToCheck` with the port number (9389 in this case).

      This command checks if the specified port is open on at least one domain controller. If the command shows a successful connection, it indicates that the necessary port is open.

## Domain join validation

### Issue: Test management servers failed to join the domain

**Cause:** Occurs because of an incorrect OU path, incorrect credentials, or a problem in the network connectivity.

**Resolution:**
      
1. Check the credentials created in your Key vault. The username and password secret must reflect the correct username (domain\username) and password which have permissions to join a machine to the domain. By default, user accounts can only add up to 10 computers to the domain. To configure, see [Default limit to number if workstations a user can join to the domain](/troubleshoot/windows-server/identity/default-workstation-numbers-join-domain).
2. Verify that the OU Path is correct and doesn't block new computers from joining the domain.

### General troubleshooting steps

1. Create a virtual machine in the subnet selected for SCOM Managed Instance creation and sign in to the VM.

2. Join the domain to a VM using the domain account that is used in SCOM Managed Instance creation.
      For joining the domain to a machine using credentials, run the following command:
      ```powershell

        $domainName = "<domainname>"
        
        $domainJoinCredentials = New-Object pscredential -ArgumentList ([pscustomobject]@{
            UserName = "<username>
            Password = "password"
        })
		$ouPath = "<OU path>"
		if (![String]::IsNullOrWhiteSpace($ouPath)) {
			$domainJoinResult = Add-Computer -DomainName $domainName -Credential $domainJoinCredentials -OUPath $ouPath -Force -WarningAction SilentlyContinue -ErrorAction SilentlyContinue
		}
		else {
			$domainJoinResult = Add-Computer -DomainName $domainName -Credential $domainJoinCredentials -Force -WarningAction SilentlyContinue -ErrorAction SilentlyContinue
		}   

## Static IP and LB FQDN association

### Issue: Tests couldn't be run since the servers failed to join the domain

**Resolution:** Ensure that the machines can join the domain. Follow the troubleshooting steps from the [Domain join validation section](#domain-join-validation).

### Issue: DNS Name \<DNS Name\> couldn't be resolved

**Resolution:** The DNS Name provided doesn't exist in the DNS records. Check the DNS name and ensure it is correctly associated with the Static IP provided.

### Issue: The provided static IP \<static IP\> and Load Balancer DNS \<DNS Name\> doesn't match

**Resolution:** Check the DNS records and provide the correct DNS Name/Static IP combination. For more information, see [Create a static IP and confiure the DNS name](/system-center/scom/create-operations-manager-managed-instance?&tabs=prereqs-active#create-a-static-ip-and-configure-the-dns-name).

### General troubleshooting steps

1. Create a virtual machine in the subnet that is selected for SCOM Managed Instance creation and sign in to the VM.

2. Join the domain to a VM using the domain account that is used in SCOM Managed Instance creation.
      To join the domain to a machine using credentials, follow the steps provided in the [Domain join validation section](#domain-join-validation).

3. Verify that the servers have successfully joined the domain:
     - If the servers haven't joined the domain, provide instructions to resolve the domain join issue, such as checking network connectivity, domain name configuration, and domain join credentials.

4. Get IP address and associated DNS name and run the following commands to see if they match.
      Resolve the DNS name and fetch the actual IP address:

      ```powershell
      $DNSRecord = Resolve-DnsName -Name $DNSName
      $ActualIP = $DNSRecord.IPAddress
      ```
  
      If the DNS name can't be resolved, ensure that the DNS name is valid and associated with the correct IP address.

## Computer group validations

### Issue: Test couldn't be run since the servers failed to join the domain

**Resolution:** Ensure that the machines can join the domain. Follow the troubleshooting steps specified in the [Domain join validation section](#domain-join-validation).

### Issue: Computer group with name \<computer group name\> couldn't be found in your domain

**Resolution:** Verify the existence of the group and check the name provided or create a new one if not created already.

### Issue: The input computer group \<computer group name\> isn't managed by the user \<domain username\>

**Resolution:** Navigate to the group properties and set this user as the manager. For more information, see [Create and configure a computer group](/system-center/scom/create-operations-manager-managed-instance?&tabs=prereqs-active#create-and-configure-a-computer-group).

### Issue: The manager \<domain username\> of the input computer group \<computer group name\> doesn't have the necessary permissions to manage group membership

**Resolution:** Navigate to the group properties and check the Manage can update membership list checkbox. For more details, see [Create and configure a computer group](/system-center/scom/create-operations-manager-managed-instance?&tabs=prereqs-active#create-and-configure-a-computer-group).

### General troubleshooting steps

1. Create a virtual machine in the subnet selected for SCOM Managed Instance creation and sign in to the VM.

2. Join the domain to a VM using the domain account that is used in SCOM Managed Instance creation. To join the domain to a machine using credentials, follow the steps provided in Domain join validation section.

3. Open a PowerShell session with administrative privileges.

4. To verify if the VM is joined to the domain, run the following command:

      ```powershell
      Get-WmiObject -Class Win32_ComputerSystem | Select-Object -ExpandProperty PartOfDomain
      ```

5. To verify the existence of the user in the domain, run the following command:

      ```powershell
      Get-ADUser -Filter "SamAccountName -eq '$username'" -ErrorAction SilentlyContinue
      ```

6. To verify the existence of the computer group in the domain, run the following command:

      ```powershell
      Get-ADGroup -Filter "Name -eq '$computerGroupName'" -ErrorAction SilentlyContinue
      ```

7. If the user and computer group exist, verify the group management configuration:

      Determine if the user is the manager of the computer group:

      ```powershell
      Get-ADGroup -Identity $computerGroupName -Properties ManagedBy | Select-Object -ExpandProperty ManagedBy
      ```

      If the output matches the user's distinguished name, it means the user is the manager of the group. If not, update the computer group configuration accordingly.

      Check if the manager can update group membership:

      ```powershell
      Get-ADGroup -Identity $computerGroupName | Get-ADPermission | Where-Object {$_.ExtendedRights -contains "WriteProperty" -and $_.User -eq $username}
      ```

      If no results are returned, it means the manager doesn't have the necessary permissions to manage group membership. Update the group membership permissions for the manager.

## gMSA account validations

### Issue: Test doesn't run since the servers failed to join the domain

**Resolution:** Ensure that the machines can join the domain. Follow the troubleshooting steps specified in the [Domain join validation section](#domain-join-validation).

### Issue: Computer group with name \<computer group name\> isn't found in your domain. The members of this group must be able to retrieve the gMSA password

**Resolution:** Verify the existence of the group and check the name provided.

### Issue: gMSA with name \<domain gMSA\> couldn't be found in your domain

**Resolution:** Verify the existence of the account and check the name provided or create a new one if it has not been created already.

### Issue: gMSA \<domain gMSA\> isn't enabled

**Resolution:** Enable it using the following command:

```powershell
Set-ADServiceAccount -Identity <domain gMSA> -Enabled $true
```

### Issue: gMSA  \<domain gMSA\> needs to have its DNS Host Name set to \<DNS Name\>

**Resolution:** The gMSA doesn't have the DNSHostName property set correctly. Set the DNSHostName property using the following command:

```powershell
Set-ADServiceAccount -Identity <domain gMSA> -DNSHostName <DNS Name>
```

### Issue: The Sam Account Name for gMSA \<domain gMSA\> exceeds the limit of 15 characters

**Resolution:** Set the SamAccountName using the following command:

```powershell
Set-ADServiceAccount -Identity <domain gMSA> -SamAccountName <shortname$>
```

### Issue: Computer  Group \<computer group name\> needs to be set as the PrincipalsAllowedToRetrieveManagedPassword for gMSA \<domain gMSA\>

**Resolution:** The gMSA doesn't have PrincipalsAllowedToRetrieveManagedPassword set correctly. Set the PrincipalsAllowedToRetrieveManagedPassword using the following command:

```powershell
Set-ADServiceAccount -Identity <domain gMSA> - PrincipalsAllowedToRetrieveManagedPassword <computer group name>
```

### Issue: The SPNs haven't been set correctly for the gMSA \<domain gMSA\>

**Resolution:** The gMSA doesn't have correct Service Principal Names set. Set the Service Principal Names using the following command:

```powershell
Set-ADServiceAccount -Identity <domain gMSA> -ServicePrincipalNames <set of SPNs>
```

### General troubleshooting steps

1. To verify that the servers have successfully joined the domain, run the following command:

      `(Get-WmiObject -Class Win32_ComputerSystem).PartOfDomain`

2. To check the existence of the computer group, run the following command:

      `Get-ADGroup -Identity <ComputerGroupName>`
   
3. To check the existence of the gMSA account, run the following command:

      `Get-ADServiceAccount -Identity <GmsaAccount>`

4. To validate the gMSA account properties, run the following command:
      - Check if the gMSA account is enabled:

        `(Get-ADServiceAccount -Identity <GmsaAccount>).Enabled`

      If the command returns **False**, enable the account in the domain.

      Verify that the DNS Host Name of the gMSA account matches the provided DNS name (LB DNS name), run the following commands:

      `(Get-ADServiceAccount -Identity <GmsaAccount>).DNSHostName`

      If the command doesn't return the expected DNS name, provide instructions to update the DNS Host Name.

      Ensure that the Sam Account Name for the gMSA account doesn't exceed the limit of 15 characters:

      `(Get-ADServiceAccount -Identity <GmsaAccount>).SamAccountName.Length`

5. To validate the PrincipalsAllowedToRetrieveManagedPassword property, run the following commands:

      Check if the Computer Group specified is set as the PrincipalsAllowedToRetrieveManagedPassword for the gMSA account:

      `(Get-ADServiceAccount -Identity <GmsaAccount>).PrincipalsAllowedToRetrieveManagedPassword -contains (Get-ADGroup -Identity <ComputerGroupName>).DistinguishedName`

6. To validate the Service Principal Names (SPNs) for the gMSA account, run the following command:

      - $CorrectSPNs = @("MSOMSdkSvc/$dnsHostName", "MSOMSdkSvc/$dnsName", "MSOMHSvc/$dnsHostName", "MSOMHSvc/$dnsName")
      - Check if the correct SPNs are set for the gMSA account:

        `(Get-ADServiceAccount -Identity <GmsaAccount>).ServicePrincipalNames`
      - Check if the results have Correct SPNs.

## Group policy validations

### Issue: This test couldn't be run since the servers failed to join the domain

**Resolution:** Ensure that the machines join the domain. Follow the troubleshooting steps from the [Domain join validation section](#domain-join-validation).

### Issue: gMSA with name \<domain gMSA\> couldn't be found in your domain. This account needs to be a local administrator on the server

**Resolution:** Verify the existence of the account and check the name provided.

### Issue: The accounts \<domain username\> and \<domain gMSA\> couldn't be added to the local Administrators group on the test management servers or did not persist in the group after group policy update

**Resolution:** Ensure that the domain username and gMSA inputs provided are correct, including the full name (domain\account). Also check if there are any group policies overriding the local Administrators group on OU containing the test management servers.

### Issue: SCOM Managed Instance failed

**Cause:** A group policy in your domain (name: \<group policy name\>) is overriding the local Administrators group on test management servers, either on the OU containing the servers or the root of the domain.

**Resolution:** Ensure that the OU for SCOM Managed Instance Management Servers (\<OU Path\>) isn't affected by this policy and that no policies override the group.

### General troubleshooting steps

1. To verify if the servers have successfully joined the domain, run the following command:

      `(Get-WmiObject -Class Win32_ComputerSystem).PartOfDomain`

      The command must return **True**.

2. To check the existence of the gMSA account, run the following command:

      `Get-ADServiceAccount -Identity <GmsaAccount>`

3. To validate the presence of user accounts in the local Administrators group, run the following command:

      `  $addToAdminResult = Add-LocalGroupMember -Group "Administrators" -Member $userName, $gMSAccount -ErrorAction SilentlyContinue
            $gpUpdateResult = gpupdate /force
            $LocalAdmins = Get-LocalGroupMember -Group 'Administrators' | Select-Object -ExpandProperty Name `

      Replace the `<UserName>` and `<GmsaAccount>` with the actual user account names.

4. To determine the domain and organizational unit (OU) details, run the following command:
Retrieve OU details using the following command:

      ` Get-ADOrganizationalUnit -Filter "DistinguishedName -like '$ouPathDN'" -Properties CanonicalName -Credential $domainUserCredentials`

      Replace the \<OuPathDN\> with the actual OU path and provide actual $domainUserCredentials.

5. To get the GPO (Group Policy Object) report from the domain and check for overriding policies on the local Administrators group, run the following command:

      `[XML] $gpoReport = Get-GPOReport -All -ReportType Xml `
      foreach ($GPO in $gpoReport.GPOS.GPO) {
         if (($GPO.LinksTo.SOMPath -eq $domainName) -or ($GPO.LinksTo.SOMPath -eq $ouPathCN)) {
             if ($GPO.Computer.ExtensionData.Extension.LocalUsersAndGroups.Group) {
                 $GroupPolicy = $GPO.Computer.ExtensionData.Extension.LocalUsersAndGroups.Group | Select-Object @{Name='RemoveUsers';Expression={$_.Properties.deleteAllUsers}},@{Name='RemoveGroups';Expression={$_.Properties.deleteAllGroups}},@{Name='GroupName';Expression={$_.Properties.groupName}}
                 if (($GroupPolicy.groupName -eq "Administrators (built-in)") -and (($GroupPolicy.RemoveUsers -eq 1) -or ($GroupPolicy.RemoveGroups -eq 1))) {
                     # Overriding policy found
                     $overridingPolicyFound = $true
                     $overridingPolicyName = $GPO.Name
                 }
             }
         }
     }
