---
title: Testa en Adobe Target-implementering med Adobe Experience Platform Debugger
description: Lär dig hur du använder Adobe Experience Platform Debugger för att testa och felsöka en webbplats som är aktiverad med Adobe Target.
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: c3b5b63767a934be16a479d04853e1250b3bf775
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 0%

---

# Testa en Adobe Target-implementering med Adobe Experience Platform Debugger

Adobe Experience Platform Debugger innehåller ett antal användbara verktyg för att testa och felsöka en webbplats som har verktygats med en Adobe Target-implementering. Den här guiden innehåller några vanliga arbetsflöden och metodtips för att använda Platform Debugger på en målaktiverad webbplats.

## Förutsättningar

Om du vill använda Platform Debugger för Target måste webbplatsen använda [at.js-bibliotek](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) version 1.x eller senare. Tidigare versioner stöds inte.

## Initierar plattformsfelsökning

Öppna webbplatsen som du vill testa i en webbläsare och öppna sedan plattformsfelsökningstillägget.

Välj **[!DNL Target]** i den vänstra navigeringen. Om plattformsfelsökaren upptäcker att en kompatibel version av at.js körs på webbplatsen visas Adobe Target implementeringsinformation.

![Målvyn som valts i plattformsfelsökaren, vilket anger att Adobe Target är aktivt på den webbläsarsida som visas](../images/solutions/target/target-initialized.png)

## Global konfigurationsinformation

Information om implementeringens globala konfiguration visas högst upp i målvyn i Platform Debugger.

![Global konfigurationsinformation för Target markerad i plattformsfelsökning](../images/solutions/target/global-config.png)

| Namn | Beskrivning |
| --- | --- |
| Klientkod | Ett unikt ID som identifierar din organisation. |
| Version | Den version av Adobe Target-biblioteket som är installerad på webbplatsen. |
| Namn på global begäran | Namnet på [global mbox](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) för Target-implementeringen, standardnamnet är `target-global-mbox`. |
| Sidinläsningshändelse | Ett booleskt värde som anger om en [sidinläsningshändelse](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) har ägt rum. Sidinläsningshändelser stöds bara för at.js 2.x. För versioner som inte är kompatibla är standardvärdet `None`. |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

Välj **[!DNL Network Requests]** för att visa sammanfattningsinformation om varje nätverksbegäran som görs på sidan.

![The [!DNL Network Requests] för Target som valts inom plattformsfelsökning](../images/solutions/target/network-requests.png)

När du utför åtgärder på sidan (inklusive läser in sidan igen) läggs nya kolumner automatiskt till i tabellen, så att du kan visa åtgärdssekvensen och hur värdena ändras mellan varje begäran.

![The [!DNL Network Requests] för Target som valts inom plattformsfelsökning](../images/solutions/target/new-request.png)

Följande värden hämtas:

