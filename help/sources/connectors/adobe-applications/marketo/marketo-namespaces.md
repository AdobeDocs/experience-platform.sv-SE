---
title: B2B-namnutrymmen och scheman
description: Det här dokumentet innehåller en översikt över anpassade namnutrymmen som krävs när du skapar en B2B-källkoppling.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 5e8bb04ca18159eab98b2f7f0bba8cb1488a1f26
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 0%

---

# B2B-namnutrymmen och scheman

>[!NOTE]
>
>Du kan använda mallar i Adobe Experience Platform användargränssnitt för att göra det enklare att skapa resurser för B2B- och B2C-data. Mer information finns i handboken om [användning av mallar i plattformsgränssnittet](../../../tutorials/ui/templates.md).

Det här dokumentet innehåller information om den underliggande inställningen för de namnutrymmen och scheman som ska användas med B2B-källor. Det här dokumentet innehåller även information om hur du konfigurerar det automatiseringsverktyg för Postman som krävs för att skapa B2B-namnutrymmen och scheman.

>[!IMPORTANT]
>
>Du måste ha tillgång till [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) för att B2B-scheman ska kunna delta i [kundprofilen i realtid](../../../../profile/home.md).

## Konfigurera B2B-namnutrymmen och automatisk schemagenerering

Det första steget i att använda verktyget för automatisk generering av B2B-namnområde och schema är att konfigurera din plattformsutvecklarkonsol och [!DNL Postman]-miljö.

- Du kan hämta samlingen och miljön för automatisk generering av namnområde och scheman från den här [GitHub-databasen](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Information om hur du använder plattforms-API:er, inklusive information om hur du samlar in värden för obligatoriska huvuden och läser exempel-API-anrop, finns i guiden [Komma igång med plattforms-API:er](../../../../landing/api-guide.md).
- Mer information om hur du genererar autentiseringsuppgifter för plattforms-API:er finns i självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md).
- Information om hur du konfigurerar [!DNL Postman] för plattforms-API:er finns i självstudiekursen [Konfigurera utvecklarkonsol och [!DNL Postman]](../../../../landing/postman.md).

Med en plattformsutvecklarkonsol och [!DNL Postman] konfigurerad kan du nu börja använda lämpliga miljövärden i din [!DNL Postman] -miljö.

Följande tabell innehåller exempelvärden samt ytterligare information om hur du fyller i din [!DNL Postman]-miljö:

