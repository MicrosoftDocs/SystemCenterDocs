---
title: Reports Sample Scenario - How to Include Dashboards and Reports in Custom Views
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e98cc12-263e-440e-b641-1fdd435d4f45
---

# Reports Sample Scenario - How to Include Dashboards and Reports in Custom Views

>Applies To: System Center 2016 - Service Manager

One of the benefits of using System Center - Service Manager with Microsoft SharePoint, and of including the new Microsoft Online Analytical Processing \(OLAP\) cubes in the Service Manager box, is that it is very easy to create SharePoint dashboards using PerformancePoint Services in Microsoft SharePoint&nbsp;Server&nbsp;2010 or Microsoft Excel. You can then create a custom view in Service Manager to display these dashboards.  

 Use the following procedures to create a custom view to display a SharePoint dashboard from your environment in the Service Manager console. Complete all of the following three procedures, in the order that they appear.  

### To create the dashboard management pack  

1.  In the Service Manager console, click **Administration**.  

2.  In the **Tasks** pane, click **Start PowerShell Session**.  

3.  In the Windows PowerShell window, type the following, and then press Enter:  

    ```  
    New-SCManagementPack -DisplayName Dashboards  
    ```  

4.  In the Service Manager console, click **Work Items**. In the **Work Items** pane, right\-click **Incident Management**, and then click **Create Folder**.  

5.  In the **Create new folder** dialog box, type **Dashboards** as the **Folder name**. Select **Dashboards** as the **Management pack**, and then click **OK**.  

6.  In the Windows PowerShell, type the following two commands:  

    ```  
    Get-SCManagementPack -DisplayName Dashboards | Export-SCManagementPack -Path C:\DashBoards  
    ```  

    ```  

    Get-SCManagementPack -DisplayName Dashboards | Remove-SCManagementPack  
    ```  

### To edit the dashboard management pack in Visual&nbsp;Studio  

1.  Start Microsoft Visual Studio.  

     In Visual Studio, click **File**, click **Open**, click **File**, and in the **Open File** dialog box, point to the **C:\\DashBoards** folder and open the management pack file that you just exported. The format of the file name is ManagementPack.\<GUID\>.xml.  

     Edit the management pack file in Visual Studio, as described in the next several steps.  

2.  Locate the `<Assembly>` tag, and replace it with the following code:  

    ```  
    <Assembly>EnterpriseManagement!WpfViewsAssembly</Assembly>  
    ```  

3.  Replace the current ID with **IncidentDashboards**, as follows:  

     Locate the following code block:  

    ```  
    <Identity>  
       <ID>ManagementPack.aded6801e732473d80731943d22d33dc</ID>  
       <Version>7.5.1088.276</Version>  
     </Identity>  

    ```  

     Within that block, update the `<ID>` block, as follows:  

    ```  
    <ID>IncidentDashboards</ID>  
    ```  

     Then, locate the following code block:  

    ```  
    <DisplayStrings>  
      <DisplayString ElementID="ManagementPack.aded6801e732473d80731943d22d33dc">  
        <Name>Dashboards</Name>  
      </DisplayString>  
    ```  

     Within that block, update the `<DisplayString>` tags as follows:  

    ```  
    <DisplayString ElementID="IncidentDashboards">  
    ```  

4.  Select **FileSave ManagementPack.\<GUID\>.xml As**, and in the **Save File As** dialog box, type **C:\\DashBoards\\IncidentDashboards.xml** as the **File name**.  

5.  In the `<References>` section, add a reference to the System.Library management pack. The resulting `<References>` section should look as follows:  

    ```  
    <References>  
      <Reference Alias="EnterpriseManagement">  
        <ID>Microsoft.EnterpriseManagement.ServiceManager.UI.Console</ID>  
        <Version>7.5.1088.276</Version>  
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
      </Reference>  
      <Reference Alias="IncidentManagement">  
        <ID>ServiceManager.IncidentManagement.Library</ID>  
        <Version>7.5.1088.276</Version>  
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
      </Reference>  
      <Reference Alias="System">  
        <ID>System.Library</ID>  
        <Version>7.5.1088.276</Version>  
        <PublicKeyToken>31bf3856ad364e35</PublicKeyToken>  
      </Reference>  
    </References>  

    ```  

     Save the updated file.  

6.  Add a new `PresentationsType` section between the `</Categories>` and the `<Presentation>` sections. The end result of this addition should be as follows:  

    ```  
    </Categories>  
    <PresentationTypes>  
      <ViewTypes>  
        <ViewType ID="Dashboard" Accessibility="Public">  
          <Configuration>  
            <xsd:any minOccurs="0" maxOccurs="unbounded" processContents="skip" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />  
          </Configuration>  
          <ViewImplementation>  
            <Assembly>Console!WpfViewsAssembly</Assembly>  
            <Type>Microsoft.EnterpriseManagement.UI.WpfViews.Overview</Type>  
          </ViewImplementation>  
        </ViewType>  
      </ViewTypes>  
    </PresentationTypes>  
    <Presentation>  

    ```  

     Save the updated file.  

