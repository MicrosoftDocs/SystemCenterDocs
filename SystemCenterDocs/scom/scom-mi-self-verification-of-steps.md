---
ms.assetid: 
title: SCOM Managed Instance self-verification of steps
description: This article describes the self-verification processes of Operations Manager admin, Active directory admin and Network admin.
author: jyothisuri
ms.author: jsuri
manager: jsuri
ms.date: 08/25/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# SCOM Managed Instance self-verification of steps

This article describes the self-verification processes of Operations Manager admin, Active directory admin and Network admin.

>[!Note]
> To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

After setting up the steps, run the self-validation tool. Based on the experience and data collected from telemetry, Operations Manager administrators have spent considerable time validating the accuracy of steps. Running this tool helps to identify any issues with your environment or parameters before proceeding with the actual deployment.

Many customers are benefited from this tool as it saves a significant amount of time that would otherwise be spent troubleshooting issues with steps later on. Therefore, we recommend running this tool before deployment to avoid spending excessive time diagnosing and troubleshooting on-premises parameters in the future.

In the process of SCOM Managed Instance creation, three primary personas are involved. Following is the typical flow of how the Operations Manager admin sets up the steps in enterprise organizations:

1. Operations Manager admin initiates communication with the AD admin, to configure all the Active Directory-related settings.

2. Operations Manager admin then communicates with the network admin, to establish the Virtual Network (VNet) and configure necessary firewalls, Network Security Groups (NSGs), and DNS resolution to connect to the designated Active Directory controller, as outlined in the Network prerequisites.

3. Once all the configurations are implemented, Operations Manager admin proceeds with thorough testing on a test virtual machine (VM) to ensure that everything functions as expected. This testing phase helps proactively identify and address any potential issues.

If the Operations Manager admin plays all three roles, they can independently handle and manage all the tasks without requiring the involvement of different personnel for each specific area.

With the steps provided for each persona to validate the parameters, we aim to streamline the process of setting up the steps, thereby reducing the time required for creating the SCOM Managed Instance.

By empowering each persona to verify their respective parameters, we can expedite the overall setup process and achieve faster SCOM Managed Instance deployment.

## Operations Manager admin self-verification of steps

Running Operations Manager admin self-verification is essential to understand the correctness of steps.

[Demonstration of how to run the self-validation tool.]

>[!Important]
> Initially, create a new test Windows Server (2022/2019) virtual machine (VM) in the same subnet selected for SCOM Managed Instance creation. Subsequently, both your AD admin and Network admin can individually use this VM to verify the effectiveness of their respective changes. This approach significantly saves time spent on back-and-forth communication between the AD admin and Network admin.

Follow these steps to run the validation script:

1. Generate a new virtual machine (VM) running on Windows Server 2022 or 2019 within the chosen subnet for SCOM Managed Instance creation. Sign in to the VM and configure its DNS server to use the same DNS server IP that is planned to utilize during the creation of the SCOM managed instance. For example, see the following to set the DNS server IP:

     :::image type="DNS server IP" source="media/scom-mi-self-verification-of-steps/dns-server-ip.png" alt-text="Screenshot of DNS server IP.":::

2. Download the validation script to the test VM and extract. It consists of five files: 
     - Readme.txt
     - ScomValidation.ps1
     - RunValidationAsSCOMAdmin.ps1
     - RunValidationAsActiveDirectoryAdmin.ps1
     - RunValidationAsNetworkAdmin.ps1

3. Follow the steps mentioned in the Readme.txt file to run the *RunValidationAsSCOMAdmin.ps1*. Ensure to fill the settings value in *RunValidationAsSCOMAdmin.ps1* with applicable values before running it.

   ```powershell
   # $settings = @{
   #   Configuration = @{
   #         DomainName="test.com"                 
   #         OuPath= "DC=test,DC=com"           
   #         DNSServerIP = "190.36.1.55"           
   #         UserName="test\testuser"              
   #         Password = "password"                 
   #         SqlDatabaseInstance= "test-sqlmi-instance.023a29518976.database.windows.net" 
   #         ManagementServerGroupName= "ComputerMSG"      
   #         GmsaAccount= "test\testgMSA$"
   #         DnsName= "lbdsnname.test.com"
   #         LoadBalancerIP = "10.88.78.200"
   #     }
   # }
   # Note : Before running this script, please make sure you have provided all the parameters in the settings
   $settings = @{
   Configuration = @{
   DomainName="<domain name>"
   OuPath= "<OU path>"
   DNSServerIP = "<DNS server IP>"
   UserName="<domain user name>"
   Password = "<domain user password>"
   SqlDatabaseInstance= "<SQL MI Host name>"
   ManagementServerGroupName= "<Computer Management server group name>"
   GmsaAccount= "<GMSA account>"
   DnsName= "<DNS name associated with the load balancer IP address>"
   LoadBalancerIP = "<Load balancer IP address>"
   }
   }
   ```

