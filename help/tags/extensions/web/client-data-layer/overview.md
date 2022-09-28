---
title: Adobe Client Data Layer Extension
description: Läs mer om taggtillägget Adobe Client Data Layer i Adobe Experience Platform.
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Tillägget Adobe Client Data Layer

Den här dokumentationen innehåller exempel och metodtips om hur du använder tillägget Adobe Client Data Layer.

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## Installation

Om du vill installera tillägget går du till tilläggskatalogen i användargränssnittet för Experience Platform eller datainsamlingen och väljer Adobe Client Data Layer.

![ACDL-tilläggsvy i katalog](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## Tilläggsvy

ACDL-skriptet skapar som standard ett nytt datalager med variabelnamnet `adobeDataLayer`. I tilläggsvyn kan du ändra det här namnet om du vill. Namnet som du har angett instansieras när taggar läses in.

>[!NOTE]
>
>När objektnamnet ändras är originalet `adobeDataLayer` objektet instansieras fortfarande och dupliceras sedan till det nya variabelnamnet som du har valt.

## Händelser

Tillägget ger dig möjlighet att lyssna på händelser i datalagret. Följande händelser är tillgängliga:

### Lyssna på alla dataändringar

Om du väljer det här alternativet avlyssnar händelseavlyssnaren alla ändringar som görs i datalagret.

>[!IMPORTANT]
>
>När du trycker på händelser ändras inte själva datalagret.

Följande exempel på push-händelser spåras av avlyssnaren:

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

Följande exempel på push-händelse spåras inte av avlyssnaren:

* ` adobeDataLayer.push({"event":"myevent"})`

### Lyssna på alla händelser

Om du väljer det här alternativet avlyssnar händelseavlyssnaren alla händelser som skickas till datalagret.

Följande exempel på push-händelser spåras av avlyssnaren:

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

Följande exempel på push-händelse spåras inte av avlyssnaren:

* ` adobeDataLayer.push({"data":"something"}) `

### Lyssna efter en specifik händelse

Om du anger en händelse spårar händelseavlyssnaren alla händelser som matchar en viss sträng.

Ange till exempel `myEvent` när du använder den här konfigurationen spåras endast följande push-händelse i avlyssnaren:

* `adobeDataLayer.push({"event":"myEvent"})`

Du kan också ändra omfattningen för din händelseavlyssnare. De olika alternativen sammanfattas nedan:

* `all`: Det här är standardalternativet och aktiverar regeln varje gång det villkor du har valt ovan har uppfyllts tidigare, eller kommer att pushas in i framtiden. Det här är det säkraste alternativet om du använder en asynkron implementering.
* `future`: Med det här alternativet aktiveras regeln endast när nya push-händelser som matchar ditt villkor skickas till datalagret.
* `past`: Det här alternativet utlöser endast regeln för gamla push-händelser som matchar ditt villkor. Nya penslar som matchar ditt villkor ignoreras och utlöser inte regeln längre.

## Instruktioner

I följande avsnitt beskrivs de åtgärder som stöds av tillägget.

### Återställ datalager

Tillägget ger dig ett sätt att återställa datalagrets längd, vilket kan hjälpa dig att behålla en begränsad storlek för ett enkelsidigt program (SPA).

Det finns dock för närvarande ingen möjlighet att helt ta bort information som tidigare ställts in under push-metoderna.

The **Återställ och ange beräknat läge** åtgärden kopierar det senaste beräknade läget, tömmer datalagret och återställer det senaste läget.

### Överför till datalager

Tillägget ger dig en åtgärd för att överföra JSON-innehåll till själva datalagret. Den här åtgärden gör det möjligt att använda dataelement direkt i JSON. I JSON-redigeraren ska dataelement refereras med procentnotation (till exempel `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

## Dataelement

Avsnitten nedan beskriver de unika dataelementtyperna som tillägget tillhandahåller.

### Beräknat läge

Datalagrets dataelement för beräknat läge kan returnera en av två saker, beroende på hur du konfigurerar det:

* Det fullständiga datalagrets tillstånd: Som standard returneras hela datalagrets beräknade läge.
* En specifik sökväg: Du kan ange den sökväg som du vill returnera i datalagret. Banor anges med punktnotation (till exempel `data.foo`).

### Datalagerstorlek

Det här dataelementet returnerar datalagrets storlek. Datalagrets storlek representeras av antalet element som har skickats till det här objektet.

Med följande lista över push-händelser returnerar det här dataelementet heltalet `2`:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
