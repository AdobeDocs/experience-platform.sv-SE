---
title: Salesforce-mappningsfält
description: Tabellerna nedan innehåller mappningarna mellan Salesforce-källfält och deras motsvarande XDM-fält.
exl-id: 33ee76f2-0495-4acd-a862-c942c0fa3177
source-git-commit: ec42cf27c082611acb1a08500b7bbd23fc34d730
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# [!DNL Salesforce] fältkopplingar

Tabellerna nedan innehåller mappningarna mellan [!DNL Salesforce] källfält och deras motsvarande XDM-fält (Experience Data Model).

## Kontakt {#contact}

Läs [Översikt över enskilda XDM-profiler](../../../../xdm/classes/individual-profile.md) för mer information om klassen XDM. Mer information om XDM-fältgrupper finns i [Schemafältgrupp för XDM Business Person Details](../../../../xdm/field-groups/profile/business-person-details.md) stödlinje och [Schemafältgrupp för XDM Business Person Components](../../../../xdm/field-groups/profile/business-person-components.md) guide.

| Källfält | Sökväg till mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `AccountId` | `b2b.accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.accountKey` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", AccountId, "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceAccountKey` |
| `"Salesforce"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `Birthdate` | `person.birthDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Department` | `extendedWorkDetails.departments` |
| `Email` | `workEmail.address` | Sekundär identitet. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `HomePhone` | `homePhone.number` |
| `isDeleted` | `isDeleted` |
| `Id` | `b2b.personKey.sourceID` |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |
| `Id` | `personComponents.sourcePersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `MailingCity` | `workAddress.city` |
| `MailingCountry` | `workAddress.country` |
| `MailingLatitude` | `workAddress._schema.latitude` |
| `MailingLongitude` | `workAddress._schema.longitude` |
| `MailingPostalCode` | `workAddress.postalCode` |
| `MailingState` | `workAddress.state` |
| `MailingStreet` | `workAddress.street1` |
| `MobilePhone` | `mobilePhone.number` |
| `Name` | `person.name.fullName` |
| `OtherCity` | `otherAddress.city` |
| `OtherCountry` | `otherAddress.country` |
| `OtherLatitude` | `otherAddress._schema.latitude` |
| `OtherLongitude` | `otherAddress._schema.longitude` |
| `OtherPhone` | `otherPhone.number` |
| `OtherPostalCode` | `otherAddress.postalCode` |
| `OtherState` | `otherAddress.state` |
| `OtherStreet` | `otherAddress.street1` |
| `Phone` | `workPhone.number` |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |
| `Salutation` | `person.name.courtesyTitle` |
| `Title` | `extendedWorkDetails.jobTitle` |
| `"Contact"` | `b2b.personType` |

{style="table-layout:auto"}

## Lead {#lead}

Läs [Översikt över enskilda XDM-profiler](../../../../xdm/classes/individual-profile.md) för mer information om klassen XDM. Mer information om XDM-fältgrupper finns i [Schemafältgrupp för XDM Business Person Details](../../../../xdm/field-groups/profile/business-person-details.md) stödlinje och [Schemafältgrupp för XDM Business Person Components](../../../../xdm/field-groups/profile/business-person-components.md) guide.

| Källfält | Sökväg till mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `City` | `workAddress.city` |
| `ConvertedDate` | `b2b.convertedDate` |
| `Country` | `workAddress.country` |
| `Email` | `workEmail.address` | Sekundär identitet. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `IsConverted` | `b2b.isConverted` |
| `isDeleted` | `isDeleted` |
| `"Salesforce"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` |
| `Id` | `b2b.personKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |
| `Id` | `personComponents.sourcePersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `Latitude` | `workAddress._schema.latitude` |
| `Longitude` | `workAddress._schema.longitude` |
| `Name` | `person.name.fullName` |
| `PostalCode` | `workAddress.postalCode` |
| `Salutation` | `person.name.courtesyTitle` |
| `State` | `workAddress.state` |
| `Status` | `b2b.personStatus` |
| `Status` | `personComponents.personStatus` |
| `Street` | `workAddress.street1` |
| `Title` | `extendedWorkDetails.jobTitle` |
| `Suffix` | `person.name.suffix` |
| `Company` | `b2b.companyName` |
| `Website` | `b2b.companyWebsite` |
| `ConvertedContactId` | `b2b.convertedContactKey.sourceID` |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.convertedContactKey` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `"Lead"` | `b2b.personType` |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", ConvertedContactId, "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceConvertedContactKey` |

{style="table-layout:auto"}

## Konto {#account}

Läs [Översikt över XDM Business Account-detaljer](../../../../xdm/classes/b2b/business-account.md) för mer information om klassen XDM.

| Källfält | Sökväg till mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Salesforce"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `AccountNumber` | `accountNumber` |
| `AccountSource` | `accountSourceType` |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |
| `BillingCity` | `accountBillingAddress.city` |
| `BillingCountry` | `accountBillingAddress.country` |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |
| `BillingState` | `accountBillingAddress.state` |
| `BillingStreet` | `accountBillingAddress.street1` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `accountDescription` |
| `DunsNumber` | `accountOrganization.DUNSNumber` | data.com-funktion |
| `Fax` | `accountFax.number` |
| `isDeleted` | `isDeleted` |
| `Id` | `accountKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `accountKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `Industry` | `accountOrganization.industry` |
| `Jigsaw` | `accountOrganization.jigsaw` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `NaicsCode` | `accountOrganization.NAICSCode` | data.com-funktion |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | data.com-funktion |
| `Name` | `accountName` |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `Ownership` | `accountOwnership` |
| `ParentId` | `accountParentKey.sourceID` |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountParentKey` |
| `Phone` | `accountPhone.number` |
| `ShippingCity` | `accountShippingAddress.city` |
| `ShippingCountry` | `accountShippingAddress.country` |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |
| `ShippingState` | `accountShippingAddress.state` |
| `ShippingStreet` | `accountShippingAddress.street1` |
| `Sic` | `accountOrganization.SICCode` |
| `SicDesc` | `accountOrganization.SICDescription` |
| `Site` | `accountSite` |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |
| `Tradestyle` | `accountTradeStyle` | data.com-funktion |
| `Type` | `accountType` |
| `Website` | `accountOrganization.website` |

