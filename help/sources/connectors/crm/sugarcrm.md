---
title: Källöversikt för SugarCRM
description: Lär dig hur du ansluter SugarCRM till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badge: Beta
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# (Beta) [!DNL SugarCRM]

>[!NOTE]
>
>The [!DNL SugarCRM] källan är i betaversion. Se [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inhämtning av data från ett CRM-program från tredje part. Stöd för CRM-leverantörer innefattar [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) är ett CRM-system (customer relationship management). [!DNL SugarCRM]Funktionerna omfattar automatisering av säljstyrkan, marknadsföringskampanjer, kundsupport, samarbete, Mobile CRM, Social CRM och rapportering.

The [!DNL SugarCRM] kan du importera konton, kontakter och händelsedata från följande API-slutpunkter:

* [Konton](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Kontakter](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Händelser](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] använder lagervariabler som en autentiseringsmekanism för att kommunicera med [!DNL SugarCRM] Konto- och kontakt-API:er och [!DNL SugarCRM] Händelse-API.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Förutsättningar

Innan du kan skapa en [!DNL SugarCRM] måste du först kontrollera att du har följande:

* A [!DNL SugarMarket] konto. Du måste kontakta din [!DNL SugarCRM] kontohanteraren för att erhålla en giltig [!DNL SugarMarket] om du inte redan har ett konto.

* Ett unikt API-användarnamn och konto som är skilt från alla användarkonton som är kopplade till marknadsförings- eller försäljningsprocessen. Den här unika kombinationen av användarnamn och konto måste ha API-åtkomstbehörighet. Mer information om hur du skapar ett konto finns på [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) dokumentation.

## Anslut [!DNL SugarCRM Accounts & Contacts] till plattform

* [Skapa en källanslutning att hämta [!DNL SugarCRM Accounts & Contacts] data till plattformen med API:er](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Skapa en källanslutning att hämta [!DNL SugarCRM Accounts & Contacts] data till plattformen via användargränssnittet](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Skapa ett dataflöde för en CRM-källa med API:t för Flow Service](../../tutorials/api/collect/crm.md)


## Anslut [!DNL SugarCRM Events] till plattform

* [Skapa en källanslutning att hämta [!DNL SugarCRM Events] data till plattformen med API:er](../../tutorials/api/create/crm/sugarcrm-events.md).
* [Skapa en källanslutning att hämta [!DNL SugarCRM Events] data till plattformen via användargränssnittet](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Skapa ett dataflöde för en CRM-källanslutning i användargränssnittet](../../tutorials/ui/dataflow/crm.md)
