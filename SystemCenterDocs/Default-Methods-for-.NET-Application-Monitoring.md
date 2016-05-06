---
title: Default Methods for .NET Application Monitoring
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6874fc3d-646b-46e7-965c-9ec6bac88500
---
# Default Methods for .NET Application Monitoring
Application Performance Monitoring in [!INCLUDE[om12short](../Token/om12short_md.md)] includes many functions and resources calls that are monitored by default.

## Functions Monitored by Default
Application Performance Monitoring includes many well\-known Microsoft .NET Framework functions that are monitored for slow performance or exception data collection.

### For SharePoint
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.Office.Excel.WebUI.ExcelWebRenderer.OnPreRender

-   Microsoft.Office.Excel.WebUI.InternalEwr.OnPreRender

-   Microsoft.SharePoint.Portal.WebControls.ContactFieldControl.OnPreRender

-   Microsoft.SharePoint.Portal.WebControls.IndicatorWebpart.OnPreRender

-   Microsoft.SharePoint.Portal.WebControls.KPIListWebPart.OnPreRender

-   Microsoft.SharePoint.WebPartPages.ContentEditorWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.ContentEditorWebPart.OnPreRender

-   Microsoft.SharePoint.WebPartPages.ListFormWebPart.OnPreRender

-   Microsoft.SharePoint.WebPartPages.ListFormWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.ListViewWebPart.CreateChildControls

-   Microsoft.SharePoint.WebPartPages.ListViewWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.ListViewWebPart.OnInit

-   Microsoft.SharePoint.WebPartPages.ListViewWebPart.OnPreRender

-   Microsoft.SharePoint.Portal.WebControls.BusinessDataActionsWebPart.RenderWebPart

-   Microsoft.SharePoint.Portal.WebControls.GroupDetailWebPart.RenderWebPart

-   Microsoft.SharePoint.Portal.WebControls.RelatedGroupsWebPart.RenderWebPart

-   Microsoft.SharePoint.Portal.WebControls.WebPartLoc.OnPreRender

-   Microsoft.SharePoint.Portal.WebControls.WebPartLoc.RenderWebPart

-   Microsoft.SharePoint.Search.Internal.WebControls.SearchPagingWebPart.OnPreRender

-   Microsoft.SharePoint.Search.Internal.WebControls.SearchPagingWebPart.RenderWebPart

-   Microsoft.SharePoint.Search.Internal.WebControls.SearchStatsWebPart.OnPreRender

-   Microsoft.SharePoint.Search.Internal.WebControls.SearchStatsWebPart.RenderWebPart

-   Microsoft.SharePoint.Search.Internal.WebControls.SearchSummaryWebPart.RenderWebPart

-   Microsoft.SharePoint.Search.Internal.WebControls.SearchSummaryWebPart.OnPreRender

-   Microsoft.SharePoint.WebPartPages.ImageWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.PageViewerWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.XmlWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.XmlWebPart.OnPreRender

-   Microsoft.SharePoint.WebPartPages.AggregationWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.ChartViewWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.DataViewWebPart.OnPreRender

-   Microsoft.SharePoint.WebPartPages.DataViewWebPart.RenderWebPart

-   Microsoft.SharePoint.WebPartPages.ListFormWebPart.OnLoad

-   Microsoft.SharePoint.WebPartPages.ListFormWebPart.OnInit

-   Microsoft.SharePoint.Portal.WebControls.BusinessDataWebPart.GetCallbackResult

-   Microsoft.SharePoint.Portal.WebControls.BusinessDataDetailsWebPart.CreateChildControls

-   Microsoft.SharePoint.Portal.WebControls.BusinessDataListWebPart.CreateChildControls

-   Microsoft.Office.Server.ApplicationRegistry.MetadataModel.Entity.ExecuteInternal

-   Microsoft.Office.Server.ApplicationRegistry.SystemSpecific.WebService.WebServiceSystemUtility.ExecuteStatic

-   Microsoft.Office.Server.ApplicationRegistry.SystemSpecific.Db.DbSystemUtility.ExecuteStatic

-   Microsoft.SharePoint.WebPartPages.DataFormWebPart.OnPreRender

### For SharePoint: Base Classes Monitoring
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   System.Web.UI.WebControls.WebParts.WebPart.OnDataBinding

-   System.Web.UI.WebControls.WebParts.WebPart.OnPreRender

-   System.Web.UI.WebControls.WebParts.WebPart.OnInit

-   System.Web.UI.WebControls.WebParts.WebPart.OnLoad

-   System.Web.UI.WebControls.WebParts.WebPart.Render

-   System.Web.UI.WebControls.WebParts.WebPart.RenderWebPart

-   System.Web.UI.WebControls.WebParts.WebPart.OnUnload

-   \[System.Web.UI.WebControls.WebParts.WebPart\].OnDataBinding

-   \[System.Web.UI.WebControls.WebParts.WebPart\].OnPreRender

-   \[System.Web.UI.WebControls.WebParts.WebPart\].OnInit

-   \[System.Web.UI.WebControls.WebParts.WebPart\].OnLoad

-   \[System.Web.UI.WebControls.WebParts.WebPart\].Render

-   \[System.Web.UI.WebControls.WebParts.WebPart\].RenderWebPart

-   \[System.Web.UI.WebControls.WebParts.WebPart\].OnUnload

-   \[Microsoft.SharePoint.WebPartPages.WebPart\].OnDataBinding

-   \[Microsoft.SharePoint.WebPartPages.WebPart\].OnPreRender

-   \[Microsoft.SharePoint.WebPartPages.WebPart\].OnInit

-   \[Microsoft.SharePoint.WebPartPages.WebPart\].OnLoad

-   \[Microsoft.SharePoint.WebPartPages.WebPart\].Render

-   \[Microsoft.SharePoint.WebPartPages.WebPart\].RenderWebPart

-   \[Microsoft.SharePoint.WebPartPages.WebPart\].OnUnload

### For SharePoint: SPrequest Methods, Basic SharePoint 2007 APIs
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.SharePoint.Library.SPRequest.AccessContentTypes

-   Microsoft.SharePoint.Library.SPRequest.AddField

-   Microsoft.SharePoint.Library.SPRequest.AddGroup

-   Microsoft.SharePoint.Library.SPRequest.AddMeeting

-   Microsoft.SharePoint.Library.SPRequest.AddMeetingFromEvent

-   Microsoft.SharePoint.Library.SPRequest.AddMeetingFromICal

-   Microsoft.SharePoint.Library.SPRequest.AddNavigationNode

-   Microsoft.SharePoint.Library.SPRequest.AddOnProvision

-   Microsoft.SharePoint.Library.SPRequest.AddOrDeleteUrl

-   Microsoft.SharePoint.Library.SPRequest.AddOrUpdateItem

-   Microsoft.SharePoint.Library.SPRequest.AddRoleDef

-   Microsoft.SharePoint.Library.SPRequest.AddSubscription

-   Microsoft.SharePoint.Library.SPRequest.AddWebPart

