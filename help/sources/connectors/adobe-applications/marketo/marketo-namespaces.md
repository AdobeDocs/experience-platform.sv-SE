---
keywords: Experience Platform;hem;populära ämnen;Marketo källanslutning;namnutrymmen;scheman
solution: Experience Platform
title: Marketo namnutrymmen
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över anpassade namnutrymmen som krävs när du skapar en Marketo Engage-källkoppling.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 609b951cbde880a9f354b343adb1796def0a812c
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 1%

---

# (Beta) [!DNL Marketo Engage] namnutrymmen och scheman

>[!IMPORTANT]
>
>Källan [!DNL Marketo Engage] är för närvarande i betaversion. Funktionen och dokumentationen ändras.

Det här dokumentet innehåller information om den underliggande inställningen för B2B-namnutrymmen och scheman som används med [!DNL Marketo Engage] (kallas nedan &quot;[!DNL Marketo]&quot;). Det här dokumentet innehåller även information om hur du konfigurerar Postman-automatiseringsverktyget som krävs för att generera [!DNL Marketo] B2B-namnutrymmen och scheman.

## Konfigurera namnutrymmet [!DNL Marketo] och verktyget för automatisk schemagenerering

Det första steget i att använda namnutrymmet [!DNL Marketo] och verktyget för automatisk schemagenerering är att konfigurera plattformsutvecklarkonsolen och [!DNL Postman]-miljön.

- Du kan hämta samlingen och miljön för den automatiska genereringen av namnutrymmet och schemat från den här [GitHub-databasen](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Information om hur du använder plattforms-API:er, inklusive information om hur du samlar in värden för obligatoriska huvuden och läser exempel-API-anrop, finns i guiden [komma igång med plattforms-API:er](../../../../landing/api-guide.md).
- Mer information om hur du genererar autentiseringsuppgifter för plattforms-API:er finns i självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md).
- Mer information om hur du konfigurerar [!DNL Postman] för plattforms-API:er finns i självstudiekursen [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../../landing/postman.md).

Med en plattformsutvecklarkonsol och [!DNL Postman] konfigurerad kan du nu börja använda lämpliga miljövärden i din [!DNL Postman]-miljö.

Följande tabell innehåller exempelvärden samt ytterligare information om hur du fyller i din [!DNL Postman]-miljö:

| Variabel | Beskrivning | Exempel |
| --- | --- | --- |
| `CLIENT_SECRET` | En unik identifierare som används för att generera din `{ACCESS_TOKEN}`. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) är en autentiseringsuppgift som används för att generera {ACCESS_TOKEN}. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md) finns mer information om hur du skapar din `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | En unik identifierare som används för att autentisera anrop till API:er för Experience Platform. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Med avseende på [!DNL Marketo] är det här värdet fast och är alltid inställt på: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Behållaren `global` innehåller alla standardklasser som tillhandahålls av Adobe och Experience Platform partner, schemafältgrupper, datatyper och scheman. Med avseende på [!DNL Marketo] är det här värdet fast och ställs alltid in på `global`. | `global` |
| `PRIVATE_KEY` | En autentiseringsuppgift som används för att autentisera din [!DNL Postman]-instans till Experience Platform API:er. Se självstudiekursen om hur du konfigurerar utvecklarkonsolen och [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../../landing/postman.md) för instruktioner om hur du hämtar {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | En autentiseringsuppgift som används för att integrera med Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) utgör ramverket för autentisering till Adobe-tjänster. Med avseende på [!DNL Marketo] är det här värdet fast och ställs alltid in på: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../../landing/postman.md) för instruktioner om hur du hämtar din `{IMS_ORG}`-information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Namnet på den virtuella sandlådepartition som du använder. | `prod` |
| `TENANT_ID` | Ett ID som används för att se till att de resurser du skapar namnges korrekt och finns i IMS-organisationen. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | URL-slutpunkten som du gör API-anrop till. Detta värde är fast och ställs alltid in på: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | Det unika ID:t för ditt [!DNL Marketo]-konto. I självstudiekursen om [autentisering av din [!DNL Marketo] instans](./marketo-auth.md) finns mer information om hur du hämtar din `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | Organisations-ID för ditt [!DNL Salesforce]-konto. Se följande [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) för mer information om hur du skaffar ditt [!DNL Salesforce] organisations-ID. | `00D4W000000FgYJUA0` |
| `msd_org_id` | Organisations-ID för ditt [!DNL Dynamics]-konto. Se följande [[!DNL Microsoft Dynamics] guide](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) för mer information om hur du skaffar ditt [!DNL Dynamics] organisations-ID. | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Köra skript

När du har konfigurerat din [!DNL Postman]-samling och -miljö kan du nu köra skriptet via gränssnittet [!DNL Postman].

I gränssnittet [!DNL Postman] väljer du rotmappen för verktyget för autogenerering och sedan **[!DNL Run]** i det övre huvudet.

![root-folder](../images/marketo/root-folder.png)

Gränssnittet [!DNL Runner] visas. Se till att alla kryssrutor är markerade och välj sedan **[!DNL Run Adobe I/O Access Token Generation + Automate Namespace creation]**.

![run-generator](../images/marketo/run-generator.png)

En lyckad begäran skapar B2B-namnutrymmen och scheman enligt betaspecifikationerna.

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
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | autogenererad | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
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

| Visningsnamn | Identitetssymbol | Identitetstyp | Utfärdartyp | Typ av utfärdarentitet | [!DNL Dynamics] Exempel på prenumerationsorganisations-ID |
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

Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera schemafältgrupper.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [grunderna för schemakomposition](../../../../xdm/schema/composition.md).