4. In general, *RunValidationAsSCOMAdmin.ps1* runs all the validations. If you wish to run a specific check, then open *ScomValidation.ps1* and comment all other checks, which are at the end of the file. You can also add break point in the specific check to debug the check and understand the issues better.

   ```powershell
	    # Default mode is - SCOMAdmin, by default if mode is not passed then it will run all the validations 
	    # adding all the checks to result set
	    try {
	        # Connectivity checks
	        $validationResults += Invoke-ValidateStorageConnectivity $settings
	        $results = ConvertTo-Json $validationResults -Compress
	        
	        $validationResults += Invoke-ValidateSQLConnectivity $settings
	        $results = ConvertTo-Json $validationResults -Compress
	
	        $validationResults += Invoke-ValidateDnsIpAddress $settings
	        $results = ConvertTo-Json $validationResults -Compress
	
	        $validationResults += Invoke-ValidateDomainControllerConnectivity $settings
	        $results = ConvertTo-Json $validationResults -Compress
	
	        # Parameter validations
	        $validationResults += Invoke-ValidateDomainJoin $settings
	        $results = ConvertTo-Json $validationResults -Compress
	
	        $validationResults += Invoke-ValidateStaticIPAddressAndDnsname $settings
	        $results = ConvertTo-Json $validationResults -Compress
	
	        $validationResults += Invoke-ValidateComputerGroup $settings
	        $results = ConvertTo-Json $validationResults -Compress
	
	        $validationResults += Invoke-ValidategMSAAccount $settings
	        $results = ConvertTo-Json $validationResults -Compress
	            
	        $validationResults += Invoke-ValidateLocalAdminOverideByGPO $settings
	        $results = ConvertTo-Json $validationResults -Compress
	    }
	    catch {
	        Write-Verbose -Verbose  $_
    }
   ```
	
>[!Note]
>Operations Manager admin validations include a check for any GPO policies overriding the local administrator group. It may take a long time to complete since the check queries all the policies for assessment.

5. The validation script displays all the validation checks and their respective errors, which will help in resolving the validation issues. For fast resolution, run the script in PowerShell ISE with break point, which can speed up the debugging process.

     If all the checks pass successfully, return to the onboarding page and start the onboarding process.

## Active directory admin self-verification of steps

To minimize back-and-forth communication with the Operations Manager admin, it is considered as a good practice for the Active Directory admin to independently assess the Active Directory parameters. If needed, you can seek assistance from the Operations Manager admin to run the validation tool, ensuring a smoother and more efficient process of parameter evaluation.

Performing Active Directory admin self-verification is an optional step, and we provide the flexibility to each organization to decide whether to undertake this process based on their convenience and specific requirements.

Follow these steps to run the validation script:

1. Generate a new virtual machine (VM) running on Windows Server 2022 or 2019 within the chosen subnet for SCOM Managed Instance creation. Sign in to the VM and configure its DNS server to use the same DNS server IP that is planned to utilize during the creation of the SCOM Managed Instance. If the test VM is already created by Operations Manager admin, then use the test VM. For example, see the following to set the DNS server IP:

     :::image type="DNS server IP" source="media/scom-mi-self-verification-of-steps/dns-server-ip.png" alt-text="Screenshot of DNS server IP.":::

2. Download the validation script to the test VM and extract. It consists of five files: 
     - Readme.txt
     - ScomValidation.ps1
     - RunValidationAsSCOMAdmin.ps1
     - RunValidationAsActiveDirectoryAdmin.ps1
     - RunValidationAsNetworkAdmin.ps1

3. Follow the steps mentioned in the Readme.txt file to run the *RunValidationAsActiveDirectoryAdmin.ps1*. Ensure to fill the settings value in *RunValidationAsActiveDirectoryAdmin.ps1* with applicable values before running it.

   ```powershell
   # $settings = @{
   #   Configuration = @{
   #         DomainName="test.com"                 
   #         OuPath= "DC=test,DC=com"           
   #         DNSServerIP = "190.36.1.55"           
   #         UserName="test\testuser"              
   #         Password = "password"                 
   #         ManagementServerGroupName= "ComputerMSG"      
   #         GmsaAccount= "test\testgMSA$"
   #         DnsName= "lbdsnname.test.com"
   #         LoadBalancerIP = "10.88.78.200"
   #     }
   # }
   # Note : Before running this script, please make sure you have provided all the parameters in the settings
   $settings = @{
   Configuration = @{
   DomainName="<domain name>"
   OuPath= "<OU path>"
   DNSServerIP = "<DNS server IP>"
   UserName="<domain user name>"
   Password = "<domain user password>"
   ManagementServerGroupName= "<Computer Management server group name>"
   GmsaAccount= "<GMSA account>"
   DnsName= "<DNS name associated with the load balancer IP address>"
   LoadBalancerIP = "<Load balancer IP address>"
   }
   }
   ```

