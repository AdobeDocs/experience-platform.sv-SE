---
solution: Experience Platform
title: Salesforce Marketing Cloud källöversikt
description: Lär dig hur du ansluter Salesforce Marketing Cloud till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform stöder inmatning av data från externa automatiseringssystem. Stöd för leverantörer av automatiserad marknadsföring innefattar [!DNL Salesforce Marketing Cloud].

## Förutsättningar

Innan du kan ansluta [!DNL Salesforce Marketing Cloud] från källa till plattform måste du se till att följande **behörighetsomfång** är tilldelade [!DNL Salesforce Marketing Cloud] kombination av klient-ID och klienthemlighet:

* `campaign_read`
* `list_and_subscribers_read`

Du kan begära omfång genom att ringa `v2/userinfo` resursen för [!DNL Salesforce Marketing Cloud] API. Se [[!DNL Salesforce Marketing Cloud] Dokument för API-integreringsbehörigheter](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) om du vill ha vägledning om hur du begär och jämför omfattningar.

Mer information om omfattningar inklusive en lista över deras relaterade behörigheter och beteenden finns i detta [[!DNL Salesforce Marketing Cloud] REST API-dokument](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Inmatning av anpassade objekt stöds för närvarande inte av [!DNL Salesforce Marketing Cloud] källintegration.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Anslut [!DNL Salesforce Marketing Cloud] till plattform med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce Marketing Cloud] till plattform med API:er:

* [Skapa en Salesforce Marketing Cloud-basanslutning med API:t för Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en källa för automatiserad marknadsföring med API:t för Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Anslut [!DNL Salesforce Marketing Cloud] till plattform med användargränssnittet

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce Marketing Cloud] till plattform med användargränssnittet:

* [Skapa en Salesforce Marketing Cloud-källanslutning i användargränssnittet](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Skapa ett dataflöde för en källanslutning för automatiserad marknadsföring i användargränssnittet](../../tutorials/ui/dataflow/marketing-automation.md)
