---
title: Översikt över SAP Hybris Source
description: Lär dig hur du ansluter SAP Hybris till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 32e2c13dcdbf2f13b4025354dfc50f5ccaf5f664
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# [!DNL SAP Hybris]

>[!NOTE]
>
>The [!DNL SAP Hybris] källan är i betaversion. Se [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

[[!DNL SAP Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), en molnbaserad e-handelsplattformslösning för B2B- och B2C-företag, ingår i SAP:s kundupplevelseportfölj. [[!DNL SAP] Prenumerationsfakturering](https://www.sap.com/products/financial-management/subscription-billing.html) är en produkt som ingår i portföljen och möjliggör en komplett hantering av prenumerationens livscykel med förenklade försäljnings- och betalningsupplevelser via standardiserade integreringar.

The [!DNL SAP Hybris] kan du importera kunder och kontaktinformation till plattformen från [[!DNL SAP] Prenumerationsfakturering](https://www.sap.com/products/financial-management/subscription-billing.html) API-slutpunkter för affärspartners nedan:

* [Kunder](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Kontakter](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Dessutom, om [!DNL SAP Hybris] körs för att hämta kunddata, [Kundkontaktsrelationer](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API anropas också för att hämta kundens kontaktinformation.

## IP-adress tillåtelselista {#ip-allow-list}

En lista med IP-adresser kan behöva läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Förutsättningar {#prerequisites}

Innan du kan ta med [!DNL SAP Hybris] data till Experience Platform måste du först se till att du har följande:

* A [!DNL SAP Subscription Billing] konto. Om du inte redan har ett giltigt faktureringskonto kontaktar du [!DNL SAP] kontoansvarig. Se [[!DNL SAP] Plattformskonfiguration](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) för mer information.

* [!DNL SAP] tjänstnyckel. The [!DNL SAP] kan du komma åt [!DNL SAP Subscription Billing] API via Experience Platform. [!DNL SAP Hybris] kräver följande:
   * Klient-ID
   * Klienthemlighet
   * URL. URL-mönstret ser ut så här: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Det här värdet används senare för att hämta värden för `region` och `tokenEndpoint` när du [Skapa basanslutning](../../tutorials/api/create/crm/sap-hybris.md#base-connection) med API:t eller när du [Koppla samman [!DNL SAP Hybris] konto](../../tutorials/ui/create/crm/sap-hybris.md#connect-account) via plattformsgränssnittet.

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

Dokumentationen nedan innehåller information om hur du ansluter [!DNL SAP Hybris] till Plattform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde som ger [!DNL SAP Hybris] data till plattformen med API:er](../../tutorials/api/create/crm/sap-hybris.md).
* [Koppla samman [!DNL SAP Hybris] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/crm/sap-hybris.md).
* [Skapa ett dataflöde för en CRM-källa med användargränssnittet](../../tutorials/ui/dataflow/crm.md)
