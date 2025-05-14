---
title: Slutpunkt för offentligt certifikat
description: Lär dig hur du hämtar offentliga certifikat med slutpunkten /public-certificate i MTLS Service API.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Slutpunkt för offentligt certifikat

>[!NOTE]
>
>Adobe har inte längre stöd för statisk hämtning av publika mTLS-certifikat. Använd detta API för att hämta giltiga certifikat för dina integreringar. Automatisk hämtning krävs nu för att undvika avbrott i tjänsten.

Den här guiden förklarar hur du använder slutpunkten för det offentliga certifikatet för att på ett säkert sätt hämta offentliga certifikat för organisationens Adobe-program. Det innehåller ett exempel på API-anrop och detaljerade anvisningar som hjälper utvecklare att autentisera och verifiera datautbyten.

## Komma igång

Innan du fortsätter bör du läsa [kom igång-guiden](./getting-started.md) för att få viktig information om nödvändiga huvuden och hur du tolkar exempel-API-anrop.

## API-sökvägar {#paths}

Följande information är de viktigaste API-sökvägarna som du behöver för att använda API:t för mTLS-tjänsten. Detta inkluderar plattformens gateway-URL, bassökvägen för API:t och ett exempel på en fullständig sökväg för att hämta ett offentligt certifikat.

- PLATFORM Gateway-URL: `https://platform.adobe.io/`
- Bassökväg för detta API: `/data/core/mtls`
- Exempel på en fullständig sökväg: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Hämta dina offentliga certifikat {#list}

Gör en GET-begäran till slutpunkten `/v1/certificate/public-certificate` om du vill hämta offentliga certifikat för något av organisationens Adobe-program.

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

## Automatisering av certifikatets livscykel {#certificate-lifecycle-automation}

Adobe automatiserar livscykeln för offentliga mTLS-certifikat för att säkerställa kontinuitet och minska antalet avbrott i tjänsten.

- Certifikat utfärdas igen 60 dagar innan de upphör att gälla.
- Certifikat återkallas 30 dagar innan de upphör att gälla.

>[!NOTE]
>
>Dessa tidslinjer kommer att förkortas över tid i enlighet med [CA/B Forum-riktlinjerna](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), som syftar till att minska certifikatets livstid till högst 47 dagar.

Du måste uppdatera integreringarna så att de stöder automatisk hämtning via API:t. Förlita dig inte på manuella certifikathämtningar eller statiska kopior eftersom dessa kan resultera i utgångna eller återkallade certifikat.

## Nästa steg

När du har hämtat dina offentliga certifikat med API måste du uppdatera integreringarna så att slutpunkten anropas regelbundet innan certifikaten upphör att gälla. Om du vill testa det här samtalet interaktivt går du till [MTLS API-referenssidan](https://developer.adobe.com/experience-platform-apis/references/mtls-service/). Mer information om certifikatbaserade integreringar finns i [Datakrypteringen i Adobe Experience Platform-översikten](../../landing/governance-privacy-security/encryption.md) eller [Datastyrningsöversikten](../home.md).
