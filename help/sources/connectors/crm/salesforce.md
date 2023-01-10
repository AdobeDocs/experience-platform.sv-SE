---
keywords: Experience Platform;hem;populära ämnen;crm schema;crm;CRM;salesforce;Salesforce
solution: Experience Platform
title: Salesforce Source Connector - översikt
description: Lär dig hur du ansluter Salesforce till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---

# [!DNL Salesforce] koppling

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från ett CRM-system från tredje part. Stöd för CRM-leverantörer innefattar [!DNL Salesforce].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Fältmappning från [!DNL Salesforce] till XDM

Så här upprättar du en källanslutning mellan [!DNL Salesforce] och Platform [!DNL Salesforce] källdatafält måste mappas till rätt mål-XDM-fält innan de kan hämtas till Platform.

Mer information om fältmappningsreglerna mellan [!DNL Salesforce] datauppsättningar och plattform:

- [Kontakter](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Konton](../adobe-applications/mapping/salesforce.md#account)
- [Möjligheter](../adobe-applications/mapping/salesforce.md#opportunity)
- [Kontaktroller för affärsmöjlighet](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Kampanjer](../adobe-applications/mapping/salesforce.md#campaign)
- [Kampanjmedlemmar](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Kontaktrelation för konto](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Konfigurera [!DNL Salesforce] program för automatisk generering av namnutrymme och schema

Så här använder du [!DNL Salesforce] källa som en del av [!DNL B2B-CDP]måste du först konfigurera en [!DNL Postman] för att automatiskt generera [!DNL Salesforce] namnutrymmen och scheman. Följande dokumentation innehåller ytterligare information om hur du konfigurerar [!DNL Postman] utility:

- Du kan hämta samlingen och miljön för automatisk generering av namnutrymme och scheman från den här [GitHub-databas](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Mer information om hur du använder Platform API:er, inklusive information om hur du samlar in värden för obligatoriska huvuden och läser exempel-API-anrop, finns i handboken på [komma igång med plattforms-API:er](../../../landing/api-guide.md).
- Mer information om hur du genererar autentiseringsuppgifter för plattforms-API:er finns i självstudiekursen om [autentisera och komma åt Experience Platform API:er](../../../landing/api-authentication.md).
- Mer information om hur du konfigurerar [!DNL Postman] för plattforms-API:er, se självstudiekursen om [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md).

Med en plattformsutvecklarkonsol och [!DNL Postman] kan du nu börja använda rätt miljövärden i [!DNL Postman] miljö.

Följande tabell innehåller exempelvärden samt ytterligare information om hur du fyller i [!DNL Postman] miljö:

| Variabel | Beskrivning | Exempel |
| --- | --- | --- |
| `CLIENT_SECRET` | En unik identifierare som används för att generera `{ACCESS_TOKEN}`. Se självstudiekursen om [autentisera och komma åt Experience Platform API:er](../../../landing/api-authentication.md) om du vill ha information om hur du hämtar `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) är en autentiseringsuppgift som används för att generera {ACCESS_TOKEN}. Se självstudiekursen om [autentisera och komma åt Experience Platform API:er](../../../landing/api-authentication.md) för information om hur du genererar `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | En unik identifierare som används för att autentisera anrop till API:er för Experience Platform. Se självstudiekursen om [autentisera och komma åt Experience Platform API:er](../../../landing/api-authentication.md) om du vill ha information om hur du hämtar `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. Se självstudiekursen om [autentisera och komma åt Experience Platform API:er](../../../landing/api-authentication.md) om du vill ha information om hur du hämtar `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Med avseende på [!DNL Marketo]är det här värdet fast och alltid inställt på: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | The `global` behållaren innehåller alla klasser som tillhandahålls av Adobe och Experience Platform partner, schemafältgrupper, datatyper och scheman. Med avseende på [!DNL Marketo], det här värdet är fast och alltid inställt på `global`. | `global` |
| `PRIVATE_KEY` | En autentiseringsuppgift som används för att autentisera [!DNL Postman] -instans till Experience Platform API:er. Se självstudiekursen om hur du konfigurerar utvecklarkonsolen och [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | En autentiseringsuppgift som används för att integrera med Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) utgör ramverket för autentisering till Adobes tjänster. Med avseende på [!DNL Marketo], är det här värdet fast och ställs alltid in på: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen om [konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar `{ORG_ID}` information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Namnet på den virtuella sandlådepartition som du använder. | `prod` |
| `TENANT_ID` | Ett ID som används för att se till att de resurser du skapar namnges korrekt och finns i IMS-organisationen. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | URL-slutpunkten som du gör API-anrop till. Detta värde är fast och ställs alltid in på: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | Unikt ID för din [!DNL Marketo] konto. Se självstudiekursen om [autentisera [!DNL Marketo] instance](../adobe-applications/marketo/marketo-auth.md) om du vill ha information om hur du hämtar `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | Organisations-ID för din [!DNL Salesforce] konto. Se följande [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) om du vill ha mer information om hur du skaffar [!DNL Salesforce] organisations-ID. | `00D4W000000FgYJUA0` |
| `has_abm` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Köra skript

Med [!DNL Postman] samling och miljö kan du nu köra skriptet via [!DNL Postman] gränssnitt.

I [!DNL Postman] väljer du rotmappen för verktyget för autogenerering och sedan väljer du **[!DNL Run]** i det övre sidhuvudet.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

The [!DNL Runner] -gränssnittet visas. Se till att alla kryssrutor är markerade och markera sedan **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

En lyckad begäran skapar B2B-namnutrymmen och scheman enligt betaspecifikationerna.

## Anslut [!DNL Salesforce] till plattform med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce] till Plattform med API:er eller användargränssnittet:

- [Skapa en Salesforce-basanslutning med API:t för Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)

## Anslut [!DNL Salesforce] till plattform med användargränssnittet

- [Skapa en Salesforce-källanslutning i användargränssnittet](../../tutorials/ui/create/crm/salesforce.md)
- [Skapa ett dataflöde för en CRM-anslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)
