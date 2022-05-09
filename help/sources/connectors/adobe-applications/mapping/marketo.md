---
keywords: Experience Platform;hem;populära ämnen;Marketo Engage;markering för att engagera;Marketo;mappning
solution: Experience Platform
title: Mappningsfält för Marketo Engage-källan
topic-legacy: overview
description: Tabellerna nedan innehåller mappningarna mellan fälten i Marketo datamängder och deras motsvarande XDM-fält.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: 52162fa1bbb3ab4c8ccb81b95e90c515f931c6fa
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# [!DNL Marketo Engage] fältkopplingar

Tabellerna nedan innehåller mappningarna mellan fälten i de nio [!DNL Marketo] datauppsättningar och deras motsvarande XDM-fält (Experience Data Model).

>[!TIP]
>
>Alla [!DNL Marketo] datauppsättningar förutom `Activities` nu support `isDeleted`. Befintliga dataflöden inkluderar automatiskt `isDeleted`, men kommer bara att importera flaggan för nya importerade data. Om du vill använda flaggan för alla dina historiska data måste du stoppa dina befintliga dataflöden och återskapa dem med den nya mappningen. Observera att om du tar bort `isDeleted`så har du inte längre tillgång till funktionerna. Det är viktigt att mappningen behålls efter att den har fyllts i automatiskt.

## Aktiviteter {#activities}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `"Marketo"` | `personKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `personID` | `personKey.sourceID` |
| `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `eventType` | `eventType` |
| `producedBy` | `producedBy` |
| `timestamp` | `timestamp` |
| `web.webPageDetails.URL` | `web.webPageDetails.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |
| `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |
| `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |
| `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |
| `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |
| `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |

{style=&quot;table-layout:auto&quot;}

## Program {#programs}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `campaignKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `id` | `campaignKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey.sourceKey` | Sekundär identitet. Värdena för `{CRM_ORG_ID}` och `{CRM_TYPE}` ersätts automatiskt. |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |
| `integrationPartner` | `integrationPartnerName` |
| `webinarSessionName` | `webinarSessionName` |
| `webinarSessionDescription` | `webinarSessionDescription` |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## Programmedlemskap {#program-memberships}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `id` | `campaignMemberKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Relation |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relation |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey.sourceKey` | Sekundär identitet. Värdena för `{CRM_ORG_ID}` och `{CRM_TYPE}` ersätts automatiskt. |
| `sfdc.lastStatus` | `lastStatus` |
| `sfdc.hasResponded` | `hasResponded` |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## Företag {#companies}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| <ul><li>`iif(mktoCdpExternalId != null && mktoCdpExternalId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", mktoCdpExternalId, "sourceKey", concat(mktoCdpExternalId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(msftCdpExternalId != null && msftCdpExternalId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", msftCdpExternalId,"sourceKey", concat(msftCdpExternalId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `extSourceSystemAudit.externalKey.sourceKey` | Sekundär identitet. Värdena för `{CRM_ORG_ID}` och `{CRM_TYPE}` ersätts automatiskt. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## Statiska listor {#static-lists}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | `"${MUNCHKIN_ID}"` ersätts som en del av Utforska API. |
| `id` | `marketingListKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## Statiska listmedlemskap {#static-list-memberships}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | Relation |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relation |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## Namngivna konton {#named-accounts}

>[!IMPORTANT]
>
>Datauppsättningen med namngivna konton är bara nödvändig med funktionen Marketo kontobaserad marknadsföring (ABM). Om du inte använder ABM behöver du inte konfigurera mappningar för namngivna konton.

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey.sourceKey` | Sekundär identitet. Värdena för `{CRM_ORG_ID}` och `{CRM_TYPE}` ersätts automatiskt. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |
| `sourceType` | `accountSourceType` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## Möjligheter {#opportunities}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `id` | `opportunityKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey.sourceKey` | Sekundär identitet. Värdena för `{CRM_ORG_ID}` och `{CRM_TYPE}` ersätts automatiskt. |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | Relation |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `iif(mktoCdpSourceCampaignId != null && mktoCdpSourceCampaignId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", mktoCdpSourceCampaignId, "sourceKey", concat(mktoCdpSourceCampaignId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Den här källdatauppsättningen är bara tillgänglig för användare med [!DNL Salesforce] integrering. |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## Kontaktroller för affärsmöjlighet {#opportunity-contact-roles}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `opportunityPersonKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `id` | `opportunityPersonKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts som en del av Utforska API. |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey.sourceKey` | Sekundär identitet. Värdena för `{CRM_ORG_ID}` och `{CRM_TYPE}` ersätts automatiskt. |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | Relation |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relation |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

## Personer {#persons}

| Källdatauppsättning | XDM-målfält | Anteckningar |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `b2b.personKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `id` | `b2b.personKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | Primär identitet. Värdet för `"${MUNCHKIN_ID}"` ersätts automatiskt. |
| `iif(unsubscribed == 'true', 'n', 'y' ))` | `consents.marketing.email.val` | Om du avbryter prenumerationen `true` (till exempel value = `1`), sedan ange `consents.marketing.email.val` as (`n`). Om du avbryter prenumerationen `false` (till exempel value = `0`), sedan ange `consents.marketing.email.val` as `null`. |
| `unsubscribedReason` | `consents.marketing.email.reason` |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| <ul><li>`iif(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null), "sourceKey", concat(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null), "sourceKey", concat(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `extSourceSystemAudit.externalKey.sourceKey` | The `extSourceSystemAudit.externalKey.sourceKey` är den sekundära identiteten. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `organizations` / `b2b.companyName` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` |
| <ul><li>`iif(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null), "sourceKey", concat(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null), "sourceKey", concat(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `personComponents.sourceExternalKey` |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |
| `iif(ecids != null, to_object('ECID',arrays_to_objects('id',explode(ecids))), null)` | `identityMap` | Detta är ett beräkningsfält. |
| `marketoIsDeleted` | `isDeleted` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>The `to_object('ECID',arrays_to_objects('id',explode(ecids)))` källfält är ett beräkningsfält som måste läggas till med [!UICONTROL Add calculated field] i användargränssnittet för plattformen. Se självstudiekursen om [lägga till beräknade fält](../../../../data-prep/ui/mapping.md#calculated-fields) för mer information.

## Nästa steg

Genom att läsa det här dokumentet har du fått insikt i mappningsförhållandet mellan [!DNL Marketo] datauppsättningar och deras motsvarande XDM-fält. Se självstudiekursen om [skapa [!DNL Marketo] källanslutning](../../../tutorials/ui/create/adobe-applications/marketo.md) för att slutföra [!DNL Marketo] dataflöde.
