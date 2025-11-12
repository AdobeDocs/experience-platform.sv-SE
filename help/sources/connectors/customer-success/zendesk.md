---
title: Zendesk Source Connector - översikt
description: Lär dig hur du ansluter Zendesk till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# [!DNL Zendesk]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från tredjepartsprogram. Stöd för leverantörer av kundframgångar omfattar [!DNL Zendesk].

Denna [källa](https://experienceleague.adobe.com/docs/experience-platform/sources/home.htmll?lang=sv) i Adobe Experience Platform använder [Zendesk Search API > Exportera sökresultat](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) som returnerar användarinformation till Experience Platform från Zendesk för vidare bearbetning.

## IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

## Autentisera ditt [!DNL Zendesk]-konto

[!DNL Zendesk] använder innehavartoken som autentiseringsmekanism för att kommunicera med API:t [!DNL Zendesk].

I det här avsnittet beskrivs nödvändiga steg som måste utföras för att ditt [!DNL Zendesk]-konto ska kunna autentiseras.

* Det första steget för att autentisera ditt [!DNL Zendesk]-konto är att kontrollera att du har ett [!DNL Zendesk]-supportkonto. Om du inte redan har någon kan du se [[!DNL Zendesk] registreringssidan](https://www.zendesk.com/register/) för att registrera och skapa ditt Zendesk-konto.
* När du har registrerat dig går du till [[!DNL Zendesk] webbplatsen](https://www.zendesk.com/login/) och anger din **underdomän**.
* Välj sedan **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Hämta slutligen din API-token från avsnittet **[!DNL API token]**.

![Zendesk API-token](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Mer information om hur du hämtar din underdomän finns i [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->). Mer information om hur du genererar API-token finns i [[!DNL Zendesk] guiden om hur du genererar en ny API-token](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Zendesk] till Experience Platform med API:er eller användargränssnittet:

## Anslut [!DNL Zendesk] till Experience Platform med API:er

* [Skapa en källanslutning och ett dataflöde för  [!DNL Zendesk] med API:t för Flow Service](../../tutorials/api/create/customer-success/zendesk.md)

## Anslut [!DNL Zendesk] till Experience Platform med användargränssnittet

* [Skapa en  [!DNL Zendesk ]källanslutning i användargränssnittet](../../tutorials/ui/create/customer-success/zendesk.md)
* [Skapa ett dataflöde för en källanslutning till en lyckad kund i användargränssnittet](../../tutorials/ui/dataflow/customer-success.md)
