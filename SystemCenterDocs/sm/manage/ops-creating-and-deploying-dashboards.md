---
title: Create and deploy dashboards
description: Explains how to create and deploy Service Manager dashboards.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08d397c0-f3af-424c-a2cf-9490b4825834
---

# Create and deploy Service Manager dashboards

>Applies To: System Center 2016 - Service Manager

You can use PerformancePoint Dashboard Designer with Service Manager to create and manage SharePoint dashboards and their elements to measure, monitor, and manage business performance with live data from the Service Manager data warehouse. Dashboards are mechanisms that display hierarchical arrangements of key performance indicators \(KPIs\).  

 You can use Dashboard Designer to define multiple filters for a dashboard, such as filters that are defined over time, by geography, or against different KPI destinations. When you publish dashboards to a SharePoint site, end users can navigate them by using page filters and drill\-up and drill\-down functionality. You can also use Dashboard Designer to create views and elements, such as scorecard elements, KPIs, data sources, indicators, and reports for use in dashboards.  

 This section is an example showing how you can create a PerformancePoint Services dashboard using the Analysis Services ServiceManager WorkItems Cube. This involves creating a data source for the cube and then creating a scorecard that and creating a resolved incidents KPI. Then, you can create an example single\-page dashboard using a filter, a scorecard, and a report. Finally, you complete the example by exploring the deployed dashboard and its interactive features. You must have Microsoft SharePoint&nbsp;Designer&nbsp;2010 installed to complete the examples in the following topics.  

