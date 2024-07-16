---
title: SugarCRM Source - översikt
description: Lär dig hur du ansluter SugarCRM till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# [!DNL SugarCRM]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inhämtning av data från ett CRM-program från tredje part. Stöd för CRM-providers omfattar [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) är ett CRM-system (customer relationship management). [!DNL SugarCRM]-funktionaliteten omfattar säljkraftsautomatisering, marknadsföringskampanjer, kundsupport, samarbete, Mobile CRM, Social CRM och rapportering.

Med källan [!DNL SugarCRM] kan du importera konton, kontakter och händelsedata från följande API-slutpunkter:

* [Konton](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Kontakter](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Händelser](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] använder innehavartoken som autentiseringsmekanism för att kommunicera med [!DNL SugarCRM] konto- och kontakt-API:erna och [!DNL SugarCRM] events API.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Förhandskrav

Innan du kan skapa en [!DNL SugarCRM]-källanslutning måste du se till att du har följande:

* Ett [!DNL SugarMarket]-konto. Du måste kontakta din kontohanterare för [!DNL SugarCRM] för att få ett giltigt [!DNL SugarMarket]-konto om du inte redan har ett.

* Ett unikt API-användarnamn och konto som är skilt från alla användarkonton som är kopplade till marknadsförings- eller försäljningsprocessen. Den här unika kombinationen av användarnamn och konto måste ha API-åtkomstbehörighet. Mer information om hur du konfigurerar ett konto finns i dokumentationen för [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro).

## Anslut [!DNL SugarCRM Accounts & Contacts] till plattformen

* [Skapa en källanslutning för att hämta [!DNL SugarCRM Accounts & Contacts] data till plattformen med API:er](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Skapa en källanslutning för att hämta [!DNL SugarCRM Accounts & Contacts] data till plattformen med användargränssnittet](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)


## Anslut [!DNL SugarCRM Events] till plattformen

* [Skapa en källanslutning för att hämta [!DNL SugarCRM Events] data till plattformen med API:er](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Skapa en källanslutning för att hämta [!DNL SugarCRM Events] data till plattformen med användargränssnittet](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Skapa ett dataflöde för en CRM-källanslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)
