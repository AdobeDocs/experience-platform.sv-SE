---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fields;schemas;scheman;device;data type;data type;
solution: Experience Platform
title: Enhetsdatatyp
description: Läs mer om datatypen Device XDM.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Datatypen [!UICONTROL Device]

[!UICONTROL Device] är en standard-XDM-datatyp som beskriver en identifierad enhet. En enhet är en program- eller webbläsarinstans som kan spåras mellan sessioner, vanligtvis via cookies.

![](../images/data-types/device.png){width=450}

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `colorDepth` | Heltal | Det antal färger som visningen kan representera. |
| `manufacturer` | Sträng | Namnet på den organisation som äger designen och skapandet av enheten. |
| `model` | Sträng | Namnet på enhetens modell. Det här är det vanliga, läsbara namnet eller marknadsföringsnamnet för enheten. &quot;iPhone 6S&quot; är till exempel en viss modell av mobiltelefon. |
| `modelNumber` | Sträng | Den unika modellnummerbeteckningen som tilldelats av tillverkaren för den här enheten. Modellnummer är inte versioner, utan unika identifierare som identifierar en viss modellkonfiguration. |
| `screenHeight` | Heltal | Antalet lodräta pixlar för enhetens aktiva visning i standardorienteringen. |
| `screenOrientation` | Sträng | Den aktuella skärmorienteringen. Godkända värden är `portrait` och `landscape`. |
| `screenWidth` | Sträng | Antalet vågräta pixlar för enhetens aktiva visning i standardorienteringen. |
| `type` | Sträng | Den typ av enhet som spåras. Godkända värden är: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Sträng | En identifierare för enheten. Detta kan vara en identifierare från DeviceAtlas eller en annan tjänst som identifierar den maskinvara som används. |
| `typeIDService` | Sträng | Namnutrymmet för den tjänst som används för att identifiera enhetstypen. Mer information om godkända värden finns i [bilagan](#typeIDService). |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Bilaga

Följande avsnitt innehåller ytterligare information om datatypen [!UICONTROL Device].

## Godkända värden för typeIDService {#typeIDService}

I följande tabell visas godkända värden för `typeIDService` och deras associerade betydelse:

| Värde | Beskrivning |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Enheten har identifierats med DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Enheten har identifierats med Adobe Campaign. |
