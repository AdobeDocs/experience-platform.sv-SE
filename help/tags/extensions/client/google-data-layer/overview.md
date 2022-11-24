---
title: Google Data Layer Extension
description: Läs mer om taggtillägget Google Client Data Layer i Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---

# Google Data Layer-tillägg (beta)

>[!IMPORTANT]
>
>Tillägget är för närvarande i betaversion och har inte testats fullständigt i produktionen.

Med Google datalagertillägg kan du använda ett Google-datalager i taggimplementeringen. Tillägget kan användas fristående eller samtidigt med Google-lösningar och med Google öppen källkod [Hjälpbibliotek för datalager](https://github.com/google/data-layer-helper).

Hjälpbiblioteket har liknande händelsestyrda funktioner som Adobe Client Data Dayer (ACDL). Dataelementen, reglerna och åtgärderna i Google-datalagrets tillägg har liknande funktionalitet som i [ACDL-tillägg](../client-data-layer/overview.md).

## Löptid

Version 1.0.x av tillägget är en betaversion. Utbyggnaden har inte testats fullt ut i produktionen.

## Installation

Om du vill installera tillägget går du till tilläggskatalogen i användargränssnittet för Experience Platform eller datainsamlingen och väljer **Google datalager**.

När tillägget har installerats skapas eller används ett datalager varje gång som taggbiblioteket läses in på webbplatsen.

## Tilläggsvy

När tillägget konfigureras (antingen när tillägget installeras eller genom att välja **[!UICONTROL Configure]** från tilläggskatalogen) måste du definiera namnet på datalagret som tillägget använder. Om det inte finns något datalager med det konfigurerade namnet när biblioteket läses in skapas ett lager i stället.

>[!NOTE]
>
>Det spelar ingen roll om Google- eller Adobe-kod läses in först och skapar datalagret. Båda systemen skapar datalagret om det inte finns något, eller använder det befintliga datalagret.

Som standard använder datalagret Google standardnamn `dataLayer`.

## Händelser

Tillägget gör att du kan lyssna efter ändringar (händelser) i datalagret. En händelse kan vara något av följande:

* Tagga händelser (till exempel ett bibliotek som läses in)
* JavaScript-händelser
* Data överförs till datalagret med `event` nyckelord.

Det är viktigt att förstå hur [`event` nyckelord](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) när data skickas till ett Google-datalager, på samma sätt som datalagret Adobe Client. The `event` nyckelordet ändrar beteendet för Google-datalagret och därför uppdateras tilläggets beteende i enlighet med detta.

Avsnitten nedan visar de olika händelsetyper som tillägget kan avlyssna.

### Lyssna efter alla penslar till datalagret

Om du väljer det här alternativet avlyssnar tillägget eventuella ändringar som gjorts i datalagret.

### Lyssna efter push-meddelanden exklusive händelser

Om du väljer det här alternativet avlyssnar tillägget allt som skickas till datalagret, exklusive händelser.

Följande exempel på push-händelse spåras av avlyssnaren:

```js
dataLayer.push({"data":"something"})
```

Följande exempel på push-händelser spåras inte av avlyssnaren:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Lyssna efter alla händelser

Om du väljer det här alternativet avlyssnar tillägget alla händelser som skickas till datalagret.

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

Om du vill lyssna efter en viss händelse väljer du det här alternativet så att händelseavlyssnaren spårar alla händelser som matchar en viss sträng.

Ange till exempel `myEvent` när du använder den här konfigurationen spåras endast följande push-händelse i avlyssnaren:

```js
dataLayer.push({"event":"myEvent"})
```

Du kan också använda en regex-sträng för att matcha händelsenamn. Ange till exempel `myEvent\d` spårar händelser som börjar med `myEvent` följt av en siffra:

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Instruktioner

Avsnitten nedan beskriver de olika åtgärder som tillägget kan utföra när det ingår i en [regel](../../../ui/managing-resources/rules.md).

### Överför till datalager {#push-to-data-layer}

Den här åtgärden överför JSON-innehåll till själva datalagret, vilket gör det möjligt att använda dataelement direkt i JSON-nyttolasterna. I den angivna JSON-redigeraren kan du referera till dataelement med procentnotation (till exempel `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Google DL Återställ till beräknat tillstånd

>[!NOTE]
>
>Den här åtgärden är tillgänglig från v1.0.5 och framåt.

Den här åtgärden återställer datalagret. Om datalagret används i en regel som bearbetar en ändring i ett Google-datalager, återställs det till det beräknade läget för datalagret när regeln utlöstes. Om åtgärden används i en regel som inte bearbetar en ändring i ett Google-datalager töms datalagret av åtgärden.

## Dataelement

Tillägget tillhandahåller ett unikt dataelement som använder en nyckel för att komma åt datalagret (till exempel `page.url` i [textutdrag ovan](#push-to-data-layer)).

Dataelementet kan innehålla något av följande:

* Ett specifikt värde från datalagret (till exempel `page.url`)
* Hela datalagrets array (tomt nyckelfält)
* Värden från en datalagerhändelse med hjälp av tangenten (om `event` nyckelord användes)
* Hela händelseobjektet (tomt nyckelfält)

Tillägget prioriterar alltid händelseinformation. Om ett datalager `event` behandlas, värden läses alltid från den händelsen. Om en `event` finns inte. Värden läses i stället från det direkta datalagret.

## Ytterligare information

Ytterligare information finns i [VIKTIGT](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) och i tilläggets dialogrutor för dataelement och händelser.
