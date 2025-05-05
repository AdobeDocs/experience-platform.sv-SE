---
title: Fältgruppen Adobe Analytics ExperienceEvent Full Extension Schema
description: Läs mer om schemafältgruppen Adobe Analytics ExperienceEvent Full Extension.
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Adobe Analytics ExperienceEvent Full Extension]

[!UICONTROL Adobe Analytics ExperienceEvent Full Extension] är en standardschemafältgrupp för [[!DNL XDM ExperienceEvent] klassen](../../classes/experienceevent.md), som samlar in vanliga mått som samlas in av Adobe Analytics.

Det här dokumentet beskriver strukturen och användningsfallet för fältgruppen för Analytics-tillägget.

>[!NOTE]
>
>På grund av storleken och antalet upprepade element i den här fältgruppen har många av fälten som visas i den här guiden komprimerats för att spara utrymme. Om du vill utforska den fullständiga strukturen för den här fältgruppen kan du [leta upp den i Experience Platform-gränssnittet](../../ui/explore.md) eller visa hela schemat i den [publika XDM-databasen](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Fältgruppstruktur

Fältgruppen tillhandahåller ett enskilt `_experience`-objekt till ett schema, som i sin tur innehåller ett enskilt `analytics`-objekt.

![Fält på översta nivån för analysfältgruppen](../../images/field-groups/analytics-full-extension/full-schema.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `customDimensions` | Objekt | Hämtar anpassade dimensioner som spåras av Analytics. Mer information om innehållet i det här objektet finns i [underavsnittet nedan](#custom-dimensions). |
| `endUser` | Objekt | Hämtar webbinteraktionsinformationen för slutanvändaren som utlöste händelsen. Mer information om innehållet i det här objektet finns i [underavsnittet nedan](#end-user). |
| `environment` | Objekt | Hämtar information om den webbläsare och det operativsystem som utlöste händelsen. Mer information om innehållet i det här objektet finns i [underavsnittet nedan](#environment). |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Objekt | Fältgruppen innehåller objektfält för att fånga upp till 1 000 anpassade händelser. Mer information om dessa fält finns i [underavsnittet nedan](#events). |
| `session` | Objekt | Hämtar information om sessionen som utlöste händelsen. Mer information om innehållet i det här objektet finns i [underavsnittet nedan](#session). |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions` hämtar anpassade [dimensioner](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html?lang=sv-SE) som spåras av Analytics.

![customDimensions-fält](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `eVars` | Objekt | Ett objekt som hämtar upp till 250 konverteringsvariabler ([eVars](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=sv-SE)). Egenskaperna för det här objektet är `eVar1`-keyade för `eVar250` och accepterar bara strängar för deras datatyp. |
| `hierarchies` | Objekt | Ett objekt som hämtar upp till fem anpassade hierarkivariabler ([hiers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html?lang=sv-SE)). Egenskaperna för det här objektet är nedtonade `hier1` till `hier5`, som i sin tur är objekt med följande underegenskaper:<ul><li>`delimiter`: Den ursprungliga avgränsaren som användes för att generera listan under `values`.</li><li>`values`: En avgränsad lista med namn på hierarkinivåer, representerat som en sträng.</li></ul> |
| `listProps` | Objekt | Ett objekt som hämtar upp till 75 [listproppar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=sv-SE#list-props). Egenskaperna för det här objektet är nedtonade `prop1` till `prop75`, som i sin tur är objekt med följande underegenskaper:<ul><li>`delimiter`: Den ursprungliga avgränsaren som användes för att generera listan under `values`.</li><li>`values`: En avgränsad lista med värden för propen, representerad som en sträng.</li></ul> |
| `lists` | Objekt | Ett objekt som hämtar upp till tre [listor](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html?lang=sv-SE). Egenskaperna för det här objektet är nedtonade `list1` till `list3`. Var och en av dessa egenskaper innehåller en enda `list`-matris med [[!UICONTROL Key Value Pair]](../../data-types/key-value-pair.md)-datatyper. |
| `props` | Objekt | Ett objekt som hämtar upp till 75 [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html?lang=sv-SE). Egenskaperna för det här objektet är `prop1`-keyade för `prop75` och accepterar bara strängar för deras datatyp. |
| `postalCode` | Sträng | Ett postnummer som kunden angett. |
| `stateProvince` | Sträng | En klienttillhandahållen stat eller provinsplats. |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser` samlar in webbinteraktionsinformation för slutanvändaren som utlöste händelsen.

![endUser-fält](../../images/field-groups/analytics-full-extension/endUser.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Web Information]](../../data-types/web-information.md) | Informationen om webbsida, länk och referens från den första Experience Event-händelsen för den här slutanvändaren. |
| `firstTimestamp` | Heltal | En Unix-tidsstämpel för den första ExperienceEvent-händelsen för den här slutanvändaren. |

## `environment` {#environment}

`environment` samlar in information om den webbläsare och det operativsystem som utlöste händelsen.

![miljöfält](../../images/field-groups/analytics-full-extension/environment.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `browserIDStr` | Sträng | Adobe Analytics-identifieraren för den webbläsare som används (kallas även [webbläsartypdimension](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html?lang=sv-SE)). |
| `operatingSystemIDStr` | Sträng | Adobe Analytics-identifieraren för det operativsystem som används (kallas annars för [operativsystemtypsdimensionen](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html?lang=sv-SE)). |

## Anpassade händelsefält {#events}

Fältgruppen Analytics-tillägg innehåller tio objektfält som samlar in upp till 100 [anpassade händelsemått](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html?lang=sv-SE) vardera, vilket ger totalt 1 000 för fältgruppen.

Varje händelseobjekt på den översta nivån innehåller de enskilda händelseobjekten för respektive intervall. `event101to200` innehåller t.ex. händelser som har sparats från `event101` till `event200`.

Alla jämna objekt använder datatypen [[!UICONTROL Measure]](../../data-types/measure.md), vilket ger en unik identifierare och ett kvantifierbart värde.

![Anpassat händelsefält](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` samlar in information om sessionen som utlöste händelsen.

![sessionsfält](../../images/field-groups/analytics-full-extension/session.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `search` | [[!UICONTROL Search]](../../data-types/search.md) | Hämtar information om webb- eller mobilsökning för sessionsposten. |
| `web` | [[!UICONTROL Web Information]](../../data-types/web-information.md) | Hämtar information om länkklick, webbsidesinformation, referensinformation och webbläsarinformation för sessionsposten. |
| `depth` | Heltal | Slutanvändarens aktuella sessionsdjup (till exempel sidnummer). |
| `num` | Heltal | Slutanvändarens aktuella sessionsnummer. |
| `timestamp` | Heltal | En Unix-tidsstämpel för sessionsposten. |

## Nästa steg

Det här dokumentet innehöll struktur och användningsfall för fältgruppen för Analytics-tillägget. Mer information om själva fältgruppen finns i [den offentliga XDM-databasen](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Om du använder den här fältgruppen för att samla in Analytics-data med Adobe Experience Platform Web SDK kan du läsa guiden [Konfigurera ett datastream](../../../datastreams/overview.md) för att lära dig hur du mappar data till XDM på serversidan.
