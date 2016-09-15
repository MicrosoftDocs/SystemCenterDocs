---
title:  Configuring a Firewall for Operations Manager
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-08-29
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---


# Configuring a Firewall for Operations Manager

>Applies To: System Center 2016 - Operations Manager

This section describes how to configure your firewall to allow communication between the different Operations Manager features on your network.  

## Port assignments
The following table shows Operations Manager feature interaction across a firewall, including information about the ports used for communication between the features, which direction to open the inbound port, and whether the port number can be changed.

|Operations Manager Feature A|Port Number and Direction|Operations Manager Featuret B|Configurable|Note|
|--------------------------------|-----------------------------|---------------------------------|----------------|--------|
|management server|1433 --->|Operations Manager database|Yes (Setup)||
|management server|5723, 5724 --->|management server|No|Port 5724 must be open to install this feature and can be closed after this feature has been installed.|
|gateway server|5723 --->|management server|No||
|management server|1433 --->|Reporting data warehouse|No||
|Reporting server|5723, 5724 --->|management server|No|Port 5724 must be open to install this feature and can be closed after this feature has been installed.|
|Operations console|5724 --->|management server|No||
|Connector framework source|51905 --->|management server|No||
|web console server|Web site port --->|management server|No||
|web console browser|51908 --->|web console server|Yes (IIS Admin)|Port 51908 is the default port used when selecting Windows Authentication. If you select Forms Authentication, you will need to install an SSL certificate and configure an available port for https functionality for the Operations Manager web console web site.|
|connected management server (Local)|5724 --->|connected management server (Connected)|No||
|Agent installed using MOMAgent.msi|5723 --->|management server|Yes (Setup)||
|Agent installed using MOMAgent.msi|5723 --->|gateway server|Yes (Setup)||
|gateway server|5723 --->|management server|Yes (Setup)||
|Agent (Audit Collection Services forwarder)|51909 --->|management server Audit Collection Services collector|Yes (Registry)||
|Agentless Exception Monitoring data from client|51906 --->|management server Agentless Exception Monitoring file share|Yes (Client Monitoring Wizard)||
|Customer Experience Improvement Program data from client|51907 --->|management server (Customer Experience Improvement Program End) Point|Yes (Client Monitoring Wizard)||
|Operations console (reports)|80 --->|SQL Reporting Services|No|The Operations console uses Port 80 to connect to the SQL Reporting Services web site.|
|Reporting server|1433 --->|Reporting data warehouse|Yes||
|management server (Audit Collection Services collector)|1433 --->|Audit Collection Services database|Yes||



