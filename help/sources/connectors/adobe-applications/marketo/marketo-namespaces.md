---
keywords: Experience Platform;hem;populära ämnen;Marketo källanslutning;namnutrymmen;scheman;b2b;B2B
solution: Experience Platform
title: B2B-namnutrymmen och scheman
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över anpassade namnutrymmen som krävs när du skapar en B2B-källkoppling.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: a67e411c7d07bc5d94876b6bafbbea5056b7a9bc
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 1%

---

# B2B-namnutrymmen och scheman

Det här dokumentet innehåller information om den underliggande inställningen för de namnutrymmen och scheman som ska användas med B2B-källor. Det här dokumentet innehåller även information om hur du konfigurerar Postman-automatiseringsverktyget som krävs för att generera B2B-namnutrymmen och scheman.

## Konfigurera B2B-namnutrymmen och automatisk schemagenerering

Det första steget i att använda verktyget för automatisk generering av B2B-namnutrymme och schema är att konfigurera din plattformsutvecklarkonsol och [!DNL Postman]-miljö.

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
| `IMS` | Identity Management System (IMS) utgör ramverket för autentisering till Adobes tjänster. Med avseende på [!DNL Marketo] är det här värdet fast och ställs alltid in på: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../../landing/postman.md) för instruktioner om hur du hämtar din `{IMS_ORG}`-information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Namnet på den virtuella sandlådepartition som du använder. | `prod` |
| `TENANT_ID` | Ett ID som används för att se till att de resurser du skapar namnges korrekt och finns i IMS-organisationen. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | URL-slutpunkten som du gör API-anrop till. Detta värde är fast och ställs alltid in på: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style=&quot;table-layout:auto&quot;}

### Köra skript

När du har konfigurerat din [!DNL Postman]-samling och -miljö kan du nu köra skriptet via gränssnittet [!DNL Postman].

I gränssnittet [!DNL Postman] väljer du rotmappen för verktyget för autogenerering och sedan **[!DNL Run]** i det övre huvudet.

![root-folder](../images/marketo/root-folder.png)

Gränssnittet [!DNL Runner] visas. Se till att alla kryssrutor är markerade och välj sedan **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../images/marketo/run-generator.png)

En lyckad begäran skapar de namnutrymmen och scheman som krävs för B2B.

## B2B-namnutrymmen

Identitetsnamnutrymmen är en komponent i [[!DNL Identity Service]](../../../../identity-service/home.md) som används för att skilja kontexten eller typen för en identitet. En fullständigt kvalificerad identitet innehåller ett ID-värde och ett namnutrymme. Mer information finns i [översikten över namnutrymmen](../../../../identity-service/namespaces.md).

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

{style=&quot;table-layout:auto&quot;}

## B2B-scheman

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera schemafältgrupper.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [grunderna för schemakomposition](../../../../xdm/schema/composition.md).

Följande tabell innehåller information om de underliggande inställningarna för B2B-scheman.

>[!NOTE]
>
>Rulla åt vänster/höger för att visa hela innehållet i tabellen.

