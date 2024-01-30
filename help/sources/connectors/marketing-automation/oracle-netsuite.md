---
title: Oracle NetSuite - källöversikt
description: Lär dig hur du ansluter Oracle NetSuite till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>The [!DNL Oracle NetSuite] källan är i betaversion. Läs [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för att importera data från externa leverantörer av automatiseringssystem för marknadsföring. Stöd för leverantörer av automatiserad marknadsföring innefattar [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) är en molnbaserad serie för affärshantering som omfattar ERP/ekonomi-, CRM- och e-handelslösningar.

Du kan använda två olika källor för att importera data från [!DNL Oracle NetSuite] till Experience Platform:

* Använd [!DNL Oracle NetSuite Activities] källa till import av händelsedata.
* Använd [!DNL Oracle NetSuite Entities] källa för att importera kund- och kontaktdata.

Se följande tabell för mer information om de två [!DNL Oracle NetSuite] Källor.

| Källa | Typ | Beskrivning |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Händelse | Hämta schemalagda aktiviteter som lagts till i din kalender. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kund | Hämta specifika kunddata, t.ex. kundnamn, adresser och nyckelidentifierare. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kontakt | Hämta kontaktnamn, e-post, telefonnummer och anpassade kontaktrelaterade fält som är kopplade till kunder. |

## IP-adress tillåtelselista {#ip-allow-list}

En lista med IP-adresser kan behöva läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Förutsättningar {#prerequisites}

Innan du kan ta med [!DNL Oracle NetSuite] data till Experience Platform måste du först se till att du har följande:

* **An [!DNL Oracle NetSuite] konto**.
   * Kontakt [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) om du inte redan har ett giltigt konto.
* An **aktiv prenumeration** till [!DNL Oracle NetSuite] produkt.
* An **konto-ID**.
   * The [!DNL Oracle NetSuite] använder OAuth 2.0 för att kommunicera med [!DNL Oracle NetSuite] API. Om du inte har ditt konto-ID kan du gå till [!DNL Oracle] dokumentation om [hur du hämtar ditt konto-ID](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **klient-ID** och **klienthemlighet** kombinationen.
   * Klient-ID och klienthemlighet krävs för åtkomst [!DNL Oracle NetSuite] API. Under det här steget måste du även se till att administratören har:
      * Aktiverade OAuth 2.0-funktionen och konfigurerade lämpliga OAuth 2.0-roller.
      * Tilldelade användare till OAuth 2.0-rollerna och skapade de nödvändiga integrationsposterna.
* An **åtkomsttoken** och **uppdatera token**.
   * Se [!DNL Oracle] stödlinje på [OAuth 2.0 Authorization Code Grant Flow](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) om du vill ha information om hur du genererar och uppdaterar token.

### Samla in nödvändiga inloggningsuppgifter {#gather-credentials}

För att kunna ansluta [!DNL Oracle NetSuite] till Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Klient-ID | Klient-ID-värdet som genereras när du skapar integreringsposten i [!DNL Oracle NetSuite]. Läs [!DNL Oracle] guide om hur [skapa integrationsposter](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) för mer information. | `7fce.....b42f`<br>Värdet är en 64-teckensträng. |
| Klienthemlighet | Klientens hemliga värde som genereras när du skapar integreringsposten. Läs [!DNL Oracle] guide om hur [skapa integrationsposter](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) för mer information. | `5c98.....1b46`<br>Värdet är en 64-teckensträng. |
| Test-URL för auktorisering | (Valfritt) [!DNL NetSuite] verifieringstestets URL. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Åtkomsttoken | Åtkomsttoken är i JSON Web Token-format (JWT) och är endast giltig i 60 minuter. Mer information om hur du hämtar din åtkomsttoken finns i [!DNL Oracle] stödlinje på [OAuth 2.0-auktorisering för NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> Värdet är en 1 024-teckensträng som är formaterad som JSON Web Token (JWT). |
| Uppdatera token | Använd uppdateringen för att generera en ny åtkomsttoken när din åtkomsttoken har upphört att gälla. Uppdateringstoken gäller i sju dagar. Mer information om hur du hämtar din åtkomsttoken finns i [!DNL Oracle] stödlinje på [OAuth 2.0-auktorisering för NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> Värdet är en 1 024-teckensträng som är formaterad som JSON Web Token (JWT). |
| Åtkomsttoken-URL | Den tokenslutpunkt som programmet skickar POSTEN begäranden till. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>När en uppdateringstoken upphör att gälla måste du skapa ett nytt konto i Experience Platform med dina uppdaterade tokens.

## Anslut [!DNL Oracle NetSuite Activities] till plattform {#oracle-netsuite-activities}

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Oracle NetSuite Activities] till Plattform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde som ger [!DNL Oracle NetSuite Activities] data till plattformen med API:er](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Koppla samman [!DNL Oracle NetSuite Activities] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Skapa ett dataflöde för en källanslutning med användargränssnittet](../../tutorials/ui/dataflow/marketing-automation.md).

## Anslut [!DNL Oracle NetSuite Entities] till plattform {#oracle-netsuite-entities}

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Oracle NetSuite Entities] till Plattform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde som ger [!DNL Oracle NetSuite Entities] data till plattformen med API:er](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Koppla samman [!DNL Oracle NetSuite Entities] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Skapa ett dataflöde för en källanslutning med användargränssnittet](../../tutorials/ui/dataflow/marketing-automation.md).
