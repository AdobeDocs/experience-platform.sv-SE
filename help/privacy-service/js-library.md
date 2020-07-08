---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över JavaScript-biblioteket för Adobes sekretess
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 3%

---


# Översikt över JavaScript-biblioteket för Adobes sekretess

Som personuppgiftsbiträde behandlar Adobe personuppgifter i enlighet med ditt företags tillstånd och instruktioner. Som personuppgiftsansvarig bestämmer du vilka personuppgifter Adobe behandlar och lagrar för din räkning. Beroende på vilken information du väljer att skicka via Adobe Experience Cloud-lösningar kan Adobe lagra privat information som är tillämplig på sekretessbestämmelser som Allmänna dataskyddsförordningen (GDPR) och California Consumer Privacy Act (CCPA). Mer information om hur Experience Cloud lösningar samlar in privata data finns i dokumentet om [sekretess i Adobe Experience Cloud](https://www.adobe.com/privacy/marketing-cloud.html) .

Med **Adobe Privacy JavaScript Library** kan personuppgiftsansvariga automatisera hämtningen av alla registrerade identiteter som genererats av Experience Cloud-lösningar för en viss domän. Med hjälp av API:t från [Adobe Experience Platform Privacy Servicen](home.md)kan dessa identiteter sedan användas för att skapa åtkomst- och borttagningsbegäranden för privata data som tillhör de registrerade.

>[!NOTE]
>
>JS-biblioteket för sekretess behöver normalt bara installeras på sekretessrelaterade sidor och behöver inte installeras på alla sidor på en webbplats eller en domän.

## Funktioner

JS-biblioteket för sekretess innehåller flera funktioner för att hantera identiteter i Privacy Service. Dessa funktioner kan bara användas för att hantera identiteter som lagras i webbläsaren för en viss besökare. De kan inte användas för att skicka information direkt till Experience Cloud Centraltjänst.

Följande tabell visar de olika funktionerna i biblioteket:

|  -funktion | Beskrivning |
| --- | --- |
| `retrieveIdentities` | Returnerar en array med matchande identiteter (`validIds`) som har hämtats från Privacy Servicen samt en array med identiteter som inte hittades (`failedIds`). |
| `removeIdentities` | Tar bort varje matchande (giltig) identitet från webbläsaren. Returnerar en array med matchande identiteter (`validIds`), där varje identitet innehåller ett `isDeleteClientSide` booleskt värde som anger om detta ID har tagits bort. |
| `retrieveThenRemoveIdentities` | Hämtar en array med matchande identiteter (`validIds`) och tar sedan bort dessa identiteter från webbläsaren. Även om den här funktionen liknar `removeIdentities`den är bäst att använda när den Adobe-lösning du använder kräver en åtkomstbegäran innan det går att ta bort den (till exempel när en unik identifierare måste hämtas innan den kan tas bort). |

>[!NOTE]
>
>`removeIdentities` och ta `retrieveThenRemoveIdentities` bara bort identiteter från webbläsaren för specifika Adobe-lösningar som stöder dem. Adobe Audience Manager tar t.ex. inte bort de demdex-ID:n som lagras i cookies från tredje part, medan Adobe Target tar bort alla cookies som lagrar deras ID:n.

Eftersom alla tre funktionerna representerar asynkrona processer måste alla hämtade identiteter hanteras med återanrop eller löften.


## Installation

Om du vill börja använda JS-biblioteket för sekretess måste du installera det på datorn på något av följande sätt:

* Installera med npm genom att köra följande kommando: `npm install @adobe/adobe-privacy`
* Använd Adobe Launch Extension under namnet `AdobePrivacy`
* Hämta från [https://github.com/Adobe-Marketing-Cloud/adobe-privacy](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instansiera JS-biblioteket för sekretess

Alla program som använder JS-biblioteket för sekretess måste initiera ett nytt `AdobePrivacy` objekt, som måste konfigureras till en viss Adobe-lösning. En instans för Adobe Analytics ser till exempel ut ungefär så här:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

En fullständig lista över parametrar som stöds för olika Adobe-lösningar finns i bilagan om [Adobe-lösningens konfigurationsparametrar](#adobe-solution-configuration-parameters)som stöds.

## Kodexempel

I följande kodexempel visas hur du använder JS-biblioteket för sekretess för flera vanliga scenarier, förutsatt att du inte använder Launch eller DTM.

### Hämta identiteter

I det här exemplet visas hur du hämtar en lista med identiteter från Experience Cloud.

#### JavaScript

I följande kod definieras en funktion `handleRetrievedIDs`som ska användas som ett återanrop eller löfte för att hantera de identiteter som hämtas av `retrieveIdentities`.

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
| `failedIDs` | Ett JSON-objekt som innehåller alla ID:n som inte hämtades från Privacy Servicen, eller som på annat sätt inte kunde hittas. |

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

I följande kod definieras en funktion `handleRemovedIDs`som ska användas som ett återanrop eller löfte för att hantera identiteter som hämtas av `removeIdentities` efter att de har tagits bort från webbläsaren.

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
| `failedIDs` | Ett JSON-objekt som innehåller alla ID:n som inte hämtades från Privacy Servicen, eller som på annat sätt inte kunde hittas. |

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

Genom att läsa det här dokumentet har du lagts till i de viktigaste funktionerna i Privacy JS Library. När du har använt biblioteket för att hämta en lista över identiteter kan du använda dessa identiteter för att skapa dataåtkomst och ta bort begäranden till Privacy Service-API:t. Mer information finns i [Privacy Servicens utvecklarhandbok](api/getting-started.md) .

## Bilaga

Det här avsnittet innehåller ytterligare information om hur du använder JS-biblioteket för sekretess.

### Adobe Solution configuration parameters

Nedan följer en lista över godkända konfigurationsparametrar för de Adobe-lösningar som stöds, som används när ett AdobePrivacy-objekt [](#instantiate-the-privacy-js-library)instansieras.

**Adobe Analytics**

| Parameter | Beskrivning |
| --- | --- |
| `cookieDomainPeriods` | Antalet perioder i en domän för cookie-spårning (standard är 2). |
| `dataCenter` | Datacenter för datainsamling från Adobe. Detta bör bara inkluderas om det anges i JavaScript-webbfyren. Möjliga värden är: <ul><li>&quot;d1&quot;: San Jose datacenter.</li><li>&quot;d2&quot;: Dallas datacenter.</li></ul> |
| `reportSuite` | Rapportera Suite-ID enligt inställningarna i JavaScript-webbfyren (till exempel &quot;s_code.js&quot; eller &quot;dtm&quot;). |
| `trackingServer` | Domän för datainsamling (inte SSL). Detta bör bara inkluderas om det anges i JavaScript-webbfyren. |
| `trackingServerSecure` | Domän för datainsamling (SSL). Detta bör bara inkluderas om det anges i JavaScript-webbfyren. |
| `visitorNamespace` | Namnutrymme som används för att gruppera besökare. Detta bör bara inkluderas om det anges i JavaScript-webbfyren. |

**Adobe Target**

| Parameter | Beskrivning |
| --- | --- |
| `clientCode` | Klientkod som identifierar en klient i Adobe Target System. |

**Adobe Audience Manager**

| Parameter | Beskrivning |
| --- | --- |
| `aamUUIDCookieName` | Namnet på den cookie som innehåller det unika användar-ID som returnerats från Adobe Audience Manager. |

**Adobe ID Service (ECID)**

| Parameter | Beskrivning |
| --- | --- |
| `imsOrgID` | Ditt IMS-organisations-ID. |