---
title: Azure-databaser
description: Läs mer om de nödvändiga stegen som krävs för att ansluta Azure-databaser till Experience Platform.
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: 16de2879f5f5da533ce640d93871571f03aa74c2
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# [!DNL Azure Databricks]

[!DNL Azure Databricks] är en molnbaserad plattform som utformats för dataanalys, maskininlärning och AI. Du kan använda [!DNL Databricks] för att integrera med [!DNL Azure] och tillhandahålla en helhetsmiljö för att bygga, distribuera och hantera datalösningar i stor skala.

Du kan använda källan [!DNL Databricks] för att ansluta ditt konto och importera dina [!DNL Databricks]-data till Adobe Experience Platform.

## Förhandskrav

Slutför de nödvändiga stegen för att ansluta ditt [!DNL Databricks]-konto till Experience Platform.

### Hämta autentiseringsuppgifter för behållaren

Hämta dina inloggningsuppgifter för Experience Platform [!DNL Azure Blob Storage] så att ditt [!DNL Databricks]-konto kan komma åt det senare.

Om du vill hämta dina autentiseringsuppgifter skickar du en GET-begäran till `/credentials`-slutpunkten för API:t [!DNL Connectors].

**API-format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**Begäran**

Följande begäran hämtar autentiseringsuppgifterna för din Experience Platform [!DNL Azure Blob Storage].

+++Exempel på visningsbegäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Svar**

Ett lyckat svar ger dina autentiseringsuppgifter (`containerName`, `SASToken`, `storageAccountName`) för senare användning i [!DNL Apache Spark]-konfigurationen för [!DNL Databricks].

+++Visa svarsexempel

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `containerName` | Namnet på [!DNL Azure Blob Storage]-behållaren. Du kommer att använda det här värdet senare när du slutför din [!DNL Apache Spark]-konfiguration för [!DNL Databricks]. |
| `SASToken` | Underskriftstoken för delad åtkomst för din [!DNL Azure Blob Storage]. Strängen innehåller all information som krävs för att godkänna en begäran. |
| `storageAccountName` | Namnet på ditt lagringskonto. |
| `SASUri` | Den delade åtkomstsignaturens URI för din [!DNL Azure Blob Storage]. Den här strängen är en kombination av URI:n till [!DNL Azure Blob Storage] som du autentiseras mot och dess motsvarande SAS-token. |
| `expiryDate` | Det datum då din SAS-token upphör att gälla. Du måste uppdatera din token före förfallodatumet för att kunna fortsätta använda den i ditt program för att överföra data till [!DNL Azure Blob Storage]. Om du inte uppdaterar din token manuellt före det angivna förfallodatumet uppdateras den automatiskt och en ny token skapas när GET-inloggningsanropet utförs. |

+++

### Uppdatera dina autentiseringsuppgifter

>[!NOTE]
>
>Dina befintliga autentiseringsuppgifter återkallas när du uppdaterar dina autentiseringsuppgifter. Därför måste du uppdatera [!DNL Spark]-konfigurationerna så att de stämmer när du uppdaterar dina inloggningsuppgifter för lagring. Annars misslyckas dataflödet.

Uppdatera dina autentiseringsuppgifter genom att göra en POST-begäran och inkludera `action=refresh` som en frågeparameter.

**API-format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**Begäran**

Följande begäran uppdaterar autentiseringsuppgifterna för din [!DNL Azure Blob Storage].

+++Exempel på visningsbegäran

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Svar**

Ett lyckat svar returnerar dina nya autentiseringsuppgifter.

+++Visa svarsexempel

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### Konfigurera åtkomst till din [!DNL Azure Blob Storage]

>[!IMPORTANT]
>
>* Om klustret har avslutats startas det om automatiskt under en flödeskörning. Du måste dock se till att klustret är aktivt när du skapar en anslutning eller ett dataflöde. Dessutom måste klustret vara aktivt om du utför åtgärder som dataförhandsgranskning eller utforskning, eftersom dessa åtgärder inte kan föreslå automatisk omstart av ett avslutat kluster.
>
>* [!DNL Azure]-behållaren innehåller en mapp med namnet `adobe-managed-staging`. **Ändra inte** den här mappen om du vill att data ska kunna hämtas utan synliga skarvar.


Därefter måste du se till att ditt [!DNL Databricks]-kluster har åtkomst till Experience Platform [!DNL Azure Blob Storage]-kontot. Om du gör det kan du använda [!DNL Azure Blob Storage] som en tillfällig plats för att skriva [!DNL delta lake] tabelldata.

Du måste konfigurera en SAS-token i klustret [!DNL Databricks] som en del av din [!DNL Apache Spark]-konfiguration för att kunna ge åtkomst.

I [!DNL Databricks]-gränssnittet väljer du **[!DNL Advanced options]** och anger sedan följande i indatarutan [!DNL Spark config].

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| Egenskap | Beskrivning |
| --- | --- |
| Behållarnamn | Namnet på behållaren. Du kan hämta det här värdet genom att hämta dina [!DNL Azure Blob Storage]-autentiseringsuppgifter. |
| Lagringskonto | Namnet på ditt lagringskonto. Du kan hämta det här värdet genom att hämta dina [!DNL Azure Blob Storage]-autentiseringsuppgifter. |
| SAS-token | Underskriftstoken för delad åtkomst för din [!DNL Azure Blob Storage]. Du kan hämta det här värdet genom att hämta dina [!DNL Azure Blob Storage]-autentiseringsuppgifter. |

![Användargränssnittet för databaser på Azure.](../../images/tutorials/create/databricks/databricks-ui.png)

## Anslut [!DNL Databricks] till Experience Platform med API:er

Nu när du har slutfört de nödvändiga stegen kan du nu gå vidare till guiden om att [ansluta ditt [!DNL Databricks] konto till Experience Platform med API:t](../../tutorials/api/create/databases/databricks.md).