-   Microsoft.SharePoint.Library.SPRequest.AddWebPartPageToLibrary

-   Microsoft.SharePoint.Library.SPRequest.AddWebPartRightsCheck

-   Microsoft.SharePoint.Library.SPRequest.AddWorkflowAssociation

-   Microsoft.SharePoint.Library.SPRequest.AddWorkflowToListItem

-   Microsoft.SharePoint.Library.SPRequest.AddWorkItem

-   Microsoft.SharePoint.Library.SPRequest.ApplyAutoHyperLinking

-   Microsoft.SharePoint.Library.SPRequest.ApplyTheme

-   Microsoft.SharePoint.Library.SPRequest.ApplyViewToListWebPart

-   Microsoft.SharePoint.Library.SPRequest.ApplyWebTemplate

-   Microsoft.SharePoint.Library.SPRequest.BackupSite

-   Microsoft.SharePoint.Library.SPRequest.BreakRoleDefsInheritance

-   Microsoft.SharePoint.Library.SPRequest.BuildCabinetFile

-   Microsoft.SharePoint.Library.SPRequest.BypassUseRemoteApis

-   Microsoft.SharePoint.Library.SPRequest.CalculatePermissionsForCurrentThread

-   Microsoft.SharePoint.Library.SPRequest.CallCalcEngine

-   Microsoft.SharePoint.Library.SPRequest.CancelMeeting

-   Microsoft.SharePoint.Library.SPRequest.CancelWorkflow

-   Microsoft.SharePoint.Library.SPRequest.ChangeAccountPassword

-   Microsoft.SharePoint.Library.SPRequest.CheckInFile

-   Microsoft.SharePoint.Library.SPRequest.CheckOutFile

-   Microsoft.SharePoint.Library.SPRequest.CheckZoneProps

-   Microsoft.SharePoint.Library.SPRequest.ClearAllVars

-   Microsoft.SharePoint.Library.SPRequest.ClearListCache

-   Microsoft.SharePoint.Library.SPRequest.ClearTimerStoreServer

-   Microsoft.SharePoint.Library.SPRequest.CloseStream

-   Microsoft.SharePoint.Library.SPRequest.CompleteInProgressWorkItems

-   Microsoft.SharePoint.Library.SPRequest.ConfirmUsage

-   Microsoft.SharePoint.Library.SPRequest.CreateAuditEntry

-   Microsoft.SharePoint.Library.SPRequest.CreateAuditEntryForUrl

-   Microsoft.SharePoint.Library.SPRequest.CreateCustomList

-   Microsoft.SharePoint.Library.SPRequest.CreateFolderOnImport

-   Microsoft.SharePoint.Library.SPRequest.CreateList

-   Microsoft.SharePoint.Library.SPRequest.CreateListFromFormPost

-   Microsoft.SharePoint.Library.SPRequest.CreateListOnImport

-   Microsoft.SharePoint.Library.SPRequest.CreateListViewPart

-   Microsoft.SharePoint.Library.SPRequest.CreateOrUpdateFileAndItem

-   Microsoft.SharePoint.Library.SPRequest.CreateSite

-   Microsoft.SharePoint.Library.SPRequest.CreateView

-   Microsoft.SharePoint.Library.SPRequest.CreateViewOnImport

-   Microsoft.SharePoint.Library.SPRequest.CreateWeb

-   Microsoft.SharePoint.Library.SPRequest.CrossListQuery

-   Microsoft.SharePoint.Library.SPRequest.CustomizeCssFile

-   Microsoft.SharePoint.Library.SPRequest.DeleteAllFileVersions

-   Microsoft.SharePoint.Library.SPRequest.DeleteAllListItemVersions

-   Microsoft.SharePoint.Library.SPRequest.DeleteCommentsOfDocs

-   Microsoft.SharePoint.Library.SPRequest.DeleteFileVersion

-   Microsoft.SharePoint.Library.SPRequest.DeleteInProgressWorkItems

-   Microsoft.SharePoint.Library.SPRequest.DeleteItem

-   Microsoft.SharePoint.Library.SPRequest.DeleteList

-   Microsoft.SharePoint.Library.SPRequest.DeleteListItemVersion

-   Microsoft.SharePoint.Library.SPRequest.DeleteNavigationNode

-   Microsoft.SharePoint.Library.SPRequest.DeleteSite

-   Microsoft.SharePoint.Library.SPRequest.DeleteSubscription

-   Microsoft.SharePoint.Library.SPRequest.DeleteView

-   Microsoft.SharePoint.Library.SPRequest.DeleteWeb

-   Microsoft.SharePoint.Library.SPRequest.DeleteWebPart

-   Microsoft.SharePoint.Library.SPRequest.DeleteWebPartPagePersonalization

-   Microsoft.SharePoint.Library.SPRequest.DeleteWebPartPagePersonalizationForAUser

-   Microsoft.SharePoint.Library.SPRequest.DeleteWebPartPersonalization

-   Microsoft.SharePoint.Library.SPRequest.DeleteWorkflowAssociation

-   Microsoft.SharePoint.Library.SPRequest.DeleteWorkItem

-   Microsoft.SharePoint.Library.SPRequest.DetectOrphans

-   Microsoft.SharePoint.Library.SPRequest.DispatchTimerJob

-   Microsoft.SharePoint.Library.SPRequest.EnableModule

-   Microsoft.SharePoint.Library.SPRequest.EnableModuleFromXml

-   Microsoft.SharePoint.Library.SPRequest.EnsureSystemAccount

-   Microsoft.SharePoint.Library.SPRequest.EnsureUserExists

-   Microsoft.SharePoint.Library.SPRequest.ExecSiteSearch

-   Microsoft.SharePoint.Library.SPRequest.ExecuteBatchReorder

-   Microsoft.SharePoint.Library.SPRequest.ExpandListSchemaForExport

-   Microsoft.SharePoint.Library.SPRequest.ExportNavigationXml

-   Microsoft.SharePoint.Library.SPRequest.ExtractFilesFromCabinet

-   Microsoft.SharePoint.Library.SPRequest.FetchActiveFeaturesFromSessionCache

-   Microsoft.SharePoint.Library.SPRequest.FIrmProtectorFor

-   Microsoft.SharePoint.Library.SPRequest.ForceDeleteList

-   Microsoft.SharePoint.Library.SPRequest.FormatDateAsString

-   Microsoft.SharePoint.Library.SPRequest.GenerateChangeNumber

-   Microsoft.SharePoint.Library.SPRequest.GetAcceptHeaderExtensionsAsStringList

-   Microsoft.SharePoint.Library.SPRequest.GetAclForCurrentWeb

-   Microsoft.SharePoint.Library.SPRequest.GetAclForScope

-   Microsoft.SharePoint.Library.SPRequest.GetAdminRecycleBinItems

-   Microsoft.SharePoint.Library.SPRequest.GetAdminRecycleBinItemsForUI

-   Microsoft.SharePoint.Library.SPRequest.GetAdminRecycleBinStatistics

