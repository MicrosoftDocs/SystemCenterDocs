---
ms.assetid: 29218447-0e0b-4aba-86c6-dbb1a35e05e0
title: Microsoft.SystemCenter.WebApplication.UrlProbe
description: This article provides schema for URLprobe.
author: JYOTHIRMAISURI
ms.author: V-jysur
manager: vvithal
ms.date: 02/24/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
MonikerRange: 'sc-om-2019'
---

# Microsoft.SystemCenter.WebApplication.UrlProbe

The **Microsoft.SystemCenter.WebApplication.UrlProbe** probe module connects to one or more URLs and returns **Microsoft.SystemCenter.WebApplication.WebApplicationData.** This data can then be used with other modules from the **Microsoft.SystemCenter.WebApplication.Library** to evaluate the health state of various aspects of the target web site.

## Usage

The primary function of **Microsoft.SystemCenter.WebApplication.UrlProbe** is to send a request to one or more URLs and report on the results. The format of the request is a complex type, and is used with other modules to evaluate the health state of the target URL. Because large numbers of requests can be made with a single probe, and because the results of the request can contain a large amount of data, the probe itself carries out some evaluation of the request before producing the output. For example, instead of just providing the status code from the queried URL as output, the module compares the status code against a specified range, and provides a success or failure code as output. The module can also match the content of the HTML that is returned by the request, for example, matching the word “error” to determine if an error page was returned. This evaluation performed by the module removes the need for complex expression matching logic in your rule or monitor.

