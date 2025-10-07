---
ms.assetid: 9332f5fb-b26f-4d05-9cc6-c13727cd5967
title:  Microsoft.SystemCenter.WebApplication.UrlProbe
description: This article details the schema for the System Center Operations Manager URL probe module.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 1825-days
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
monikerRange: '>=sc-om-2019'
ms.custom: UpdateFrequency5, engagement-fy24
---

# Microsoft.SystemCenter.WebApplication.UrlProbe

The **Microsoft.SystemCenter.WebApplication.UrlProbe** probe module connects to one or more URLs and returns **Microsoft.SystemCenter.WebApplication.WebApplicationData**. This data can then be used with other modules from the **Microsoft.SystemCenter.WebApplication.Library** to evaluate the health state of various aspects of the target website.

## Usage

The primary function of **Microsoft.SystemCenter.WebApplication.UrlProbe** is to send a request to one or more URLs and report on the results. The format of the request is a complex type and is used with other modules to evaluate the health state of the target URL. Because large numbers of requests can be made with a single probe, and because the results of the request can contain a large amount of data, the probe itself carries out some evaluation of the request before producing the output. For example, instead of just providing the status code from the queried URL as output, the module compares the status code against a specified range and provides a success or failure code as output. The module can also match the content of the HTML that's returned by the request, for example, matching the word error to determine if an error page was returned. This evaluation performed by the module removes the need for complex expression matching logic in your rule or monitor.

This module is often commonly triggered using [Microsoft.SystemCenter.WebApplication.PerProbe.Scheduler](/previous-versions/system-center/developer/hh442320%28v%3dmsdn.10%29).

The **Microsoft.SystemCenter.WebApplication.UrlProbe** module is commonly used with a number of condition detection modules, which are intended to evaluate its output. The module evaluates different aspects of the health of the URL based on parameters defined in the request and returns the appropriate output for each.

Some of those parameters evaluate directly to a health state. For these parameters, you would use three condition detection modules, each of which matches a specific integer output from the probe indicating a particular health state, as shown in the following table:

| **Condition Detection Module** | **Matched value** |
| --- | --- |
| **Microsoft.SystemCenter.WebApplication.OKCriteriaMatch** | 1 |
| **Microsoft.SystemCenter.WebApplication.WarningCriteriaMatch** | 2 |
| **Microsoft.SystemCenter.WebApplication.ErrorCriteriaMatch** | 3 |

Other parameters return a binary status. For those cases, two condition detection modules are used, each of which matches a Boolean type from the probe as shown in the following table:

| **Condition Detection Module** | **Matched value** |
| --- | --- |
| **Microsoft.SystemCenter.WebApplication.Boolean.CriteriaDoesNotMatch** | false |
| **Microsoft.SystemCenter.WebApplication.Boolean.CriteriaMatch** | true |

Finally, some raw values are returned, which you can either collect for analysis and reporting or use with expression filter condition detection modules.

## Type definition

