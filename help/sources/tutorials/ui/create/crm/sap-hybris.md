---
title: Skapa en källanslutning för SAP Hybris i användargränssnittet
description: Lär dig hur du skapar en källanslutning för SAP Hybris med hjälp av Adobe Experience Platform-gränssnittet.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 2c029eb48fba8f3c92bf5a8b92973eb413128078
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 1%

---

# Skapa en [!DNL SAP Hybris] källanslutning i användargränssnittet

>[!NOTE]
>
>The [!DNL SAP Hybris] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

I följande självstudiekurs får du hjälp med att skapa en [!DNL SAP Hybris] källanslutning som ska hämta [[!DNL SAP] Prenumerationsfakturering](https://www.sap.com/products/financial-management/subscription-billing.html) kontakter och kunddata med Adobe Experience Platform användargränssnitt.

## Komma igång {#getting-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL SAP Hybris] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter {#gather-credentials}

För att kunna ansluta [!DNL SAP Hybris] till Experience Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Klient-ID | Värdet för `clientId` från tjänstnyckeln. |
| Klienthemlighet | Värdet för `clientSecret` från tjänstnyckeln. |
| Tokenslutpunkt | Värdet för `url` från tjänstnyckeln kommer den att likna `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Län | Datacentrets plats. Regionen finns i `url` och har ett värde som liknar `eu10` eller `us10`. Om `url` är `https://eu10.revenue.cloud.sap/api` du kommer att behöva `eu10`. |

Mer information finns i [[!DNL SAP Hybris] dokumentation](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### Skapa ett plattformsschema {#create-platform-schema}

Innan du skapar en [!DNL SAP Hybris] måste du också se till att du först skapar ett Experience Platform-schema som du kan använda för källan. Se självstudiekursen om [skapa ett plattformsschema](../../../../../xdm/schema/composition.md) om du vill ha omfattande anvisningar om hur du skapar ett schema.

Expandera följande avsnitt för att visa ett exempelschema.

+++ Visa schemaexempel

```
{
  "_extconndev": {
    "addresses": [
      {
        "addressUUID": "{ADDRESS_UUID}",
        "city": "Burnaby",
        "country": "Canada",
        "email": "chandni@acme.com",
        "houseNumber": "27",
        "isDefault": false,
        "phone": "123-456-7890",
        "postalCode": "V3J 1X9",
        "state": "British Columbia",
        "street": "Beresford"
      }
    ],
    "changedAt": "1687204041",
    "changedBy": "vero@acme.com",
    "contactNumber": "123-456-7980",
    "corporateInfo": {
      "company": "acme"
    },
    "createAt": "1687204041",
    "createdBy": "vero@acme.com",
    "customReferences": [
      {
        "id": "Sample value",
        "typeCode": "Sample value"
      }
    ],
    "customerNumber": "Sample value",
    "customerType": "Sample value",
    "defaultAddress": {
      "addressUUID": "Sample value",
      "city": "North Vancouver",
      "country": "Canada",
      "email": "chandni@acme.come",
      "houseNumber": "34",
      "isDefault": false,
      "phone": "123-456-7890",
      "postalCode": "V7H 2P1",
      "state": "British Columbia",
      "street": "Maple"
    },
    "externalObjectReferences": [
      {
        "externalId": "{EXTERNAL_ID}",
        "externalIdTypeCode": "{EXTERNAL_ID_TYPE_CODE}",
        "externalSystemId": "{EXTERNAL_SYSTEM_ID}"
      }
    ],
    "markets": [
      {
        "active": false,
        "country": "USA",
        "currency": "USD",
        "marketId": "Sample value",
        "priceinfo": {
          "incoterms": "{INCO_TERMS}",
          "incotermsLocation": "{INCO_TERMS_LOCATION}",
          "priceGroup": "{PRICE_GROUP}",
          "priceListType": "{PRICE_LIST_TYPE}"
        },
        "salesArea": {
          "distributionChannel": "{DISTRIBUTION_CHANNEL}",
          "division": "{DIVISION}",
          "salesOrganization": "{SALES_ORGANIZATION}"
        }
      }
    ],
    "personalInfo": {
      "firstName": "Chandni",
      "lastName": "Kaur"
    }
  },
  "_id": "/uri-reference",
  "_repo": {
    "createDate": "2004-10-23T12:00:00-06:00",
    "modifyDate": "2004-10-23T12:00:00-06:00"
  },
  "createdByBatchID": "/uri-reference",
  "modifiedByBatchID": "/uri-reference",
  "personID": "{PERSON_ID}",
  "repositoryCreatedBy": "kevin@acme.com",
  "repositoryLastModifiedBy": "kevin@acme.com"
}
```

+++

## Koppla samman [!DNL SAP Hybris] konto {#connect-account}

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *CRM* kategori, välj **[!UICONTROL SAP Hybris]** och sedan markera **[!UICONTROL Add data]**.

![Skärmbild för plattformsgränssnitt för katalog med SAP Hybris-kort](../../../../images/tutorials/create/crm/sap-hybris-subscription-billing-customers-and-contacts/catalog-card.png)

The **[!UICONTROL Connect SAP Hybris account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto {#existing-account}

Om du vill använda ett befintligt konto väljer du [!DNL SAP Hybris] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![Skärmbild för användargränssnittet för plattformen som används för att ansluta SAP Hybris-kontot till ett befintligt konto](../../../../images/tutorials/create/crm/sap-hybris-subscription-billing-customers-and-contacts/existing.png)

### Nytt konto {#new-account}

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och dina uppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Skärmbild för användargränssnittet för plattformen för att ansluta SAP Hybris-kontot med ett nytt konto](../../../../images/tutorials/create/crm/sap-hybris-subscription-billing-customers-and-contacts/new.png)

### Markera data {#select-data}

Slutligen måste du välja den objekttyp som du vill importera till plattformen.

| Objekttyp | Beskrivning |
| --- | --- |
| `Customers` | Enheter som har prenumerationer. |
| `Contacts` | Kontaktuppgifter för kunder. |

>[!BEGINTABS]

>[!TAB Kunder]

Välj **[!UICONTROL Customers]** som objekttyp och sedan markera **[!UICONTROL Next]**.

![Skärmbild av användargränssnittet för SAP Hybris som visar konfigurationen med alternativet Kunder valt](../../../../images/tutorials/create/crm/sap-hybris-subscription-billing-customers-and-contacts/configuration-customers.png)

>[!TAB Kontakter]

Om du vill importera kontaktdata väljer du **[!UICONTROL Contacts]** som objekttyp och sedan markera **[!UICONTROL Next]**.

![Skärmbild för användargränssnittet för SAP Hybris visar konfiguration med alternativet Kontakter valt](../../../../images/tutorials/create/crm/sap-hybris-subscription-billing-customers-and-contacts/configuration-contacts.png)

>[!ENDTABS]

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL SAP Hybris] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta CRM-data till plattformen](../../dataflow/crm.md).

## Ytterligare resurser {#additional-resources}

I avsnitten nedan finns ytterligare resurser som du kan använda när du använder [!DNL SAP Hybris] källa.

### Mappning {#mapping}

Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](../../../../../data-prep/ui/mapping.md).

