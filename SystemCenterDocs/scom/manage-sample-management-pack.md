---
ms.assetid: 
title:  Sample Linux log file management pack 
description: This article describes a sample management pack for creating an alert from a log file on Linux in System Center Preview 1711 Operations Manager.    
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/3/2017
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1711'
ms.technology: operations-manager
ms.topic: article
---

# Sample Linux log file management pack
This is a sample management pack to create an alert from a log file in Linux with System Center Preview 1711 - Operations Manager.  You can copy and paste the contents into an XML file and install in Operations Manager.

This management pack will create an alert for every collected event.  There is another rule in the comments of the management pack that will only create an alert for events with a specific event number.  To use this rule, remove the comments and replace the event number with one that you require.


    <ManagementPack>
        <Manifest>
            <Identity>
            <ID>OMEDEvent</ID>
            <Version>1.0.0.1</Version>
            </Identity>
            <Name>OMEDEvent</Name>
            <References>
                <Reference Alias="Health">
                    <ID>System.Health.Library</ID>
                    <Version>7.0.8437.0</Version>
                    <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
                </Reference>
                <Reference Alias="SystemCenter">
                    <ID>Microsoft.SystemCenter.Library</ID>
                    <Version>7.0.8437.0</Version>
                    <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
                </Reference>
                <Reference Alias="Windows">
                    <ID>Microsoft.Windows.Library</ID>
                    <Version>7.5.8501.0</Version>
                    <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
                </Reference>
                <Reference Alias="System">
                    <ID>System.Library</ID>
                    <Version>7.5.8501.0</Version>
                    <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
                </Reference>
                <Reference Alias="Unix">
                    <ID>Microsoft.Unix.Library</ID>
                    <Version>7.4.4515.0</Version>
                    <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
                </Reference>
                <Reference Alias="Linux">
                    <ID>Microsoft.Linux.Library</ID>
                    <Version>7.6.1081.0</Version>
                    <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>
                </Reference>
            </References>
        </Manifest>
        <Monitoring>
            <!--This rule looks for all the events from the datasource OMED.EventDataSource and would generate an Alert in SCOM.  -->
            <Rules>
                <Rule ID="RuleForAllEvents" Enabled="true" Target="Linux!Microsoft.Linux.Computer" >
                    <Category>EventCollection</Category>
                    <DataSources>
                        <!-- check data source id -->
                        <DataSource TypeID="Linux!Microsoft.Linux.OMED.EventDataSource" ID="Rule0DS0">
                            <ComputerName>$Target/Property[Type="Unix!Microsoft.Unix.Computer"]/NetworkName$</ComputerName>
                            <ManagedEntityId>$Target/Id$</ManagedEntityId>
                        </DataSource>
                    </DataSources>
                    <WriteActions>
                        <WriteAction ID="GenerateAlert" TypeID="Health!System.Health.GenerateAlert">
                            <!-- Alert Priority and Severity is set to 2, this is configurable -->
                            <Priority>2</Priority>
                            <Severity>2</Severity>
                                
                            <!--Alert description would be the event description. This description and the event ID are defined in the fluentd configuration 
                            file by the user for log file monitoring.-->
                    
                            <AlertMessageId>$MPElement[Name="EventProvider.Alert"]$</AlertMessageId>
                            <AlertParameters>
                <AlertParameter1>$Data/EventDescription$</AlertParameter1>
                            </AlertParameters>
                            <Suppression />

                            </WriteAction>
                    </WriteActions>
                </Rule>
                <!-- Below is a sample MP Rule that could be used, if the user wants to add a rule to look for any specific event and generate alert -->
                <!--
                <Rule ID="RuleForEvent404" Enabled="true" Target="Windows!Microsoft.Windows.Computer" >
                    <Category>EventCollection</Category>
                    <DataSources>
                        <DataSource TypeID="Linux!Microsoft.Linux.OMED.EventDataSource" ID="Rule1DS0">  
                            <ComputerName>$Target/Property[Type="Unix!Microsoft.Unix.Computer"]/NetworkName$</ComputerName>
                            <ManagedEntityId>$Target/Id$</ManagedEntityId>
                            <EventNumber>404</EventNumber>
                        </DataSource>
                    </DataSources>
                    <WriteActions>
                        <WriteAction ID="GenerateAlert" TypeID="Health!System.Health.GenerateAlert">
                            <Priority>2</Priority>
                            <Severity>2</Severity>
                            <AlertMessageId>$MPElement[Name="EventProvider.Alert"]$</AlertMessageId>
                            <AlertParameters>
                                <AlertParameter1>$Data/EventDescription$</AlertParameter1>
                            </AlertParameters>
                            <Suppression />
                        </WriteAction>
                    </WriteActions>
                </Rule>
                -->
            </Rules>
        </Monitoring>
        <Presentation>
            <StringResources>
                <StringResource ID="EventProvider.Alert" />
            </StringResources>
        </Presentation>
        <LanguagePacks>
            <LanguagePack ID="ENU" IsDefault="true">
                <DisplayStrings>
                    <DisplayString ElementID="EventProvider.Alert">
                        <Name> Event Provider Alert</Name>
                        <Description>{0}</Description>
                    </DisplayString>
                </DisplayStrings>
            </LanguagePack>
        </LanguagePacks>
    </ManagementPack>
