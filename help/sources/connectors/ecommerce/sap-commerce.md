---
title: SAP Commerce Source - översikt
description: Lär dig hur du ansluter SAP Commerce till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>Källan [!DNL SAP Commerce] är i betaversion. Mer information om hur du använder betatecknade källor finns i [källöversikten](../../home.md#terms-and-conditions).

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), en molnbaserad e-handelsplattform för B2B- och B2C-företag, ingår i SAP:s kundupplevelseportfölj. [[!DNL SAP] Prenumerationsfakturering](https://www.sap.com/products/financial-management/subscription-billing.html) är en produkt som ingår i portföljen och möjliggör en fullständig hantering av prenumerationens livscykel med förenklade försäljnings- och betalningsupplevelser via standardiserade integreringar.

Med källan [!DNL SAP Commerce] kan du importera kunder och kontaktinformation till plattformen från [[!DNL SAP] API-slutpunkterna för prenumerationsfakturering](https://www.sap.com/products/financial-management/subscription-billing.html) för affärspartners nedan:

* [Kunder](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Kontakter](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Om [!DNL SAP Commerce] dessutom körs för att hämta kunddata anropas API:t [Kundkontakter](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) även för att hämta kundens kontaktinformation.

## IP-adress tillåtelselista {#ip-allow-list}

En lista med IP-adresser kan behöva läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Förhandskrav {#prerequisites}

Innan du kan överföra dina [!DNL SAP Commerce]-data till Experience Platform måste du först se till att du har följande:

* Ett [!DNL SAP Subscription Billing]-konto. Om du inte redan har ett giltigt faktureringskonto kontaktar du kontohanteraren för [!DNL SAP]. Mer information finns i dokumentet [[!DNL SAP] Plattformskonfiguration](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf).

* [!DNL SAP] tjänstnyckel. Med tjänstnyckeln [!DNL SAP] kan du komma åt API:t för [!DNL SAP Subscription Billing] via Experience Platform. [!DNL SAP Commerce] kräver följande:
   * Klient-ID
   * Klienthemlighet
   * URL. URL-mönstret är följande: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Det här värdet används senare för att hämta värden för `region` och `tokenEndpoint` när du [skapar basanslutningen](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) med API:t eller när du [ansluter ditt [!DNL SAP Commerce] konto](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) via plattformsgränssnittet.

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

Dokumentationen nedan innehåller information om hur du ansluter [!DNL SAP Commerce] till plattformen med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde för att hämta [!DNL SAP Commerce] data till plattformen med API:er](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Anslut ditt [!DNL SAP Commerce] konto till Experience Platform med användargränssnittet](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Skapa ett dataflöde för en källa med användargränssnittet](../../tutorials/ui/dataflow/ecommerce.md)
