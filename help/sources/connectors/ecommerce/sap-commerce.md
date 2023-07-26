---
title: Översikt över SAP Commerce Source
description: Lär dig hur du ansluter SAP Commerce till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
source-git-commit: a848ea11e388678ade780fd81ef3ff6a3477b741
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>The [!DNL SAP Commerce] källan är i betaversion. Se [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), en molnbaserad e-handelsplattformslösning för B2B- och B2C-företag, ingår i SAP:s kundupplevelseportfölj. [[!DNL SAP] Prenumerationsfakturering](https://www.sap.com/products/financial-management/subscription-billing.html) är en produkt som ingår i portföljen och möjliggör en komplett hantering av prenumerationens livscykel med förenklade försäljnings- och betalningsupplevelser via standardiserade integreringar.

The [!DNL SAP Commerce] kan du importera kunder och kontaktinformation till plattformen från [[!DNL SAP] Prenumerationsfakturering](https://www.sap.com/products/financial-management/subscription-billing.html) API-slutpunkter för affärspartners nedan:

* [Kunder](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Kontakter](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Dessutom, om [!DNL SAP Commerce] körs för att hämta kunddata, [Kundkontaktsrelationer](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API anropas också för att hämta kundens kontaktinformation.

## IP-adress tillåtelselista {#ip-allow-list}

En lista med IP-adresser kan behöva läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Förutsättningar {#prerequisites}

Innan du kan ta med [!DNL SAP Commerce] data till Experience Platform måste du först se till att du har följande:

* A [!DNL SAP Subscription Billing] konto. Om du inte redan har ett giltigt faktureringskonto kontaktar du [!DNL SAP] kontoansvarig. Se [[!DNL SAP] Plattformskonfiguration](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) om du vill ha mer information.

* [!DNL SAP] tjänstnyckel. The [!DNL SAP] kan du komma åt [!DNL SAP Subscription Billing] API via Experience Platform. [!DNL SAP Commerce] kräver följande:
   * Klient-ID
   * Klienthemlighet
   * URL. URL-mönstret ser ut så här: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Det här värdet används senare för att hämta värden för `region` och `tokenEndpoint` när du [Skapa basanslutning](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) med API:t eller när du [Koppla samman [!DNL SAP Commerce] konto](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) via plattformsgränssnittet.

+++Välj för att se ett exempel på tjänstnyckeln

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## Nästa steg

Dokumentationen nedan innehåller information om hur du ansluter [!DNL SAP Commerce] till Plattform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde som ger [!DNL SAP Commerce] data till plattformen med API:er](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Koppla samman [!DNL SAP Commerce] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Skapa ett dataflöde för en källa med användargränssnittet](../../tutorials/ui/dataflow/ecommerce.md)