{style="table-layout:auto"}

## Möjligheter {#opportunity}

Läs [Översikt över affärsmöjligheter i XDM](../../../../xdm/classes/b2b/business-opportunity.md) för mer information om klassen XDM.

| Källfält | Sökväg till mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Salesforce"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `AccountId` | `accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` | Relation. |
| `Amount` | `opportunityAmount.amount` |
| `CampaignId` | `campaignKey.sourceID` |
| `iif(CampaignId != null && CampaignId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")), null)` | `campaignKey` |
| `CloseDate` | `expectedCloseDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `opportunityDescription` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `FiscalQuarter` | `fiscalQuarter` |
| `FiscalYear` | `fiscalYear` |
| `ForecastCategory` | `forecastCategory` |
| `ForecastCategoryName` | `forecastCategoryName` |
| `Id` | `opportunityKey.sourceID` |
| `IsClosed` | `isClosed` |
| `isDeleted` | `isDeleted` |
| `IsWon` | `isWon` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `leadSource` |
| `Name` | `opportunityName` |
| `NextStep` | `nextStep` |
| `Probability` | `probabilityPercentage` |
| `StageName` | `opportunityStage` |
| `TotalOpportunityQuantity` | `opportunityQuantity` |
| `Type` | `opportunityType` |
| `CurrencyIsoCode` | `opportunityAmount.currencyCode` |

{style="table-layout:auto"}

## Kontaktroll för affärsmöjlighet {#opportunity-contact-role}

Läs [Översikt över klassen XDM Business Opportunity Person Relation](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) för mer information om klassen XDM.

| Källfält | Sökväg till mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Salesforce"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `"Salesforce"` | `personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personKey.sourceInstanceID` |
| `ContactId` | `personKey.sourceID` |
| `concat(ContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Id` | `opportunityPersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityPersonKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `isDeleted` | `isDeleted` |
| `IsPrimary` | `isPrimary` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `"Salesforce"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` |
| `OpportunityId` | `opportunityKey.sourceID` |
| `concat(OpportunityId,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` |
| `Role` | `personRole` |

{style="table-layout:auto"}

## Campaign {#campaign}

Läs [Översikt över klassen XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) för mer information om klassen XDM. Mer information om XDM-fältgrupper finns i [Schemafältgrupp för XDM Business Campaign-information](../../../../xdm/field-groups/b2b-campaign/details.md) guide.

| Källfält | Sökväg till mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Salesforce"` | `campaignKey.sourceType` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `isDeleted` | `isDeleted` |
| `Id` | `campaignKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `Name` | `campaignName` |
| `ParentId` | `parentCampaignKey.sourceID` |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `parentCampaignKey` |
| `Type` | `campaignType` |
| `Status` | `campaignStatus` |
| `StartDate` | `campaignStartDate` |
| `EndDate` | `campaignEndDate` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `BudgetedCost` | `budgetedCost.amount` |
| `ActualCost` | `actualCost.amount` |
| `ExpectedResponse` | `expectedResponse` |
| `IsActive` | `isActive` |
| `Description` | `campaignDescription` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `CurrencyIsoCode` | `actualCost.currencyCode` |

## Kampanjmedlem {#campaign-member}

Läs [Översikt över medlemmar i XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign-members.md) för mer information om klassen XDM. Mer information om XDM-fältgrupper finns i [Schemafältgrupp för XDM Business Campaign-medlemsinformation](../../../../xdm/field-groups/b2b-campaign/details.md) -dokument.

| Källfält | Sökväg till mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Salesforce"` | `campaignMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `campaignMemberKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `isDeleted` | `isDeleted` |
| `Id` | `campaignMemberKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignMemberKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `"Salesforce"` | `campaignKey.sourceType` |
| `${CRM_ORG_ID}` | `campaignKey.sourceInstanceID` |
| `CampaignId` | `campaignKey.sourceID` |
| `concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` |
| `"Salesforce"` | `personKey.sourceType` |
| `${CRM_ORG_ID}` | `personKey.sourceInstanceID` |
| `LeadOrContactId` | `personKey.sourceID` |
| `concat(LeadOrContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |
| `Status` | `memberStatus` |
| `HasResponded` | `hasResponded` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `FirstRespondedDate` | `firstRespondedDate` |
| `Type` | `b2b.personType` |

## Kontaktrelation för konto {#account-contact-relation}

Läs [XDM Business Account Person Relation-klass](../../../../xdm/classes/b2b/business-account-person-relation.md) för mer information om klassen XDM.

| Källfält | Sökväg till mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `AccountId` | `accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` |
| `ContactId` | `personKey.sourceID` |
| `iif(ContactId != null && ContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personKey` |
| `CreatedById` | `extSourceSystemAudit.createdBy` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `EndDate` | `relationEndDate` |
| `IsDeleted` | `isDeleted` |
| `Id` | `accountPersonKey.sourceID` |
| `"Salesforce"` | `accountPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountPersonKey.sourceInstanceID` |
| `concat(Id, "@${CRM_ORG_ID}.Salesforce")` | `accountPersonKey.sourceKey` | Primär identitet. |
| `IsActive` | `IsActive` |
| `IsDirect` | `IsDirect` |
| `LastModifiedById` | `extSourceSystemAudit.lastUpdatedBy` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `explode(Roles,";")` | `personRoles[]` |
| `StartDate` | `relationStartDate` |

## Nästa steg

Genom att läsa det här dokumentet har du fått insikt i mappningsförhållandet mellan [!DNL Salesforce] källfält och deras motsvarande XDM-fält. Läs dokumentationen om [skapa [!DNL Salesforce] källanslutning](../../../connectors/crm/salesforce.md) för mer information.
