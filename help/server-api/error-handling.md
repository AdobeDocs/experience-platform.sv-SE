---
title: Felhantering
description: Lär dig mer om eventuella fel som kan uppstå när du utför API-begäranden till API:t för Adobe Experience Platform Edge Network Server.
exl-id: f6b8435c-b163-4046-b5fb-50a13a897637
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 1%

---

# Felhantering

## Översikt {#overview}

API-fel i API:t för Adobe Experience Platform Edge Network Server kan ha en rad olika orsaker, interna (Edge Network) eller externa (indata, konfiguration eller uppströms).

## Feltyper {#error-types}

| Fel | Typ | Beskrivning | Statuskod |
| --- | --- | --- | --- |
| `RequestProcessingError` | Intern | Allmänt fel som utfärdas av Adobe Experience Platform Edge Network vid oväntade omständigheter. | `500` |
| `InputError` | Extern | Inkluderar fel orsakade av felaktigt formaterade indata samt entitetsverifieringsfel. | `4xx` |
| `ConfigurationError` | Extern | Konfigurationsfel på serversidan. | `422` |
| `UpstreamError` | Extern | Kommunikationsfel med tjänster som ligger uppströms. | `207 Multi-Status` |

## Allvarlighetsgrad

Server-API-fel kan också delas upp efter allvarlighetsgrad:

* **Allvarliga fel** kommer att stoppa utsändningslinjen.
* **Icke-allvarliga fel** kan signalera en partiell bearbetning, samtidigt som behandlingen av begäranden kan fortsätta.
   * Om det finns någon ändrar den övergripande statuskoden för begäran till `207 Multi-Status`.

| Fel | Typ | Anmärkningar |
| --- | --- | --- |
| `RequestProcessingError` | Allvarligt | Kan inträffa när som helst under bearbetningen av begäran. |
| `InputError` | Allvarligt | Händer när begäran godkänns, innan den skickas uppströms. |
| `ConfigurationError` | Allvarligt | Händer när begäran godkänns, innan den skickas uppströms. |
| `UpstreamError` | Icke-dödlig | Kommunikationsfel med tjänster som ligger uppströms. |

### Allvarliga fel {#fatal-errors}