```
<ProbeActionModuleType ID="Microsoft.SystemCenter.WebApplication.UrlProbe" Accessibility="Public" Batching="false" PassThrough="false">
   <Configuration>
      <IncludeSchemaTypes>
         <SchemaType>Microsoft.SystemCenter.WebApplication.WebModulesSchema</SchemaType>
      </IncludeSchemaTypes>
      <xsd:element name="Proxy" type="xsd:string" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="ProxyUserName" type="xsd:string" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="ProxyPassword" type="xsd:string" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="ProxyAuthenticationScheme" type="AuthenticationSchemeType" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="CredentialUserName" type="xsd:string" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="CredentialPassword" type="xsd:string" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="AuthenticationScheme" type="AuthenticationSchemeType" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="IgnoreServerCertError" type="xsd:boolean"  xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="FollowRedirects" type="xsd:boolean" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="RetryCount" type="xsd:unsignedInt" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="RequestTimeout" type="xsd:unsignedInt" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="Requests" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
         <xsd:complexType>
            <xsd:sequence>
               <xsd:element name="Request" type="RequestType" minOccurs="0" maxOccurs="unbounded" />
            </xsd:sequence>
         </xsd:complexType>
      </xsd:element>
      <xsd:element name="TransactionResponseTimeWarningCriteria" type="RequestEvaluationNumericCriteriaType" minOccurs="0" maxOccurs="1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="TransactionResponseTimeErrorCriteria" type="RequestEvaluationNumericCriteriaType" minOccurs="0" maxOccurs="1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
      <xsd:element name="PerformanceCollectionFrequencyInCycles" type="xsd:unsignedInt" minOccurs="0" maxOccurs="1" default="1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" />
   </Configuration>
   <OverridableParameters>
      <OverridableParameter ID="Proxy" Selector="$Config/Proxy$" ParameterType="string" />
      <OverridableParameter ID="ProxyUserName" Selector="$Config/ProxyUserName$" ParameterType="string" />
      <OverridableParameter ID="ProxyPassword" Selector="$Config/ProxyPassword$" ParameterType="string" />
      <OverridableParameter ID="ProxyAuthenticationScheme" Selector="$Config/ProxyAuthenticationScheme$" ParameterType="string" />
      <OverridableParameter ID="CredentialUserName" Selector="$Config/CredentialUserName$" ParameterType="string" />
      <OverridableParameter ID="CredentialPassword" Selector="$Config/CredentialPassword$" ParameterType="string" />
      <OverridableParameter ID="AuthenticationScheme" Selector="$Config/AuthenticationScheme$" ParameterType="string" />
      <OverridableParameter ID="IgnoreServerCertError" Selector="$Config/IgnoreServerCertError$"  ParameterType="bool"/>
      <OverridableParameter ID="FollowRedirects" Selector="$Config/FollowRedirects$" ParameterType="bool" />
      <OverridableParameter ID="RetryCount" Selector="$Config/RetryCount$" ParameterType="int" />
      <OverridableParameter ID="RequestTimeout" Selector="$Config/RequestTimeout$" ParameterType="int" />
   </OverridableParameters>
   <ModuleImplementation Isolation="Any">
      <Native>
         <ClassID>92C599FD-6639-4A9F-90DA-E1350162A318</ClassID>
      </Native>
   </ModuleImplementation>
   <OutputType>Microsoft.SystemCenter.WebApplication.WebApplicationData</OutputType>
   <TriggerOnly>true</TriggerOnly>
</ProbeActionModuleType>
```

## Parameters

The **Microsoft.SystemCenter.WebApplication.UrlProbe** module supports the configuration parameters described in the following table.

| **Parameter** | **Type** | **Overridable** | **Description** |
| --- | --- | --- | --- |
| _Proxy_ | **String** | True | Required parameter, but can be empty. Specifies the name of the proxy server if the agent requires one to access the URL. |
| _ProxyUserName_ | **String** | True | Required parameter, but can be empty. Specifies the username to be used with the proxy server if the specified proxy server requires authentication. |
| _ProxyPassword_ | **String** | True | Required parameter, but can be empty. Specifies the password to be used with the proxy server if the specified proxy server requires authentication. |
| _ProxyAuthenticationScheme_ | **AuthenticationSchemeType** | True | Required parameter. Specifies the authentication scheme to be used with the proxy server, if the agent requires one to access the URL. Valid values are  **None**, **Basic**, **NTLM**, **Digest**, and **Negotiate**. |
| _CredentialUserName_ | **String** | True | Required parameter, but can be empty. Specifies the username to be used with the URL being queried. |
| _CredientialPassword_ | **String** | True | Required parameter, but can be empty. Specifies the password to be used with the URL being queried. |
| _AuthenticationScheme_ | **AuthenticationSchemeType** | True | Required parameter. Specifies the authentication scheme to be used with the URL being queried. Valid values are **None**, **Basic**, **NTLM**, **Digest**, and **Negotiate**. |
| _IgnoreServerCertError_ | **Boolean** | True | Specifies whether the server certificate errors should be ignored. |
| _FollowRedirects_ | **Boolean** | True | Required parameter. Specifies whether the query should follow URL redirects. |
| _RetryCount_ | **Integer** | True | Required parameter. Specifies the number of times the module should retry the specified URL before timing out. |
| _RequestTimeout_ | **Integer** | True | Required parameter. Specifies the length of time to wait for a response from the specified URL before retrying. |
| _Requests_ | Complex Type | False | Collection of **Request** elements (see below). |
| _TransactionResponseTimeWarningCriteria_ | **RequestEvaluationNumericCriteriaType** | False | Optional parameter. Specifies the response time at which to specify a warning. |
| _TransactionResponseTimeErrorCriteria_ | **RequestEvaluationNumericCriteriaType** | False | Optional Parameter. Specifies the response time at which to specify an error. |
| _PerformanceCollectionFrequencyInCycles_ | **Integer** | False | Optional Parameter. Specifies how many query intervals must be completed before each collection. If the value is 1, then the counters will be collected each time the browser session is run. If it's 2, then the counters will only be collected every second time the browser session is run, and so on. |

