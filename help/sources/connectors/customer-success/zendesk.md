---
title: Översikt över Zendesk Source Connector
description: Lär dig hur du ansluter Zendesk till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# [!DNL Zendesk]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inhämtning av data från tredjepartsprogram. Bland leverantörerna av nöjda kunder finns [!DNL Zendesk].

Detta Adobe Experience Platform [källor](https://experienceleague.adobe.com/docs/experience-platform/sources/home.htmll?lang=sv) utnyttjar [Zendesk Search API > Exportera sökresultat](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) som returnerar användarinformation till Experience Platform från Zendesk för vidare bearbetning.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Autentisera [!DNL Zendesk] konto

[!DNL Zendesk] använder lagervariabler som en autentiseringsmekanism för att kommunicera med [!DNL Zendesk] API.

I det här avsnittet beskrivs nödvändiga steg som måste utföras för att autentisera [!DNL Zendesk] konto.

* Det första steget för att autentisera [!DNL Zendesk] kontot är till för att säkerställa att du har [!DNL Zendesk] supportkonto. Om du inte redan har en kan du se [[!DNL Zendesk] registersida](https://www.zendesk.com/register/) för att registrera och skapa ditt Zendesk-konto.
* När du har registrerat dig går du till [[!DNL Zendesk] webbplats](https://www.zendesk.com/login/) och tillhandahåller **underdomän**.
* Nästa, välj **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Hämta slutligen din API-token från **[!DNL API token]** -avsnitt.

![Zendesk API-token](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Se [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) om du vill ha information om hur du hämtar din underdomän. Mer information om hur du genererar API-token finns i [[!DNL Zendesk] guide för generering av en ny API-token](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Zendesk] till Plattform med API:er eller användargränssnittet:

## Anslut [!DNL Zendesk] till plattform med API:er

* [Skapa en källanslutning och ett dataflöde för [!DNL Zendesk] med API:t för Flow Service](../../tutorials/api/create/customer-success/zendesk.md)

## Anslut [!DNL Zendesk] till plattform med användargränssnittet

* [Skapa en [!DNL Zendesk ]källanslutning i användargränssnittet](../../tutorials/ui/create/customer-success/zendesk.md)
* [Skapa ett dataflöde för en källanslutning till en lyckad kund i användargränssnittet](../../tutorials/ui/dataflow/customer-success.md)