| Namn | Beskrivning |
| --- | --- |
| [!DNL Page Title] | Titeln på sidan som initierade den här begäran. |
| [!DNL Page URL] | URL-adressen till sidan som initierade begäran. |
| [!DNL URL] | Begärans rå-URL. |
| [!DNL Method] | HTTP-metoden för begäran. |
| [!DNL Query String] | Frågesträngen för begäran, tagen från URL:en. |
| [!DNL POST Body] | Innehållet i begäran (anges endast för POST-begäranden). |
| [!DNL Pathname] | Sökvägen till begärande-URL:en. |
| [!DNL Hostname] | Värdnamnet för begärande-URL. |
| [!DNL Domain] | Domänen för begärande-URL. |
| [!DNL Timestamp] | En tidsstämpel som anger när begäran (eller händelsen) ägde rum inom webbläsarens tidszon. |
| [!DNL Time Since Page Load] | Förfluten tid sedan sidan först lästes in vid tidpunkten för begäran. |
| [!DNL Initiator] | Initieraren av begäran. Med andra ord, vem gjorde förfrågan? |
| [!DNL clientCode] | Identifieraren för organisationens konto som identifieras av Target. |
| [!DNL requestType] | Det API som användes för begäran. Om at.js 1.x används är värdet `/json`. Om at.js 2.x används är värdet `delivery`. |
| [!DNL Audience Manager Blob] | Tillhandahåller information om krypterade Audience Manager-metadata som kallas&quot;blob&quot;. |
| [!DNL Audience Location Hint] | Datainsamlingens region-ID. Detta är en numerisk identifierare för den geografiska platsen för ett visst ID-tjänstdatacenter. Mer information finns i Audience Manager-dokumentationen om [DCS-region-ID, -platser och -värdnamn](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) och Experience Cloud Identity Service Guide på [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | Webbläsarens höjd i pixlar. |
| [!DNL Browser Time Offset] | Webbläsarens tidsförskjutning som är associerad med dess tidszon. |
| [!DNL Browser Width] | Webbläsarens bredd i pixlar. |
| [!DNL Color Depth] | Skärmens färgdjup. |
| [!DNL context] | Ett objekt som innehåller sammanhangsberoende information om webbläsaren som användes för att göra begäran, inklusive skärmdimensioner och klientplattform. |
| [!DNL prefetch] | Parametrarna som används i under `prefetch` bearbetning. |
| [!DNL execute] | Parametrarna som används under `execute` bearbetning. |
| [!DNL Experience Cloud Visitor ID] | Om något av detta upptäcks, innehåller information om [Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) som tilldelats den aktuella besökaren. |
| [!DNL experienceCloud] | Innehåller Experience Cloud-ID:n för den här specifika användarsessionen: en A4T [ID för kompletterande data](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)och en [besökar-ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | The [Mål-ID](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) för besökaren. |
| [!DNL Mbox Host] | The [värd](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) som Target-begäran gjordes till. |
| [!DNL Mbox PC] | En sträng som kapslar in [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) sessions-ID och [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) platstips. Det här värdet används av at.js för att säkerställa att sessionen och Edge-platsen förblir fästa. |
| [!DNL Mbox Referrer] | URL-refereraren för den specifika [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) begäran. |
| [!DNL Mbox URL] | URL:en för [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) server. |
| [!DNL Mbox Version] | Versionen av [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) används. |
| [!DNL mbox3rdPartyId] | The [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) som tilldelats den aktuella besökaren. |
| [!DNL mboxRid] | The [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) begärande-ID. |
| [!DNL requestId] | Ett unikt ID för begäran. |
| [!DNL Screen Height] | Skärmens höjd i pixlar. |
| [!DNL Screen Width] | Skärmens bredd i pixlar. |
| [!DNL Supplemental Data ID] | Ett systemgenererat ID som används för att matcha besökare med motsvarande Adobe Target- och Adobe Analytics-samtal. Se [A4T - felsökningsguide](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) för mer information. |
| [!DNL vst] | The [API-konfiguration för Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | Anger information om WebGL-renderaren som används på sidan, om tillämpligt. |

{style="table-layout:auto"}

Om du vill visa information om en parameter för en viss nätverkshändelse markerar du tabellcellen i fråga. En pover med mer information om parametern visas, inklusive en beskrivning och dess värde. Om värdet är ett JSON-objekt innehåller dialogrutan en fullt navigerbar vy av objektets struktur.

![The [!DNL Network Requests] för Target som valts inom plattformsfelsökning](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Välj **[!DNL Configuration]** om du vill aktivera eller inaktivera ett urval av ytterligare felsökningsverktyg för Target.

![The [!DNL Configuration Requests] för Target som valts inom plattformsfelsökning](../images/solutions/target/configuration.png)

| Felsökningsverktyg | Beskrivning |
| --- | --- |
| [!DNL Target Console Logging] | När det här alternativet är aktiverat kan du komma åt loggarna at.js på konsolfliken i webbläsaren. Den här funktionen kan även aktiveras genom att en `mboxDebug` query param (med valfritt värde) to the browser URL. |
| [!DNL Target Diable] | När det här alternativet är aktiverat inaktiveras alla Target-funktioner på sidan. Detta kan användas för att avgöra om ett Target-specifikt erbjudande är orsaken till problemet på sidan. |
| [!DNL Target Trace] | **Anteckning**: Du måste vara inloggad för att kunna aktivera den här funktionen.<br><br>När det här alternativet är aktiverat skickas spårningstoken med varje begäran och ett spårningsobjekt returneras i varje svar. `at.js` tolkar svaret `window.__targetTraces`. Varje trace-objekt innehåller samma information som [[!DNL Network Requests] tab], with the following additions:<ul><li>En ögonblicksbild av en profil som gör att du kan se attribut före och efter en begäran.</li><li>Matchade och omatchade [verksamhet](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), som visar varför den aktuella profilen var eller inte var kvalificerad för vissa aktiviteter.<ul><li>Detta kan hjälpa till att identifiera vilka målgrupper en profil kvalificerar sig för vid en viss tidpunkt och varför.</li><li>Måldokumenten innehåller mer information om olika aktivitetstyper</li></ul></li></ul> |

{style="table-layout:auto"}
