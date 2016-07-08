---
title: Script Monitors and Rules
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26b778f2-1255-487c-868a-b09c7fc5ab28
author:markgalioto
---
# Script Monitors and Rules
Monitoring scripts are used when the required data cannot be collected through other standard means such as an event or performance counter. The script collects data from information on the agent and creates a property bag by using the MOM.ScriptAPI object that is installed with the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] agent.  
  
Monitoring scripts may be written in any script language that can access the MOM.ScriptAPI object that is installed on all [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] agents. You can use the Operations console to create scripts in VBScript or JScript. To use a [!INCLUDE[powshellshortname](../../om/manage/includes/powshellshortname_md.md)] script, you must use another Authoring tool such as the [Operations Manager R2 Authoring Console](../../om/manage/Authoring-Tools.md#AuthoringConsole) or [MP Author](../../om/manage/Authoring-Tools.md#MPAuthor).  
  
## <a name="PropertyBags"></a>Property Bags  
Monitoring scripts send any output data as a property bag so that it can be evaluated in an expression for a monitor or mapped into performance data or an event for a collection rule. A property bag is a set of values that each has a name. Any name can be assigned although it is a best practice to use a name descriptive of the particular value. A property bag only exists during the life of the workflow. The next time that the workflow runs, the script is run and creates a new property bag with new values.  
  
One property bag can have any number values, although the whole set of data may not exceed 4 MB. Most scripts will only require some values with a total size far under this limit. There is no requirement for all the values to be used by the workflow.  
  
Scripts create property bags by using the CreatePropertyBag method on the MOM.ScriptAPI object. The workflow uses values from a property bag with a $Data variable that uses the following syntax:  
  
```vbs  
$Data/Property[@Name="PropertyName"]  
```  
  
For example, a script creating performance data might create a property bag with values in the following table. This table shows the name of the value created by the script and the corresponding $Data variable that would be used to map the property bag data to performance data.  
  
|Property Bag Value Name|Sample Value|Variable|  
|---------------------------|----------------|------------|  
|ObjectName|MyObject|$Data\/Property\[@Name\='ObjectName'\]$|  
|CounterName|MyCounter|$Data\/Property\[@Name\='CounterName'\]$|  
|InstanceName|MyInstance|$Data\/Property\[@Name\='InstanceName'\]$|  
|Value|10|$Data\/Property\[@Name\='Value'\]$|  
  
## <a name="ScriptStructure"></a>Script Structure  
The following code shows a sample monitoring script to illustrate the basic structure of a monitoring script. This sample script has the following characteristics.  
  
-   Accepts arguments for the name of the computer that is running the script and a path of the location of the application.  
  
-   Creates a property bag with the values named ComputerName, InstanceName, and PerfValue.  
  
```vbs  
  
sComputerName = WScript.Arguments(0)   
sApplicationPath = WScript.Arguments(1)  
  
Set oAPI = CreateObject("MOM.ScriptAPI")  
Set oBag = oAPI.CreatePropertyBag()  
  
oBag.AddValue "ComputerName", sComputerName  
oBag.AddValue "InstanceName", "MyInstance"  
oBag.AddValue "Value", 1.0  
  
oAPI.Return(oBag)  
  
```  
  
Details of each section of the script are discussed here.  
  
```vbs  
  
sComputerName = WScript.Arguments(0)   
sApplicationPath = WScript.Arguments(1)  
```  
  
The first two lines of the script accept arguments. These values would be expected to be in the Arguments parameter of the rule or monitor running the script. The script can use any number of arguments that are required for the logic of the script.  
  
```vbs  
  
Set oAPI = CreateObject("MOM.ScriptAPI")  
Set oBag = oAPI.CreatePropertyBag()  
  
```  
  
The next two lines create a property bag. These lines will also be unchanged in most monitoring scripts. The main purpose of the rest of the script will be to add values to the property bag by using data that is collected from the agent computer.  
  
```vbs  
  
oBag.AddValue "ComputerName", sComputerName  
oBag.AddValue "InstanceName", "MyInstance"  
oBag.AddValue "Value", 1.0  
  
```  
  
After the property bag is created, any number of values can be added to it. You do this with the AddValue method on the property bag object by using the name of the item followed its value. This example uses explicit values. In actual monitoring script, additional code would be expected that would collect information from the agent computer to include in these values.  
  
```vbs  
  
oAPI.Return(oBag)  
  
```  
  
After all values are added to the property bag, it is returned into the workflow. This line is required, and without it the property bag is discarded when the script ends. This method is only used when the script creates only a single property bag. For more information about scripts that return multiple property bags and conditions when such a strategy is used, refer to the [Cookdown](http://go.microsoft.com/fwlink/?LinkID=232864) section of the [System Center Operations Manager 2007 R2 Authoring Guide](http://go.microsoft.com/fwlink/?LinkID=188119).  
  
## <a name="ScriptArguments"></a>Script Arguments  
Most scripts use arguments, which are values that are sent to the script from the command line when the script is run. Using arguments allows a single script to be used for multiple scenarios without modifying the script itself.  
  
In a monitoring script, arguments are critical because there may be information that the script requires that will be different on each agent where the script runs. Any property of the target object for the monitor or rule can be used for the value of a script argument. This value is resolved individually on each agent at the time that the script is run.  
  
Arguments are accessed in the Operations console from the **Parameters** button. Individual arguments should be separated by spaces in the order that they are accessed in the script. This is identical to the command line that would be provided if the script were run on a command line.  
  
Each argument can be either an explicit value or a $Target variable to use the value of a property on the target object. Any $Target variables are resolved when the script is run so that the script is provided with the resolved values on the command line. You can type in the $Target variable if you know the proper syntax. It is easier though to select the property from **Target** button which will list all of the properties of the target object and its parents.  
  
> [!IMPORTANT]  
> Any $Target variable that might resolve to a value that includes a space should be enclosed with quotation marks. If a value includes spaces and does not have quotation marks, then it will be seen by the script as two separate arguments. The quotation marks will ensure that the value is seen as a single argument. If you select the property from **Target** menu, it will not include the quotation marks for you. You need to type these in after selecting the property.  
  
For example, the sample script earlier expects two arguments for the computer name and the application path. Assuming this was part of a monitor or rule targeted at a class hosted by the **Windows Computer** class, the computer name could be retrieved from the PrincipalName property. If the application path were a property on the target class, then the arguments might look similar to the following example. Notice the quotation marks around the ApplicationPath property, because this could resolve to a value that contains a space.  
  
```vbs  
  
$Target/Host/Property[Type="Windows!Microsoft.Windows.Computer"]/PrincipalName$ "$Target/Property[Type="MyApp.MyClass"]/ApplicationPath$"  
```  
  
Assuming that you gave the script a name of **MyScript.vbs**, the computer name was **MyServer01**, and the application path was **C:\\Program Files\\Contoso\\My Application**, the command line that would be run for this script would be:  
  
```  
MyScript.vbs MyServer01 "C:\Program Files\Contoso\My Application"  
```  
  
## Script Monitors and Rules Topics  
  
-   [Script Collection Rules](../../om/manage/Script-Collection-Rules.md)  
  
    Creating a rule that uses a script to collect performance or event data.  
  
-   [Script Monitors](../../om/manage/Script-Monitors.md)  
  
    Creating a monitor that evaluates the results of a script to set its health state.  
  
-   [UNIX - Linux Shell Command Monitors](../../om/manage/UNIX---Linux-Shell-Command-Monitors.md)  
  
    Creating a monitor that evaluates the output of execution of an UNIX\/Linux command, script, or one\-line sequence of multiple commands \(using pipeline operators\).  
  
