---
title: Använd väderdata från DNL The Weather Channel
description: Använd väderdata från DNL Weather Channel för att förbättra de data ni samlar in via datastreams.
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 1%

---

# Använd väderdata från [!DNL The Weather Channel]

Adobe har samarbetat med [!DNL [The Weather Company]](https://www.ibm.com/weather) för att ge den information som samlas in via datastreams ett extra sammanhang för USA:s väder. Ni kan använda dessa data för analyser, målinriktning och segmentskapande i Experience Platform.

Det finns tre typer av data som är tillgängliga från [!DNL The Weather Channel]:

* **[!UICONTROL Current Weather]**: Användarens aktuella väderförhållanden, baserat på var användaren befinner sig. Detta inkluderar aktuell temperatur, kryptering, molntäckning med mera.
* **[!UICONTROL Forecasted Weather]**: Prognosen innehåller prognosen på 1,2,3,5,7 och 10 dagar för användarplatsen.
* **[!UICONTROL Triggers]**: Utlösare är specifika kombinationer som mappar till olika semantiska väderförhållanden. Det finns tre olika typer av väderutlösare:

   * **[!UICONTROL Weather Triggers]**: Semantiskt meningsfulla förhållanden, till exempel kallt eller regnigt väder. Dessa kan skilja sig åt i definitioner mellan olika klimat.
   * **[!UICONTROL Product Triggers]**: Villkor som skulle leda till inköp av olika typer av produkter. Till exempel: kalla väderprognoser kan innebära att inköp av regnrockar är mer sannolikt.
   * **[!UICONTROL Severe Weather Triggers]**: Allvarliga vädervarningar, som vinterstorm eller orkanvarningar.

## Förutsättningar {#prerequisites}

Innan du använder väderdata bör du kontrollera att du uppfyller följande krav:

* Du måste licensiera väderdata som du kan använda från [!DNL The Weather Channel]. De aktiverar det sedan på ditt konto.
* Väderdata är bara tillgängliga via datastreams. Om du vill använda väderdata måste du använda [!DNL Web SDK], [!DNL Mobile Edge Extension] eller [Server-API](../../../server-api/overview.md) för att utnyttja dessa data.
* Ditt datastream måste ha [[!UICONTROL Geo Location]](../configure.md#advanced-options) aktiverat.
* Lägg till [väderfältgrupp](#schema-configuration) till det schema du använder.

## Provisionering {#provisioning}

När du har licensierat data från [!DNL The Weather Channel]kommer de att göra det möjligt för ditt konto att komma åt data. Sedan måste du kontakta Adobe kundtjänst för att aktivera data på din datastam. När det här alternativet är aktiverat läggs data automatiskt till.

Du kan validera att det läggs till genom att köra en kantspårning med felsökaren eller genom att använda Assurance för att spåra en träff i [!DNL Edge Network].

### Schemakonfiguration {#schema-configuration}

Du måste lägga till de väderfältsgrupper i ditt Experience Platform-schema som motsvarar den händelsedatamängd som du använder i din datastam. Det finns fem fältgrupper:

* [!UICONTROL Forecasted Weather]
* [!UICONTROL Current Weather]
* [!UICONTROL Product Triggers]
* [!UICONTROL Relative Triggers]
* [!UICONTROL Severe Weather Triggers]

## Få åtkomst till väderdata {#access-weather-data}

När era data är licensierade och tillgängliga kan ni komma åt dem på flera olika sätt via Adobes tjänster.

### Adobe Analytics {#analytics}

I [!DNL Adobe Analytics]kan väderdata mappas via bearbetningsregler, tillsammans med resten av [!DNL XDM] schema.

Du hittar listan med fält som du kan mappa i [väderreferens](weather-reference.md) sida. Som med alla [!DNL XDM] scheman, tangenterna prefixeras med `a.x`. Ett fält med namnet `weather.current.temperature.farenheit` skulle visas i [!DNL Analytics] as `a.x.weather.current.temperature.farenheit`.

![Gränssnitt för bearbetningsregel](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

I [!DNL Adobe Customer Journey Analytics], är väderdata tillgängliga i den datauppsättning som anges i datastream. Så länge väderattributen är [läggs till i ditt schema](#prerequisites-prerequisites)kommer de att vara tillgängliga för [lägga till i en datavy](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

Väderdata är tillgängliga i [Real-time Customer Data Platform](../../../rtcdp/overview.md), som används i segment. Väderdata bifogas till händelser.

![Segmentbyggaren som visar väderhändelser](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

Eftersom väderförhållandena ändras ofta rekommenderar Adobe att du anger tidsbegränsningar för segmenten, vilket visas i exemplet ovan. Att ha en kall dag den sista dagen eller två är mycket mer effektfullt än att ha en kall dag för sex månader sedan.

Se [väderreferens](weather-reference.md) för de tillgängliga fälten.

### Adobe Target {#target}

I [!DNL Adobe Target]kan ni använda väderdata för att driva personaliseringen i realtid. Väderdata skickas till [!DNL Target] as [!UICONTROL mBox] parametrar och du kan komma åt dem via [!UICONTROL mBox] parameter.

![Target Audience Builder](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

Parametern är [!DNL XDM] sökväg till ett visst fält. Se [väderreferens](weather-reference.md) för de tillgängliga fälten och deras motsvarande sökvägar.

## Nästa steg {#next-steps}

När du har läst det här dokumentet får du nu en bättre förståelse för hur du kan använda väderdata i olika Adobe-lösningar. Mer information om mappning av väderdatafält finns i [fältmappningsreferens](weather-reference.md).