Mappningskonfigurationerna för dataflödet varierar beroende på schemat och vilken objekttyp du väljer att importera.

>[!BEGINTABS]

>[!TAB Kunder]

För kunddata [!DNL SAP Hybris] använder [kunder](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) och [kundrelationer](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) slutpunkter för [!DNL SAP Business Partners] API för att hämta data

Följande är ett exempel på mappningskonfigurationer för [!DNL SAP Hybris] dataflöde för kunddata:

| Målfält | Beskrivning |
| --- | --- |
| `customerNumber` | Kundens nummer. |
| `corporateInfo` | Kundens nummer. |
| `customerType` | Kundtypen. |
| `createdAt` | En tidsstämpel som anger när kunden skapades. |
| `changedAt` | En tidsstämpel som anger när kunden senast uppdaterades. |
| `markets[*].country` | Kundmarknaderna, hämtade som ett arrayobjekt. |
| `addresses[*].email` | E-postmeddelanden som är kopplade till kundens flera adresser, hämtade som ett arrayobjekt. |
| `addresses[*].city` | Städer som är kopplade till kundens flera adresser, hämtade som ett arrayobjekt. |
| `addresses[*].addressUUID` | ID:n som är kopplade till kundens flera adresser, hämtade som ett arrayobjekt. |
| `externalObjectReferences[*].externalSystemId` | Ytterligare data, hämtade som ett arrayobjekt. |
| `externalObjectReferences[*].externalId` | Ytterligare data, hämtade som ett arrayobjekt. |
| `customReferences[*].id` | Ytterligare data, hämtade som ett arrayobjekt. |
| `customReferences[*].typeCode` | Ytterligare data, hämtade som ett arrayobjekt. |

![Mappningssteget för källarbetsflödet.](../../../../images/tutorials/create/crm/sap-hybris-subscription-billing-customers-and-contacts//mapping-customers.png)

>[!TAB Kontakter]

För kontaktdata [!DNL SAP Hybris] använder [kontakter](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) slutpunkt för [!DNL SAP Business Partners] API för att hämta data.

Följande är ett exempel på mappningskonfigurationer för [!DNL SAP Hybris] dataflöde för kontaktdata:

| Målfält | Beskrivning |
| --- | --- |
| `contactNumber` | Kontaktens nummer. |
| `createdAt` | En tidsstämpel som anger när kontakten skapades. |
| `changedAt` | En tidsstämpel som anger när kontakten senast uppdaterades. |
| `personalInfo.lastName` | Kontaktens efternamn. |
| `personalInfo.firstName` | Kontaktens förnamn. |
| `externalObjectReferences[*].externalSystemId` | Ytterligare data, hämtade som ett arrayobjekt. |
| `externalObjectReferences[*].externalId` | Ytterligare data, hämtade som ett arrayobjekt. |
| `externalObjectReferences[*].externalIdTypeCode` | Ytterligare data, hämtade som ett arrayobjekt. |

![Mappningssteget för källarbetsflödet.](../../../../images/tutorials/create/crm/sap-hybris-subscription-billing-customers-and-contacts/mapping-contacts.png)

>[!ENDTABS]

