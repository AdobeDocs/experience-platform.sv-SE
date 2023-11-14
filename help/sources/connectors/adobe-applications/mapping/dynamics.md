---
title: Mappningsfält för Microsoft Dynamics
description: Tabellerna nedan innehåller mappningarna mellan källfälten i Microsoft Dynamics och deras motsvarande XDM-fält.
exl-id: 32f51761-5de3-4192-8f23-c1412ca12c08
source-git-commit: ec42cf27c082611acb1a08500b7bbd23fc34d730
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics] fältkopplingar

Tabellerna nedan innehåller mappningarna mellan [!DNL Microsoft Dynamics] källfält och deras motsvarande XDM-fält (Experience Data Model).

## Kontakter {#contacts}

| Källfält | Mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `assistantname` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `assistantphone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `birthdate` | `person.birthDate` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `contactid` | `b2b.personKey.sourceID` |
| `concat(contactid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `iif(contactid != null && contactid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", contactid, "sourceKey", concat(contactid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `department` | `extendedWorkDetails.departments` |
| `fullname` | `person.name.fullName` |
| `suffix` | `person.name.suffix` |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey", concat(parentcustomerid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourceAccountKey` |
| `iif(parentcustomerid != null && parentcustomerid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", parentcustomerid, "sourceKey",  concat(parentcustomerid, "@${CRM_ORG_ID}.Dynamics")), null)` | `b2b.accountKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | Sekundär identifierare. |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `lastname` | `person.name.lastName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |
| `telephone1` | `workPhone.number` |

{style="table-layout:auto"}

## Leads {#leads}

| Källfält | Mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `address1_addressid` | `workAddress._id` |
| `address1_city` | `workAddress.city` |
| `address1_country` | `workAddress.country` |
| `address1_county` | `workAddress.stateProvince` |
| `address1_latitude` | `workAddress._schema.latitude` |
| `address1_line1` | `workAddress.street1` |
| `address1_line2` | `workAddress.street2` |
| `address1_line3` | `workAddress.street3` |
| `address1_longitude` | `workAddress._schema.longitude` |
| `address1_postalcode` | `workAddress.postalCode` |
| `address1_postofficebox` | `workAddress.postOfficeBox` |
| `address1_stateorprovince` | `workAddress.state` |
| `telephone1` | `workPhone.number` |
| `mobilephone` | `mobilePhone.number` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `emailaddress1` | `workEmail.address` | Sekundär identifierare |
| `emailaddress2` | `personalEmail.address` |
| `emailaddress1` | `personComponents.workEmail.address` |
| `fax` | `faxPhone.number` |
| `firstname` | `person.name.firstName` |
| `fullname` | `person.name.fullName` |
| `jobtitle` | `extendedWorkDetails.jobTitle` |
| `lastname` | `person.name.lastName` |
| `"Dynamics"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `leadid` | `b2b.personKey.sourceID` |
| `concat(leadid,"@${CRM_ORG_ID}.Dynamics")` | `b2b.personKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `iif(leadid != null && leadid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", leadid, "sourceKey", concat(leadid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personComponents.sourcePersonKey` |
| `middlename` | `person.name.middleName` |
| `mobilephone` | `mobilePhone.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `salutation` | `person.name.courtesyTitle` |

{style="table-layout:auto"}

## Konton {#accounts}

| Källfält | Mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Dynamics"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `accountid` | `accountKey.sourceID` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `accountnumber` | `accountNumber` |
| `accountratingcode` | `accountOrganization.rating` |
| `address1_addressid` | `accountPhysicalAddress._id` |
| `address1_city` | `accountPhysicalAddress.city` |
| `address1_country` | `accountPhysicalAddress.country` |
| `address1_county` | `accountPhysicalAddress.region` |
| `address1_latitude` | `accountPhysicalAddress._schema.latitude` |
| `address1_line1` | `accountPhysicalAddress.street1` |
| `address1_line2` | `accountPhysicalAddress.street2` |
| `address1_line3` | `accountPhysicalAddress.street3` |
| `address1_longitude` | `accountPhysicalAddress._schema.longitude` |
| `address1_name` | `accountPhysicalAddress.label` |
| `address1_postalcode` | `accountPhysicalAddress.postalCode` |
| `address1_postofficebox` | `accountPhysicalAddress.postOfficeBox` |
| `address1_stateorprovince` | `accountPhysicalAddress.state` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `accountDescription` |
| `fax` | `accountFax.number` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `name` | `accountName` |
| `numberofemployees` | `accountOrganization.numberOfEmployees` |
| `revenue` | `accountOrganization.annualRevenue.amount` |
| `sic` | `accountOrganization.SICCode` |
| `telephone1` | `accountPhone.number` |
| `tickersymbol` | `accountOrganization.tickerSymbol` |
| `websiteurl` | `accountOrganization.website` |
| `concat(accountid,"@${CRM_ORG_ID}.Dynamics")` | `accountKey.sourceKey` |

{style="table-layout:auto"}

## Möjligheter {#opportunities}

| Källfält | Mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `name` | `opportunityName` |
| `"Dynamics"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `iif(parentaccountid != null && parentaccountid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", parentaccountid, "sourceKey", concat(parentaccountid, "@${CRM_ORG_ID}.Dynamics")), null)` | `accountKey` |
| `actualclosedate` | `actualCloseDate` |
| `actualvalue` | `opportunityAmount.amount` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `campaignKey` |
| `closeprobability` | `probabilityPercentage` |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `description` | `opportunityDescription` |
| `estimatedclosedate` | `expectedCloseDate` |
| `estimatedvalue` | `expectedRevenue.amount` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `opportunityid` | `opportunityKey.sourceID` |
| `concat(opportunityid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `salesstage` | `opportunityStage` |
| `stepname` | `nextStep` |

{style="table-layout:auto"}

## Kontaktroller för affärsmöjlighet {#opportunity-contact-roles}

| Källfält | Mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Dynamics"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `connectionid` | `opportunityPersonKey.sourceID` |
| `concat(connectionid,"@${CRM_ORG_ID}.Dynamics")` | `opportunityPersonKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `iif(record1id != null && record1id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record1id, "sourceKey", concat(record1id,"@${CRM_ORG_ID}.Dynamics")), null)` | `opportunityKey` |
| `iif(record2id != null && record2id != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", record2id, "sourceKey", concat(record2id,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `connectionrole1.name` | `personRole` |
| `record1objecttypecode` | *En anpassad fältgrupp måste definieras som ett målschema.* Anvisningar om hur du gör detta finns i avsnittet Bilaga [mappa ett källfält av typen picklist till ett mål-XDM-schema](#picklist-type-fields) för mer information. | För en lista över möjliga värden och värden och etiketter för `record1objecttypecode` källfält, se detta [[!DNL Microsoft Dynamics] referensdokument för anslutningsenhet](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record1objecttypecode-options). |
| `record2objecttypecode` | *En anpassad fältgrupp måste definieras som ett målschema.* Anvisningar om hur du gör detta finns i avsnittet Bilaga [mappa ett källfält av typen picklist till ett mål-XDM-schema](#picklist-type-fields) för mer information. | För en lista över möjliga värden och värden och etiketter för `record2objecttypecode` källfält, se detta [[!DNL Microsoft Dynamics] referensdokument för anslutningsenhet](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/connection?view=op-9-1#record2objecttypecode-options). |

{style="table-layout:auto"}

## Kampanjer {#campaigns}

| Källfält | Mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `campaignid` | `campaignKey.sourceID` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `concat(campaignid,"@${CRM_ORG_ID}.Dynamics")` | `campaignKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `"Dynamics"` | `campaignKey.sourceType` |
| `iif(campaignid != null && campaignid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", campaignid, "sourceKey", concat(campaignid,"@${CRM_ORG_ID}.Dynamics")), null)` | `extSourceSystemAudit.externalKey` | The `extSourceSystemAudit.externalKey` är sekundär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `createdon` | `extSourceSystemAudit.createdDate` |
| `modifiedby` | `extSourceSystemAudit.lastUpdatedBy` |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `description` | `campaignDescription` |
| `name` | `campaignName` |
| `totalactualcost` | `actualCost.amount` |
| `budgetedcost` | `budgetedCost.amount` |
| `expectedrevenue` | `expectedRevenue.amount` |
| `actualend` | `campaignEndDate` |
| `actualstart` | `campaignStartDate` |
| `expectedresponse` | `expectedResponse` |
| `utcconversiontimezonecode` | `timeZone` |
| `utcconversiontimezonecode` | `timezoneName` |

{style="table-layout:auto"}

## Marknadsföringslista {#marketing-list}

| Källfält | Mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Dynamics"` | `marketingListKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `description` | `marketingListDescription` |
| `listname` | `marketingListName` |
| `listid` | `marketingListKey.sourceID` |
| `concat(listid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `modifiedon` | `extSourceSystemAudit.lastUpdatedDate` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## Medlemmar i marknadsföringslistan {#marketing-list-members}

| Källfält | Mål-XDM-fält | Anteckningar |
| --- | --- | --- |
| `"Dynamics"` | `marketingListMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `marketingListMemberKey.sourceInstanceID` | Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `iif(entityid != null && entityid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", entityid, "sourceKey", concat(entityid,"@${CRM_ORG_ID}.Dynamics")), null)` | `personKey` |
| `listmemberid` | `marketingListMemberKey.sourceID` |
| `concat(listmemberid,"@${CRM_ORG_ID}.Dynamics")` | `marketingListMemberKey.sourceKey` | Primär identitet. Värdet för `"${CRM_ORG_ID}"` ersätts automatiskt. |
| `iif(listid != null && listid != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", listid, "sourceKey", concat(listid,"@${CRM_ORG_ID}.Dynamics")), null)` | `marketingListKey` |
| `createdon` | `extSourceSystemAudit.createdDate` |

{style="table-layout:auto"}

## Bilaga

I avsnitten nedan finns ytterligare information som du kan använda när du konfigurerar B2B-mappningar för dina [!DNL Microsoft] Dynamics-källa.

### Fält för plocklistetyp {#picklist-type-fields}

Du kan använda [beräknade fält](../../../../data-prep/ui/mapping.md#calculated-fields) för att mappa ett källfält av plocklistetyp från [!DNL Microsoft Dynamics] till ett mål-XDM-fält.

Till exempel `genderCode` -fältet innehåller två alternativ:

| Värde | Etikett |
| --- | --- |
| 1 | `male` |
| 2 | `female` |

Du kan använda följande alternativ för att mappa `genderCode` källfält till `person.gender` målfält:

#### Använd en logisk operator

| Källfält | Mål-XDM-fält |
| --- | --- |
| `decode(genderCode, "1", "male", "2", "female", "default")` | `person.gender` |

I det här fallet motsvarar värdet tangenten, om tangenten finns i alternativen, eller `default`, if `default` finns och nyckeln kan inte hittas. Värdet motsvarar `null` om alternativen är `null` eller det inte finns `default` och nyckeln hittades inte.

#### Använd ett beräknat fält

| Källfält | Mål-XDM-fält |
| --- | --- |
| `iif(gendercode.equals("1"),"male",iif(gendercode.equals("2"),"female",null))` | `person.gender` |

>[!TIP]
>
>En kapslad iteration av ovanstående åtgärd skulle likna: `iif(condition, iif(cond1, tv1, fv1), iif(cond2, tv2, fv2))`.

Mer information finns i [dokument om logiska operatorer i [!DNL Data Prep]](../../../../data-prep/functions.md##logical-operators)
