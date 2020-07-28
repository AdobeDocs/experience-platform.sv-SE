---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över JavaScript-biblioteket Adobe Privacy
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 3%

---


# Översikt över JavaScript-biblioteket Adobe Privacy

Som personuppgiftsbiträde behandlar Adobe personuppgifter i enlighet med ditt företags tillstånd och instruktioner. Som personuppgiftsansvarig bestämmer du vilka personuppgifter Adobe behandlar och lagrar för din räkning. Beroende på vilken information du väljer att skicka via Adobe Experience Cloud lösningar kan Adobe lagra privat information som är tillämplig på sekretessbestämmelser som [!DNL General Data Protection Regulation] (GDPR) och [!DNL California Consumer Privacy Act] (CCPA). Mer information om hur Experience Cloud lösningar samlar in privata data finns i dokumentet om [sekretess i Adobe Experience Cloud](https://www.adobe.com/privacy/marketing-cloud.html) .

Med **Adobe Privacy JavaScript Library** kan personuppgiftsansvariga automatisera hämtningen av alla registrerade identiteter som genererats av [!DNL Experience Cloud] lösningar för en viss domän. Med hjälp av API:t från [Adobe Experience Platform Privacy Servicen](home.md)kan dessa identiteter sedan användas för att skapa åtkomst- och borttagningsbegäranden för privata data som tillhör de registrerade.

>[!NOTE]
>
>Vanligtvis behöver den bara installeras på sekretessrelaterade sidor och behöver inte installeras på alla sidor på en webbplats eller en domän. [!DNL Privacy JS Library]

## Funktioner

I [!DNL Privacy JS Library] finns flera funktioner för att hantera identiteter i [!DNL Privacy Service]. Dessa funktioner kan bara användas för att hantera identiteter som lagras i webbläsaren för en viss besökare. De kan inte användas för att skicka in information direkt till [!DNL Experience Cloud Central Service] .

Följande tabell visar de olika funktionerna i biblioteket:

|  -funktion | Beskrivning |
| --- | --- |
| `retrieveIdentities` | Returnerar en array med matchande identiteter (`validIds`) som hämtades från [!DNL Privacy Service]samt en array med identiteter som inte hittades (`failedIds`). |
| `removeIdentities` | Tar bort varje matchande (giltig) identitet från webbläsaren. Returnerar en array med matchande identiteter (`validIds`), där varje identitet innehåller ett `isDeleteClientSide` booleskt värde som anger om detta ID har tagits bort. |
| `retrieveThenRemoveIdentities` | Hämtar en array med matchande identiteter (`validIds`) och tar sedan bort dessa identiteter från webbläsaren. Även om den här funktionen liknar `removeIdentities`den är bäst att använda när Adobe-lösningen som du använder kräver en åtkomstbegäran innan det går att ta bort den (till exempel när en unik identifierare måste hämtas innan den kan tas bort). |

>[!NOTE]
>
>`removeIdentities` och ta `retrieveThenRemoveIdentities` bara bort identiteter från webbläsaren för specifika Adobe-lösningar som stöder dem. Adobe Audience Manager tar t.ex. inte bort de demdex-ID:n som lagras i cookies från tredje part, medan Adobe Target tar bort alla cookies som lagrar deras ID:n.

Eftersom alla tre funktionerna representerar asynkrona processer måste alla hämtade identiteter hanteras med återanrop eller löften.


## Installation

Om du vill börja använda [!DNL Privacy JS Library]programmet måste du installera det på datorn på något av följande sätt:

* Installera med npm genom att köra följande kommando: `npm install @adobe/adobe-privacy`
* Använd Adobe Launch Extension under namnet `AdobePrivacy`
* Hämta från [https://github.com/Adobe-Marketing-Cloud/adobe-privacy](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instansiera [!DNL Privacy JS Library]

Alla program som använder [!DNL Privacy JS Library] måste skapa ett nytt `AdobePrivacy` objekt som måste konfigureras till en viss Adobe-lösning. En instans för Adobe Analytics skulle till exempel se ut ungefär så här:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

En fullständig lista över parametrar som stöds för olika Adobe-lösningar finns i bilagan om konfigurationsparametrar [för](#adobe-solution-configuration-parameters)Adobe-lösningar som stöds.

## Kodexempel

I följande kodexempel visas hur du använder [!DNL Privacy JS Library] för flera vanliga scenarier, förutsatt att du inte använder [!DNL Launch] eller DTM.

### Hämta identiteter

I det här exemplet visas hur du hämtar en lista med identiteter från [!DNL Experience Cloud].

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
| `failedIDs` | Ett JSON-objekt som innehåller alla ID:n som inte hämtades från [!DNL Privacy Service]eller på annat sätt inte kunde hittas. |

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
| `failedIDs` | Ett JSON-objekt som innehåller alla ID:n som inte hämtades från [!DNL Privacy Service]eller på annat sätt inte kunde hittas. |

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

Genom att läsa det här dokumentet har du lagts till i de centrala funktionerna i [!DNL Privacy JS Library]. När du har använt biblioteket för att hämta en lista över identiteter kan du använda dessa identiteter för att skapa dataåtkomst och ta bort begäranden till [!DNL Privacy Service] API. Mer information finns i [Privacy Servicens utvecklarhandbok](api/getting-started.md) .

## Bilaga

Detta avsnitt innehåller ytterligare information om hur du använder [!DNL Privacy JS Library].

### Konfigurationsparametrar för Adobe-lösningar

Nedan följer en lista över godkända konfigurationsparametrar för Adobe-lösningar som stöds, som används vid [instansiering av ett AdobePrivacy-objekt](#instantiate-the-privacy-js-library).

**Adobe Analytics**

| Parameter | Beskrivning |
| --- | --- |
| `cookieDomainPeriods` | Antalet perioder i en domän för cookie-spårning (standard är 2). |
| `dataCenter` | Datacenter för datainsamling i Adobe. Detta bör bara inkluderas om det anges i JavaScript-webbfyren. Möjliga värden är: <ul><li>&quot;d1&quot;: San Jose datacenter.</li><li>&quot;d2&quot;: Dallas datacenter.</li></ul> |
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