Allvarliga fel stoppar bearbetningen av begäran och orsakar att en svarsstatus som inte är 2xx returneras. Kolla in [feltyper](#error-types) för att se den förväntade statuskoden, som motsvarar varje feltyp.

Felen kommer att åtföljas av ett svarsorgan som innehåller ett felobjekt. I det här fallet innehåller svarstexten en problemdetalj, som definieras av [RFC 7807 Probleminformation för HTTP-API:er](https://tools.ietf.org/html/rfc7807).

Den returnerade innehållstypen är `application/problem+json` medietyp. Det här svaret innehåller maskinläsbar information om felet, om det finns någon. Probleminformationen innehåller en URI-typ.

Alla felobjekt har en `type`, `status`, `title`, `detail` och `report` meddelandeegenskaper så att API-klienten kan avgöra vad problemet är.

| Egenskap | Typ | Beskrivning |
| -------- | ------ | ----------- |
| `type` | Sträng | En URI-referens (RFC3986) som identifierar problemtypen efter formatet `https://ns.adobe.com/aep/errors/<ERROR-CODE>`. |
| `status` | Nummer | HTTP-statuskoden som servern genererat för den här förekomsten av problemet. |
| `title` | Sträng | En kort, läsbar sammanfattning av problemtypen. |
| `detail` | Sträng | En kort, läsbar beskrivning av problemtypen. |
| `report` | Objekt | En karta över ytterligare egenskaper som är till hjälp vid felsökning, t.ex. begärande-ID eller organisation-ID. I vissa fall kan den innehålla data som är specifika för det aktuella felet, till exempel en lista med valideringsfel. |

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0104-422",
   "status":422,
   "title":"Unprocessable entity",
   "detail":"Invalid request (report attached). Please check your input and try again.",
   "report":{
      "errors":[
         "Allowed Adobe version is 1.0 for standard 'Adobe' at index 0",
         "Allowed IAB version is 2.0 for standard 'IAB TCF' at index 1",
         "IAB consent string value must not be empty for standard 'IAB TCF' at index 1"
      ],
      "requestId":"0f8821e5-ed1a-4301-b445-5f336fb50ee8",
      "orgId":"53A16ACB5CC1D3760A495C99@AdobeOrg"
   }
}
```

### Icke-allvarliga fel {#non-fatal-errors}

Icke-allvarliga fel kan delas upp ytterligare i:

* Fel: Problem som uppstod när begäran bearbetades, men som inte ledde till att hela begäran avvisades (t.ex. ett icke-kritiskt fel uppströms).
* Varningar: Meddelanden från tjänster som ligger uppströms kan signalera att en partiell bearbetning av begäran har utförts.

När icke-allvarliga fel (exklusive varningar) påträffas [!DNL Server API] ändrar svarsstatus till `207 Multi-Status`.

Varningar är å andra sidan i huvudsak informativa, eftersom de i allmänhet utgör ett potentiellt övergående tillstånd som inte till fullo påverkade begäran. Ett exempel här är en delvis profilläsning i segmenteringsmotorn. I så fall påverkas noggrannheten i viss utsträckning, men funktionaliteten är fortfarande tillgänglig.

Icke-allvarliga fel visas i _Probleminformation_ -format, men är inbäddade direkt i Edge gatewayens standardsvar, som är av typen `application/json`.

```json
{
  "requestId": "72eaa048-207e-4dde-bf16-0cb2b21336d5",
  "handle": [
  ],
  "errors": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0201-503",
      "status": 503,
      "title": "The 'com.adobe.experience.platform.ode' service is temporarily unable to serve this request. Please try again later."
    }
  ],
  "warnings": [
    {
      "type": "https://ns.adobe.com/aep/errors/EXEG-0204-200",
      "status": 200,
      "title": "A warning occurred while calling the 'com.adobe.audiencemanager' service for this request.",
      "report": {
        "cause": {
          "message": "Cannot read related customer for device id: ...",
          "code": 202
        }
      }
    }
  ]
}
```

## Hantering `4xx` och `5xx` Svar

| Felkod | Beskrivning |
|---|---|
| `4xx Bad Request` | Mest `4xx` fel, som 400, 403, 404, får inte provas igen för klientens räkning, förutom `429`. Detta är klientfel och kommer inte att lyckas. Klienten måste åtgärda felet innan den försöker utföra begäran igen. |
| `429 Too Many Requests` | `429` HTTP-svarskoden indikerar att Adobe Experience Platform Edge Network eller en tjänst i uppströmmen hastighetsbegränsar förfrågningarna. I det här fallet måste anroparen i ett sådant fall respektera `Retry-After` svarshuvud. Alla svar som returneras måste innehålla HTTP-svarskoden med en domänspecifik felkod. |
| `500 Internal Server Error` | `500` fel är generiska fel som fångar upp alla. `500` fel får inte provas igen, förutom `502` och `503`. Förmedlare måste svara med en `500` och kan svara med en generisk felkod/ett allmänt felmeddelande eller en mer domänspecifik felkod/ett mer domänspecifikt felmeddelande. |
| `502 Bad Gateway` | Anger att Adobe Experience Platform Edge Network fick ett ogiltigt svar från överordnade servrar. Detta kan inträffa på grund av nätverksproblem mellan servrar. Det temporära nätverksproblemet kan lösas och därför kan ett nytt försök åtgärda problemet, så att mottagare av `502` fel kan göra om begäran efter en stund. |
| `503 Service Unavailable` | Felkoden anger att tjänsten inte är tillgänglig för tillfället. Detta kan inträffa under underhållsperioder. Mottagare av `503` fel kan göra ett nytt försök att utföra begäran, men måste respektera `Retry-After` header. |
| `504 Gateway Timeout` | Anger att tidsgränsen för Adobe Experience Platform Edge Network-begäran till de överordnade servrarna har överskridits. Detta kan bero på nätverksproblem mellan servrar, DNS-problem eller andra nätverksproblem. De temporära nätverksproblemen kan lösas efter en stund och ett nytt försök kan lösa problemet. |