-   Microsoft.SharePoint.Library.SPRequest.GetAllAclsForCurrentSite

-   Microsoft.SharePoint.Library.SPRequest.GetAllAuthenticatedUsersString

-   Microsoft.SharePoint.Library.SPRequest.GetAllRolesForCurrentUser

-   Microsoft.SharePoint.Library.SPRequest.GetAllWebsOfSite

-   Microsoft.SharePoint.Library.SPRequest.GetAttachmentsInfo

-   Microsoft.SharePoint.Library.SPRequest.GetCachedNavigationData

-   Microsoft.SharePoint.Library.SPRequest.GetColumnDistinctAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetContainingList

-   Microsoft.SharePoint.Library.SPRequest.GetContentTypeSchema

-   Microsoft.SharePoint.Library.SPRequest.GetContentTypeWorkflowAssociationsAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetContextEventReceivers

-   Microsoft.SharePoint.Library.SPRequest.GetCurrentUserPermissionOnGroup

-   Microsoft.SharePoint.Library.SPRequest.GetCustomizedDocumentsInWeb

-   Microsoft.SharePoint.Library.SPRequest.GetDbNow

-   Microsoft.SharePoint.Library.SPRequest.GetDeadWebInfo

-   Microsoft.SharePoint.Library.SPRequest.GetDocEventReceivers

-   Microsoft.SharePoint.Library.SPRequest.GetDocsHavingComments

-   Microsoft.SharePoint.Library.SPRequest.GetEffectiveRightsForCurrentUser

-   Microsoft.SharePoint.Library.SPRequest.GetEventReceivers

-   Microsoft.SharePoint.Library.SPRequest.GetExecuteUrl

-   Microsoft.SharePoint.Library.SPRequest.GetExpandedFolderNSPath

-   Microsoft.SharePoint.Library.SPRequest.GetExternalSecurityProviderConfiguration

-   Microsoft.SharePoint.Library.SPRequest.GetExternalSecurityProviderId

-   Microsoft.SharePoint.Library.SPRequest.GetFieldsSchemaXml

-   Microsoft.SharePoint.Library.SPRequest.GetFieldTypeInfo

-   Microsoft.SharePoint.Library.SPRequest.GetFile

-   Microsoft.SharePoint.Library.SPRequest.GetFileAndFolderProperties

-   Microsoft.SharePoint.Library.SPRequest.GetFileAndFpMetaInfo

-   Microsoft.SharePoint.Library.SPRequest.GetFileAndMetaInfo

-   Microsoft.SharePoint.Library.SPRequest.GetFileAsByteArray

-   Microsoft.SharePoint.Library.SPRequest.GetFileAsStream

-   Microsoft.SharePoint.Library.SPRequest.GetFileUrlFromViewTitle

-   Microsoft.SharePoint.Library.SPRequest.GetFileVersionAsByteArray

-   Microsoft.SharePoint.Library.SPRequest.GetFileVersions

-   Microsoft.SharePoint.Library.SPRequest.GetFirstUniqueAncestorWebUrl

-   Microsoft.SharePoint.Library.SPRequest.GetFolderContentTypeId

-   Microsoft.SharePoint.Library.SPRequest.GetFolderContentTypeOrder

-   Microsoft.SharePoint.Library.SPRequest.GetGhostedFile

-   Microsoft.SharePoint.Library.SPRequest.GetGlobalContentTypeXml

-   Microsoft.SharePoint.Library.SPRequest.GetGroupsDataAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetHash

-   Microsoft.SharePoint.Library.SPRequest.GetHtmlTrCacheItemIfValid

-   Microsoft.SharePoint.Library.SPRequest.GetHtmlTrUrlFromExt

-   Microsoft.SharePoint.Library.SPRequest.GetIcon

-   Microsoft.SharePoint.Library.SPRequest.GetIgnoreCanary

-   Microsoft.SharePoint.Library.SPRequest.GetInfoFromCabinet

-   Microsoft.SharePoint.Library.SPRequest.GetLanguageAttributes

-   Microsoft.SharePoint.Library.SPRequest.GetLinkInfo

-   Microsoft.SharePoint.Library.SPRequest.GetListAndChildrenNSInfo

-   Microsoft.SharePoint.Library.SPRequest.GetListContentTypes

-   Microsoft.SharePoint.Library.SPRequest.GetListCurrentFolderInfo

-   Microsoft.SharePoint.Library.SPRequest.GetListItemDataAndRenderedViewWithCallback

-   Microsoft.SharePoint.Library.SPRequest.GetListItemDataWithCallback

-   Microsoft.SharePoint.Library.SPRequest.GetListItemPerm

-   Microsoft.SharePoint.Library.SPRequest.GetListItemWorkflowAsSafeArrayAndLock

-   Microsoft.SharePoint.Library.SPRequest.GetListItemWorkflowsAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetListScopeDataAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetListsWithCallback

-   Microsoft.SharePoint.Library.SPRequest.GetListTemplates

-   Microsoft.SharePoint.Library.SPRequest.GetListWorkflowAssociationsAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetMetadataForUrl

-   Microsoft.SharePoint.Library.SPRequest.GetMinFieldTypeInfo

-   Microsoft.SharePoint.Library.SPRequest.GetModules

-   Microsoft.SharePoint.Library.SPRequest.GetMtgInstanceID

-   Microsoft.SharePoint.Library.SPRequest.GetMtgResponseCookie

-   Microsoft.SharePoint.Library.SPRequest.GetNavigationNode

-   Microsoft.SharePoint.Library.SPRequest.GetNavigationNodeChild

-   Microsoft.SharePoint.Library.SPRequest.GetNavigationNodeProperties

-   Microsoft.SharePoint.Library.SPRequest.GetNTFullNameandEmailfromLogin

-   Microsoft.SharePoint.Library.SPRequest.GetNTFullNamefromLogin

-   Microsoft.SharePoint.Library.SPRequest.GetNTFullNamefromLoginEx

-   Microsoft.SharePoint.Library.SPRequest.GetPageListId

-   Microsoft.SharePoint.Library.SPRequest.GetParentWebUrl

-   Microsoft.SharePoint.Library.SPRequest.GetPermissionsDataAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetPortalServerSettings

-   Microsoft.SharePoint.Library.SPRequest.GetPortalSubscriptionUrl

-   Microsoft.SharePoint.Library.SPRequest.GetPropertiesXmlForUncustomizedViews

-   Microsoft.SharePoint.Library.SPRequest.GetRarelyUsedWebProps

-   Microsoft.SharePoint.Library.SPRequest.GetRecycleBinItems

-   Microsoft.SharePoint.Library.SPRequest.GetRecycleBinItemsForUI

-   Microsoft.SharePoint.Library.SPRequest.GetRoleDefsDataAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetRunnableWorkItemsAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetSchemaXML

-   Microsoft.SharePoint.Library.SPRequest.GetSecurityInfo

-   Microsoft.SharePoint.Library.SPRequest.GetServerFileRedirect

-   Microsoft.SharePoint.Library.SPRequest.GetSingleViewSchemaXml

