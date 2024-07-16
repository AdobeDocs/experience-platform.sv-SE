---
title: Vyn Valideringsredigerare
description: Den här vägledningen innehåller information om valideringsredigeringsvyn i Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# Vyn Valideringsredigerare

Med valideringsredigeraren kan du snabbt och enkelt hantera JavaScript-funktioner för att validera händelser i en Adobe Experience Platform Assurance-session. Varje funktion tar emot händelserna i en Assurance-session. Du kan skriva funktioner för att validera klientens konfiguration, händelseförhållanden, tester och användningsfall.

## Kom igång med valideringsredigeraren

När [du har konfigurerat Assurance](../tutorials/implement-assurance.md) väljer du **[!UICONTROL Validation Editor]** i vyn **[!UICONTROL Home]**.

![Validation-Editor-screen-shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Skriva en valideringsfunktion

Med den här funktionen kan du skapa, redigera eller ta bort valideringsfunktioner för dina Adobe Experience Platform Assurance-sessioner.

1. Välj **[!UICONTROL Create a New Validation]**.
2. Ange ett **namn** för att identifiera valideringen och ange sedan en **kategori** och en **beskrivning**.
3. Redigera koden i redigeraren för att validera händelserna för din Assurance-session.

När funktionstesterna är klara väljer du **[!UICONTROL Publish]** för att spara din validering.

### Händelsedefinition

| Nyckel | Typ | Beskrivning |
| :--- | :--- | :--- |
| `uuid` | Sträng | Universellt unik identifierare för händelsen. |
| `timestamp` | Nummer | Tidsstämpel från klienten när händelsen skickades till Assurance. |
| `eventNumber` | Nummer | Används för att beställa när händelsen skickades. Den här nyckeln är användbar när händelser har samma tidsstämpel. |
| `vendor` | Sträng | Sträng för leverantörsidentifiering i det omvända domännamnsformatet (t.ex. com.adobe.assertill). |
| `type` | Sträng | Används för att ange händelsetyp. |
| `payload` | Objekt | Definierar data för händelsen och innehåller unika och gemensamma egenskaper. Vissa vanliga egenskaper är `ACPExtensionEventSource` och `ACPExtensionEventType`. |
| `annotations` | Array | En array med anteckningsobjekt. |

### Anteckningsdefinition

| Nyckel | Typ | Beskrivning |
| :--- | :--- | :--- |
| `uuid` | Sträng | Universellt unik identifierare för anteckningen. |
| `type` | Sträng | Används för att ange anteckningstypen och är vanligtvis namnet på plugin-programmet (till exempel analytics). |
| `payload` | Objekt | Definierar de data som ska komplettera händelsen. För Adobe Analytics är det här de efterbearbetade träffdata finns. |

### Valideringsresultat

Valideringsfunktionen förväntas returnera ett objekt som innehåller följande:

| Nyckel | Typ | Beskrivning |
| :--- | :--- | :--- |
| `message` | Sträng | Valideringsmeddelandet som ska visas i sammanfattningsresultatet. |
| `events` | Array | En array med händelsehjälpmedel som ska rapporteras som matchade eller inte matchade. |
| `links` | Array | En array med `ValidationResultLink` objekt som refererar till dokumentation och andra resurser `{( type: 'doc'|'product', url: String )}` |
| `result` | Sträng | Detta är valideringsresultatet och förväntas vara en av de uppräknade strängarna: &quot;matched&quot;, &quot;not matched&quot;, &quot;unknown&quot; |

## Visa valideringsresultat

Resultatet av funktionen visas i resultatavsnittet nedanför kodredigeraren. Om valideringsresultatet är `unknown` eller `not matched` och arrayen `events` har en eller flera `uuids` markeras händelserna på tidslinjen med följande färger:

* Grön - matchad
* Orange - okänd
* Röd - inte matchad

![Timeling-validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Felsökning

Du kan lägga till `console.log()` i funktionen för att skriva ut objekt på utvecklarkonsolen. Du kan också använda egenskapen message för resultatobjektet för att felsöka meddelanden på resultatpanelen.

Om ett fel inträffar i JavaScript kodredigerare visas felstatus tillsammans med orsaken.

Mer information om valideringar finns på [Adobe Experience Platform Assurance-valideringar](https://github.com/adobe/griffon-validation-plugins) GitHub. Här finns exempel på valideringar som ägs av Adobe. Mer information om valideringar finns i [wiki](https://github.com/adobe/griffon-validation-plugins/wiki).
