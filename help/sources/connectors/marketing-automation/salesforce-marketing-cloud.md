---
solution: Experience Platform
title: Salesforce Marketing Cloud Source - översikt
description: Lär dig hur du ansluter Salesforce Marketing Cloud till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-04-29T00:00:00Z
source-git-commit: ce96dbc64845fddb40ebee709828c56d51a6c6ba
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]-källan kommer att bli inaktuell i januari 2026. En ny källa kommer att släppas senare i år som ett alternativ. När den nya källan har släppts måste du planera migreringen till den nya källan genom att skapa nya kontoanslutningar och dataflöden före utgången av januari 2026.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från externa automatiseringssystem. Stöd för leverantörer av automatiserad marknadsföring inkluderar [!DNL Salesforce Marketing Cloud].

## Förhandskrav

Innan du kan ansluta din [!DNL Salesforce Marketing Cloud]-källa till Experience Platform måste du se till att följande **behörighetsomfattningar** har tilldelats din [!DNL Salesforce Marketing Cloud]-klient-ID och kombination av klienthemlighet:

* `campaign_read`
* `list_and_subscribers_read`

Du kan begära omfång genom att anropa `v2/userinfo`-resursen för API:t [!DNL Salesforce Marketing Cloud]. I dokumentet [[!DNL Salesforce Marketing Cloud] Behörighetsintervall för API-integrering](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) finns mer information om hur du begär och jämför omfattningar.

Mer information om omfattningar inklusive en lista över deras relaterade behörigheter och beteenden finns i det här [[!DNL Salesforce Marketing Cloud] REST API-dokumentet](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Inläsning av anpassade objekt stöds för närvarande inte av källintegreringen [!DNL Salesforce Marketing Cloud].

## IP-adress tillåtelselista

Du måste lägga till regionspecifika IP-adresser i tillåtelselista innan du kan ansluta dina källor till Experience Platform. Mer information finns i guiden om att [tillåtslista IP-adresser för att ansluta till Experience Platform](../../ip-address-allow-list.md).

>[!WARNING]
>
>Om du inte lägger till de nödvändiga IP-adresserna i tillåtelselista kommer ditt [!DNL Salesforce Marketing Cloud]-konto inte att ansluta till Experience Platform.

## Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce Marketing Cloud] till Experience Platform med API:er:

* [Skapa en Salesforce Marketing Cloud-basanslutning med API:t för Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Utforska datatabeller med API:t för Flow Service](../../tutorials/api/explore/tabular.md)
* [Skapa ett dataflöde för en källa för automatiserad marknadsföring med API:t för Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform med användargränssnittet

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Salesforce Marketing Cloud] till Experience Platform med användargränssnittet:

* [Skapa en källanslutning till Salesforce Marketing Cloud i användargränssnittet](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Skapa ett dataflöde för en källanslutning för automatiserad marknadsföring i användargränssnittet](../../tutorials/ui/dataflow/marketing-automation.md)
