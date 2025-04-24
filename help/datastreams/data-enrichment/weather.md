---
title: Förbättra datainsamlingen med väderdata från DNL The Weather Channel
description: Förbättra de data ni samlar in via datastreams med väderdata från DNL The Weather Channel.
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 1%

---

# Förbättra datainsamling med väderdata från [!DNL The Weather Channel]

Adobe har samarbetat med [!DNL [The Weather Company]](https://www.ibm.com/weather) för att ge den ytterligare kontexten för USA-väder till data som samlats in via datastreams. Ni kan använda dessa data för analyser, målgruppsanpassning och målgruppsskapande i Experience Platform.

Det finns tre typer av data som är tillgängliga från [!DNL The Weather Channel]:

* **[!UICONTROL Current Weather]**: Användarens aktuella väderförhållanden, baserat på deras plats. Detta inkluderar aktuell temperatur, utfällning, molntäckning med mera.
* **[!UICONTROL Forecasted Weather]**: Prognosen innehåller prognosen 1, 2, 3, 5, 7 och 10 dagar för användarplatsen.
* **[!UICONTROL Triggers]**: Utlösare är specifika kombinationer som mappar till olika semantiska väderförhållanden. Det finns tre olika typer av väderutlösare:

   * **[!UICONTROL Weather Triggers]**: Semantiskt meningsfulla förhållanden, till exempel kallt eller regnigt väder. Dessa kan skilja sig åt i definitioner mellan olika klimat.
   * **[!UICONTROL Product Triggers]**: Villkor som skulle leda till inköp av olika typer av produkter. Exempel: väderprognoser kan innebära att inköp av regnrockar är mer sannolika.
   * **[!UICONTROL Severe Weather Triggers]**: Allvarliga vädervarningar, som vinterstorm eller orkanvarningar.

## Förhandskrav {#prerequisites}

Innan du använder väderdata bör du kontrollera att du uppfyller följande krav:

* Du måste licensiera väderdata som du kommer att använda från [!DNL The Weather Channel]. De aktiverar det sedan på ditt konto.
* Väderdata är bara tillgängliga via datastreams. Om du vill använda väderdata måste du använda [!DNL Web SDK], [!DNL Mobile Edge Extension] eller [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/) för att inkludera dessa data.
* [[!UICONTROL Geo Location]](../configure.md#advanced-options) måste vara aktiverat för din datastream.
* Lägg till [väderfältgruppen](#schema-configuration) i schemat som du använder.

## Provisionering {#provisioning}

När du har licensierat data från [!DNL The Weather Channel] aktiverar de ditt konto för åtkomst till data. Därefter kontaktar du Adobe kundtjänst för att aktivera data på din datastam. När det här alternativet är aktiverat läggs data automatiskt till.

Du kan validera att det läggs till genom att köra en kantspårning med felsökaren eller genom att använda Assurance för att spåra en träff genom [!DNL Edge Network].

### Schemakonfiguration {#schema-configuration}

Du måste lägga till de väderfältsgrupper i ditt Experience Platform-schema som motsvarar den händelsedatamängd som du använder i din datastam. Det finns fem fältgrupper:

* [!UICONTROL Forecasted Weather]
* [!UICONTROL Current Weather]
* [!UICONTROL Product Triggers]
* [!UICONTROL Relative Triggers]
* [!UICONTROL Severe Weather Triggers]

## Få åtkomst till väderdata {#access-weather-data}

När era data är licensierade och tillgängliga kan ni få tillgång till dem på olika sätt via Adobes tjänster.

### Adobe Analytics {#analytics}

I [!DNL Adobe Analytics] är väderdata tillgängliga för mappning via bearbetningsregler, tillsammans med resten av [!DNL XDM]-schemat.

Du hittar listan med fält som du kan mappa på sidan [väderreferens](weather-reference.md). Precis som för alla [!DNL XDM]-scheman har tangenterna prefixet `a.x`. Ett fält med namnet `weather.current.temperature.farenheit` skulle till exempel visas i [!DNL Analytics] som `a.x.weather.current.temperature.farenheit`.

![Bearbetar regelgränssnitt](../assets/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

I [!DNL Adobe Customer Journey Analytics] är väderdata tillgängliga i datauppsättningen som anges i datastream. Så länge väderattributen [har lagts till i ditt schema](#prerequisites-prerequisites) är de tillgängliga för [att lägga till i en datavy](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) i [!DNL Customer Journey Analytics].

### Plattform för kunddata i realtid {#rtcdp}

Väderdata är tillgängliga i [Real-Time Customer Data Platform](../../rtcdp/overview.md) som kan användas i målgrupper. Väderdata bifogas till händelser.

![Segmentbyggaren visar väderhändelser](../assets/data-enrichment/weather/schema-builder.png)

Eftersom väderförhållandena ändras ofta rekommenderar Adobe att du anger tidsbegränsningar för målgrupperna, vilket visas i exemplet ovan. Att ha en kall dag den sista dagen eller två är mycket mer effektfullt än att ha en kall dag för sex månader sedan.

Se [väderreferensen](weather-reference.md) för tillgängliga fält.

### Adobe Target {#target}

I [!DNL Adobe Target] kan du använda väderdata för att driva personaliseringen i realtid. Väderdata skickas till [!DNL Target] som [!UICONTROL mBox]-parametrar och du kan komma åt dem via en anpassad [!UICONTROL mBox]-parameter.

![Målpublikbyggaren](../assets/data-enrichment/weather/target-audience-builder.png)

Parametern är sökvägen [!DNL XDM] till ett specifikt fält. Se [väderreferensen](weather-reference.md) för tillgängliga fält och deras motsvarande sökvägar.

## Nästa steg {#next-steps}

När du har läst det här dokumentet får du nu en bättre förståelse för hur du kan använda väderdata i olika Adobe-lösningar. Mer information om mappning av väderdatafält finns i [fältmappningsreferensen](weather-reference.md).