| Schemanamn | Basklass | Fältgrupper | [!DNL Profile] i schema | Primär identitet | Namnutrymme för primär identitet | Sekundär identitet | Namnutrymme för sekundär identitet | Relation | Anteckningar |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-konto | XDM Business Account | XDM Business Account Details | Aktiverad | `accountKey.sourceKey` i basklassen | B2B-konto | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-konto | <ul><li>`accountParentKey.sourceKey` i fältgruppen XDM Business Account Details</li><li>Destinationsegenskap: `/accountKey/sourceKey`</li><li>Typ: en-till-en</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li></ul> |
| B2B-person | Individuell XDM-profil | <ul><li>Information om XDM Business Person</li><li>XDM Business Person Components</li><li>IdentityMap</li><li>Information om samtycke och inställningar</li></ul> | Aktiverad | `b2b.personKey.sourceKey` i fältgruppen XDM Business Person Details | B2B-person | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` fältgruppen XDM Business Person Details</li><li>`workEmail.address` fältgruppen XDM Business Person Details</ol></li> | <ol><li>B2B-person</li><li>E-post</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` fältgruppen XDM Business Person Components</li><li>Typ: Många-till-ett</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li><li>Destinationsegenskap: accountKey.sourceKey</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| B2B-säljprojekt | XDM - affärsmöjlighet | Information om affärsmöjligheter i XDM | Aktiverad | `opportunityKey.sourceKey` i basklassen | B2B-säljprojekt | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-säljprojekt | <ul><li>`accountKey.sourceKey` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: B2B-konto</li><li>Namnutrymme: B2B-konto</li><li>Destinationsegenskap: `accountKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Konto</li><li>Relationsnamn från referensschema: Möjligheter</li></ul> |
| Personrelation för B2B-säljprojekt | XDM - affärsmöjlighet, personrelation | Ingen | Aktiverad | `opportunityPersonKey.sourceKey` i basklassen | Personrelation för B2B-säljprojekt | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | Personrelation för B2B-säljprojekt | **Första relationen**<ul><li>`personKey.sourceKey` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Destinationsegenskap: b2b.personKey.sourceKey</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Möjligheter</li></ul>**Andra relationen**<ul><li>`opportunityKey.sourceKey` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: B2B-säljprojekt </li><li>Namnutrymme: B2B-säljprojekt </li><li>Destinationsegenskap: `opportunityKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Möjligheter</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| B2B-kampanj | XDM Business Campaign | Information om XDM Business Campaign | Aktiverad | `campaignKey.sourceKey` i basklassen | B2B-kampanj | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-kampanj |
| B2B-kampanjmedlem | XDM Business Campaign-medlem | Information om XDM Business Campaign-medlem | Aktiverad | `ccampaignMemberKey.sourceKey` i basklassen | B2B-kampanjmedlem | `extSourceSystemAudit.externalKey.sourceKey` i basklassen | B2B-kampanjmedlem | **Första relationen**<ul><li>`personKey.sourceKey` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Destinationsegenskap: `b2b.personKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Kampanjer</li></ul>**Andra relationen**<ul><li>`campaignKey.sourceKey` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: B2B-kampanj</li><li>Namnutrymme: B2B-kampanj</li><li>Destinationsegenskap: `campaignKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Campaign</li><li>Relationsnamn från referensschema: Folk</li></ul> |
| B2B-marknadsföringslista | XDM Business Marketing List | Ingen | Aktiverad | `marketingListKey.sourceKey` i basklassen | B2B-marknadsföringslista | Ingen | Ingen | Ingen | Statisk lista synkroniseras inte från [!DNL Salesforce] och har därför ingen sekundär identitet. |
| B2B Marketing List-medlem | XDM Business Marketing List-medlemmar | Ingen | Aktiverad | `marketingListMemberKey.sourceKey` i basklassen | B2B Marketing List-medlem | Ingen | Ingen | **Första relationen**<ul><li>`PersonKey.sourceKey` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: B2B-person</li><li>Namnutrymme: B2B-person</li><li>Destinationsegenskap: `b2b.personKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Person</li><li>Relationsnamn från referensschema: Marknadsföringslistor</li></ul>**Andra relationen**<ul><li>`marketingListKey.sourceKey` i basklassen</li><li>Typ: Många-till-ett</li><li>Referensschema: B2B-marknadsföringslista</li><li>Namnutrymme: B2B-marknadsföringslista</li><li>Destinationsegenskap: `marketingListKey.sourceKey`</li><li>Relationsnamn från aktuellt schema: Marknadsföringslista</li><li>Relationsnamn från referensschema: Folk</li></ul> | Den statiska listmedlemmen synkroniseras inte från [!DNL Salesforce] och har därför ingen sekundär identitet. |
| B2B-verksamhet | XDM ExperienceEvent | <ul><li>Besök WebPage</li><li>Nytt lead</li><li>Konvertera lead</li><li>Lägg till i lista</li><li>Ta bort från lista</li><li>Lägg till i affärsmöjlighet</li><li>Ta bort från affärsmöjlighet</li><li>Formuläret har fyllts i</li><li>Länkklickningar</li><li>E-post levererad</li><li>E-post öppnad</li><li>E-post klickad</li><li>E-post studsade</li><li>Mjuk e-poststudsning</li><li>Avbeställ e-post</li><li>Poängen har ändrats</li><li>Affärsmöjligheten har uppdaterats</li><li>Status i kampanjförloppet har ändrats</li><li>Personidentifierare</li><li>Marketo Web URL</li><li>Intressant stund</li></ul> | Aktiverad | `personKey.sourceKey` fältgrupp för personidentifierare | B2B-person | Ingen | Ingen | **Första relationen**<ul><li>`listOperations.listKey.sourceKey` fält</li><li>Typ: en-till-en</li><li>Referensschema: B2B-marknadsföringslista</li><li>Namnutrymme: B2B-marknadsföringslista</li></ul>**Andra relationen**<ul><li>`opportunityEvent.opportunityKey.sourceKey` fält</li><li>Typ: en-till-en</li><li>Referensschema: B2B-säljprojekt</li><li>Namnutrymme: B2B-säljprojekt</li></ul>**Tredje relationen**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` fält</li><li>Typ: en-till-en</li><li>Referensschema: B2B-kampanj</li><li>Namnutrymme: B2B-kampanj</li></ul> | `ExperienceEvent` skiljer sig från entiteter. Identiteten för upplevelsehändelsen är den person som utförde aktiviteten. |

{style=&quot;table-layout:auto&quot;}

## Nästa steg

Om du vill lära dig hur du ansluter dina [!DNL Marketo]-data till plattformen kan du läsa självstudiekursen om att [skapa en Marketo-källkoppling i användargränssnittet](../../../tutorials/ui/create/adobe-applications/marketo.md).