### Request element

The **Requests** element is a collection of one or more **Request** elements. Each **Request** element has a **RequestID** subelement which uniquely identifies the request within that set of **Requests**. Requests are processed in order, according to their **RequestID**. The **Request** element consists of the following elements:

| **Element** | **Type** | **Description** |
| --- | --- | --- |
| _RequestID_ | **Integer** | Because each probe can initiate multiple requests, the  **RequestID** uniquely identifies each request and specifies the order that the requests will be processed. |
| _URL_ | **String** | The URL to be queried. |
| _Verb_ | **VerbType** | Indicates the verb to use with the URL request. Can take any of the following values: GET, HEAD, or POST. |
| _Version_ | **VersionType** | Indicates the HTTP type for the request. Valid values are HTTP/1.0 and HTTP/1.1. |
| _HttpHeaders_ | **HttpHeadersType** | HTTP headers for the request. The  **HttpHeadersType** is a complex type consisting of 0 or more  **HttpHeader**  elements, which are of type **NameValueType**. The  **NameValueType**, in turn consists of two required elements, **Name** and **Value**. |
| _Body_ | **String** | The value will be empty if the **VerbType** is GET or HEAD. If the **VerbType** is POST. This is the body of the request submitted by the post. |
| _CheckContentChange_ | **Boolean** | If true, provides additional content validation. |
| _ContentHash_ | **ContentHashType** | Consists of a string of 36 characters, hexadecimal 8-4-4-4-12. |
| _Depth_ | **Integer** | Specifies the number of levels of external links to collect. If the value is 0, only the links on the page itself are evaluated. If the value is 1, then the links on each target page are evaluated. If the value is 2, then the links on those target pages are evaluated, and so on. |
| _ThinkTime_ | **Integer** | Amount of time to wait between the request and collection of the body. |
| _CheckInternalLinks_ | **Boolean** | Enables collection of the status of each internal link and includes internal links in the evaluation of the monitor for the request. An internal link is a link that refers to a location on the same page. |
| _CheckExternalLinks_ | **Boolean** | Enables collection of the status of each external link and includes external links in the evaluation of the monitor for the request. An external link is a link that refers to a location outside the current page. |
| _CheckResources_ | **Boolean** | If true, the monitor returns the status of the resources for the page. Instead of measuring each individual resource, the total of all resources are evaluated. If false, the resource monitor isn't functional for the request. |
| _RequestEvaluationCriteria_ | **RequestEvaluationCriteriaType** | A complex type that evaluates the data returned by the request (see below). |
| _FormsAuthCredentials_ | **FormsAuthCredentialsType** | Complex type that consists of **CredentialName**, **UserName**, and **Password** strings. |

### RequestEvaluationCriteria element

The **RequestEvaluationCriteria** element provides the ability to evaluate the data returned by the request and determine the health of the URL. Each element is a complex type, which contains criteria that can be matched in one of three ways:

- Numeric criteria. This is the most common and is used to evaluate a measurable value, such as a returned status code or response time.
- Content match criteria. This is used to evaluate the content of the returned HTML to determine whether it contains a particular string of text.
- Custom criteria. This is an expression that matches on a variety of different available parameters defined by the user.

Any number of numeric criteria or custom criteria can be used, but only one content match criterion is allowed. The **RequestEvaluationCriteriaType** consists of the following elements:

