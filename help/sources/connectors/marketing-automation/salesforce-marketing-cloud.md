---
solution: Experience Platform
title: Salesforce Marketing Cloud Source - översikt
description: Lär dig hur du ansluter Salesforce Marketing Cloud till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: a32d0d7ed7d18454099d2b55b3f6809cfbcd9b62
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]-källan kommer att bli inaktuell i slutet av maj 2025.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform stöder inmatning av data från externa automatiseringssystem. Stöd för leverantörer av automatiserad marknadsföring inkluderar [!DNL Salesforce Marketing Cloud].

## Förhandskrav

Innan du kan ansluta [!DNL Salesforce Marketing Cloud]-källan till plattformen måste du se till att följande **behörighetsområden** har tilldelats din kombination av [!DNL Salesforce Marketing Cloud] klient-ID och klienthemlighet:

* `campaign_read`
* `list_and_subscribers_read`

Du kan begära omfång genom att anropa `v2/userinfo`-resursen för API:t [!DNL Salesforce Marketing Cloud]. I dokumentet [[!DNL Salesforce Marketing Cloud] Behörighetsintervall för API-integrering](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) finns mer information om hur du begär och jämför omfattningar.

Mer information om omfattningar inklusive en lista över deras relaterade behörigheter och beteenden finns i det här [[!DNL Salesforce Marketing Cloud] REST API-dokumentet](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Inläsning av anpassade objekt stöds för närvarande inte av källintegreringen [!DNL Salesforce Marketing Cloud].

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Anslut [!DNL Salesforce Marketing Cloud] till plattformen med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce Marketing Cloud] till plattformen med API:er:

* [Skapa en Salesforce Marketing Cloud base-anslutning med API:t för Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en källa för automatiserad marknadsföring med API:t för Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Anslut [!DNL Salesforce Marketing Cloud] till plattformen med användargränssnittet

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce Marketing Cloud] till plattformen med användargränssnittet:

* [Skapa en Salesforce Marketing Cloud-källanslutning i användargränssnittet](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Skapa ett dataflöde för en källanslutning för automatiserad marknadsföring i användargränssnittet](../../tutorials/ui/dataflow/marketing-automation.md)
