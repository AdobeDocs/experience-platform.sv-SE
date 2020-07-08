---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Direktinmatningsvalidering
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 1%

---


# Direktinmatningsvalidering

Med direktuppspelningsintag kan du överföra data till Adobe Experience Platform med direktuppspelningsslutpunkter i realtid. API:er för direktuppspelning stöder två valideringslägen - synkron och asynkron.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
- [Direktuppspelningsinmatning](../streaming-ingestion/overview.md): En av de metoder som data kan skickas med till Experience Platform.

### Läser exempel-API-anrop

I den här självstudiekursen finns exempel-API-anrop som visar hur du formaterar dina begäranden. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Samla in värden för obligatoriska rubriker

För att kunna ringa anrop till Platform API:er måste du först slutföra [autentiseringssjälvstudiekursen](../../tutorials/authentication.md). När du slutför självstudiekursen för autentisering visas värdena för var och en av de obligatoriska rubrikerna i alla API-anrop för Experience Platform, vilket visas nedan:

- Behörighet: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform, inklusive de som tillhör schemaregistret, är isolerade till specifika virtuella sandlådor. Alla förfrågningar till Platform API:er kräver en rubrik som anger namnet på sandlådan som åtgärden ska utföras i:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Mer information om sandlådor i Platform finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden som innehåller en nyttolast (POST, PUT, PATCH) kräver ytterligare en rubrik:

- Innehållstyp: `application/json`

### Valideringstäckning

Streaming Validation Service omfattar validering inom följande områden:
- Intervall
- Närvaro
- Enum
- Mönster
- Typ
- Format

## Synkron validering

Synkron validering är en valideringsmetod som ger omedelbar feedback om varför ett intag misslyckades. Vid fel tas dock de poster som inte godkänns vid valideringen bort och kan inte skickas längre fram i kedjan. Därför bör synkron validering endast användas under utvecklingsprocessen. När synkron validering utförs informeras anroparna om både resultatet av XDM-valideringen och, om det misslyckas, orsaken till felet.

Synkron validering är inte aktiverat som standard. Om du vill aktivera den måste du ange den valfria frågeparametern `synchronousValidation=true` när du gör API-anrop. Dessutom är synkron validering för närvarande bara tillgängligt om strömslutpunkten finns i datacentret VA7.

Om ett meddelande misslyckas under synkron validering kommer meddelandet inte att skrivas till utdatakön, vilket ger omedelbar feedback till användarna.

**API-format**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Värdet `id` för den direktuppspelningsanslutning som skapades tidigare. |

**Begäran**

Skicka följande begäran om att importera data till datainmatningen med synkron validering:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | JSON-delen av data som du vill importera. |

**Svar**

När synkron validering är aktiverat innehåller ett lyckat svar alla påträffade valideringsfel i nyttolasten:

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

Svaret ovan visar hur många schemaöverträdelser som har påträffats och vilka dessa överträdelser var. Det här svaret anger till exempel att nycklarna `workEmail` och `person` inte definierades i schemat och därför inte är tillåtna. Det flaggar också värdet för `_id` som felaktigt eftersom schemat förväntade ett `string`värde, men ett värde `long` infogades i stället. Observera att när fem fel har påträffats kommer valideringstjänsten att **sluta** bearbeta meddelandet. Andra meddelanden kommer dock att fortsätta att analyseras.

## Asynkron validering

Asynkron validering är en valideringsmetod som inte ger omedelbar feedback. I stället skickas data till en misslyckad batch i Data Lake för att förhindra dataförlust. Data som inte fungerar kan hämtas senare för ytterligare analys och repriser. Denna metod bör användas i produktionen. Om inget annat anges används direktuppspelningsuppläsning i asynkront valideringsläge.

**API-format**

```http
POST /collection/{CONNECTION_ID}
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{CONNECTION_ID}` | Värdet `id` för den direktuppspelningsanslutning som skapades tidigare. |

**Begäran**

Skicka följande begäran om att importera data till datainmatningen med asynkron validering:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beskrivning |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | JSON-delen av data som du vill importera. |

>[!NOTE]
>
>Ingen extra frågeparameter krävs eftersom asynkron validering är aktiverat som standard.

**Svar**

När asynkron validering är aktiverat returnerar ett lyckat svar följande:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

Observera hur svaret anger att synkron validering har hoppats över, eftersom det inte uttryckligen har begärts.

## Bilaga

Det här avsnittet innehåller information om vad de olika statuskoderna innebär för svar på inhämtning av data.

### Statuskoder

| Statuskod | Vad det betyder |
| ----------- | ------------- |
| 200 | Lyckades. För synkron validering innebär det att valideringskontrollerna har slutförts. För asynkron validering innebär det att meddelandet endast har tagits emot. Användarna kan ta reda på den slutliga meddelandestatusen genom att observera datauppsättningen. |
| 400 | Fel. Det är något fel på din begäran. Ett felmeddelande med mer information tas emot från Streaming Validation Services. |
| 401 | Fel. Din begäran är inte auktoriserad - du måste begära med en innehavartoken. Mer information om hur du begär åtkomst finns i den här [självstudiekursen](../../tutorials/authentication.md) eller i det här [blogginlägget](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Fel. Det finns ett internt systemfel. |
| 501 | Fel. Det innebär att synkron validering **inte** stöds för den här platsen. |
| 503 | Fel. Tjänsten är inte tillgänglig just nu. Kunderna bör försöka igen minst tre gånger med en exponentiell strategi för bakåtjustering. |