This module is often commonly triggered using [Microsoft.SystemCenter.WebApplication.PerProbe.Scheduler](https://docs.microsoft.com/previous-versions/system-center/developer/jj130146(v%3dmsdn.10)).

The **Microsoft.SystemCenter.WebApplication.UrlProbe** module is commonly used with a number of condition detection modules which are intended to evaluate its output. The module evaluates different aspects of the health of the URL based on parameters defined in the request and returns appropriate output for each.

Some of those parameters evaluate directly to a health state. For these parameters, you would use three condition detection modules, each of which matches a specific integer output from the probe indicating a particular health state, as shown in the following table:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Condition Detection Module</th>
<th>Matched value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Microsoft.SystemCenter.WebApplication.OKCriteriaMatch</strong></p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><strong>Microsoft.SystemCenter.WebApplication.WarningCriteriaMatch</strong></p></td>
<td><p>2</p></td>
</tr>
<tr class="odd">
<td><p><strong>Microsoft.SystemCenter.WebApplication.ErrorCriteriaMatch</strong></p></td>
<td><p>3</p></td>
</tr>
</tbody>
</table>


Other parameters return a binary status. For those cases, two condition detection modules are used, each of which matches a Boolean type from the probe as shown in the following table:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Condition Detection Module</th>
<th>Matched value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Microsoft.SystemCenter.WebApplication.Boolean.CriteriaDoesNotMatch</strong></p></td>
<td><p>false</p></td>
</tr>
<tr class="even">
<td><p><strong>Microsoft.SystemCenter.WebApplication.Boolean.CriteriaMatch</strong></p></td>
<td><p>true</p></td>
</tr>
</tbody>
</table>


Finally, some raw values are returned, which you can either collect for analysis and reporting or use with expression filter condition detection modules.

## Type Definition

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
       <OverrideableParameters>
          <OverrideableParameter ID="Proxy" Selector="$Config/Proxy$" ParameterType="string" />
          <OverrideableParameter ID="ProxyUserName" Selector="$Config/ProxyUserName$" ParameterType="string" />
          <OverrideableParameter ID="ProxyPassword" Selector="$Config/ProxyPassword$" ParameterType="string" />
          <OverrideableParameter ID="ProxyAuthenticationScheme" Selector="$Config/ProxyAuthenticationScheme$" ParameterType="string" />
                    <OverrideableParameter ID="CredentialUserName" Selector="$Config/CredentialUserName$" ParameterType="string" />
          <OverrideableParameter ID="CredentialPassword" Selector="$Config/CredentialPassword$" ParameterType="string" />
          <OverrideableParameter ID="AuthenticationScheme" Selector="$Config/AuthenticationScheme$" ParameterType="string" />
          <OverrideableParameter ID="IgnoreServerCertError" Selector="$Config/IgnoreServerCertError$"  ParameterType="bool"/>
          <OverrideableParameter ID="FollowRedirects" Selector="$Config/FollowRedirects$" ParameterType="bool" />
          <OverrideableParameter ID="RetryCount" Selector="$Config/RetryCount$" ParameterType="int" />
          <OverrideableParameter ID="RequestTimeout" Selector="$Config/RequestTimeout$" ParameterType="int" />
       </OverrideableParameters>
       <ModuleImplementation Isolation="Any">
          <Native>
             <ClassID>92C599FD-6639-4A9F-90DA-E1350162A318</ClassID>
          </Native>
       </ModuleImplementation>
       <OutputType>Microsoft.SystemCenter.WebApplication.WebApplicationData</OutputType>
       <TriggerOnly>true</TriggerOnly>
    </ProbeActionModuleType>

## Parameters

The **Microsoft.SystemCenter.WebApplication.UrlProbe** module supports the configuration parameters described in the following table.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Type</th>
<th>Overrideable</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Proxy</em></p></td>
<td><p><strong>String</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter, but can be empty. Specifies the name of the proxy server if the agent requires one to access the URL.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyUserName</em></p></td>
<td><p><strong>String</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter, but can be empty. Specifies the username to be used with the proxy server if the specified proxy server requires authentication.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyPassword</em></p></td>
<td><p><strong>String</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter, but can be empty. Specifies the password to be used with the proxy server if the specified proxy server requires authentication.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyAuthenticationScheme</em></p></td>
<td><p><strong>AuthenticationSchemeType</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter. Specifies the authentication scheme to be used with the proxy server, if the agent requires one to access the URL. Valid values are <strong>None</strong>, <strong>Basic</strong>, <strong>NTLM</strong>, <strong>Digest</strong>, and <strong>Negotiate</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>CredentialUserName</em></p></td>
<td><p><strong>String</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter, but can be empty. Specifies the username to be used with the URL being queried.</p></td>
</tr>
<tr class="even">
<td><p><em>CredientialPassword</em></p></td>
<td><p><strong>String</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter, but can be empty. Specifies the password to be used with the URL being queried.</p></td>
</tr>
<tr class="odd">
<td><p><em>AuthenticationScheme</em></p></td>
<td><p><strong>AuthenticationSchemeType</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter. Specifies the authentication scheme to be used with the URL being queried. Valid values are <strong>None</strong>, <strong>Basic</strong>, <strong>NTLM</strong>, <strong>Digest</strong>, and <strong>Negotiate</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Ignore Server Certifcate</em></p></td>
<td><p><strong>Boolean</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter. Specifies whether the server certificate errors should be ignored.</p></td>
</tr>
<tr class="even">
<td><p><em>FollowRedirects</em></p></td>
<td><p><strong>Boolean</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter. Specifies whether the query should follow URL redirects.</p></td>
</tr>
<tr class="odd">
<td><p><em>RetryCount</em></p></td>
<td><p><strong>Integer</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter. Specifies the number of times the module should retry the specified URL before timing out.</p></td>
</tr>
<tr class="even">
<td><p><em>RequestTimeout</em></p></td>
<td><p><strong>Integer</strong></p></td>
<td><p>True</p></td>
<td><p>Required parameter. Specifies the length of time to wait for a response from the specified URL before retrying.</p></td>
</tr>
<tr class="odd">
<td><p><em>Requests</em></p></td>
<td><p>Complex Type</p></td>
<td><p>False</p></td>
<td><p>Collection of <strong>Request</strong> elements (see below).</p></td>
</tr>
<tr class="even">
<td><p><em>TransactionResponseTimeWarningCriteria</em></p></td>
<td><p><strong>RequestEvaluationNumericCriteriaType</strong></p></td>
<td><p>False</p></td>
<td><p>Optional parameter. Specifies the response time at which to specify a warning.</p></td>
</tr>
<tr class="odd">
<td><p><em>TransactionResponseTimeErrorCriteria</em></p></td>
<td><p><strong>RequestEvaluationNumericCriteriaType</strong></p></td>
<td><p>False</p></td>
<td><p>Optional Parameter. Specifies the response time at which to specify an error.</p></td>
</tr>
<tr class="even">
<td><p><em>PerformanceCollectionFrequencyInCycles</em></p></td>
<td><p><strong>Integer</strong></p></td>
<td><p>False</p></td>
<td><p>Optional Parameter. Specifies how many query intervals must be completed before each collection. If the value is 1, then the counters will be collected each time the browser session is run. If it is 2, then the counters will only be collected every second time the browser session is run, and so on.</p></td>
</tr>
</tbody>
</table>


### Request Element

The **Requests** element is a collection of one or more **Request** elements. Each **Request** element has a **RequestID** subelement which uniquely identifies the request within that set of **Requests**. Requests are processed in order, according to their **RequestID**. The **Request** element consists of the following elements:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Element</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestID</em></p></td>
<td><p><strong>Integer</strong></p></td>
<td><p>Because each probe can initiate multiple requests, the <strong>RequestID</strong> uniquely identifies each request and specifies the order that the requests will be processed.</p></td>
</tr>
<tr class="even">
<td><p><em>URL</em></p></td>
<td><p><strong>String</strong></p></td>
<td><p>The URL to be queried.</p></td>
</tr>
<tr class="odd">
<td><p><em>Verb</em></p></td>
<td><p><strong>VerbType</strong></p></td>
<td><p>Indicates the verb to use with the URL request. Can take any of the following values: GET, HEAD, or POST.</p></td>
</tr>
<tr class="even">
<td><p><em>Version</em></p></td>
<td><p><strong>VersionType</strong></p></td>
<td><p>Indicates the HTTP type for the request. Valid values are HTTP/1.0 and HTTP/1.1.</p></td>
</tr>
<tr class="odd">
<td><p><em>HttpHeaders</em></p></td>
<td><p><strong>HttpHeadersType</strong></p></td>
<td><p>HTTP headers for the request. The <strong>HttpHeadersType</strong> is a complex type consisting of 0 or more <strong>HttpHeader</strong> elements, which are of type <strong>NameValueType</strong>. The <strong>NameValueType</strong>, in turn consists of two required elements, Name and Value.</p></td>
</tr>
<tr class="even">
<td><p><em>Body</em></p></td>
<td><p><strong>String</strong></p></td>
<td><p>The value will be empty if the <strong>VerbType</strong> is GET or HEAD. If the <strong>VerbType</strong> is POST. This is the body of the request submitted by the post.</p></td>
</tr>
<tr class="odd">
<td><p><em>CheckContentChange</em></p></td>
<td><p><strong>Boolean</strong></p></td>
<td><p>If true, provides additional content validation.</p></td>
</tr>
<tr class="even">
<td><p><em>ContentHash</em></p></td>
<td><p><strong>ContentHashType</strong></p></td>
<td><p>Consists of a string of 36 characters, hexadecimal 8-4-4-4-12.</p></td>
</tr>
<tr class="odd">
<td><p><em>Depth</em></p></td>
<td><p><strong>Integer</strong></p></td>
<td><p>Specifies the number of levels of external links to collect. If the value is 0, only the links on the page itself are evaluated. If the value is 1, then the links on each target page are evaluated. If the value is 2, then the links on those target pages are evaluated, and so on.</p></td>
</tr>
<tr class="even">
<td><p><em>ThinkTime</em></p></td>
<td><p><strong>Integer</strong></p></td>
<td><p>Amount of time to wait between the request and collection of the body.</p></td>
</tr>
<tr class="odd">
<td><p><em>CheckInternalLinks</em></p></td>
<td><p><strong>Boolean</strong></p></td>
<td><p>Enables collection of the status of each internal link and includes internal links in the evaluation of the monitor for the request. An internal link is a link that refers to a location on the same page.</p></td>
</tr>
<tr class="even">
<td><p><em>CheckExternalLinks</em></p></td>
<td><p><strong>Boolean</strong></p></td>
<td><p>Enables collection of the status of each external link and includes external links in the evaluation of the monitor for the request. An external link is a link that refers to a location outside the current page.</p></td>
</tr>
<tr class="odd">
<td><p><em>CheckResources</em></p></td>
<td><p><strong>Boolean</strong></p></td>
<td><p>If true, the monitor returns the status of the resources for the page. Instead of measuring each individual resource, the total of all resources are evaluated. If false, the resource monitor is not functional for the request.</p></td>
</tr>
<tr class="even">
<td><p><em>RequestEvaluationCriteria</em></p></td>
<td><p><strong>RequestEvaluationCriteriaType</strong></p></td>
<td><p>A complex type that evaluates the data returned by the request (see below).</p></td>
</tr>
<tr class="odd">
<td><p><em>FormsAuthCredentials</em></p></td>
<td><p><strong>FormsAuthCredentialsType</strong></p></td>
<td><p>Complex type that consists of <strong>CredentialName</strong>, <strong>UserName</strong>, and <strong>Password</strong> strings.</p></td>
</tr>
</tbody>
</table>


### RequestEvaluationCriteria Element

The **RequestEvaluationCriteria** element provides the ability to evaluate the data returned by the request and determine the health of the URL. Each element is a complex type, which contains criteria that can be matched in one of three ways:

  - Numeric criteria. This is the most common and is used to evaluate a measurable value, such as a returned status code or response time.  

  - Content match criteria. This is used to evaluate the content of the returned HTML to determine whether it contains a particular string of text.  

  - Custom criteria. This is an expression that matches on a variety of different available parameters defined by the user.  


Any number of numeric criteria or custom criteria can be used, but only one content match criterion is allowed. The **RequestEvaluationCriteriaType** consists of the following elements:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Element</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>StopProcessingIfWarningCriteriaIsMet</p></td>
<td><p>Boolean</p></td>
<td><p>If true, stops processing the request once the warning condition has been met.</p></td>
</tr>
<tr class="even">
<td><p>StopProcessingIfErrorCriteriaIsMet</p></td>
<td><p>Boolean</p></td>
<td><p>If true, stops processing the request once the error condition has been met.</p></td>
</tr>
<tr class="odd">
<td><p>BasePageEvaluationCriteria</p></td>
<td><p>Complex type</p></td>
<td><p>Consists of two elements evaluating the base page, <strong>WarningCriteria</strong> and <strong>ErrorCriteria</strong>, both of type <strong>BasePageEvaluationCriteriaType</strong>.</p>
<p><strong>BasePageEvaluationCriteriaType</strong> is used to evaluate the health status of the base page retrieved by the URL. Consists of zero or more <strong>NumericCriteriaExpressions</strong> of type <strong>RequestEvaluationNumericCriteriaType</strong>, zero or one <strong>ContentMatchCriteria</strong> of type <strong>RequestEvaluationStringCriteriaType</strong>, and zero or more <strong>CustomCriteria</strong> of type <strong>ExpressionType</strong>.</p></td>
</tr>
<tr class="even">
<td><p>LinksEvaluationCriteria</p></td>
<td><p>Complex type</p></td>
<td><p>Consists of two elements evaluating the links on the page, <strong>WarningCriteria</strong> and <strong>ErrorCriteria</strong>, both of type <strong>ChildRequestsEvaluationCriteriaType</strong>.</p>
<p><strong>ChildRequestsEvaluationCriteriaType</strong> consists of zero or more <strong>NumericCriteriaExpressions</strong> of type <strong>RequestEvaluationNumericCriteriaType</strong>, zero or one <strong>StatusCodeCriteria</strong> of type <strong>ListNumericRequestCriteriaType</strong>, and zero or more <strong>CustomCriteria</strong> of type <strong>ExpressionType</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>ResourcesEvaluationCriteria</p></td>
<td><p>Complex type</p></td>
<td><p>Consists of two elements evaluating the resources on the page, <strong>WarningCriteria</strong> and <strong>ErrorCriteria</strong>, both of type <strong>ChildRequestsEvaluationCriteriaType</strong>.</p>
<p><strong>ChildRequestsEvaluationCriteriaType</strong> consists of zero or more <strong>NumericCriteriaExpressions</strong> of type <strong>RequestEvaluationNumericCriteriaType</strong>, zero or one <strong>StatusCodeCriteria</strong> of type <strong>ListNumericRequestCriteriaType</strong>, and zero or one <strong>CustomCriteria</strong> of type <strong>ExpressionType</strong>.</p></td>
</tr>
<tr class="even">
<td><p>WebPageTotalEvaluationCritieria</p></td>
<td><p>Complex type</p></td>
<td><p>Consists of two elements, <strong>WarningCriteria</strong> and <strong>ErrorCriteria</strong>, both of type <strong>WebPageTotalEvaluationCriteriaType</strong> (see below).</p>
<p><strong>WebPageTotalEvaluationCriteriaType</strong> measures the total statistics for the page, including the base page, links, and resources, and is of type <strong>WebPageTotalEvaluationCriteriaType</strong>. <strong>WebPageTotalEvaluationCriteriaType</strong> consists only of zero or more instances of <strong>NumericCriteriaExpression</strong>, which is of <strong>RequestEvaluationNumericCriteriaType</strong>, described below.</p></td>
</tr>
<tr class="odd">
<td><p>DepthEvaluationCriteria</p></td>
<td><p>Complex type</p></td>
<td><p>Consists of two elements, <strong>WarningCriteria</strong> and <strong>ErrorCriteria</strong>, both of type <strong>DepthEvaluationCriteriaType</strong>.</p>
<p><strong>DepthEvaluationCriteriaType</strong> consists of zero or one instances of <strong>ListNumericRequestCriteriaType</strong>, discussed below.</p></td>
</tr>
</tbody>
</table>


The most common type of evaluation is numeric, in which an item of returned data, such as a resolution time, is compared against a configured threshold. **NumericCriteriaExpression** is of type **RequestEvaluationNumericCriteriaType**, which has three elements: **NumericRequestMetric**, **Operator**, and **Value**.

**NumericRequestMetric** is of type **NumericRequestMetricType**, which is an enumeration that can consist one of a number of metrics. Each metric is associated with a specific evaluation criterion, as follows:


<table xmlns="http://www.w3.org/1999/xhtml">
            <tr>
              <th>
											Criteria
										</th>
              <th>
											Metric
										</th>
            </tr>
            <tr>
              <td rowspan="10">
                <p>BasePageData</p>
              </td>
              <td>
                <p>DNSResolutionTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>TCPConnectTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>TimeToFirstByte</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>TimeToLastByte</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>RedirectTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>DownloadTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>TotalResponseTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>ContentSize</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>StatusCode</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>DaysToExpiry</p>
              </td>
            </tr>
            <tr>
              <td rowspan="8">
                <p>LinkData</p>
              </td>
              <td>
                <p>AggregateDNSResolutionTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTCPConnectTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTimeToFirstByte</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTimeToLastByte</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateRedirectTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateDownloadTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTotalResponseTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateContentSize</p>
              </td>
            </tr>
            <tr>
              <td rowspan="8">
                <p>ResourceData</p>
              </td>
              <td>
                <p>AggregateDNSResolutionTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTCPConnectTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTimeToFirstByte</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTimeToLastByte</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateRedirectTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateDownloadTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTotalResponseTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateContentSize</p>
              </td>
            </tr>
            <tr>
              <td rowspan="8">
                <p>TotalData</p>
              </td>
              <td>
                <p>AggregateDNSResolutionTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTCPConnectTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTimeToFirstByte</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTimeToLastByte</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateRedirectTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateDownloadTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateTotalResponseTime</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>AggregateContentSize</p>
              </td>
            </tr>
            <tr>
              <td>
                <p>None</p>
              </td>
              <td>
                <p>TransactionResponseTime</p>
              </td>
            </tr>
          </table>


The **Operator** element is of type **CriteriaCompareType**, which consists of one of the following: **Equal**, **NotEqual**, **Greater**, **Less**, **GreaterEqual**, or **LessEqual**.

The **Value** element is of type **double**, and specifies the type of the value being compared.

If the returned data item you wish to evaluate is not numeric, such as a content evaluation, you will need to compare against a string. **ContentMatchCriteria** is of type **RequestEvaluationStringCriteriaType**, which has two subelements: **Operator** and **Value**. **Operator** can be one of two types:

  - **SimpleStringOperator**, which is of type **CriteriaCompareType**, which is an enumeration consisting of **Equal**, **NotEqual**, **Greater**, **Less**, or **GreaterEqual**.  

  - **RegExOperator**, which is of type **RegExCompareType**, which is an enumeration type consisting of **ContainsSubstring**, **MatchesWildcard**, **MatchesRegularExpression**, **MatchesMOM2005RegularExpression**, **MatchesMOM2005BooleanRegularExpression**, **DoesNotContainSubstring**, **DoesNotMatchWildcard**, **DoesNotMatchRegularEspression**, **DoesNotMatchMOM2005RegularExpression**, or **DoesNotMatchMOM2005BooleanRegularExpression**  


The other element of **RequestEvaluationStringCriteriaType** is **Value**, which is a string to be compared.

The **CustomCriteria** element is of type **ExpressionType**.

The **StatusCodeCriteria** element found in **LinksEvaluationCriteria** and **ResourcesEvaluationCriteria** is of type **ListNumericRequestCriteriaType**. **ListNumericRequestCriteriaType** consists of a sequence of three elements: **ListNumericRequestMetric**, which can only be the string “StatusCode”, **Operator**, which is of **CriteriaCompareType**, covered earlier, and a **Value**, which must be of type double.

The key to creating a useful URL probe is in the **Request** element, and usually in the **NumericRequestMetric**. If you know what part of the web page you’re trying to evaluate, you can choose the correct metric from the enumeration. However, be sure to select the correct category of metric. The metrics for link data, resource data, and total data are all aggregates, and are available for all three categories, so be sure to specify the correct category and ask for it in the correct part of the **Request** element.

If you only want to evaluate the status code for a particular part of the page (base page, links), use the **StatusCodeCriteria** element, which would look like this:

    <StatusCodeCriteria>
      <ListNumericRequestMetric>StatusCode</ListNumericRequestMetric>
      <Operator>GreaterEqual</Operator>
      <Value>400</Value>
    </StatusCodeCriteria>

This **StatusCodeCriteria** section checks for a success response from the probe (Status code greater than or equal to 400).

## Composition

The **Microsoft.SystemCenter.WebApplication.UrlProbe** module is a native module.

## Related Modules


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Module Type</th>
<th>Usage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Microsoft.SystemCenter.WebApplication.OKCriteriaMatch</strong></p></td>
<td><p>Condition detection module used to evaluate when the data source module returns a value of 1 (OK).</p></td>
</tr>
<tr class="even">
<td><p><strong>Microsoft.SystemCenter.WebApplication.WarningCriteriaMatch</strong></p></td>
<td><p>Condition detection module used to evaluate when the data source module returns a value of 1 (Warning).</p></td>
</tr>
<tr class="odd">
<td><p><strong>Microsoft.SystemCenter.WebApplication.ErrorCriteriaMatch</strong></p></td>
<td><p>Condition detection module used to evaluate when the data source module returns a value of 1 (Error).</p></td>
</tr>
<tr class="even">
<td><p><strong>Microsoft.SystemCenter.WebApplication.Boolean.CriteriaDoesNotMatch</strong></p></td>
<td><p>Condition detection module used to evaluate when the data source module returns a value of false.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Microsoft.SystemCenter.WebApplication.Boolean.CriteriaMatch</strong></p></td>
<td><p>Condition detection module used to evaluate when the data source module returns a value of true.</p></td>
</tr>
</tbody>
</table>


## External Module References


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Module Type</th>
<th>Usage</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Microsoft.SystemCenter.WebApplication.SingleUrlProbe</strong></p></td>
<td><p>Tests a single URL to determine if the status code is anything other than 200.</p></td>
</tr>
</tbody>
</table>


## Sample

The following example carries out a simple URL probe against the URL http://www.microsoft.com. The data source evaluates the status code returned for the base page, and returns a value of 3 if the status code is greater than 400, indicating an error state. It also evaluates the status code returned for the resources, and links, and returns a value of 2 if the status code is greater than 400, indicating a warning state.

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


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th> </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Module Type</p></td>
<td><p><a href="bb465288(v=msdn.10).md">ProbeActionModuleType</a></p></td>
</tr>
<tr class="even">
<td><p>Input Type</p></td>
<td><p>None</p></td>
</tr>
<tr class="odd">
<td><p>Output Type</p></td>
<td><p>Microsoft.SystemCenter.WebApplication.WebApplicationData</p></td>
</tr>
<tr class="even">
<td><p>Implementation</p></td>
<td><p>Native</p></td>
</tr>
<tr class="odd">
<td><p>Library</p></td>
<td><p><strong>Microsoft.SystemCenter.WebApplication.Library</strong></p></td>
</tr>
</tbody>
</table>