4. In general, *RunValidationAsActiveDirectoryAdmin.ps1* runs all the validations. If you wish to run a specific check, then open *ScomValidation.ps1* and comment all other checks, which are under Active directory admin checks. You can also add break point in the specific check to debug the check and understand the issues better.

   ```powershell
   # Mode is AD admin then following validations/test will be performed
   if ($mode -eq "ADAdmin") {

       try {
           # Mode is AD admin then following validations/test will be performed
           $validationResults += Invoke-ValidateDnsIpAddress $settings
           $results = ConvertTo-Json $validationResults -Compress

           $validationResults += Invoke-ValidateDomainControllerConnectivity $settings
           $results = ConvertTo-Json $validationResults -Compress

           # Parameter validations
           $validationResults += Invoke-ValidateDomainJoin $settings
           $results = ConvertTo-Json $validationResults -Compress

           $validationResults += Invoke-ValidateStaticIPAddressAndDnsname $settings
           $results = ConvertTo-Json $validationResults -Compress

           $validationResults += Invoke-ValidateComputerGroup $settings
           $results = ConvertTo-Json $validationResults -Compress

           $validationResults += Invoke-ValidategMSAAccount $settings
           $results = ConvertTo-Json $validationResults -Compress
            
           $validationResults += Invoke-ValidateLocalAdminOverideByGPO $settings
           $results = ConvertTo-Json $validationResults -Compress
       }
       catch {
           Write-Verbose -Verbose  $_
       }
   }
   ```

>[!Note]
>Active directory admin validations include a check for any GPO policies overriding the local administrator group. It may take a long time to complete since the check queries all the policies for assessment.

5. The validation script displays all the validation checks and their respective errors, which will help in resolving the validation issues. For fast resolution, run the script in PowerShell ISE with break point, which can speed up the debugging process.

     If all the checks pass successfully, then there is no issues with the active directory parameters.

## Network admin self-verification of steps

To minimize back-and-forth communication with the Operations Manager admin, Network admin must independently assess the Network configuration. If needed, they can seek assistance from the Operations Manager admin to run the validation tool, ensuring a smoother and more efficient process of parameter evaluation.

Performing network admin self-verification is an optional step, and we provide the flexibility to each organization to decide whether to undertake this process based on their convenience and specific requirements.

Follow these steps to run the validation script:

1. Generate a new virtual machine (VM) running on Windows Server 2022 or 2019 within the chosen subnet for SCOM Managed Instance creation. Sign in to the VM and configure its DNS server to use the same DNS server IP that is planned to utilize during the creation of the SCOM managed instance. If the test VM is already created by Operations Manager admin, then use the test VM. For example, see the following to set the DNS server IP:

     :::image type="DNS server IP" source="media/scom-mi-self-verification-of-steps/dns-server-ip.png" alt-text="Screenshot of DNS server IP.":::

2. Download the validation script to the test VM and extract. It consists of five files:
     - Readme.txt
     - ScomValidation.ps1
     - RunValidationAsSCOMAdmin.ps1
     - RunValidationAsActiveDirectoryAdmin.ps1
     - RunValidationAsNetworkAdmin.ps1

3. Follow the steps mentioned in the Readme.txt file to run the *RunValidationAsNetworkAdmin.ps1*. Ensure to fill the settings value in *RunValidationAsNetworkAdmin.ps1* with applicable values before running it.

   ```powershell
   # $settings = @{
   #   Configuration = @{
   #         DomainName="test.com"                 
   #         DNSServerIP = "190.36.1.55"
   #	     SqlDatabaseInstance= "<SQL MI Host name>"           
   #     }
   # }
   # Note : Before running this script, please make sure you have provided all the parameters in the settings
   $settings = @{
   Configuration = @{
   DomainName="<domain name>"
   DNSServerIP = "<DNS server IP>"
   SqlDatabaseInstance= "<SQL MI Host name>"
   }
   }
   ```

4. In general, *RunValidationAsNetworkAdmin.ps1* runs all the validations related to network configuration. If you wish to run a specific check, then open *ScomValidation.ps1* and comment all other checks, which are under Network admin checks. You can also add break point in the specific check to debug the check and understand the issues better.

   ```powershell
	       # Mode is Network admin then following validations/test will be performed
	       try {
	           $validationResults += Invoke-ValidateStorageConnectivity $settings
	           $results = ConvertTo-Json $validationResults -Compress
	        
	           $validationResults += Invoke-ValidateSQLConnectivity $settings
	           $results = ConvertTo-Json $validationResults -Compress
	
	           $validationResults += Invoke-ValidateDnsIpAddress $settings
	           $results = ConvertTo-Json $validationResults -Compress
	
	           $validationResults += Invoke-ValidateDomainControllerConnectivity $settings
	           $results = ConvertTo-Json $validationResults -Compress
	       }
	       catch {
	           Write-Verbose -Verbose  $_
       }
   ```

5. The validation script displays all the validation checks and their respective errors, which will help resolving the validation issues. For fast resolution, run the script in PowerShell ISE with break point, which can speed up the debugging process.

     If all the checks pass successfully, then there is no issues with the network configuration.

## Next steps

- [Create an instance of Azure Monitor SCOM Managed Instance (preview)](create-operations-manager-managed-instance.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
