---
title: Google Data Layer Extension
description: Läs mer om taggtillägget Google Client Data Layer i Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: c61afdc2c3df98a0ef815d7cb034ba2907c52908
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---

# Google Data Layer-tillägg

Med Google datalagertillägg kan du använda ett Google-datalager i taggimplementeringen. Tillägget kan användas fristående eller samtidigt med Google-lösningar och med Google öppen källkod [Hjälpbibliotek för datalager](https://github.com/google/data-layer-helper).

Hjälpbiblioteket har liknande händelsestyrda funktioner som Adobe Client Data Layer (ACDL). Dataelementen, reglerna och åtgärderna i Google Data Layer-tillägget har liknande funktioner som i [ACDL-tillägg](../client-data-layer/overview.md).

## Installation

Om du vill installera tillägget går du till tilläggskatalogen i användargränssnittet för datainsamling och väljer **[!UICONTROL Google Data Layer]**.

När tillägget har installerats skapas eller används ett datalager vid varje inläsning av Adobe Experience Platform Tags-biblioteket.

## Tilläggsvy

Tilläggskonfigurationen kan användas för att definiera namnet på datalagret som tillägget använder. Om det inte finns något datalager med det konfigurerade namnet när Adobe Experience Platform Tags läses in skapas ett lager av tillägget.

Standardnamnet för datalagret är Google standardnamn `dataLayer`.

>[!NOTE]
>
>Det spelar ingen roll om Google- eller Adobe-kod läses in först och skapar datalagret. Båda systemen fungerar på samma sätt - skapa datalagret om det inte finns eller använd det befintliga datalagret.

## Händelser

>[!NOTE]
>
>Ordet _event_ överbelastas när ett händelsestyrt datalager används i Adobe Experience Platform Tags. _Händelser_ kan vara:
> - Adobe Experience Platform Tags-händelser (Bibliotek inläst och så vidare).
> - JavaScript-händelser.
> - Data överförs till datalagret med _event_ nyckelord.

Tillägget ger dig möjlighet att lyssna efter ändringar i datalagret.

>[!NOTE]
>
>Det är viktigt att förstå hur _event_ nyckelord när data skickas till ett Google-datalager, på samma sätt som datalagret Adobe Client. The _event_ nyckelordet ändrar beteendet för Google datalager och därför det här tillägget.\
> Läs Google dokumentation eller gör en undersökning om du är osäker.

### Google Event Types

Google har stöd för två metoder för push-händelser: Google Tag Manager med `push()` och Google Analytics 4 med `gtag()` -metod.

Tilläggsversioner för Google datalager före 1.2.1 stöds endast händelser som skapats av `push()`, vilket visas i kodexemplen på den här sidan.

Versioner 1.2.1 och senare supporthändelser som skapats med `gtag()`.  Detta är valfritt och kan aktiveras i dialogrutan för tilläggskonfiguration.

Mer information om `push()` och `gtag()` händelser, se [Google-dokumentation](https://developers.google.com/analytics/devguides/collection/ga4/reference/events?client_type=gtag).  Information finns också i dialogrutorna för konfiguration och regel för tillägget.

### Lyssna efter alla penslar till datalagret

Om du väljer det här alternativet avlyssnar händelseavlyssnaren alla ändringar som görs i datalagret.

### Lyssna efter push-meddelanden exklusive händelser

Om du väljer det här alternativet avlyssnar händelseavlyssnaren alla datapush-meddelanden till datalagret, med undantag för händelser.

Följande exempel på push-händelser spåras av avlyssnaren:

```js
dataLayer.push({"data":"something"})
```

Följande exempel på push-händelser spåras inte av avlyssnaren:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Lyssna efter alla händelser

Om du väljer det här alternativet avlyssnar händelseavlyssnaren alla händelser som skickas till datalagret.

Följande exempel på push-händelser spåras av avlyssnaren:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

Följande exempel på push-händelse spåras inte av avlyssnaren:

```js
dataLayer.push({"data":"something"})
```

### Lyssna efter specifik händelse

Om du anger en händelse spårar händelseavlyssnaren alla händelser som matchar en viss sträng.

Ange till exempel `myEvent` när du använder den här konfigurationen spåras endast följande push-händelse i avlyssnaren:

```js
dataLayer.push({"event":"myEvent"})
```

En (ECMAScript/JavaScript)-regex kan användas för att matcha händelsenamn.

Om du till exempel anger &#39;myEvent\d&#39; spåras `myEvent` med en siffra (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Instruktioner

### Överför till datalager {#push-to-data-layer}

Tillägget ger dig två åtgärder för att överföra JSON till datalagret, ett fritextfält för att manuellt skapa JSON som ska skjutas upp och från version 1.2.0, en dialogruta för nyckelvärdesmultifält.

#### JSON för fritext

Åtgärden för fri text gör det möjligt att använda dataelement direkt i JSON. I JSON-redigeraren ska dataelement refereras med procentnotation. Till exempel: `%dataElementName%`.

```json
{
  "page": {
    "url": "%url%",
    "previous_url": "%previous_url%",
    "concatenated_values": "static string %dataElement%"
  }
}
```

#### Multifält för nyckelvärde

Den nyare multifältsdialogrutan för nyckelvärden är ett användarvänligt gränssnitt där en push-funktion kan konfigureras utan att JSON behöver skrivas manuellt.

### Google DL Återställ till beräknat tillstånd

Tillägget ger dig en åtgärd för att återställa datalagret. Om datalagret används i en regel som bearbetar en ändring i ett Google-datalager, återställs det till det beräknade läget för datalagret när regeln utlöstes. Om åtgärden används i en regel som inte bearbetar en ändring i ett Google-datalager töms datalagret av åtgärden.

## Dataelement

Det angivna dataelementet kan användas under körningen av en regel som utlöses av en ändring i Google datalager (push-händelse) eller i en icke-relaterad regel som Inläst i bibliotek. I det tidigare fallet returnerar dataelementet ett värde som tagits från det beräknade läget vid tidpunkten för datalagrets ändring. I det senare fallet används det beräknade läget vid tidpunkten för regelkörningen.

Med en växlingsväxling kan du välja om dataelementet ska returnera värden från hela det beräknade läget eller endast från händelseinformation (om det används i en regel som utlöses av en datalagerändring).

Dataelementet kan därför returnera:

- Tomt fält: datalagrets beräknade läge.
- Fält med nyckel (t.ex. page.previous_url i exemplet ovan): värdet på nyckeln i händelseobjektet eller det beräknade läget.

## Ytterligare information

Tilläggets dialogrutor för dataelement och händelser innehåller detaljerad användarinformation och exempel.

Ytterligare allmän information finns i [README för projekt](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