-   Microsoft.SharePoint.Library.SPRequest.GetSiteFlags

-   Microsoft.SharePoint.Library.SPRequest.GetSiteItemSizes

-   Microsoft.SharePoint.Library.SPRequest.GetSiteQuota

-   Microsoft.SharePoint.Library.SPRequest.GetSiteUsageSummary

-   Microsoft.SharePoint.Library.SPRequest.GetSizeOfWebPartsOnPage

-   Microsoft.SharePoint.Library.SPRequest.GetStackTraceOnCreate

-   Microsoft.SharePoint.Library.SPRequest.GetSTSVersion

-   Microsoft.SharePoint.Library.SPRequest.GetSubscriptions

-   Microsoft.SharePoint.Library.SPRequest.GetSubwebs

-   Microsoft.SharePoint.Library.SPRequest.GetSubwebsFiltered

-   Microsoft.SharePoint.Library.SPRequest.GetTimerRunningJobs

-   Microsoft.SharePoint.Library.SPRequest.GetTimeZoneInfo

-   Microsoft.SharePoint.Library.SPRequest.GetTimeZoneMoveParameters

-   Microsoft.SharePoint.Library.SPRequest.GetTokenOfCurrentUser

-   Microsoft.SharePoint.Library.SPRequest.GetUncustomizedDefaultView

-   Microsoft.SharePoint.Library.SPRequest.GetUncustomizedViewByBaseViewId

-   Microsoft.SharePoint.Library.SPRequest.GetUserAccountDirectoryPath

-   Microsoft.SharePoint.Library.SPRequest.GetUserRegionalSettings

-   Microsoft.SharePoint.Library.SPRequest.GetUsersDataAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetUserStorageInfo

-   Microsoft.SharePoint.Library.SPRequest.GetUserToken

-   Microsoft.SharePoint.Library.SPRequest.GetVersionIndependentProp

-   Microsoft.SharePoint.Library.SPRequest.GetVersionIndependentProps

-   Microsoft.SharePoint.Library.SPRequest.GetViewsSchemaXml

-   Microsoft.SharePoint.Library.SPRequest.GetViewStylesXML

-   Microsoft.SharePoint.Library.SPRequest.GetWebAncestry

-   Microsoft.SharePoint.Library.SPRequest.GetWebAndChildrenNSInfo

-   Microsoft.SharePoint.Library.SPRequest.GetWebListPermMask

-   Microsoft.SharePoint.Library.SPRequest.GetWebMetainfo

-   Microsoft.SharePoint.Library.SPRequest.GetWebPartPagePersonalizations

-   Microsoft.SharePoint.Library.SPRequest.GetWebSubscriptionsUniqueUsers

-   Microsoft.SharePoint.Library.SPRequest.GetWebsWithTimestamps

-   Microsoft.SharePoint.Library.SPRequest.GetWebTemplates

-   Microsoft.SharePoint.Library.SPRequest.GetWebThemeComposite

-   Microsoft.SharePoint.Library.SPRequest.GetWebUrl

-   Microsoft.SharePoint.Library.SPRequest.GetWebUsageData

-   Microsoft.SharePoint.Library.SPRequest.GetWorkflowAssociationAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetWorkflowDataForItemAsSafeArrays

-   Microsoft.SharePoint.Library.SPRequest.GetWorkItemAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GetWorkItemsAsSafeArray

-   Microsoft.SharePoint.Library.SPRequest.GregorianISOToIntlISODate

-   Microsoft.SharePoint.Library.SPRequest.HandleCookieOrAcceptTypes

-   Microsoft.SharePoint.Library.SPRequest.ImportNavigationXml

-   Microsoft.SharePoint.Library.SPRequest.InitHeap

-   Microsoft.SharePoint.Library.SPRequest.InsertAlertEvent

-   Microsoft.SharePoint.Library.SPRequest.InvalidateWebIdCache

-   Microsoft.SharePoint.Library.SPRequest.InvokeTimerJob

-   Microsoft.SharePoint.Library.SPRequest.IrmClientPresent

-   Microsoft.SharePoint.Library.SPRequest.IrmClientReady

-   Microsoft.SharePoint.Library.SPRequest.IsAttachment

-   Microsoft.SharePoint.Library.SPRequest.IsCurrentUserMachineAdmin

-   Microsoft.SharePoint.Library.SPRequest.IsCurrentUserMemberOfGroup

-   Microsoft.SharePoint.Library.SPRequest.IsCurrentUserSiteAdmin

-   Microsoft.SharePoint.Library.SPRequest.IsUrlSafeForRedirect

-   Microsoft.SharePoint.Library.SPRequest.IsValidLoginName

-   Microsoft.SharePoint.Library.SPRequest.IsVotingAllowed

-   Microsoft.SharePoint.Library.SPRequest.ListRegionalOptions

-   Microsoft.SharePoint.Library.SPRequest.LocalizeText

-   Microsoft.SharePoint.Library.SPRequest.LocalizeXml

-   Microsoft.SharePoint.Library.SPRequest.LogBinary

-   Microsoft.SharePoint.Library.SPRequest.LogHelper

-   Microsoft.SharePoint.Library.SPRequest.ManageAdminRecycleBin

-   Microsoft.SharePoint.Library.SPRequest.ManageRecycleBin

-   Microsoft.SharePoint.Library.SPRequest.MapUrlToListAndView

-   Microsoft.SharePoint.Library.SPRequest.MigrateUserAccount

-   Microsoft.SharePoint.Library.SPRequest.MiniSproc

-   Microsoft.SharePoint.Library.SPRequest.ModifySubscription

-   Microsoft.SharePoint.Library.SPRequest.MoveNavigationNode

-   Microsoft.SharePoint.Library.SPRequest.MoveUrl

-   Microsoft.SharePoint.Library.SPRequest.NavStructContainsPage

-   Microsoft.SharePoint.Library.SPRequest.OpenSite

-   Microsoft.SharePoint.Library.SPRequest.OpenWeb

-   Microsoft.SharePoint.Library.SPRequest.OpenWebInternal

-   Microsoft.SharePoint.Library.SPRequest.ParseMetaInfo

-   Microsoft.SharePoint.Library.SPRequest.PatchUrl

-   Microsoft.SharePoint.Library.SPRequest.PreInitServer

-   Microsoft.SharePoint.Library.SPRequest.ProcessBatchData

-   Microsoft.SharePoint.Library.SPRequest.PublishFile

-   Microsoft.SharePoint.Library.SPRequest.PutFile

-   Microsoft.SharePoint.Library.SPRequest.QueryGroups

-   Microsoft.SharePoint.Library.SPRequest.QueryGroupsByIds

-   Microsoft.SharePoint.Library.SPRequest.QueryUserInfo

-   Microsoft.SharePoint.Library.SPRequest.ReadAuditFlags

-   Microsoft.SharePoint.Library.SPRequest.ReadPagesRightsCheck

-   Microsoft.SharePoint.Library.SPRequest.RecalculateSiteDiskUsed