|             **Element**              |   **Type**   |                                                                                                                                                                                                                                                      **Description**                                                                                                                                                                                                                                                       |
|--------------------------------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| StopProcessingIfWarningCriteriaIsMet |   Boolean    |                                                                                                                                                                                                                       If true, stops processing the request once the warning condition has been met.                                                                                                                                                                                                                       |
|  StopProcessingIfErrorCriteriaIsMet  |   Boolean    |                                                                                                                                                                                                                        If true, stops processing the request once the error condition has been met.                                                                                                                                                                                                                        |
|      BasePageEvaluationCriteria      | Complex type |                                                                                                                                                                                    Consists of two elements evaluating the base page,  **WarningCriteria**  and  **ErrorCriteria** , both of type  **BasePageEvaluationCriteriaType**.                                                                                                                                                                                     |
|       LinksEvaluationCriteria        | Complex type |                              Consists of two elements evaluating the links on the page, **WarningCriteria** and **ErrorCriteria**, both of type  **ChildRequestsEvaluationCriteriaType**. **ChildRequestsEvaluationCriteriaType** consists of zero or more **NumericCriteriaExpressions** of type  **RequestEvaluationNumericCriteriaType**, zero or one **StatusCodeCriteria** of type  **ListNumericRequestCriteriaType**, and zero or more **CustomCriteria** of type  **ExpressionType**.                              |
|     ResourcesEvaluationCriteria      | Complex type |                            Consists of two elements evaluating the resources on the page, **WarningCriteria** and **ErrorCriteria**, both of type  **ChildRequestsEvaluationCriteriaType**. **ChildRequestsEvaluationCriteriaType** consists of zero or more **NumericCriteriaExpressions** of type  **RequestEvaluationNumericCriteriaType**, zero or one **StatusCodeCriteria** of type  **ListNumericRequestCriteriaType**, and zero or one **CustomCriteria** of type  **ExpressionType**.                             |
|   WebPageTotalEvaluationCritieria    | Complex type | Consists of two elements,  **WarningCriteria** and **ErrorCriteria**, both of type  **WebPageTotalEvaluationCriteriaType** (see below). **WebPageTotalEvaluationCriteriaType** measures the total statistics for the page, including the base page, links, and resources, and is of type **WebPageTotalEvaluationCriteriaType**.  **WebPageTotalEvaluationCriteriaType** consists only of zero or more instances of  **NumericCriteriaExpression**, which is of **RequestEvaluationNumericCriteriaType**, described below. |
|       DepthEvaluationCriteria        | Complex type |                                                                                                                                       Consists of two elements, **WarningCriteria**  and **ErrorCriteria**, both of type **DepthEvaluationCriteriaType**. **DepthEvaluationCriteriaType** consists of zero or one instance(s) of  **ListNumericRequestCriteriaType**, discussed below.                                                                                                                                       |

The most common type of evaluation is numeric, in which an item of returned data, such as a resolution time, is compared against a configured threshold. **NumericCriteriaExpression** is of type **RequestEvaluationNumericCriteriaType**, which has three elements: **NumericRequestMetric**, **Operator**, and **Value**.

**NumericRequestMetric** is of type **NumericRequestMetricType**, which is an enumeration that can consist one of a number of metrics. Each metric is associated with a specific evaluation criterion, as follows:

| **Criteria** | **Metric** |
| --- | --- |
| BasePageData | DNSResolutionTime |
|| TCPConnectTime |
|| TimeToFirstByte |
|| TimeToLastByte |
|| RedirectTime |
|| DownloadTime |
|| TotalResponseTime |
|| ContentSize |
|| StatusCode |
|| DaysToExpiry |
| LinkData | AggregateDNSResolutionTime |
|| AggregateTCPConnectTime |
|| AggregateTimeToFirstByte |
|| AggregateTimeToLastByte |
|| AggregateRedirectTime |
|| AggregateDownloadTime |
|| AggregateTotalResponseTime |
|| AggregateContentSize |
| ResourceData | AggregateDNSResolutionTime |
|| AggregateTCPConnectTime |
|| AggregateTimeToFirstByte |
|| AggregateTimeToLastByte |
|| AggregateRedirectTime |
|| AggregateDownloadTime |
|| AggregateTotalResponseTime |
|| AggregateContentSize |
| TotalData | AggregateDNSResolutionTime |
|| AggregateTCPConnectTime |
|| AggregateTimeToFirstByte |
|| AggregateTimeToLastByte |
|| AggregateRedirectTime |
|| AggregateDownloadTime |
|| AggregateTotalResponseTime |
|| AggregateContentSize |
| None | TransactionResponseTime |

