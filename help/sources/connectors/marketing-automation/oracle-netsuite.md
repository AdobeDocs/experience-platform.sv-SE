---
title: Oracle NetSuite Source - översikt
description: Lär dig hur du ansluter Oracle NetSuite till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>Källan [!DNL Oracle NetSuite] är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från automatiseringssystem för tredjepartsmarknadsföring. Stöd för leverantörer av automatiserad marknadsföring inkluderar [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) är en molnbaserad Business Management-svit som omfattar ERP/ekonomi-, CRM- och e-handelslösningar.

Du kan använda två olika källor för att importera data från [!DNL Oracle NetSuite] till Experience Platform:

* Använd källan [!DNL Oracle NetSuite Activities] för att importera händelsedata.
* Använd källan [!DNL Oracle NetSuite Entities] för att importera kund- och kontaktdata.

Visa följande tabell för mer information om de två [!DNL Oracle NetSuite]-källorna.

| Source | Typ | Beskrivning |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Händelse | Hämta schemalagda aktiviteter som lagts till i din kalender. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kund | Hämta specifika kunddata, t.ex. kundnamn, adresser och nyckelidentifierare. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Kontakt | Hämta kontaktnamn, e-post, telefonnummer och anpassade kontaktrelaterade fält som är kopplade till kunder. |

## IP-adress tillåtelselista {#ip-allow-list}

En lista med IP-adresser kan behöva läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Förhandskrav {#prerequisites}

Innan du kan överföra dina [!DNL Oracle NetSuite]-data till Experience Platform måste du se till att du har följande:

* **Ett [!DNL Oracle NetSuite]-konto**.
   * Kontakta [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) om du inte redan har ett giltigt konto.
* En **aktiv prenumeration** till valfri [!DNL Oracle NetSuite]-produkt.
* Ett **konto-ID**.
   * Källan [!DNL Oracle NetSuite] använder OAuth 2.0 för att kommunicera med API:erna för [!DNL Oracle NetSuite]. Om du inte har ditt konto-ID kan du gå till [!DNL Oracle]-dokumentationen om [hur du hämtar ditt konto-ID](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* En kombination av **klient-ID** och **klienthemlighet**.
   * Klient-ID och klienthemlighet krävs för att komma åt [!DNL Oracle NetSuite] API:er. Under det här steget måste du även se till att administratören har:
      * Aktiverade OAuth 2.0-funktionen och konfigurerade lämpliga OAuth 2.0-roller.
      * Tilldelade användare till OAuth 2.0-rollerna och skapade de nödvändiga integrationsposterna.
* En **åtkomsttoken** och en **uppdateringstoken**.
   * Mer information om hur du genererar din åtkomst och uppdaterar token finns i [!DNL Oracle]-guiden för [OAuth 2.0-auktoriseringskodens bidragsflöde](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow).

### Samla in nödvändiga inloggningsuppgifter {#gather-credentials}

För att kunna ansluta [!DNL Oracle NetSuite] till Experience Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Klient-ID | Klient-ID-värdet som genereras när du skapar integreringsposten i [!DNL Oracle NetSuite]. Läs guiden [!DNL Oracle] om hur du [skapar integrationsposter](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) om du vill ha mer information. | `7fce.....b42f`<br>Värdet är en 64-teckensträng. |
| Klienthemlighet | Klientens hemliga värde som genereras när du skapar integreringsposten. Läs guiden [!DNL Oracle] om hur du [skapar integrationsposter](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) om du vill ha mer information. | `5c98.....1b46`<br>Värdet är en 64-teckensträng. |
| Test-URL för auktorisering | (Valfritt) Din [!DNL NetSuite]-verifieringstest-URL. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Åtkomsttoken | Åtkomsttoken är i JSON Web Token-format (JWT) och är endast giltig i 60 minuter. Mer information om hur du hämtar din åtkomsttoken finns i [!DNL Oracle]-guiden för [OAuth 2.0-auktorisering för NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> Värdet är en 1 024-teckensträng som är formaterad som JSON Web Token (JWT). |
| Uppdatera token | Använd uppdateringen för att generera en ny åtkomsttoken när din åtkomsttoken har upphört att gälla. Uppdateringstoken gäller i sju dagar. Mer information om hur du hämtar din åtkomsttoken finns i [!DNL Oracle]-guiden för [OAuth 2.0-auktorisering för NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> Värdet är en 1 024-teckensträng som är formaterad som JSON Web Token (JWT). |
| Åtkomsttoken-URL | Token-slutpunkten dit programmet skickar POST-begäranden. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>När en uppdateringstoken upphör att gälla måste du skapa ett nytt konto i Experience Platform med dina uppdaterade tokens.

## Anslut [!DNL Oracle NetSuite Activities] till Experience Platform {#oracle-netsuite-activities}

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Oracle NetSuite Activities] till Experience Platform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde för att hämta [!DNL Oracle NetSuite Activities] data till Experience Platform med API:er](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Anslut ditt [!DNL Oracle NetSuite Activities] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Skapa ett dataflöde för en källanslutning med användargränssnittet ](../../tutorials/ui/dataflow/marketing-automation.md).

## Anslut [!DNL Oracle NetSuite Entities] till Experience Platform {#oracle-netsuite-entities}

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Oracle NetSuite Entities] till Experience Platform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde för att hämta [!DNL Oracle NetSuite Entities] data till Experience Platform med API:er](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Anslut ditt [!DNL Oracle NetSuite Entities] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Skapa ett dataflöde för en källanslutning med användargränssnittet ](../../tutorials/ui/dataflow/marketing-automation.md).
