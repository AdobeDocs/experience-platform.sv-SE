---
keywords: Experience Platform;hem;populära ämnen;Marketo källanslutning;namnutrymmen;scheman
solution: Experience Platform
title: 'Marketo namnutrymmen '
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över anpassade namnutrymmen som krävs när du skapar en Marketo Engage-källkoppling.
translation-type: tm+mt
source-git-commit: bea6b35627b0e913c894c38ba9553085ba0aa26f
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 1%

---


# (Beta) [!DNL Marketo Engage] namnutrymmen och scheman

>[!IMPORTANT]
>
>Källan [!DNL Marketo Engage] är för närvarande i betaversion. Funktionen och dokumentationen ändras.

Det här dokumentet innehåller information om den underliggande inställningen för B2B-namnutrymmen och scheman som används med [!DNL Marketo Engage] (kallas nedan &quot;[!DNL Marketo]&quot;). Det här dokumentet innehåller även information om hur du konfigurerar Postman-automatiseringsverktyget som krävs för att generera [!DNL Marketo] B2B-namnutrymmen och scheman.

## Förutsättningar

Innan du kan skapa dina B2B-namnutrymmen och scheman måste du först konfigurera plattformsutvecklarkonsolen och [!DNL Postman]-miljön. Mer information finns i självstudiekursen om hur du konfigurerar utvecklarkonsolen och [!DNL Postman]](../../../../landing/postman.md).[

Använd följande variabler i din [!DNL Marketo]-miljö med en plattformsutvecklarkonsol och en [!DNL Postman]-konfiguration:

| Miljövariabel | Exempelvärde | Anteckningar |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | Mer information finns i självstudiekursen om [autentisering av din [!DNL Marketo] instans](./marketo-auth.md). |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | Se följande [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) för mer information om hur du skaffar ditt organisations-ID. |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | Se följande [[!DNL Microsoft Dynamics] guide](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) för mer information om hur du skaffar ditt organisations-ID. |
| `has_abm` | `false` | Värdet är `true` om du prenumererar på kontobaserad marknadsföring. |
| `has_msi` | `false` | Värdet är `true` om du prenumererar på [!DNL Marketo Sales Insight]. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] namnutrymmen

Identitetsnamnutrymmen är en komponent i [[!DNL Identity Service]](../../../../identity-service/home.md) som fungerar som indikatorer för det sammanhang som en identitet relateras till.

En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme. Ett nytt anpassat namnutrymme krävs för varje ny [!DNL Marketo]-instans och dataset-kombination. En [!DNL Marketo]-källanslutning som anropar datauppsättningen `programs` kräver till exempel ett eget anpassat namnutrymme, och en annan Marketo-källanslutning som samlar in samma datauppsättning kräver också ett eget anpassat namnutrymme. Mer information finns i [översikten över namnutrymmen](../../../../identity-service/namespaces.md).

Namnutrymmet [!DNL Marketo] används i entitetens primära identitet.

Följande tabell innehåller information om den underliggande uppsättningen för namnutrymmen [!DNL Marketo].

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Visningsnamn | Identitetssymbol | Identitetstyp | Utfärdartyp | Typ av utfärdarentitet | Exempel på Munchkin-ID |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | autogenererad | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | autogenererad | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | autogenererad | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | autogenererad | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | autogenererad | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | autogenererad | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | autogenererad | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | autogenererad | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | autogenererad | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] namnutrymmen

Om du prenumererar på [!DNL Salesforce]-integreringen används namnutrymmet [!DNL Salesforce] i entitetens sekundära identitet.

Följande tabell innehåller information om den underliggande uppsättningen för namnutrymmen [!DNL Salesforce].

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Visningsnamn | Identitetssymbol | Identitetstyp | Utfärdartyp | Typ av utfärdarentitet | [!DNL Salesforce] Exempel på prenumerationsorganisations-ID |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | autogenererad | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | autogenererad | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | autogenererad | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | autogenererad | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | autogenererad | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | autogenererad | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] namnutrymmen

Om du prenumererar på [!DNL Dynamics]-integreringen används namnutrymmet [!DNL Dynamics] som en sekundär identitet för entiteten.

Följande tabell innehåller information om den underliggande uppsättningen för namnutrymmen [!DNL Dynamics].

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Visningsnamn | Identitetssymbol | Identitetstyp | Utfärdartyp | Typ av utfärdarentitet | [!DNL Salesforce] Exempel på prenumerationsorganisations-ID |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | autogenererad | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | autogenererad | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | autogenererad | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | autogenererad | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | autogenererad | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | autogenererad | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] scheman

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera blandningar.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [grunderna för schemakomposition](../../../../xdm/schema/composition.md).