> [!IMPORTANT]  
>  You must have the Enterprise edition of SharePoint Designer 2010 to create SharePoint PerformancePoint dashboards. For more information about upgrading to the Enterprise edition, see [Upgrade from a SharePoint Server 2010 Standard CAL to an Enterprise CAL](http://technet.microsoft.com/library/cc261946.aspx).  

 For more information about PerformancePoint Dashboard Designer, see [PerformancePoint Dashboard Designer](http://technet.microsoft.com/library/bb821195\(office.12\).aspx).  


## Configure SharePoint infrastructure for dashboards

Before you can create and deploy dashboards for use on the Self-Service Portal in Service Manager, you must configure Microsoft SharePoint&nbsp;2010 and then install Dashboard Designer.  

### To configure SharePoint infrastructure for dashboards  

1.  Open your web browser, navigate to your top\-level site in SharePoint 2010, click **Site Actions**, and then click **Site Settings**.  

2.  Under **Site Collection Administration**, click **Site collection features**. On the **Features** page, click **Activate** next to **SharePoint Server Publishing Infrastructure** and **PerformancePoint Services Site Features**.  

3.  Enable the new features at the parent **Site** level by opening the site that you want to be the parent of your Business Intelligence site. Then, under **Site Actions**, click **Site Settings**. Under **Site Actions**, click **Manage site features**. Click **Activate** next to **SharePoint Server Publishing Infrastructure** and **PerformancePoint Services Site Features**.  

4.  Next, add a Business Intelligence Center site by opening the site that you want to be the parent of the new site. Click **Site Actions**, and then click **New Site**. On the **New SharePoint Site** page, select the **Business Intelligence Center** site template, type a title and a URL name, and then click **Create**.  

5.  As an option, you can create the Business Intelligence Center Site under the  Service Manager Self\-Service Portal Site. To do this, apply the SMPortalTheme: click **Site Actions**, click **Site Settings**, and then under **Look and Feel**, click **Site theme**. Click **Specify a theme**, click **SMPortalTheme**, and then click **Apply**.  

6.  Next, configure the PerformancePoint Unattended Service Account by opening the SharePoint Central Administration page. Then, under **Application Management**, click **Manage service applications**. Click **PerformancePoint Service Application**, and then click **PerformancePoint Service Application Settings**. Type your credentials in the **Secure Store and Unattended Service Account** area, and then click **OK**.  

7.  If an error message appears that says "The Unattended Service Account cannot be set for the service application," you can resolve this problem by doing the following:  

    1.  Navigate to the **SharePoint 2012 Central Administration** page, and then under **Application Management**, click **Manage service applications**.  

    2.  Click **Secure Store Service**, and then click **Generate New Key**.  

    3.  Type a pass phrase, and then click **OK**.  

8.  On the new Business Intelligence Center site page that you created, move your mouse over the **Monitor Key Performance** area of the page, and then click **Start using PerformancePoint Services**.  

9. If an error message appears that says "An error occurred during the processing of \<FolderPath\>\/\<PageName\>.aspx. Code blocks are not allowed in this file," you can resolve this problem by inserting the following information into the Web.config file between the PageParserPaths tags of your SharePoint site:  

    ```  
    <PageParserPaths>  
    <PageParserPath VirtualPath="<FolderPath>/<PageName>.aspx" CompilationMode="Always" AllowServerSideScript="true"/>  
    </PageParserPaths>  

    ```  

10. On the new page, **click Run Dashboard Designer**, and then in the **Application Run - Security Warning** dialog box, click **Run** to install PerformancePoint Dashboard Designer. Later, you can start Dashboard Designer from the **Start** menu.   

## Create a data source for Dashboard Designer

You can use the following information to create a new data source in Service Manager and save it by using Dashboard Designer.  

 The workspace is an XML document that defines the PerformancePoint item definitions for a particular project. The saved workspace items are stored in SharePoint lists and libraries. You can add existing stored items to a workspace, based on the project requirements.  

### To create a data source for Dashboard Designer  

1.  Open PerformancePoint Dashboard Designer, and in the **Workspace Browser**, select **Data Connections**.  

2.  Click the **Create** tab, and then click **Data Source**.  

3.  In the **Select a Data Source Template** dialog box, select **Analysis Services**, and then click **OK**.  

4.  In the **New Data Source** pane, ensure that the **Editor** tab is selected, and then type information for the connection settings for the data source using the examples in the following table.  

    |Property|Value|  
    |--------------|-----------|  
    |Server|\<YourServerName\>|  
    |Database|DWASDataBase|  
    |Cube|ServiceManager WorkItems Cube|  

5.  To save the data source, in the **Workspace Browser** pane, right\-click the new data source, and then click **Save**. As an option, you can rename the data source.  

6.  To save the workspace, click **Save As**, and save the Dashboard Designer Workspace in the folder that you want.   

## Build the Resolved Incidents scorecard

Before you can use a scorecard in a dashboard in Service Manager, you must create the scorecard. Use the following procedure to use a wizard to create an example scorecard called Resolved Incidents Scorecard. The wizard also creates key performance indicators \(KPIs\) from the SystemCenterWorkItemsCube data source.  

### To build the Resolved Incidents Scorecard  

1.  Open Dashboard Designer, connect to the server that hosts the DWASDataBase, and then select **Service Manager WorkItems Cube**. Or, if you have previously saved a designer workspace file that contains the connection information, open the file.  

2.  On the **Home** tab, click **Add Lists**. In the **Add Lists** box, click **PerformancePoint Content**, and then click **OK**.  

3.  To add a scorecard to the workspace, in the **Workspace Browser**, right\-click the **PerformancePoint Content** list, point to **New**, and then click **Scorecard**.  

4.  In the **Select a Scorecard Template** window, in the **Category** tree, ensure that **Microsoft** is selected. In the **Template** list, select **Analysis Services**, and then click **OK**.  

5.  In the Create an Analysis Services Scorecard Wizard, on the **Select a data source page**, select the **SystemCenterWorkItemsCube** data source, and then click **Next**.  

    > [!NOTE]  
    >  When you use the wizard to create a scorecard based on an Analysis Services data source, there are two options that enable the creation of KPIs. You can use the first option to create KPIs based on the measures of the cube. You can use the second option to import KPIs from the cube, if the cube contains KPIs.  

6.  On the **Select a KPI Source** page, select **Create KPIs from Analysis Services measures**, and then click **Next**.  

7.  On the **Select KPIs to Import** page, click **Add KPI** and then in the new row, type **Resolved Incidents KPI** for the name.  

8.  Select **Incidents Resolved Count** under **Actual**.  

9. Select **Increasing is Better** under **Band Method**.  

10. Select **Incidents Opened** under **Targets** and then click **Next**.  

11. On the **Add Measure Filters** page, click **Next**.  

12. On the **Add Member Columns** page, click **Next**.  

13. On the **Locations** page, click **Finish**.  

14. Notice that the KPI and scorecard are added to the workspace and that the scorecard opens in the design pane. In the **Workspace Browser**, modify the name of the new scorecard to **Resolved Incidents Scorecard**, and then press **Enter**.  

15. Save the information in **Designer Workspace**.    

## Configure the KPI

Use the following procedures to configure the key performance indicators \(KPIs\) that you created in the How to Build the Resolved Incidents Scorecard section. You will later use this information in a PerformancePoint dashboard.  

 In the first procedure, you configure the Resolved Incidents KPI number formats and threshold values. In the second procedure, you configure the Resolved Incidents Scorecard and add the Incident Classification hierarchy to allow browsing of the KPI by the hierarchy members. In addition, you will format the scorecard. In the dashboard, the selection of members of the Incident Classification hierarchy will filter a report.  

### To configure the KPI  

1.  Using Dashboard Designer, open the file you saved previously that contains the Incident Resolved Scorecard.  

2.  In the **Workspace Browser**, click **Resolved Incidents KPI**.  

3.  To configure the thresholds for the Target metric, select the **Target** metric.  

4.  In the **Thresholds** section, modify the value for **Threshold&nbsp;2** to **50%**, and the value for **Threshold&nbsp;1** to **25%**.  

5.  In the Thresholds section, modify the value for **Best** to **100%**.  

6.  To save the KPI, in the **Workspace Browser**, right\-click **Resolved Incidents KPI**, and then click **Save**.  

### To configure the Resolved Incidents KPI  

1.  In the **Workspace Browser**, select the scorecard named **Resolved Incidents Scorecard**.  

2.  To refresh the scorecard with the updated KPI definition, on the **Edit** ribbon tab, inside the **View** group, click **Update**.  

3.  To add the Incident Classification hierarchy to the scorecard rows, in the **Details** pane, expand **Dimensions**, expand the **IncidentDim\_IncidentClassification** dimension, and then drag **IncidentClassificationValue** onto the **Incident** scorecard cell.  

4.  In the **Select Members** dialog box, expand the **All** member list, select all the values other than the empty value, and then click **OK**.  

5.  To refresh the scorecard, on the **Edit** ribbon tab, inside the **View** group, click **Update**.  

## Create the Incidents by Analyst Report

Use the following procedure to create an Analytic Grid report named Incidents by Analyst.  

### To create the Incidents by Analyst report  

1.  Open Dashboard Designer, connect to the server that hosts the DWASDataBase, and then click **Service Manager WorkItems Cube**. Or, if you have previously saved a designer workspace file that contains the connection information, open that file.  

2.  In the **Workspace Browser**, right\-click the **PerformancePoint Content** list, select **New**, and then click **Report**.  

3.  In the **Select a Report Template** dialog box, select the **Analytic Grid** template, and then click **OK**.  

4.  In the Create an Analytic Grid Report wizard, on the **Select a Data Source** page, select the **SystemCenterWorkItems** data source, and then click **Finish**.  

5.  In the **Workspace Browser**, modify the name of the report to **Incidents by Analyst**, and then press **Enter**.  

6.  To configure the report, in the **Details** pane, expand **Dimensions**, expand the **AssignedToUserDim** dimension, and then drag the **User Name** attribute into the **Rows** drop zone.  

7.  To configure the hierarchy member selection, in the **Rows** drop zone, click the down arrow to the right of the **AssignedToUserDim** hierarchy to open the **Select Members** dialog box.  

8.  In the **Select Members** dialog box, right\-click **All members** member, point to **Autoselect Members**, click **Select "User Name"**, and then click **OK**.  

9. In the **Details** pane, expand **Measures**, and then drag the **IncidentDimCount** and **Incidents Resolved Count** measures into the **Columns** drop zone.  

10. Right\-click the **Incidents Resolved Count** column heading, point to **Sort**, and then click **Smallest to Largest**.  

11. Right\-click anywhere in table, point to **Filter**, and then click **Filter Empty Rows**.  

12. In the **Details** pane, expand **Dimensions**, expand the **IncidentDim\_IncidentClassification** dimension, and then drag **IncidentClassificationValue** into the **Background** drop zone.  

13. On the **Edit** ribbon tab, in the **View** group, click **Settings**.  

14. In the **View Settings** window, click **Show Information Bar**, and then click **OK**.  

15. In the design pane, click the **Query** tab, and then review the MDX expression that was created automatically to support the report design.  

16. To save the report, in the **Workspace Browser**, right\-click the **Incidents by Analyst** report, and then click **Save**.

## Create the Resolved Incidents dashboard

Use the following procedure to create and assemble the Resolved Incidents Dashboard. This involves the Resolved Incidents Scorecard and the Incidents by Analyst report. You will then create connections to pass values between the dashboard items.  

### To create the Resolved Incidents dashboard  

1.  Open Dashboard Designer, connect to the server that hosts the DWASDataBase, and then click **Service Manager WorkItems Cube**. Or, if you have previously saved a designer workspace file that contains the connection information, open that file.  

2.  In the **Select a Dashboard Page Template** window, select the **2 Columns** template, and then click **OK**.  

3.  In the **Workspace Browser**, modify the name of the dashboard to **Resolved Incidents Dashboard**, and then press **Enter**.  

4.  To add the **Resolved Incidents Scorecard** to the dashboard, in the **Details** pane, expand **Scorecards**, expand the **PerformancePoint Content** list, and then drag the **Resolved Incidents Scorecard** into the **Left Column** zone.  

5.  To add the Incidents by Analyst report to the dashboard, in the **Details** pane, expand **Reports**, expand the **PerformancePoint Content** list, and then drag the **Incidents by Analyst** report into the **Right Column** zone.  

6.  To create the connection between the scorecard and the report, in the **Right Column** zone, click **Incidents by Analyst**.  

7.  On the **Edit** ribbon tab, click **Create Connection**.  

8.  In the **Connection** dialog box, in the **Get Values From** list, select **Left Column - \(1\) Resolved Incidents Scorecard**.  

9. Click the **Values** tab, and in **Connect To**, select the **Incident Classification IncidentClassificationValue** hierarchy.  

10. In the **Source Value** list, select **Member Row: Member Unique Name**, and then click **OK**.  

11. Save the dashboard and the workspace.   

## Deploy the Resolved Incidents dashboard

Use the following procedure to deploy the Resolved Incidents Dashboard to the SharePoint Dashboards library.  

 In this procedure you deploy the Resolved Incidents Dashboard to the SharePoint Dashboards library using the selected master page. Each dashboard is published as a folder that consists of a web page for each page in the dashboard.  

 After you deploy the dashboard, you can select values in the Resolved Incidents Scorecard to show information that applies only to that classification. For example, if you select an E\-Mail Problems value, only incidents with the E\-Mail Problems classification appear in the scorecard portion of the report.  

### To deploy the Resolved Incidents dashboard  

1.  Open Dashboard Designer, connect to the server that hosts the DWASDataBase, and then select **Service Manager WorkItems Cube**. Or, if you have previously saved a designer workspace file that contains the connection information, open that file.  

2.  In the Workspace Browser, right\-click the **Resolved Incidents Dashboard**, and then select **Deploy to SharePoint**.  

3.  In the **Deploy To** dialog box, notice the selection of the Dashboards library.  

4.  In the **Master Page** list, select **Minimal**, and then click **OK**.  

5.  Internet Explorer starts and opens the first dashboard page.  