The **Operator** element is of type **CriteriaCompareType**, which consists of one of the following: **Equal**, **NotEqual**, **Greater**, **Less**, **GreaterEqual**, or **LessEqual**.

The **Value** element is of type **double**, and specifies the type of the value being compared.

If the returned data item you wish to evaluate is not numeric, such as a content evaluation, you will need to compare against a string. **ContentMatchCriteria** is of type **RequestEvaluationStringCriteriaType**, which has two subelements: **Operator** and **Value**. **Operator** can be one of two types:

- **SimpleStringOperator**, which is of type **CriteriaCompareType**, which is an enumeration consisting of **Equal**, **NotEqual**, **Greater**, **Less**, or **GreaterEqual**.
- **RegExOperator**, which is of type **RegExCompareType**, which is an enumeration type consisting of  **ContainsSubstring**, **MatchesWildcard**, **MatchesRegularExpression**, **MatchesMOM2005RegularExpression**, **MatchesMOM2005BooleanRegularExpression**, **DoesNotContainSubstring**, **DoesNotMatchWildcard**, **DoesNotMatchRegularEspression**, **DoesNotMatchMOM2005RegularExpression**, or  **DoesNotMatchMOM2005BooleanRegularExpression**

The other element of **RequestEvaluationStringCriteriaType** is **Value**, which is a string to be compared.

The **CustomCriteria** element is of type **ExpressionType**.

The **StatusCodeCriteria** element found in **LinksEvaluationCriteria** and **ResourcesEvaluationCriteria** is of type  **ListNumericRequestCriteriaType**. **ListNumericRequestCriteriaType** consists of a sequence of three elements: **ListNumericRequestMetric**, which can only be the string StatusCode, **Operator**, which is of  **CriteriaCompareType**, covered earlier, and a **Value**, which must be of type double.

The key to creating a useful URL probe is in the **Request** element, and usually in the **NumericRequestMetric**. If you know what part of the web page you're trying to evaluate, you can choose the correct metric from the enumeration. However, ensure to select the correct category of metric. The metrics for link data, resource data, and total data are all aggregates, and are available for all three categories. So ensure to specify the correct category and ask for it in the correct part of the **Request** element.

If you only want to evaluate the status code for a particular part of the page (base page, links), use the **StatusCodeCriteria** element, which would look like this:

```
<StatusCodeCriteria>
  <ListNumericRequestMetric>StatusCode</ListNumericRequestMetric>
  <Operator>GreaterEqual</Operator>
  <Value>400</Value>
</StatusCodeCriteria>
```

This **StatusCodeCriteria** section checks for a success response from the probe (Status code greater than or equal to 400).

## Composition

The **Microsoft.SystemCenter.WebApplication.UrlProbe** module is a native module.

## Related modules

| **Module Type** | **Usage** |
| --- | --- |
| **Microsoft.SystemCenter.WebApplication.OKCriteriaMatch** | Condition detection module used to evaluate when the data source module returns a value of 1 (OK). |
| **Microsoft.SystemCenter.WebApplication.WarningCriteriaMatch** | Condition detection module used to evaluate when the data source module returns a value of 1 (Warning). |
| **Microsoft.SystemCenter.WebApplication.ErrorCriteriaMatch** | Condition detection module used to evaluate when the data source module returns a value of 1 (Error). |
| **Microsoft.SystemCenter.WebApplication.Boolean.CriteriaDoesNotMatch** | Condition detection module used to evaluate when the data source module returns a value of false. |
| **Microsoft.SystemCenter.WebApplication.Boolean.CriteriaMatch** | Condition detection module used to evaluate when the data source module returns a value of true. |

## External module references

| **Module Type** | **Usage** |
| --- | --- |
| **Microsoft.SystemCenter.WebApplication.SingleUrlProbe** | Tests a single URL to determine if the status code is anything other than 200. |

