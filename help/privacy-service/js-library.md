---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Adobe Privacy JavaScript Library Overview
description: Med Adobe Privacy JavaScript Library kan ni hämta registrerade identiteter för användning i Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 1%

---

# Adobe Privacy JavaScript Library - översikt

Som personuppgiftsbiträde behandlar Adobe personuppgifter i enlighet med ditt företags tillstånd och instruktioner. Som personuppgiftsansvarig avgör du vilka personuppgifter som Adobe behandlar och lagrar å dina vägnar. Beroende på vilken information du väljer att skicka via Adobe Experience Cloud-lösningar kan Adobe lagra privat information som gäller sekretessregler som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA). Mer information om hur Experience Cloud lösningar samlar in privata data finns i dokumentet om [sekretess i Adobe Experience Cloud](https://www.adobe.com/se/privacy/marketing-cloud.html).

JavaScript-biblioteket **för skydd av personuppgifter för** Adobe  gör det möjligt för personuppgiftsansvariga att automatisera hämtning av alla registrerade identiteter som genererats av [!DNL Experience Cloud]-lösningar för en specifik domän. Med hjälp av API:t från [Adobe Experience Platform Privacy Service](home.md) kan dessa identiteter sedan användas för att skapa åtkomst- och borttagningsbegäranden för privata data som tillhör de registrerade.

>[!NOTE]
>
>[!DNL Privacy JS Library] behöver normalt bara installeras på sekretessrelaterade sidor och behöver inte installeras på alla sidor på en webbplats eller domän.

## Funktioner

[!DNL Privacy JS Library] innehåller flera funktioner för att hantera identiteter i [!DNL Privacy Service]. Dessa funktioner kan bara användas för att hantera identiteter som lagras i webbläsaren för en viss besökare. De kan inte användas för att skicka information direkt till [!DNL Experience Cloud Central Service].

Följande tabell visar de olika funktionerna i biblioteket:

| Funktion | Beskrivning |
| --- | --- |
| `retrieveIdentities` | Returnerar en array med matchande identiteter (`validIds`) som hämtades från [!DNL Privacy Service], samt en array med identiteter som inte hittades (`failedIds`). |
| `removeIdentities` | Tar bort varje matchande (giltig) identitet från webbläsaren. Returnerar en matris med matchande identiteter (`validIds`), där varje identitet innehåller ett `isDeletedClientSide` booleskt värde som anger om detta ID har tagits bort. |
| `retrieveThenRemoveIdentities` | Hämtar en matris med matchande identiteter (`validIds`) och tar sedan bort dessa identiteter från webbläsaren. Även om den här funktionen liknar `removeIdentities`, är den bäst att använda när Adobe-lösningen som du använder kräver en åtkomstbegäran innan det går att ta bort den (till exempel när en unik identifierare måste hämtas innan den kan tas bort). |

>[!NOTE]
>
>`removeIdentities` och `retrieveThenRemoveIdentities` tar bara bort identiteter från webbläsaren för specifika Adobe-lösningar som stöder dem. Adobe Audience Manager tar t.ex. inte bort de demdex-ID:n som lagras i cookies från tredje part, medan Adobe Target tar bort alla cookies som lagrar deras ID:n.

Eftersom alla tre funktionerna representerar asynkrona processer måste alla hämtade identiteter hanteras med återanrop eller löften.


## Installation

Om du vill börja använda [!DNL Privacy JS Library] måste du installera det på datorn på något av följande sätt:

* Installera med npm genom att köra följande kommando: `npm install @adobe/adobe-privacy`
* Hämta från [Experience Cloud GitHub-databasen](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Du kan också installera biblioteket via ett taggtillägg. Mer information finns i översikten för taggtillägget [Adobe Privacy ](../tags/extensions/client/privacy/overview.md).

## Instansiera [!DNL Privacy JS Library]

Alla program som använder [!DNL Privacy JS Library] måste skapa en instans av ett nytt `AdobePrivacy`-objekt, som måste konfigureras till en viss Adobe-lösning. En instans för Adobe Analytics skulle till exempel se ut ungefär så här:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

En fullständig lista över parametrar som stöds för olika Adobe-lösningar finns i bilagan om [Adobe-lösningens konfigurationsparametrar](#adobe-solution-configuration-parameters) som stöds.

## Kodexempel {#samples}

I följande kodexempel visas hur du använder [!DNL Privacy JS Library] för flera vanliga scenarier, förutsatt att du inte använder taggar.

### Hämta identiteter

I det här exemplet visas hur du hämtar en lista med identiteter från [!DNL Experience Cloud].

#### JavaScript

I följande kod definieras en funktion, `handleRetrievedIDs`, som ska användas som ett återanrop eller löfte för att hantera identiteter som hämtats av `retrieveIdentities`.

```javascript
function handleRetrievedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.retrieveIdentities(handleRetrievedIDs);

// If using promises:
adobePrivacy.retrieveIdentities().then(handleRetrievedIDs);
```

| Variabel | Beskrivning |
| --- | --- |
| `validIds` | Ett JSON-objekt som innehåller alla ID:n som har hämtats. |
| `failedIDs` | Ett JSON-objekt som innehåller alla ID:n som inte hämtades från [!DNL Privacy Service], eller på annat sätt inte kunde hittas. |

#### Resultat

Om koden körs utan fel fylls `validIDs` i med en lista över hämtade identiteter.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543"
},
{
    "company": "adobe",
    "namespace": "gsurfer_id",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao"
}
```

### Ta bort identiteter

I det här exemplet visas hur du tar bort en lista med identiteter från webbläsaren.

#### JavaScript

I följande kod definieras en funktion, `handleRemovedIDs`, som ska användas som ett återanrop eller löfte att hantera identiteter som hämtats av `removeIdentities` efter att de har tagits bort från webbläsaren.

```javascript
function handleRemovedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.removeIdentities(handleRemovedIDs);

// If using promises:
adobePrivacy.removeIdentities().then(handleRemovedIDs)…
```

| Variabel | Beskrivning |
| --- | --- |
| `validIds` | Ett JSON-objekt som innehåller alla ID:n som har hämtats. |
| `failedIDs` | Ett JSON-objekt som innehåller alla ID:n som inte hämtades från [!DNL Privacy Service], eller på annat sätt inte kunde hittas. |

#### Resultat

Om koden körs utan fel fylls `validIDs` i med en lista över hämtade identiteter.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543",
    "isDeletedClientSide": false
},
{
    "company": "adobe",
    "namespace": "AMO",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao",
    "isDeletedClientSide": true
}
```

## Nästa steg

Genom att läsa det här dokumentet har du introducerats till kärnfunktionerna i [!DNL Privacy JS Library]. När du har använt biblioteket för att hämta en lista över identiteter kan du använda dessa identiteter för att skapa dataåtkomst och ta bort begäranden till API:t [!DNL Privacy Service]. Mer information finns i [Privacy Service-API-handboken](api/overview.md).

## Bilaga

Det här avsnittet innehåller ytterligare information om hur du använder [!DNL Privacy JS Library].

### Konfigurationsparametrar för Adobe-lösningar {#config-params}

Nedan följer en lista över godkända konfigurationsparametrar för Adobe-lösningar som stöds, som används när [ett AdobePrivacy-objekt instansieras](#instantiate-the-privacy-js-library).

**Alla lösningar**

| Parameter | Beskrivning |
| --- | --- |
| `key` | Ett unikt ID som identifierar användaren eller den registrerade. Den här egenskapen är avsedd att användas för dina egna interna spårningssyften och används inte av Adobe. |

**Adobe Analytics**

| Parameter | Beskrivning |
| --- | --- |
| `cookieDomainPeriods` | Antalet perioder i en domän som används för cookie-spårning (standardvärdet är `2`, t.ex. `.domain.com`). Definiera den inte här om du inte har angett det i webbfyren på JavaScript. |
| `dataCenter` | Datacentret för datainsamling i Adobe. Detta bör endast inkluderas om det anges i JavaScript webbfyr. Möjliga värden är: <ul><li>`d1`: datacenter i San Jose</li><li>`d2`: Dallas datacenter</li></ul> |
| `reportSuite` | Det Report Suite-ID som anges i JavaScript webbfyr (till exempel `s_code.js` eller `dtm`). |
| `trackingServer` | En domän för datainsamling som inte är SSL. Detta bör endast inkluderas om det anges i JavaScript webbfyr. |
| `trackingServerSecure` | En SSL-datainsamlingsdomän. Detta bör endast inkluderas om det anges i JavaScript webbfyr. |
| `visitorNamespace` | Det namnutrymme som används för att gruppera besökare. Detta bör endast inkluderas om det anges i JavaScript webbfyr. |

**Adobe Audience Manager**

| Parameter | Beskrivning |
| --- | --- |
| `aamUUIDCookieName` | Namn på cookie-filen från första part som innehåller det unika användar-ID som returnerats från Adobe Audience Manager. |

**Adobe Experience Cloud Identity Service (ECID)**

| Parameter | Beskrivning |
| --- | --- |
| `imsOrgID` | Ditt organisations-ID. |

**Adobe Target**

| Parameter | Beskrivning |
| --- | --- |
| `clientCode` | Klientkod som identifierar en klient i Adobe Target System. |
