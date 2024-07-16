---
title: Salesforce Source Connector - översikt
description: Lär dig hur du ansluter Salesforce till Adobe Experience Platform med API:er eller användargränssnittet.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# [!DNL Salesforce]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från ett CRM-system från tredje part. Stöd för CRM-providers omfattar [!DNL Salesforce].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Fältmappning från [!DNL Salesforce] till XDM

Om du vill upprätta en källanslutning mellan [!DNL Salesforce] och plattformen måste [!DNL Salesforce]-källdatafälten mappas till rätt mål-XDM-fält innan de hämtas till plattformen.

Mer information om fältmappningsregler mellan [!DNL Salesforce]-datamängder och plattformen finns i följande:

- [Kontakter](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Konton](../adobe-applications/mapping/salesforce.md#account)
- [Möjligheter](../adobe-applications/mapping/salesforce.md#opportunity)
- [Kontaktroller för affärsmöjlighet](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Kampanjer](../adobe-applications/mapping/salesforce.md#campaign)
- [Kampanjmedlemmar](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Kontaktrelation för konto](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Konfigurera det automatiska genereringsverktyget för namnutrymmet [!DNL Salesforce] och schemat

Om du vill använda källan [!DNL Salesforce] som en del av [!DNL B2B-CDP] måste du först konfigurera ett [!DNL Postman]-verktyg för att automatiskt generera [!DNL Salesforce] namnutrymmen och scheman. Följande dokumentation innehåller ytterligare information om hur du konfigurerar verktyget [!DNL Postman]:

- Du kan hämta samlingen och miljön för automatisk generering av namnområde och scheman från den här [GitHub-databasen](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Information om hur du använder plattforms-API:er, inklusive information om hur du samlar in värden för obligatoriska huvuden och läser exempel-API-anrop, finns i guiden [Komma igång med plattforms-API:er](../../../landing/api-guide.md).
- Mer information om hur du genererar autentiseringsuppgifter för plattforms-API:er finns i självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md).
- Information om hur du konfigurerar [!DNL Postman] för plattforms-API:er finns i självstudiekursen [Konfigurera utvecklarkonsol och [!DNL Postman]](../../../landing/postman.md).

Med en plattformsutvecklarkonsol och [!DNL Postman] konfigurerad kan du nu börja använda lämpliga miljövärden i din [!DNL Postman] -miljö.

Följande tabell innehåller exempelvärden samt ytterligare information om hur du fyller i din [!DNL Postman]-miljö:

| Variabel | Beskrivning | Exempel |
| --- | --- | --- |
| `CLIENT_SECRET` | En unik identifierare som används för att generera `{ACCESS_TOKEN}`. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) är en autentiseringsuppgift som används för att generera {ACCESS_TOKEN}. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du genererar `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | En unik identifierare som används för att autentisera anrop till API:er för Experience Platform. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Den auktoriseringstoken som krävs för att slutföra anrop till Experience Platform API:er. I självstudiekursen om [autentisering och åtkomst av Experience Platform API:er](../../../landing/api-authentication.md) finns mer information om hur du hämtar din `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Med avseende på [!DNL Marketo] är det här värdet fast och alltid inställt på: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | Behållaren `global` innehåller alla klasser, schemafältgrupper, datatyper och scheman som tillhandahålls av Adobe och Experience Platform-partner. Med avseende på [!DNL Marketo] är det här värdet fast och ställs alltid in på `global`. | `global` |
| `PRIVATE_KEY` | En autentiseringsuppgift som används för att autentisera din [!DNL Postman]-instans till API:er för Experience Platform. Se självstudiekursen om hur du konfigurerar utvecklarkonsolen och [konfigurerar utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | En autentiseringsuppgift som används för att integrera med Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Identity Management System (IMS) utgör ramverket för autentisering till Adobes tjänster. Med avseende på [!DNL Marketo] är det här värdet fast och alltid inställt på: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | En företagsenhet som kan äga eller licensiera produkter och tjänster och ge åtkomst till sina medlemmar. Se självstudiekursen [Konfigurera utvecklarkonsolen och [!DNL Postman]](../../../landing/postman.md) för instruktioner om hur du hämtar din `{ORG_ID}`-information. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | Namnet på den virtuella sandlådepartition som du använder. | `prod` |
| `TENANT_ID` | Ett ID som används för att se till att de resurser du skapar namnges korrekt och finns i din organisation. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | URL-slutpunkten som du gör API-anrop till. Det här värdet är fast och är alltid inställt på: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | Unikt ID för ditt [!DNL Marketo]-konto. I självstudiekursen om [autentisering av din [!DNL Marketo] instans](../adobe-applications/marketo/marketo-auth.md) finns mer information om hur du hämtar din `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | Organisations-ID för ditt [!DNL Salesforce]-konto. Se följande [[!DNL Salesforce] guide](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) för mer information om hur du skaffar ditt [!DNL Salesforce] organisations-ID. | `00D4W000000FgYJUA0` |
| `has_abm` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Ett booleskt värde som anger om du prenumererar på [!DNL Marketo Sales Insight]. | `false` |

{style="table-layout:auto"}

### Köra skript

När din [!DNL Postman]-samling och miljö är konfigurerad kan du nu köra skriptet via gränssnittet [!DNL Postman].

I gränssnittet [!DNL Postman] väljer du rotmappen för verktyget för autogenerering och sedan **[!DNL Run]** i den övre rubriken.

![root-folder](../../images/tutorials/create/salesforce/root-folder.png)

Gränssnittet [!DNL Runner] visas. Se till att alla kryssrutor är markerade och välj sedan **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![run-generator](../../images/tutorials/create/salesforce/run-generator.png)

En lyckad begäran skapar B2B-namnutrymmen och scheman enligt betaspecifikationerna.

## Anslut [!DNL Salesforce] till plattformen med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce] till plattformen med API:er eller användargränssnittet:

- [Skapa en Salesforce-basanslutning med API:t för Flow Service](../../tutorials/api/create/crm/salesforce.md)
- [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
- [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)

## Anslut [!DNL Salesforce] till plattformen med användargränssnittet

- [Skapa en Salesforce-källanslutning i användargränssnittet](../../tutorials/ui/create/crm/salesforce.md)
- [Skapa ett dataflöde för en CRM-anslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)