-   Microsoft.SharePoint.Library.SPRequest.ReCalculateWebFGP

-   Microsoft.SharePoint.Library.SPRequest.RegisterContextEventReceiver

-   Microsoft.SharePoint.Library.SPRequest.RegisterDocEventReceiver

-   Microsoft.SharePoint.Library.SPRequest.RegisterEventReceiver

-   Microsoft.SharePoint.Library.SPRequest.ReleaseResources

-   Microsoft.SharePoint.Library.SPRequest.RelinkMeeting

-   Microsoft.SharePoint.Library.SPRequest.RemoveExternalSecurityProvider

-   Microsoft.SharePoint.Library.SPRequest.RemoveField

-   Microsoft.SharePoint.Library.SPRequest.RemoveGroup

-   Microsoft.SharePoint.Library.SPRequest.RemoveRoleDef

-   Microsoft.SharePoint.Library.SPRequest.RemoveWorkflowFromListItem

-   Microsoft.SharePoint.Library.SPRequest.RenameWeb

-   Microsoft.SharePoint.Library.SPRequest.RenderColumn

-   Microsoft.SharePoint.Library.SPRequest.RenderErrorPage

-   Microsoft.SharePoint.Library.SPRequest.RenderFormAsHtml

-   Microsoft.SharePoint.Library.SPRequest.RenderFormDigest

-   Microsoft.SharePoint.Library.SPRequest.RenderListProperty

-   Microsoft.SharePoint.Library.SPRequest.RenderListRelatedTasks

-   Microsoft.SharePoint.Library.SPRequest.RenderNavigationBar

-   Microsoft.SharePoint.Library.SPRequest.RenderSearchForm

-   Microsoft.SharePoint.Library.SPRequest.RenderViewAsHtml

-   Microsoft.SharePoint.Library.SPRequest.RepairOrphans

-   Microsoft.SharePoint.Library.SPRequest.ReserveItemIdsForWorkflow

-   Microsoft.SharePoint.Library.SPRequest.ResetSecurityScope

-   Microsoft.SharePoint.Library.SPRequest.RestoreAdminRecycleBinItem

-   Microsoft.SharePoint.Library.SPRequest.RestoreFileVersion

-   Microsoft.SharePoint.Library.SPRequest.RestoreRecycleBinItem

-   Microsoft.SharePoint.Library.SPRequest.RestoreSite

-   Microsoft.SharePoint.Library.SPRequest.RevertContentStreams

-   Microsoft.SharePoint.Library.SPRequest.RevertInProgressWorkItem

-   Microsoft.SharePoint.Library.SPRequest.RevertInProgressWorkItems

-   Microsoft.SharePoint.Library.SPRequest.SaveListAsTemplate

-   Microsoft.SharePoint.Library.SPRequest.SaveWebAsTemplate

-   Microsoft.SharePoint.Library.SPRequest.SealField

-   Microsoft.SharePoint.Library.SPRequest.SeedEtag

-   Microsoft.SharePoint.Library.SPRequest.SelectSitesAndUserInfoForMigration

-   Microsoft.SharePoint.Library.SPRequest.SendMail

-   Microsoft.SharePoint.Library.SPRequest.SetAnonymousAccessMask

-   Microsoft.SharePoint.Library.SPRequest.SetAttendeeResponse

-   Microsoft.SharePoint.Library.SPRequest.SetAuditFlags

-   Microsoft.SharePoint.Library.SPRequest.SetDisableAsyncEvents

-   Microsoft.SharePoint.Library.SPRequest.SetExactWebUrlFlag

-   Microsoft.SharePoint.Library.SPRequest.SetGhostedFile

-   Microsoft.SharePoint.Library.SPRequest.SetHtmlTrCacheItem

-   Microsoft.SharePoint.Library.SPRequest.SetHttpParameters

-   Microsoft.SharePoint.Library.SPRequest.SetIgnoreCanary

-   Microsoft.SharePoint.Library.SPRequest.SetIgnoreCheckoutLock

-   Microsoft.SharePoint.Library.SPRequest.SetIPAddr

-   Microsoft.SharePoint.Library.SPRequest.SetListContentTypes

-   Microsoft.SharePoint.Library.SPRequest.SetListProps

-   Microsoft.SharePoint.Library.SPRequest.SetMondoProcHint

-   Microsoft.SharePoint.Library.SPRequest.SetMtgInstanceID

-   Microsoft.SharePoint.Library.SPRequest.SetPortalServerSettings

-   Microsoft.SharePoint.Library.SPRequest.SetRequestAccessInfo

-   Microsoft.SharePoint.Library.SPRequest.SetSiteFlags

-   Microsoft.SharePoint.Library.SPRequest.SetSiteProps

-   Microsoft.SharePoint.Library.SPRequest.SetSiteQuota

-   Microsoft.SharePoint.Library.SPRequest.SetUserAccountDirectoryPath

-   Microsoft.SharePoint.Library.SPRequest.SetVar

-   Microsoft.SharePoint.Library.SPRequest.SetVersionIndependentProps

-   Microsoft.SharePoint.Library.SPRequest.SetVersionIndependentPropsAdditive

-   Microsoft.SharePoint.Library.SPRequest.SetWebAssociatedGroups

-   Microsoft.SharePoint.Library.SPRequest.SetWebMetainfo

-   Microsoft.SharePoint.Library.SPRequest.SetWebProps

-   Microsoft.SharePoint.Library.SPRequest.SscCreateSite

-   Microsoft.SharePoint.Library.SPRequest.TakePublishFileOffline

-   Microsoft.SharePoint.Library.SPRequest.ThrowError

-   Microsoft.SharePoint.Library.SPRequest.TZConvertDate

-   Microsoft.SharePoint.Library.SPRequest.UncheckOutFile

-   Microsoft.SharePoint.Library.SPRequest.UpdateField

-   Microsoft.SharePoint.Library.SPRequest.UpdateFileOrFolderProperties

-   Microsoft.SharePoint.Library.SPRequest.UpdateGroup

-   Microsoft.SharePoint.Library.SPRequest.UpdateListItemWorkflow

-   Microsoft.SharePoint.Library.SPRequest.UpdateListItemWorkflowLock

-   Microsoft.SharePoint.Library.SPRequest.UpdateListSecurityTrim

-   Microsoft.SharePoint.Library.SPRequest.UpdateMeeting

-   Microsoft.SharePoint.Library.SPRequest.UpdateMeetingFromICal

-   Microsoft.SharePoint.Library.SPRequest.UpdateMembers

-   Microsoft.SharePoint.Library.SPRequest.UpdateNavigationNode

-   Microsoft.SharePoint.Library.SPRequest.UpdateRoleAssignment

-   Microsoft.SharePoint.Library.SPRequest.UpdateRoleDef

-   Microsoft.SharePoint.Library.SPRequest.UpdateSiteHashKey

-   Microsoft.SharePoint.Library.SPRequest.UpdateTimerRunningJobProgress

-   Microsoft.SharePoint.Library.SPRequest.UpdateUser