| Variabel | Beskrivning | Exempel |
| --- | --- | --- |
| `CLIENT_SECRET` | En unik identifierare som används för att generera `{ACCESS_TOKEN}`. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) är en autentiseringsuppgift som används för att generera {ACCESS_TOKEN}. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md) finns mer information om hur du genererar `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | En unik identifierare som används för att autentisera anrop till API:er för Experience Platform. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Med avseende på [!DNL Marketo] är det här värdet fast och alltid inställt på: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Behållaren `global` innehåller alla klasser, schemafältgrupper, datatyper och scheman som tillhandahålls av Adobe och Experience Platform-partner. Med avseende på [!DNL Marketo] är det här värdet fast och ställs alltid in på `global`. | `global` |
| `PRIVATE_KEY` | En autentiseringsuppgift som används för att autentisera din [!DNL Postman]-instans till API:er för Experience Platform. Se självstudiekursen om hur du konfigurerar utvecklarkonsolen och [konfigurerar utvecklarkonsolen och [!DNL Postman]](../../../../landing/postman.md) för instruktioner om hur du hämtar din {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | En autentiseringsuppgift som används för att integrera med Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) utgör ramverket för autentisering till Adobes tjänster. Med avseende på [!DNL Marketo] är det här värdet fast och alltid inställt på: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen [Konfigurera utvecklarkonsolen och [!DNL Postman]](../../../../landing/postman.md) för instruktioner om hur du hämtar din `{ORG_ID}`-information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Namnet på den virtuella sandlådepartition som du använder. | `prod` |
| `TENANT_ID` | Ett ID som används för att se till att de resurser du skapar namnges korrekt och finns i din organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | URL-slutpunkten som du gör API-anrop till. Det här värdet är fast och är alltid inställt på: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Köra skript

När din [!DNL Postman]-samling och miljö är konfigurerad kan du nu köra skriptet via gränssnittet [!DNL Postman].

I gränssnittet [!DNL Postman] väljer du rotmappen för verktyget för autogenerering och sedan **[!DNL Run]** i den övre rubriken.

![root-folder](../images/marketo/root-folder.png)

Gränssnittet [!DNL Runner] visas. Se till att alla kryssrutor är markerade och välj sedan **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../images/marketo/run-generator.png)

En lyckad begäran skapar de namnutrymmen och scheman som krävs för B2B.

## B2B-namnutrymmen

Identitetsnamnutrymmen är en komponent i [[!DNL Identity Service]](../../../../identity-service/home.md) som kan skilja kontexten för en identitet åt. En fullständigt kvalificerad identitet innehåller ett identitetsvärde och ett namnutrymme. Mer information finns i översikten [för namnutrymmen](../../../../identity-service/features/namespaces.md).

B2B-namnutrymmen används i entitetens primära identitet.

Följande tabell innehåller information om den underliggande inställningen för B2B-namnutrymmen.

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Visningsnamn | Identitetssymbol | Identitetstyp |
| --- | --- | --- |
| B2B-person | `b2b_person` | `CROSS_DEVICE` |
| B2B-konto | `b2b_account` | `B2B_ACCOUNT` |
| B2B-säljprojekt | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| Personrelation för B2B-säljprojekt | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B-kampanj | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B-kampanjmedlem | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B-marknadsföringslista | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B Marketing List-medlem | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B-konto, personrelation | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## B2B-scheman

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera schemafältgrupper.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [Grunderna för schemakomposition](../../../../xdm/schema/composition.md).

Följande tabell innehåller information om de underliggande inställningarna för B2B-scheman.

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Schemanamn | Basklass | Fältgrupper | [!DNL Profile] i schemat | Primär identitet | Namnutrymme för primär identitet | Sekundär identitet | Namnutrymme för sekundär identitet | Relation | Anteckningar |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-konto | [XDM Business Account](../../../../xdm/classes/b2b/business-account.md) | XDM Business Account Details | Aktiverad | `accountKey.sourceKey` i basklassen | B2B-konto | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-konto | <ul><li>`accountParentKey.sourceKey` i fältgruppen XDM Business Account Details</li><li>Målegenskap: `/accountKey/sourceKey`</li><li>Typ: en-till-en</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li></ul> |
| B2B-person | [Individuell XDM-profil](../../../../xdm/classes/individual-profile.md) | <ul><li>Information om XDM Business Person</li><li>XDM Business Person Components</li><li>IdentityMap</li><li>Information om samtycke och inställningar</li></ul> | Aktiverad | `b2b.personKey.sourceKey` i fältgruppen XDM Business Person Details | B2B-person | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` av fältgruppen XDM Business Person Details</li><li>`workEmail.address` av fältgruppen XDM Business Person Details</ol></li> | <ol><li>B2B-person</li><li>E-post</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` av fältgruppen XDM Business Person Components</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li><li>Destinationsegenskap: accountKey.sourceKey</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Personer</li></ul> |
| B2B-säljprojekt | [XDM-affärsmöjlighet](../../../../xdm/classes/b2b/business-opportunity.md) | Information om affärsmöjligheter i XDM | Aktiverad | `opportunityKey.sourceKey` i basklassen | B2B-säljprojekt | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-säljprojekt | <ul><li>`accountKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li><li>Målegenskap: `accountKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Affärsmöjligheter</li></ul> |
| Personrelation för B2B-säljprojekt | [XDM-affärsmöjlighet, personrelation](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Ingen | Aktiverad | `opportunityPersonKey.sourceKey` i basklassen | Personrelation för B2B-säljprojekt | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | Personrelation för B2B-säljprojekt | **Första relationen**<ul><li>`personKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Destinationsegenskap: b2b.personKey.sourceKey</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Affärsmöjligheter</li></ul>**Andra relationen**<ul><li>`opportunityKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-säljprojekt </li><li>Namnutrymme: B2B-säljprojekt </li><li>Målegenskap: `opportunityKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Möjlighet</li><li>Relationsnamn från referensschema: Personer</li></ul> |
| B2B-kampanj | [XDM Business Campaign](../../../../xdm/classes/b2b/business-campaign.md) | Information om XDM Business Campaign | Aktiverad | `campaignKey.sourceKey` i basklassen | B2B-kampanj | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-kampanj |
| B2B-kampanjmedlem | [XDM Business Campaign-medlemmar](../../../../xdm/classes/b2b/business-campaign-members.md) | Information om XDM Business Campaign-medlem | Aktiverad | `ccampaignMemberKey.sourceKey` i basklassen | B2B-kampanjmedlem | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-kampanjmedlem | **Första relationen**<ul><li>`personKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Målegenskap: `b2b.personKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Kampanjer</li></ul>**Andra relationen**<ul><li>`campaignKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-kampanj</li><li>Namnutrymme: B2B-kampanj</li><li>Målegenskap: `campaignKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Kampanj</li><li>Relationsnamn från referensschema: Personer</li></ul> |
| B2B-marknadsföringslista | [XDM Business Marketing List](../../../../xdm/classes/b2b/business-marketing-list.md) | Ingen | Aktiverad | `marketingListKey.sourceKey` i basklassen | B2B-marknadsföringslista | Ingen | Ingen | Ingen | Statisk lista har inte synkroniserats från [!DNL Salesforce] och har därför ingen sekundär identitet. |
| B2B Marketing List-medlem | [XDM Business Marketing List-medlemmar](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Ingen | Aktiverad | `marketingListMemberKey.sourceKey` i basklassen | B2B Marketing List-medlem | Ingen | Ingen | **Första relationen**<ul><li>`PersonKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Målegenskap: `b2b.personKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Marknadsföringslistor</li></ul>**Andra relationen**<ul><li>`marketingListKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-marknadsföringslista</li><li>Namnområde: B2B-marknadsföringslista</li><li>Målegenskap: `marketingListKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Marknadsföringslista</li><li>Relationsnamn från referensschema: Personer</li></ul> | Den statiska listmedlemmen har inte synkroniserats från [!DNL Salesforce] och har därför ingen sekundär identitet. |
| B2B-verksamhet | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Besök WebPage</li><li>Nytt lead</li><li>Konvertera lead</li><li>Lägg till i lista</li><li>Ta bort från lista</li><li>Lägg till i affärsmöjlighet</li><li>Ta bort från affärsmöjlighet</li><li>Formulär ifyllt</li><li>Länkklickningar</li><li>E-post levererad</li><li>E-post öppnad</li><li>E-post klickad</li><li>E-post studsade</li><li>Mjuk e-poststudsning</li><li>Avbeställ e-post</li><li>Resultat ändrad</li><li>Affärsmöjligheten har uppdaterats</li><li>Status i kampanjförloppet har ändrats</li><li>Identifierare för person</li><li>Marketo Web URL</li><li>Intressant stund</li><li>Ring webkrok</li><li>Ändra kampanjslut</li><li>Intäktsfas ändrad</li><li>Sammanfoga leads</li><li>E-post skickad</li><li>Ändra kampanjström</li><li>Lägg till i kampanj</li></ul> | Aktiverad | `personKey.sourceKey` i fältgruppen för personidentifierare | B2B-person | Ingen | Ingen | **Första relationen**<ul><li>Fältet `listOperations.listKey.sourceKey`</li><li>Typ: en-till-en</li><li>Referensschema: B2B-marknadsföringslista</li><li>Namnområde: B2B-marknadsföringslista</li></ul>**Andra relationen**<ul><li>Fältet `opportunityEvent.opportunityKey.sourceKey`</li><li>Typ: en-till-en</li><li>Referensschema: B2B-säljprojekt</li><li>Namnutrymme: B2B-säljprojekt</li></ul>**Tredje relationen**<ul><li>Fältet `leadOperation.campaignProgression.campaignKey.sourceKey`</li><li>Typ: en-till-en</li><li>Referensschema: B2B-kampanj</li><li>Namnutrymme: B2B-kampanj</li></ul> | `ExperienceEvent` skiljer sig från entiteter. Identiteten för upplevelsehändelsen är den person som utförde aktiviteten. |
| B2B-konto, personrelation | [XDM Business Account Person Relation](../../../../xdm/classes/b2b/business-account-person-relation.md) | Identitetskarta | Aktiverad | `accountPersonKey.sourceKey` i basklassen | B2B-konto, personrelation | Ingen | Ingen | **Första relationen**<ul><li>`personKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Målegenskap: `b2b.personKey.SourceKey`</li><li>Relationsnamn från aktuellt schema: Personer</li><li>Relationsnamn från referensschema: Konto</li></ul>**Andra relationen**<ul><li>`accountKey.sourceKey` i basklassen</li><li>Typ: Flera till ett</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li><li>Målegenskap: `accountKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Personer</li></ul> |

{style="table-layout:auto"}

## Nästa steg

Om du vill lära dig hur du ansluter dina [!DNL Marketo]-data till plattformen kan du läsa självstudiekursen om hur du [skapar en Marketo-källkoppling i användargränssnittet](../../../tutorials/ui/create/adobe-applications/marketo.md).
