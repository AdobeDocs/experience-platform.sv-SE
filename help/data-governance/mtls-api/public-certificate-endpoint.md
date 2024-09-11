---
title: Slutpunkt för offentligt certifikat
description: Lär dig hur du hämtar offentliga certifikat med slutpunkten /public-certificate i MTLS Service API.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: 754044621cdaf1445f809bceaa3e865261eb16f0
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 1%

---

# Slutpunkt för offentligt certifikat

I den här guiden beskrivs hur du använder slutpunkten för det offentliga certifikatet för att på ett säkert sätt hämta offentliga certifikat för din organisations Adobe-program. Det innehåller ett exempel på API-anrop och detaljerade anvisningar som hjälper utvecklare att autentisera och verifiera datautbyten.

## Komma igång

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information som du behöver känna till för att kunna ringa anrop till API:t, inklusive nödvändiga rubriker och hur du läser exempel-API-anrop.

## API-sökvägar {#paths}

Följande information är de viktigaste API-sökvägarna som du behöver för att använda API:t för mTLS-tjänsten. Detta inkluderar plattformens gateway-URL, bassökvägen för API:t och ett exempel på en fullständig sökväg för att hämta ett offentligt certifikat.

- PLATFORM Gateway-URL: `https://platform.adobe.io/`
- Bassökväg för detta API: `/data/core/mtls`
- Exempel på en fullständig sökväg: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Hämta dina offentliga certifikat {#list}

Du kan hämta offentliga certifikat för alla Adobe-program i din organisation genom att göra en GET-förfrågan till slutpunkten `/v1/certificate/public-certificate`.

**API-format**

```http
GET /v1/certificate/public-certificate
```

Följande valfria frågeparametrar kan användas när du hämtar dina offentliga certifikat.

| Frågeparameter | Beskrivning | Exempel |
| --------------- | ----------- | ------- |
| `page` | Anger vilken sida som resultatet av din begäran ska börja från. | `page=5` |
| `limit` | Det maximala antalet offentliga certifikat som du vill hämta per sida. | `limit=20` |

{style="table-layout:auto"}

**Begäran**

Ett exempel på en begäran om att returnera offentliga certifikat som är kopplade till din organisation visas i det infällbara avsnittet nedan.

+++Exempelbegäran

```shell
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**Svar**

Ett godkänt svar returnerar HTTP-status 200 och visar de offentliga certifikaten för din organisation.

+++Ett exempel på lyckat svar

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `certCommonName` | Certifikatets vanliga namn (CN), som vanligtvis representerar namnet eller identiteten på den server eller enhet som certifikatet utfärdas till. |
| `publicCertificate` | Det faktiska offentliga certifikatet i ett strängformat, som används för att autentisera och kryptera kommunikation. |
| `expiryDate` | Det datum och den tidpunkt då det offentliga certifikatet upphör att gälla, formaterat i ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Nästa steg

När du har läst den här guiden får du nu veta hur du hämtar dina offentliga certifikat med Adobe Experience Platform API. Mer information om hur du hanterar kunddata för att säkerställa efterlevnad av regler och organisationsprofiler finns i [Datastyrningsöversikten](../home.md).

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->