7.  Add a view declaration by adding the following between the `<Presentation>` and the `<Folders>` tags. The resulting code should look as follows:  

    ```  
    <Presentation>  
      <Views>  
        <View ID="View.IncidentDashboard" Accessibility="Public" Enabled="true" Target="System!System.Entity" TypeID="Dashboard" Visible="true">  
          <Category>NotUsed</Category>  
          <Configuration>  
            <Presentation>  
              <Header />  
              <Content>  
                <WebBrowser xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" Name="wb1" Source="http://Dashboards/IncidentDashboard.aspx"/>  
              </Content>  
            </Presentation>  
          </Configuration>  
        </View>  
      </Views>  
      <Folders>  

    ```  

    > [!NOTE]  
    >  Replace the URL in the `Source` attribute with a URL to a dashboard in your environment. This URL should display content that the user's browser can access on the Intranet or on the Internet.  

     Save the updated file.  

8.  Add a new `FolderItem` element to the `FolderItems` section. The resulting code should look as follows:  

    ```  
    <Folders>  
      <Folder ID="Folder.dd2ff258eca54d93a4f10c312df00673" Accessibility="Public" ParentFolder="IncidentManagement!ServiceManager.Console.IncidentManagement" />  
    </Folders>  
    <FolderItems>  
      <FolderItem ElementID="View.IncidentDashboard" ID="FolderItem.View.IncidentDashboard" Folder="Folder.dd2ff258eca54d93a4f10c312df00673"/>  
      <FolderItem ElementID="EnterpriseManagement!Microsoft.EnterpriseManagement.ServiceManager.UI.Console.Task.CreateGridView" ID="FolderItem.695321a1458140e7af75fe3a95888f8e" Folder="Folder.dd2ff258eca54d93a4f10c312df00673" />  
    </FolderItems>  

    ```  

    > [!IMPORTANT]  
    >  The `Folder ID` is different each time because it is generated by the console when the folder is created. Copy the `ID` attribute from the `<Folder>` element, and paste it as the `Folder` attribute in the `FolderItem` element. Ensure that the values of the `Folder` element `ID` attribute and the `FolderItem` element `Folder` attribute are identical.  

     Save the updated file.  

9. Update `DisplayString` with the `ID` from the previous step. Locate the following code:  

    ```  
    <DisplayString ElementID="Folder.<ID>"  

    ```  

     Update it with the `ID` from the previous step. This code should now resemble the following:  

    ```  
    <DisplayString ElementID="Folder.dd2ff258eca54d93a4f10c312df00673">  

    ```  

10. Add a new `ImageReference` element to the `ImageReferences` section. The resulting code should look as follows:  

    ```  
    <ImageReferences>  
      <ImageReference ElementID="View.IncidentDashboard" ImageID="IncidentManagement!IncidentMgmt_AllIncidents_16"/>  
      <ImageReference ElementID="Folder.dd2ff258eca54d93a4f10c312df00673" ImageID="EnterpriseManagement!Microsoft.EnterpriseManagement.ServiceManager.UI.Console.Image.Folder" />  
    </ImageReferences>  

    ```  

    > [!NOTE]  
    >  This `ImageReference` element points to the default **Incident** icon that is used for the **All Incidents** view in the Service Manager console. You can use a custom image resource instead.  

     Save the updated file.  

11. Add a new `DisplayString` element to the `DisplayStrings` section. The resulting code should look as follows:  

    ```  
    <LanguagePacks>  
      <LanguagePack ID="ENU" IsDefault="true">  
        <DisplayStrings>  
          <DisplayString ElementID="View.IncidentDashboard">  
            <Name>Incident Dashboard</Name>  
          </DisplayString>  
          <DisplayString ElementID="IncidentDashboards">  
            <Name>Dashboards</Name>  
          </DisplayString>  
          <DisplayString ElementID="Folder.dd2ff258eca54d93a4f10c312df00673">  
            <Name>Dashboards</Name>  
          </DisplayString>  
        </DisplayStrings>  
      </LanguagePack>  
    </LanguagePacks>  

    ```  

     Save the updated file.  

### To display the dashboard in a custom view  

1.  In the Service Manager Windows PowerShell session, run the following command to validate the IncidentDashboards management pack:  

    ```  
    Test-SCManagementPack -FullName C:\DashBoards\IncidentDashboards.xml  
    ```  

2.  If the validation is successful, import the management pack by running the following command:  

    ```  
    Import-SCManagementPack -FullName C:\DashBoards\IncidentDashboards.xml  

    ```  

3.  Close and then reopen the Service Manager console.  

4.  Click **Work Items**. In the **Work Items** pane, expand **Incident Management**, and then expand **Dashboards**. Select the **Incident Dashboard** view to view the dashboard from the SharePoint site that is hosted in the Service Manager console.  

    > [!NOTE]  
    >  If you are running this procedure in an environment that does not have the Service Manager data warehouse, the dashboard may not display actual data.