## Sample

The following example carries out a simple URL probe against the URL [http://www.microsoft.com](https://www.microsoft.com/). The data source evaluates the status code returned for the base page, and returns a value of 3 if the status code is greater than 400, indicating an error state. It also evaluates the status code returned for the resources, and links, and returns a value of 2 if the status code is greater than 400, indicating a warning state.

```
<TypeDefinitions>
 <ModuleTypes>
   <DataSourceModuleType ID="MPAuthor.WebApplications.UrlDataSource" Accessibility="Public" Batching="false">
     <Configuration />
     <ModuleImplementation Isolation="Any">
       <Composite>
         <MemberModules>
           <DataSource ID="Scheduler" TypeID="MicrosoftSystemCenterWebApplicationLibrary!Microsoft.SystemCenter.WebApplication.PerProbe.Scheduler">
             <Scheduler>
               <SimpleReccuringSchedule>
                 <Interval Unit="Seconds">120</Interval>
                 <SpreadInitializationOverInterval Unit="Seconds">120</SpreadInitializationOverInterval>
               </SimpleReccuringSchedule>
               <ExcludeDates />
             </Scheduler>
             <UniquenessKey>$Target/Id$</UniquenessKey>
           </DataSource>
           <ProbeAction ID="Probe" TypeID="MicrosoftSystemCenterWebApplicationLibrary!Microsoft.SystemCenter.WebApplication.UrlProbe">
             <Proxy />
             <ProxyUserName />
             <ProxyPassword />
             <ProxyAuthenticationScheme>None</ProxyAuthenticationScheme>
             <CredentialUserName />
             <CredentialPassword />
             <AuthenticationScheme>None</AuthenticationScheme>
             <IgnoreServerCertError>false</IgnoreServerCertError>
             <FollowRedirects>true</FollowRedirects>
             <RetryCount>0</RetryCount>
             <RequestTimeout>0</RequestTimeout>
             <Requests>
               <Request>
                 <RequestID>1</RequestID>
                 <URL>http://www.microsoft.com</URL>
                 <Verb>GET</Verb>
                 <Version>HTTP/1.1</Version>
                 <HttpHeaders>
                   <HttpHeader>
                     <Name>User-Agent</Name>
                     <Value>Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)</Value>
                   </HttpHeader>
                 </HttpHeaders>
                 <Body />
                 <CheckContentChange>false</CheckContentChange>
                 <ContentHash>00000000-0000-0000-0000-000000000000</ContentHash>
                 <Depth>0</Depth>
                 <ThinkTime>0</ThinkTime>
                 <CheckInternalLinks>false</CheckInternalLinks>
                 <CheckExternalLinks>false</CheckExternalLinks>
                 <CheckResources>false</CheckResources>
                 <RequestEvaluationCriteria>
                   <StopProcessingIfWarningCriteriaIsMet>false</StopProcessingIfWarningCriteriaIsMet>
                   <StopProcessingIfErrorCriteriaIsMet>false</StopProcessingIfErrorCriteriaIsMet>
                   <BasePageEvaluationCriteria>
                     <WarningCriteria />
                     <ErrorCriteria>
                       <NumericCriteriaExpressions>
                         <NumericCriteriaExpression>
                           <NumericRequestMetric>BasePageData/StatusCode</NumericRequestMetric>
                           <Operator>GreaterEqual</Operator>
                           <Value>400</Value>
                         </NumericCriteriaExpression>
                       </NumericCriteriaExpressions>
                     </ErrorCriteria>
                   </BasePageEvaluationCriteria>
                   <LinksEvaluationCriteria>
                     <WarningCriteria>
                       <StatusCodeCriteria>
                         <ListNumericRequestMetric>StatusCode</ListNumericRequestMetric>
                         <Operator>GreaterEqual</Operator>
                         <Value>400</Value>
                       </StatusCodeCriteria>
                     </WarningCriteria>
                     <ErrorCriteria />
                   </LinksEvaluationCriteria>
                   <ResourcesEvaluationCriteria>
                     <WarningCriteria>
                       <StatusCodeCriteria>
                         <ListNumericRequestMetric>StatusCode</ListNumericRequestMetric>
                         <Operator>GreaterEqual</Operator>
                         <Value>400</Value>
                       </StatusCodeCriteria>
                     </WarningCriteria>
                     <ErrorCriteria />
                   </ResourcesEvaluationCriteria>
                   <WebPageTotalEvaluationCriteria>
                     <WarningCriteria />
                     <ErrorCriteria />
                   </WebPageTotalEvaluationCriteria>
                   <DepthEvaluationCriteria>
                     <WarningCriteria />
                     <ErrorCriteria />
                   </DepthEvaluationCriteria>
                 </RequestEvaluationCriteria>
                 <FormsAuthCredentials />
                 <CollectResponseBody>OnContentMatchCriteria</CollectResponseBody>
                 <CollectLinksHeaders>false</CollectLinksHeaders>
                 <CollectResourcesHeaders>false</CollectResourcesHeaders>
               </Request>
             </Requests>
           </ProbeAction>
         </MemberModules>
         <Composition>
           <Node ID="Probe">
             <Node ID="Scheduler" />
           </Node>
         </Composition>
       </Composite>
     </ModuleImplementation>
     <OutputType>MicrosoftSystemCenterWebApplicationLibrary!Microsoft.SystemCenter.WebApplication.WebApplicationData</OutputType>
   </DataSourceModuleType>
 </ModuleTypes>
 <MonitorTypes>
   <UnitMonitorType ID="MPAuthor.WebApplications.BasePageErrorCodeMonitor" Accessibility="Internal">
     <MonitorTypeStates>
       <MonitorTypeState ID="ErrorCodeFailure" NoDetection="false" />
       <MonitorTypeState ID="ErrorCodeSuccess" NoDetection="false" />
     </MonitorTypeStates>
     <Configuration>
       <xsd:element minOccurs="1" name="RequestID" type="xsd:integer" />
     </Configuration>
     <MonitorImplementation>
       <MemberModules>
         <DataSource ID="DS1" TypeID="MPAuthor.WebApplications.UrlDataSource" />
         <ConditionDetection ID="CDErrorCodeFailureTrue" TypeID="System!System.ExpressionFilter">
           <Expression>
             <SimpleExpression>
               <ValueExpression>
                 <XPathQuery>RequestResults/RequestResult[@Id="$Config/RequestID$"]/BasePageData/ErrorCode</XPathQuery>
               </ValueExpression>
               <Operator>NotEqual</Operator>
               <ValueExpression>
                 <XPathQuery>0</XPathQuery>
               </ValueExpression>
             </SimpleExpression>
           </Expression>
         </ConditionDetection>
         <ConditionDetection ID="CDErrorCodeFailureFalse" TypeID="System!System.ExpressionFilter">
           <Expression>
             <SimpleExpression>
               <ValueExpression>
                 <XPathQuery>RequestResults/RequestResult[@Id="$Config/RequestID$"]/BasePageData/ErrorCode</XPathQuery>
               </ValueExpression>
               <Operator>Equal</Operator>
               <ValueExpression>
                 <XPathQuery>0</XPathQuery>
               </ValueExpression>
             </SimpleExpression>
           </Expression>
         </ConditionDetection>
       </MemberModules>
       <RegularDetections>
         <RegularDetection MonitorTypeStateID="ErrorCodeFailure">
           <Node ID="CDErrorCodeFailureTrue">
             <Node ID="DS1" />
           </Node>
         </RegularDetection>
         <RegularDetection MonitorTypeStateID="ErrorCodeSuccess">
           <Node ID="CDErrorCodeFailureFalse">
             <Node ID="DS1" />
           </Node>
         </RegularDetection>
       </RegularDetections>
     </MonitorImplementation>
   </UnitMonitorType>
 </MonitorTypes>
</TypeDefinitions>
```

## Information

| ** ** | ** ** |
| --- | --- |
| Module Type | [ProbeActionModuleType](/previous-versions/system-center/developer/bb465288%28v%3dmsdn.10%29) |
| Input Type | None |
| Output Type | Microsoft.SystemCenter.WebApplication.WebApplicationData |
| Implementation | Native |
| Library | **Microsoft.SystemCenter.WebApplication.Library** |
