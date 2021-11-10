---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Översikt över JavaScript-biblioteket Adobe Privacy
topic-legacy: overview
description: Med Adobe Privacy JavaScript Library kan du hämta registrerade identiteter för användning i Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: 7f3a0594147a8cea292263f60aa45dc5ebb8484e
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# Översikt över JavaScript-biblioteket Adobe Privacy

Som personuppgiftsbiträde behandlar Adobe personuppgifter i enlighet med ditt företags tillstånd och instruktioner. Som personuppgiftsansvarig bestämmer du vilka personuppgifter Adobe behandlar och lagrar för din räkning. Beroende på vilken information du väljer att skicka via Adobe Experience Cloud lösningar kan Adobe lagra privat information som gäller sekretessregler som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA). Visa dokumentet på [sekretess i Adobe Experience Cloud](https://www.adobe.com/se/privacy/marketing-cloud.html) om du vill ha mer information om hur Experience Cloud lösningar samlar in privata data.

The **Adobe Privacy JavaScript Library** gör det möjligt för registeransvariga att automatisera hämtning av alla registrerade identiteter som genererats av [!DNL Experience Cloud] lösningar för en viss domän. Använda API:t från [Adobe Experience Platform Privacy Service](home.md)kan dessa identiteter sedan användas för att skapa begäran om åtkomst och radering av privata data som tillhör de registrerade.

>[!NOTE]
>
>The [!DNL Privacy JS Library] behöver oftast bara installeras på sekretessrelaterade sidor och behöver inte installeras på alla sidor på en webbplats eller domän.

## Funktioner

The [!DNL Privacy JS Library] innehåller flera funktioner för att hantera identiteter i [!DNL Privacy Service]. Dessa funktioner kan bara användas för att hantera identiteter som lagras i webbläsaren för en viss besökare. De kan inte användas för att skicka information till [!DNL Experience Cloud Central Service] direkt.

Följande tabell visar de olika funktionerna i biblioteket:

|  -funktion | Beskrivning |
| --- | --- |
| `retrieveIdentities` | Returnerar en array med matchande identiteter (`validIds`) som hämtades från [!DNL Privacy Service]samt en array med identiteter som inte hittades (`failedIds`). |
| `removeIdentities` | Tar bort varje matchande (giltig) identitet från webbläsaren. Returnerar en array med matchande identiteter (`validIds`), med varje identitet som innehåller `isDeletedClientSide` boolesk som anger om detta ID har tagits bort. |
| `retrieveThenRemoveIdentities` | Hämtar en array med matchande identiteter (`validIds`) och sedan tar bort dessa identiteter från webbläsaren. Funktionen liknar `removeIdentities`är det bäst att använda när den Adobe-lösning du använder kräver en åtkomstbegäran innan det går att ta bort den (till exempel när en unik identifierare måste hämtas innan den kan tas bort). |

>[!NOTE]
>
>`removeIdentities` och `retrieveThenRemoveIdentities` Ta bara bort identiteter från webbläsaren för specifika Adobe-lösningar som stöder dem. Adobe Audience Manager tar t.ex. inte bort de demdex-ID:n som lagras i cookies från tredje part, medan Adobe Target tar bort alla cookies som lagrar deras ID:n.

Eftersom alla tre funktionerna representerar asynkrona processer måste alla hämtade identiteter hanteras med återanrop eller löften.


## Installation

Börja använda [!DNL Privacy JS Library]måste du installera den på datorn på något av följande sätt:

* Installera med npm genom att köra följande kommando: `npm install @adobe/adobe-privacy`
* Ladda ned från [Experience Cloud GitHub-databas](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Du kan också installera biblioteket via ett taggtillägg i användargränssnittet för datainsamling. Se översikten på [Tillägget Adobe Privacy Tag](../tags/extensions/web/privacy/overview.md) för mer information.

## Instansiera [!DNL Privacy JS Library]

Alla program som använder [!DNL Privacy JS Library] måste skapa en ny `AdobePrivacy` -objekt, som måste konfigureras till en viss Adobe-lösning. En instans för Adobe Analytics skulle till exempel se ut ungefär så här:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

En fullständig lista över parametrar som stöds för olika Adobe-lösningar finns i bilagan om vilka som stöds [Konfigurationsparametrar för Adobe-lösningar](#adobe-solution-configuration-parameters).

## Kodexempel {#samples}

I följande kodexempel visas hur du använder [!DNL Privacy JS Library] för flera vanliga scenarier, förutsatt att du inte använder taggar.

### Hämta identiteter

I det här exemplet visas hur du hämtar en lista med identiteter från [!DNL Experience Cloud].

#### JavaScript

Följande kod definierar en funktion, `handleRetrievedIDs`, som används som återanrop eller löfte för att hantera identiteter som hämtas av `retrieveIdentities`.

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
| `failedIDs` | Ett JSON-objekt som innehåller alla ID:n som inte hämtades från [!DNL Privacy Service]eller på annat sätt inte kunde hittas. |

#### Resultat

Om koden körs utan fel `validIDs` innehåller en lista med hämtade identiteter.

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

Följande kod definierar en funktion, `handleRemovedIDs`, som används som återanrop eller löfte för att hantera identiteter som hämtas av `removeIdentities` när de har tagits bort från webbläsaren.

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
| `failedIDs` | Ett JSON-objekt som innehåller alla ID:n som inte hämtades från [!DNL Privacy Service]eller på annat sätt inte kunde hittas. |

#### Resultat

Om koden körs utan fel `validIDs` innehåller en lista med hämtade identiteter.

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

Genom att läsa det här dokumentet har du fått en introduktion till de viktigaste funktionerna i [!DNL Privacy JS Library]. När du har använt biblioteket för att hämta en lista över identiteter kan du använda dessa identiteter för att skapa dataåtkomst och ta bort begäranden till [!DNL Privacy Service] API. Se [API-guide för Privacy Service](api/overview.md) för mer information.

## Bilaga

Detta avsnitt innehåller ytterligare information om hur du använder [!DNL Privacy JS Library].

### Konfigurationsparametrar för Adobe-lösningar {#config-params}

Nedan följer en lista över godkända konfigurationsparametrar för Adobe-lösningar som stöds, som används när [instansiera ett AdobePrivacy-objekt](#instantiate-the-privacy-js-library).

**Alla lösningar**

| Parameter | Beskrivning |
| --- | --- |
| `key` | Ett unikt ID som identifierar användaren eller den registrerade. Den här egenskapen är avsedd att användas för dina egna interna spårningssyften och används inte av Adobe. |

**Adobe Analytics**

| Parameter | Beskrivning |
| --- | --- |
| `cookieDomainPeriods` | Antalet perioder i en domän som används för att spåra cookies (standardvärdet är `2`, t.ex. `.domain.com`). Definiera det inte här om du inte har angett det i JavaScript-webbfyren. |
| `dataCenter` | Datacentret för datainsamling i Adobe. Detta bör bara inkluderas om det anges i JavaScript-webbfyren. Möjliga värden är: <ul><li>`d1`: San Jose, datacenter</li><li>`d2`: Dallas datacenter</li></ul> |
| `reportSuite` | Det Report Suite-ID som anges i JavaScript-webbfyren (till exempel: `s_code.js` eller `dtm`). |
| `trackingServer` | En domän som inte är SSL-datainsamlingsdomän. Detta bör bara inkluderas om det anges i JavaScript-webbfyren. |
| `trackingServerSecure` | En SSL-datainsamlingsdomän. Detta bör bara inkluderas om det anges i JavaScript-webbfyren. |
| `visitorNamespace` | Det namnutrymme som används för att gruppera besökare. Detta bör bara inkluderas om det anges i JavaScript-webbfyren. |

**Adobe Audience Manager**

| Parameter | Beskrivning |
| --- | --- |
| `aamUUIDCookieName` | Namnet på cookien som innehåller det unika användar-ID som returnerats från Adobe Audience Manager. |

**Adobe Experience Cloud Identity Service (ECID)**

| Parameter | Beskrivning |
| --- | --- |
| `imsOrgID` | Ditt IMS-organisations-ID. |

**Adobe Target**

| Parameter | Beskrivning |
| --- | --- |
| `clientCode` | Klientkod som identifierar en klient i Adobe Target System. |