-   Microsoft.SharePoint.Library.SPRequest.UpdateView

-   Microsoft.SharePoint.Library.SPRequest.UpdateWebPar

-   Microsoft.SharePoint.Library.SPRequest.UpdateWebPartCache

-   Microsoft.SharePoint.Library.SPRequest.UpdateWebPartIsIncluded

-   Microsoft.SharePoint.Library.SPRequest.UpdateWebPartTypeId

-   Microsoft.SharePoint.Library.SPRequest.UpdateWorkflowAssociation

-   Microsoft.SharePoint.Library.SPRequest.UpdateWorkItem

-   Microsoft.SharePoint.Library.SPRequest.UseDefaultAssociatedGroups

-   Microsoft.SharePoint.Library.SPRequest.ValidateFormDigest

-   Microsoft.SharePoint.Library.SPRequest.ValidateSubscriptionFilter

-   Microsoft.SharePoint.Library.SPRequest.VssHelperIsEnabled

-   Microsoft.SharePoint.Library.SPRequest.VssHelperOnIdentify

-   Microsoft.SharePoint.Library.SPRequest.VssHelperOnPostRestore

-   Microsoft.SharePoint.Library.SPRequest.VssHelperOnPreBackup

-   Microsoft.SharePoint.Library.SPRequest.WebTemplateName

### For SharePoint, Help Function for Site Name Retrieving
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.SharePoint.WebPartPages.SPWebPartManager.LoadWebParts

### For SharePoint, KPI Helper
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.SharePoint.Portal.WebControls.KpiRenderer.getKpiData

### For MVC
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   System.Web.Mvc.ReflectedActionDescriptor.Execute

-   System.Web.Mvc.Async.ReflectedAsyncActionDescriptor.BeginExecute

### For Windows Azure Storage Queue
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.AddMessage

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.Clear

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.Create

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.CreateIfNotExist

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.Delete

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.UpdateMessage

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.DeleteMessage

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.Exists

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.GetMessagesInternal

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.PeekMessage

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.PeekMessages

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.FetchAttributes

-   Microsoft.WindowsAzure.StorageClient.CloudQueue.SetMetadata

### For Windows Azure Storage Table
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.WindowsAzure.StorageClient.CloudTableClient.CreateTablesFromModel

-   Microsoft.WindowsAzure.StorageClient.CloudTableClient.CreateTable

-   Microsoft.WindowsAzure.StorageClient.CloudTableClient.CreateTableIfNotExist

-   Microsoft.WindowsAzure.StorageClient.CloudTableClient.DeleteTable

-   Microsoft.WindowsAzure.StorageClient.CloudTableClient.DeleteTableIfExist

-   Microsoft.WindowsAzure.StorageClient.CloudTableClient.DoesTableExist

-   Microsoft.WindowsAzure.StorageClient.CloudTableClient.ListTablesSegmented

### For Windows Azure Storage Blob Container
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.Create

-   Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.CreateIfNotExist

-   Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.Delete

-   Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.SetPermissions

-   Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.GetPermissions

-   Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.FetchAttributes

-   Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.SetMetadata

-   Microsoft.WindowsAzure.StorageClient.CloudBlobContainer.ListBlobsSegmented

-   Microsoft.WindowsAzure.StorageClient.CloudBlobDirectory.ListBlobsSegmented

### For Windows Azure Storage Blobs
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.CopyFromBlob

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.CreateSnapshot

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.Delete

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.DeleteIfExists

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.UploadText

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.DownloadText

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.UploadFile

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.DownloadToFile

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.UploadFromStream

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.DownloadToStream

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.SetProperties

-   Microsoft.WindowsAzure.StorageClient.CloudBlob.GetSharedAccessSignature

-   Microsoft.WindowsAzure.StorageClient.CloudBlockBlob.PutBlock

-   Microsoft.WindowsAzure.StorageClient.CloudBlockBlob.PutBlockList

-   Microsoft.WindowsAzure.StorageClient.CloudBlockBlob.DownloadBlockList

-   Microsoft.WindowsAzure.StorageClient.CloudPageBlob.WritePages

-   Microsoft.WindowsAzure.StorageClient.CloudPageBlob.Create

-   Microsoft.WindowsAzure.StorageClient.CloudPageBlob.ClearPages

-   Microsoft.WindowsAzure.StorageClient.CloudPageBlob.GetPageRanges

### For Windows Azure Storage Blob Stream
For [!INCLUDE[sc2012sp1_short](../Token/sc2012sp1_short_md.md)] these resources are included:

-   Microsoft.WindowsAzure.StorageClient.BlobReadStream.Read

-   Microsoft.WindowsAzure.StorageClient.BlobWriteStream.Write

-   Microsoft.WindowsAzure.StorageClient.BlobWriteStream.Commit

-   Microsoft.WindowsAzure.StorageClient.CloudBlobClient.ListBlobsWithPrefixSegmented

-   Microsoft.WindowsAzure.StorageClient.CloudBlobClient.ListContainersSegmented