Följande tabell innehåller information om den underliggande inställningen för [!DNL Marketo] scheman.

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Schemanamn | Basklass | Blandningar | Primär identitet | Namnutrymme för primär identitet | Sekundär identitet | Namnutrymme för sekundär identitet | Relation | Anteckningar |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] Företag {MUNCHKIN_ID} | XDM Business Account | XDM Business Account Details | `accountID` i basklassen | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in XDM Business Account Details mixin</li><li>Typ: en-till-en</li><li>Referensschema: Marketo Company {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] Person {MUNCHKIN_ID} | Individuell XDM-profil | <ul><li>Information om XDM Business Person</li><li>XDM Business Person Components</li></ul> | `personID` i basklassen | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` av XDM Business Person Details</li><li>`workEmail.address` av XDM Business Person Details</li><li>`identityMap` av blandningen av identitetskarta</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>E-post</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` av XDM Business Person Components mixin</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo Company {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_company_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `accountID`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| [!DNL Marketo] Möjligheter {MUNCHKIN_ID} | XDM - affärsmöjlighet | Information om affärsmöjligheter i XDM | `opportunityID` i basklassen | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo Company {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_company_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `accountID`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Möjligheter</li></ul> |
| [!DNL Marketo] Roll för säljprojektskontakt {MUNCHKIN_ID} | XDM - affärsmöjlighet, personrelation | Ingen | `opportunityPersonID` i basklassen | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Första relationen<ul><li>`personID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo-person {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_person_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `personID`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Möjligheter</li></ul>Andra relationen<ul><li>`opportunityID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo Opportunity {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `opportunityID`</li><li>Relationsnamn från aktuellt schema: Möjligheter</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| [!DNL Marketo] Program {MUNCHKIN_ID} | XDM Business Campaign | Information om XDM Business Campaign | `campaignID` i basklassen | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] Programmedlem {MUNCHKIN_ID} | XDM Business Campaign-medlem | Information om XDM Business Campaign-medlem | `campaignMemberID` i basklassen | `marketo_program_member_{MUNCHKIN_ID}` | Ingen | Ingen | Första relationen<ul><li>`personID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo-person {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_person_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `personID`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Program</li></ul>Andra relationen<ul><li>`campaignID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo Program {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_program_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: campaignID</li><li>Relationsnamn från aktuellt schema: Program</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| [!DNL Marketo] Statisk lista {MUNCHKIN_ID} | XDM Business Marketing List | Ingen | `marketingListID` i basklassen | `marketo_static_list_{MUNCHKIN_ID}` | Ingen | Ingen | Ingen | Statisk lista synkroniseras inte från [!DNL Salesforce] och har därför ingen sekundär identitet |
| [!DNL Marketo] Statisk listmedlem {MUNCHKIN_ID} | XDM Business Marketing List-medlemmar | Ingen | `marketingListMemberID` i basklassen | `marketo_static_list_member_{MUNCHKIN_ID}` | Ingen | Ingen | Första relationen<ul><li>`personID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo-person {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_person_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `personID`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Listor</li></ul>Andra relationen<ul><li>`marketingListID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo Static List {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `marketingListID`</li><li>Relationsnamn från aktuellt schema: Lista</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| [!DNL Marketo] Namngivet konto {MUNCHKIN_ID} | XDM Business Account | XDM Business Account Details | `accountID` i basklassen | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in XDM Business Account Details mixin</li><li>Typ: en-till-en</li><li>Referensschema: Marketo Named Account {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Aktivitet {MUNCHKIN ID} | XDM Experience Event | <ul><li>Besök WebPage</li><li>Nytt lead</li><li>Konvertera lead</li><li>Lägg till i lista</li><li>Ta bort från lista</li><li>Lägg till i affärsmöjlighet</li><li>Ta bort från affärsmöjlighet</li><li>Formuläret har fyllts i</li><li>Länkklickningar</li><li>E-post levererad</li><li>E-post öppnad</li><li>E-post klickad</li><li>E-post studsade</li><li>Mjuk e-poststudsning</li><li>Avbeställ e-post</li><li>Poängen har ändrats</li><li>Affärsmöjligheten har uppdaterats</li><li>Status i kampanjförloppet har ändrats</li><li>Personidentifierare</li><li>Marketo Web URL | `personID` Personidentifierarblandning | marketo_person_{MUNCHKIN_ID} | Ingen | Ingen | Första relationen<ul><li>`listOperations.listID` fält</li><li>Typ: en-till-en</li><li>Referensschema: Marketo Static List {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Andra relationen<ul><li>`opportunityEvent.opportunityID` fält</li><li>Typ: en-till-en</li><li>Referensschema: Marketo Opportunity {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Tredje relationen<ul><li>`leadOperation.campaignProgression.campaignID` fält</li><li>Typ: en-till-en</li><li>Referensschema: Marketo Program {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Alla scheman är aktiverade för [!DNL Real-time Customer Profile]

## Nästa steg

Om du vill lära dig hur du ansluter dina [!DNL Marketo]-data till plattformen kan du läsa självstudiekursen om att [skapa en Marketo-källkoppling i användargränssnittet](../../../tutorials/ui/create/adobe-applications/marketo.md).