Följande tabell innehåller information om den underliggande inställningen för [!DNL Marketo] scheman.

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Schemanamn | Basklass | Fältgrupper | [!DNL Profile] i schema | Primär identitet | Namnutrymme för primär identitet | Sekundär identitet | Namnutrymme för sekundär identitet | Relation | Anteckningar |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | XDM Business Account | XDM Business Account Details | Aktiverad | `accountID` i basklassen | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` i fältgruppen XDM Business Account Details</li><li>Typ: en-till-en</li><li>Referensschema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | Individuell XDM-profil | <ul><li>Information om XDM Business Person</li><li>XDM Business Person Components</li><li>IdentityMap</li></ul> | Aktiverad | `personID` i basklassen | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` fältgruppen XDM Business Person Details</li><li>`workEmail.address` fältgruppen XDM Business Person Details</li><li>`identityMap` fältgrupp för identitetskarta</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>E-post</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` fältgruppen XDM Business Person Components</li><li>Typ: Många-till-ett</li><li>Referensschema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_company_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `accountID`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | XDM - affärsmöjlighet | Information om affärsmöjligheter i XDM | Aktiverad | `opportunityID` i basklassen | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_company_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `accountID`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Möjligheter</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | XDM - affärsmöjlighet, personrelation | Ingen | Aktiverad | `opportunityPersonID` i basklassen | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Första relationen<ul><li>`personID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_person_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `personID`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Möjligheter</li></ul>Andra relationen<ul><li>`opportunityID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `opportunityID`</li><li>Relationsnamn från aktuellt schema: Möjligheter</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | XDM Business Campaign | Information om XDM Business Campaign | Aktiverad | `campaignID` i basklassen | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | XDM Business Campaign-medlem | Information om XDM Business Campaign-medlem | Aktiverad | `campaignMemberID` i basklassen | `marketo_program_member_{MUNCHKIN_ID}` | Ingen | Ingen | Första relationen<ul><li>`personID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: Marketo-person {MUNCHKIN_ID}</li><li>Namnutrymme: `marketo_person_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `personID`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Program</li></ul>Andra relationen<ul><li>`campaignID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_program_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `campaignID`</li><li>Relationsnamn från aktuellt schema: Program</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | XDM Business Marketing List | Ingen | Aktiverad | `marketingListID` i basklassen | `marketo_static_list_{MUNCHKIN_ID}` | Ingen | Ingen | Ingen | Statisk lista synkroniseras inte från [!DNL Salesforce] och har därför ingen sekundär identitet. |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | XDM Business Marketing List-medlemmar | Ingen | Aktiverad | `marketingListMemberID` i basklassen | `marketo_static_list_member_{MUNCHKIN_ID}` | Ingen | Ingen | Första relationen<ul><li>`personID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_person_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `personID`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Listor</li></ul>Andra relationen<ul><li>`marketingListID` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Destinationsegenskap: `marketingListID`</li><li>Relationsnamn från aktuellt schema: Lista</li><li>Relationsnamn från referensschema: Folk</li></ul> | Den statiska listmedlemmen synkroniseras inte från [!DNL Salesforce] och har därför ingen sekundär identitet. |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | XDM Business Account | XDM Business Account Details | Aktiverad | `accountID` i basklassen | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` i basklassen | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` i fältgruppen XDM Business Account Details</li><li>Typ: en-till-en</li><li>Referensschema: `[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Aktivitet `{MUNCHKIN ID}` | XDM ExperienceEvent | <ul><li>Besök WebPage</li><li>Nytt lead</li><li>Konvertera lead</li><li>Lägg till i lista</li><li>Ta bort från lista</li><li>Lägg till i affärsmöjlighet</li><li>Ta bort från affärsmöjlighet</li><li>Formuläret har fyllts i</li><li>Länkklickningar</li><li>E-post levererad</li><li>E-post öppnad</li><li>E-post klickad</li><li>E-post studsade</li><li>Mjuk e-poststudsning</li><li>Avbeställ e-post</li><li>Poängen har ändrats</li><li>Affärsmöjligheten har uppdaterats</li><li>Status i kampanjförloppet har ändrats</li><li>Personidentifierare</li><li>Marketo Web URL | Aktiverad | `personID` fältgrupp för personidentifierare | `marketo_person_{MUNCHKIN_ID}` | Ingen | Ingen | Första relationen<ul><li>`listOperations.listID` fält</li><li>Typ: en-till-en</li><li>Referensschema: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Andra relationen<ul><li>`opportunityEvent.opportunityID` fält</li><li>Typ: en-till-en</li><li>Referensschema: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Tredje relationen<ul><li>`leadOperation.campaignProgression.campaignID` fält</li><li>Typ: en-till-en</li><li>Referensschema: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Namnutrymme: `marketo_program_{MUNCHKIN_ID}`</li></ul> | Den primära identiteten för schemat `[!DNL Marketo] Activity {MUNCHKIN_ID}` är `personID`, vilket är samma som den primära identiteten för schemat `[!DNL Marketo] Person {MUNCHKIN_ID}`. |

{style=&quot;table-layout:auto&quot;}

## Nästa steg

Om du vill lära dig hur du ansluter dina [!DNL Marketo]-data till plattformen kan du läsa självstudiekursen om att [skapa en Marketo-källkoppling i användargränssnittet](../../../tutorials/ui/create/adobe-applications/marketo.md).