-   Microsoft.WindowsAzure.StorageClient.Tasks.Task\`1.ExecuteAndWait

-   System.Data.Services.Client.DataServiceContext.SaveChanges

-   System.Data.Services.Client.DataServiceContext.Execute

-   System.Data.Services.Client.DataServiceContext.ExecuteBatch

-   Microsoft.WindowsAzure.StorageClient.TableServiceContext.SaveChangesWithRetries

### For COM\+ Services \(Client Side\)

-   System.EnterpriseServices.RemoteServicedComponentProxy.Invoke

### For COM\+ Services \(Server Side\)

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.EnterpriseServices.ServicedComponentProxy.LocalInvoke

### For SQL server

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.Data.SqlClient.SqlConnection.Open

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.Data.SqlClient.SqlConnection.Close

-   System.Data.SqlClient.SqlCommand.ExecuteReader

-   System.Data.SqlClient.SqlCommand.ExecuteNonQuery

-   System.Data.SqlClient.SqlCommand.ExecuteScalar

-   System.Data.SqlClient.SqlDataAdapter.Fill

### For OLEDB

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.Data.OleDb.OleDbConnection.Open

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.Data.OleDb.OleDbConnection.Close

-   System.Data.OleDb.OleDbCommand.ExecuteReader

-   System.Data.OleDb.OleDbCommand.System.Data.OleDb.OleDbCommand.System.Data.IDbCommand.ExecuteReader

-   System.Data.OleDb.OleDbCommand.ExecuteNonQuery

-   System.Data.OleDb.OleDbCommand.ExecuteScalar

-   System.Data.OleDb.OleDbDataAdapter.Fill

### For ODBC

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.Data.Odbc.OdbcConnection.Open

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.Data.Odbc.OdbcConnection.Close

-   System.Data.Odbc.OdbcCommand.ExecuteReader

-   System.Data.Odbc.OdbcCommand.ExecuteNonQuery

-   System.Data.Odbc.OdbcCommand.ExecuteScalar

-   System.Data.Odbc.OdbcDataAdapter.Fill

### For .NET Framework Data Provider for Oracle

-   System.Data.OracleClient.OracleCommand.ExecuteNonQuery

-   System.Data.OracleClient.OracleCommand.ExecuteReader

-   System.Data.OracleClient.OracleCommand.ExecuteScalar

-   System.Data.SqlClient.SqlConnection.Open

-   System.Data.Odbc.OdbcConnection.Open

-   System.Data.OleDb.OleDbConnection.Open

### For Oracle

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.Data.OracleClient.OracleConnection.Open

-   [!INCLUDE[sc2012sp1note](../Token/sc2012sp1note_md.md)] System.Data.OracleClient.OracleConnection.Close

-   Oracle.DataAccess.Client.OracleCommand.ExecuteReader

-   Oracle.DataAccess.Client.OracleCommand.ExecuteNonQuery

-   Oracle.DataAccess.Client.OracleCommand.ExecuteScalar

-   System.Data.Common.DbAdapter.Fill

### For System.Web.Mail

-   System.Web.Mail.SmtpMail@CdoSysHelper.Send

### For Instrumentation

-   System.Web.UI.Page.ProcessRequest

-   System.Web.UI.Page.ProcessRequest

-   System.Web.Services.Protocols.SoapHttpClientProtocol.Invoke

-   System.Web.Services.Protocols.SoapHttpClientProtocol.BeginInvoke

-   System.Web.Services.Protocols.LogicalMethodInfo.Invoke

### For Instrumentation \(Framework 1.0\)

-   System.Web.Services.Protocols.SoapHttpClientProtocol.ReadResponse

### For Instrumentation \(Framework 1.1\)

-   System.Web.Services.Protocols.SoapHttpClientProtocol.ReadResponse

-   System.Web.HttpServerUtility.ExecuteInternal

-   System.Web.UI.LosFormatter.Deserialize

### For Instrumentation \(Framework 2.0\)

-   System.Web.HttpServerUtility.Execute

### For File System Operations

-   System.IO.Directory.GetFileSystemEntries

-   System.IO.Directory.GetFiles

-   System.IO.File.Open

-   System.IO.FileStream..ctor

-   System.IO.FileStream.ReadCore

-   System.IO.FileStream.WriteCore

-   System.IO.FileStream.BeginReadCore

-   System.IO.BeginWriteCore

-   System.IO.Directory.InternalCreateDirectory

-   System.IO.Directory.Delete

-   System.IO.Directory.InternalGetFileDirectoryNames

-   System.IO.DirectoryInfo.MoveTo

-   System.IO.Directory.Move

-   System.IO.File.Delete

-   System.IO.FileInfo.Delete

-   System.IO.File.Move

-   System.IO.FileInfo.MoveTo

### For Remoting Client\-Side

-   System.Runtime.Remoting.Proxies.RemotingProxy.InternalInvoke

-   System.Runtime.Remoting.Proxies.RealProxy.HandleReturnMessage

-   System.Runtime.Remoting.Proxies.RealProxy.PrivateInvoke

### For Remoting Server\-Side

-   System.Runtime.Remoting.Messaging.ServerObjectTerminatorSink.AsyncProcessMessage

-   System.Runtime.Remoting.Messaging.ServerObjectTerminatorSink.SyncProcessMessage

### For MS Message Queuing

-   System.Messaging.MessageQueue.Send

-   ystem.Messaging.MessageQueue.Receive

### For Sockets

-   System.NET.Sockets.Socket.Connect

-   System.NET.Sockets.Socket.Receive

-   System.NET.Sockets.Socket.Send

-   System.NET.Sockets.Socket.Listen

### For System.Web

-   System.NET.FileWebRequest.GetResponse

-   System.NET.FileWebRequest.GetRequestStream

-   System.NET.HttpWebRequest.GetResponse

-   System.NET.HttpWebRequest.GetRequestStream

-   System.NET.FtpWebRequest.GetResponse

-   System.NET.FtpWebRequest.GetRequestStream

-   System.NET.WebClient.OpenRead

### For Reflection

-   System.Reflection.RuntimeConstructorInfo.Invoke

-   System.RuntimeType.InvokeMember

### For Registry

-   Microsoft.Win32.RegistryKey.OpenSubKey

### For Parsing

-   System.Byte.Parse

-   System.SByte.Parse

-   System.Int16.Parse

-   System.Int32.Parse

-   System.Int64.Parse

-   System.UInt16.Parse

-   System.UInt32.Parse

-   System.UInt64.Parse

-   System.Single.Parse

-   System.Double.Parse

-   System.Boolean.Parse

-   System.Char.Parse

-   System.Decimal.Parse

-   System.DateTime.Parse

-   System.DateTime.ParseExact

-   System.TimeSpan.Parse

-   System.SqlBoolean.Parse

-   System.SqlByte.Parse

-   System.SqlDateTime.Parse

-   System.SqlInt16.Parse

-   System.SqlInt32.Parse

-   System.SqlInt64.Parse

-   System.SqlSingle.Parse

-   System.SqlDouble.Parse

-   System.SqlMoney.Parse

### For IBM DB2

-   IBM.Data.DB2.DB2Command.ExecuteReader

-   IBM.Data.DB2.DB2Command.ExecuteReader

-   IBM.Data.DB2.DB2Command.ExecuteNonQuery

-   IBM.Data.DB2.DB2Command.ExecuteScalar

### For Sybase

-   Sybase.Data.AseClient.AseCommand.ExecuteScalarSybase.Data.AseClient.AseCommand.System.Data.IDbCommand.ExecuteReader

-   Sybase.Data.AseClient.AseCommand.ExecuteNonQuery

## Resource Calls Monitored by Default
Application Performance Monitoring includes well\-known Microsoft .NET Framework resource calls that are monitored for slow performance.

### For Custom Functions FW 1.0

-   System.Data.Common.DbDataAdapter.FillFromReader

### For Custom Functions FW 2.0

-   System.Data.Common.DataAdapter.FillFromReader

### For HTTP Handlers Calls .NET 1.1

-   System.Web.Handlers.BatchHandler.System.Web.IHttpHandler.ProcessRequest

-   System.Web.Handlers.TraceHandler.System.Web.IHttpHandler.ProcessRequest

-   System.Web.HttpDebugHandler.ProcessRequest

-   System.Web.HttpForbiddenHandler.ProcessRequest

-   System.Web.HttpMethodNotAllowedHandler.ProcessRequest

-   System.Web.HttpNotFoundHandler.ProcessRequest

-   System.Web.HttpNotImplementedHandler.ProcessRequest

-   System.Web.DefaultHttpHandler.ProcessRequest

-   System.Web.SessionState.StateApplication.ProcessRequest

-   System.Web.StaticFileHandler.ProcessRequest

-   System.Web.UI.TrivialPage.ProcessRequest

### For HTTP Handlers Calls .NET 2.0

-   System.Web.Handlers.AssemblyResourceLoader.System.Web.IHttpHandler.ProcessRequest

### For HTTP Modules Calls .NET 1.1

-   System.Web.Caching.OutputCacheModule.OnEnter

-   System.Web.Caching.OutputCacheModule.OnLeave

-   System.Web.Security.DefaultAuthenticationModule.OnEnter

-   System.Web.Security.FileAuthorizationModule.OnEnter

-   System.Web.Security.FormsAuthenticationModule.OnAuthenticate

-   System.Web.Security.PassportAuthenticationModule.OnAuthenticate

-   System.Web.Security.UrlAuthorizationModule.OnEnter

-   System.Web.Security.WindowsAuthenticationModule.OnAuthenticate

-   System.Web.SessionState.SessionStateModule.BeginAcquireState

### For HTTP Modules Calls .NET 2.0

-   System.Web.Profile.ProfileModule.OnEnter

-   System.Web.Profile.ProfileModule.OnLeave

-   System.Web.Security.AnonymousIdentificationModule.OnEnter

-   System.Web.Security.RoleManagerModule.OnEnter

-   System.Web.UrlMappingsModule.OnEnter

### For COM\+ Server\-Side

-   System.EnterpriseServices.ServicedComponentProxy.LocalInvoke

### For COM\+ Client\-Side

-   System.EnterpriseServices.RemoteServicedComponentProxy.Invoke

### For Remoting Client\-Side

-   System.Runtime.Remoting.Proxies.RemotingProxy.InternalInvoke

### For Abstract Data Access Function

-   System.Data.Common.DbDataAdapter.Update

### For SQL Server Resources

-   System.Data.SqlClient.SqlCommand.ExecuteReader

-   System.Data.SqlClient.SqlCommand.ExecuteReader

-   System.Data.SqlClient.SqlCommand.ExecuteXmlReader

-   System.Data.SqlClient.SqlCommand.ExecuteNonQuery

-   System.Data.SqlClient.SqlCommand.ExecuteScalar

-   System.Data.SqlClient.SqlConnection.Open

-   System.Data.SqlClient.SqlConnection.Close

### For SQL Server Resources FW 2.0 Specific \(Async Methods\)

-   System.Data.SqlClient.SqlCommand.BeginExecuteReader

-   System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery

### For OLEDB Resources

-   System.Data.OleDb.OleDbCommand.ExecuteReader

-   System.Data.OleDb.OleDbCommand.ExecuteNonQuery

-   System.Data.OleDb.OleDbCommand.ExecuteScalar

-   System.Data.OleDb.OleDbConnection.Open

-   System.Data.OleDb.OleDbConnection.Close

### For ODBC Resources

-   System.Data.Odbc.OdbcCommand.ExecuteReader

-   System.Data.Odbc.OdbcCommand.ExecuteNonQuery

-   System.Data.Odbc.OdbcCommand.ExecuteScalar

-   System.Data.Odbc.OdbcConnection.Open

-   System.Data.Odbc.OdbcConnection.Close

### For Oracle Resources

-   System.Data.OracleClient.OracleCommand.ExecuteReader

-   System.Data.OracleClient.OracleCommand.ExecuteNonQuery

-   System.Data.OracleClient.OracleCommand.ExecuteScalar

-   System.Data.OracleClient.OracleConnection.Open

-   System.Data.OracleClient.OracleConnection.Close

-   Oracle.DataAccess.Client.OracleCommand.ExecuteReader

-   Oracle.DataAccess.Client.OracleCommand.ExecuteNonQuery

-   Oracle.DataAccess.Client.OracleCommand.ExecuteScalar

-   Oracle.DataAccess.Client.OracleConnection.Open

-   Oracle.DataAccess.Client.OracleConnection.Close

### For IBM DB2 iSeries

-   IBM.Data.DB2.iSeries.iDB2Command.ExecuteReader

-   IBM.Data.DB2.iSeries.iDB2Command.ExecuteReader

-   IBM.Data.DB2.iSeries.iDB2Command.ExecuteNonQuery

-   IBM.Data.DB2.iSeries.iDB2Command.ExecuteScalar

-   IBM.Data.DB2.iSeries.iDB2Connection.Open

-   IBM.Data.DB2.iSeries.iDB2Connection.Close

### For Web Services Resources

-   System.Web.Services.Protocols.SoapHttpClientProtocol.Invoke

-   System.Web.Services.Protocols.SoapHttpClientProtocol.BeginInvoke

### For System.Messaging

-   System.Messaging.MessageQueue.Send

-   System.Messaging.MessageQueue.Receive

### For System.IO

-   System.IO.File.Open

-   System.IO.Directory.GetFileSystemEntries

-   System.IO.Directory.GetFiles

### For System.Web.Mail

-   System.Web.Mail.SmtpMail.Send

### For IBM DB2

-   IBM.Data.DB2.DB2Command.ExecuteReader

-   IBM.Data.DB2.DB2Command.ExecuteReader

-   IBM.Data.DB2.DB2Command.ExecuteNonQuery

-   IBM.Data.DB2.DB2Command.ExecuteScalar

-   IBM.Data.DB2.DB2Connection.Open

-   IBM.Data.DB2.DB2Connection.Close

### For WCF Client\-Side

-   System.ServiceModel.Channels.ServiceChannelProxy.InvokeService

-   System.ServiceModel.Channels.ServiceChannelProxy.InvokeBeginService

-   System.ServiceModel.Channels.ServiceChannelProxy.InvokeEndService

### For Mail

-   System.Web.Mail.SmtpMail@CdoSysHelper.Send

### For RK Sybase Resources

-   Sybase.Data.AseClient.AseCommand.ExecuteScalar

-   Sybase.Data.AseClient.AseCommand.ExecuteNonQuery

-   Sybase.Data.AseClient.AseCommand.System.Data.IDbCommand.ExecuteReader

### For LINQ

-   System.Data.Linq.SqlClient.SqlProvider.System.Data.Linq.Provider.IProvider.Execute

-   System.Data.Linq.SqlClient.SqlProvider.BuildQuery

-   System.Data.Linq.SqlClient.SqlProvider.BuildQuery

### For WWF

-   System.Workflow.ComponentModel.ActivityExecutorDelegateInfo\`1@ActivityExecutorDelegateOperation.Run

-   System.Workflow.ComponentModel.ActivityExecutor\`1.Execute

-   System.Workflow.ComponentModel.Activity.SetStatus

-   System.Workflow.ComponentModel.ActivityExecutionContext.ExecuteActivity

-   System.Workflow.ComponentModel.Activity.Invoke

### For ADOMD

-   Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet

-   Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader

-   Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteNonQuery

-   Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute

### For AJAX.NET

-   System.Web.Script.Services.RestHandler.InvokeMethod

### For WebClient

-   System.Net.WebClient.UploadBits

-   System.Net.WebClient.DownloadBits

-   System.Web.HttpPostedFile.SaveAs

### For WebClient  FW 1.1

-   System.Net.WebClient.UploadValues System.Net.WebClient.UploadBits

-   System.Net.WebClient.UploadFile

-   System.Net.WebClient.DownloadFile

