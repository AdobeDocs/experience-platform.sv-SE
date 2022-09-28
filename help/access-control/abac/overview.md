---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;attributbaserad åtkomstkontroll;
title: Attributbaserad åtkomstkontroll - översikt
description: Det här dokumentet innehåller information om attributbaserad åtkomstkontroll i Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: b095461b0c2510e84ca9a3a368f4907f8b3d5370
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 0%

---

# Attributbaserad åtkomstkontroll - översikt

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll är för närvarande tillgänglig i en begränsad version för USA-baserade vårdkunder. Den här funktionen kommer att vara tillgänglig för alla Real-time Customer Data Platform-kunder när den släpps helt.

Attributbaserad åtkomstkontroll är en funktion i Adobe Experience Platform som gör att administratörer kan styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut. Attribut kan läggas till i ett objekt, t.ex. en etikett som lagts till i ett schemafält eller segment. En administratör definierar åtkomstprinciper som innehåller attribut för att hantera behörigheter för användaråtkomst.

Med den här funktionen kan du etikettera XDM-schemafält (Experience Data Model) med etiketter som definierar användningsområde för organisationen eller data. Samtidigt kan administratörer använda användar- och rolladministrationsgränssnittet för att definiera åtkomstprinciper runt XDM-schemafält och bättre hantera åtkomsten som ges till användare eller grupper av användare (interna, externa eller externa användare). Dessutom gör attributbaserad åtkomstkontroll det möjligt för administratörer att hantera åtkomsten till specifika segment.

Med attributbaserad åtkomstkontroll kan administratören styra användarnas tillgång till känsliga personuppgifter (SPD), personligt identifierbar information (PII) och anpassad typ av data i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

## Attributbaserad åtkomstkontrollterminologi

Attributbaserad åtkomstkontroll omfattar följande komponenter:

| Terminologi | Definition |
| --- | --- |
| Attribut | Attribut är de identifierare som anger korrelationen mellan en användare och de plattformsresurser som de har åtkomst till. Attribut kan läggas till i ett objekt, t.ex. en etikett som lagts till i ett schemafält eller segment. En administratör definierar åtkomstprinciper som innehåller attribut för att hantera behörigheter för användaråtkomst. |
| Etiketter | Med etiketter kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa praxis uppmuntrar till etikettdata så snart de har importerats till Platform, eller så snart data blir tillgängliga för användning i Platform. |
| Behörigheter | Behörigheter omfattar möjligheten att visa och/eller använda plattformsfunktioner, som att skapa sandlådor, definiera scheman och hantera datauppsättningar. |
| Behörighetsuppsättningar | Behörighetsuppsättningar representerar en grupp behörigheter som en administratör kan tillämpa på en roll. En administratör kan tilldela behörighetsgrupper till en roll i stället för att tilldela enskilda behörigheter. Detta gör att du kan skapa anpassade roller från en fördefinierad roll som innehåller en grupp behörigheter. |
| Profiler | Profiler är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Profiler kan antingen vara lokala eller globala och kan åsidosätta andra profiler. |
| Resurs | En resurs är den resurs eller det objekt som ett ämne kan eller inte kan komma åt. Resurser kan vara segment eller schemafält. |
| Roller | Roller är sätt att kategorisera de typer av användare som interagerar med din plattformsinstans och är byggstenar för åtkomstkontrollprinciper. I en rollbaserad miljö för åtkomstkontroll är etableringen av användaråtkomst grupperad genom vanliga ansvarsområden och behov. En roll har en given uppsättning behörigheter och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilket synområde eller vilken skrivbehörighet de behöver. |
| Ämne | Ett ämne är den användare som begär åtkomst till en resurs för att utföra en åtgärd. |
| Användargrupper | Användargrupper är flera användare som har grupperats tillsammans och har tillgång till samma funktioner. |

## Behörigheter

>[!IMPORTANT]
>
>När din organisation har aktiverats för attributbaserad åtkomstkontroll kan du börja använda behörigheter på Adobe Experience Cloud i stället för produktprofiler i Adobe Admin Console för att hantera behörigheter för användare, funktioner, etiketter och andra resurser i din organisation.

Behörigheter är det område i Experience Cloud där administratörer kan definiera användarroller och åtkomstprinciper för att hantera åtkomstbehörigheter för funktioner och objekt i ett produktprogram.

Genom Behörigheter kan du skapa och hantera roller samt tilldela önskade resursbehörigheter för dessa roller. Med behörigheter kan du också hantera etiketter, sandlådor och användare som är kopplade till en viss roll. Mer information finns i [Behörighetsguide](ui/browse.md).

## Attributbaserad API för åtkomstkontroll

Med det attributbaserade API:t för åtkomstkontroll kan du programmässigt hantera roller, principer och produkter inom plattformen med API:er. Mer information finns i handboken på [använda API:t för att hantera attributbaserade åtkomstkontrollskonfigurationer](api/overview.md).

## Attributbaserad åtkomstkontroll i Adobe Experience Platform

I följande avsnitt finns information om hur attributbaserad åtkomstkontroll är integrerad med andra plattformskomponenter:

### Åtkomstkontroll

Plattformsanvändning [Adobe Admin Console](https://adminconsole.adobe.com) produktprofiler för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd plattformsfunktioner, inklusive datamodellering, profilhantering och sandlådeadministration. När din organisation har aktiverats för attributbaserad åtkomstkontroll kan du börja använda behörigheter på Adobe Experience Cloud i stället för produktprofiler i Adobe Admin Console för att hantera behörigheter för användare, funktioner, etiketter och andra resurser i din organisation.

Mer information om åtkomstkontroll finns i [åtkomstkontroll - översikt](../home.md).

### Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

Som administratör kan du använda attributbaserade åtkomstkontrollsfunktioner för att:

* Konfigurera användaråtkomst för att visa specifika segment i aktiveringsprocessen, baserat på roll, behörigheter och etiketter.
   * Under aktiveringsprocessen kan man behöva välja segment som man vill aktivera till ett mål. Som administratör kan du tilldela användare i organisationen att endast se segment som är märkta med etiketter som användare har tillgång till, och segment som inte innehåller några etiketter.
* Konfigurera användaråtkomst för att visa specifika fält i aktiveringsprocessen, baserat på roll, behörigheter och etiketter.
   * Under aktiveringsprocessen kan användaren behöva välja fält som ska aktiveras till ett mål. Som administratör kan du tilldela användare i din organisation behörighet att endast visa fält som är märkta med etiketter som användare har tillgång till och fält som inte innehåller några etiketter.

>[!IMPORTANT]
>
>Sammanfattningsvis bör du tänka på följande när du arbetar med mål och attributbaserad åtkomstkontroll:
>
>* Du kan bara aktivera segment som du har behörighet att komma åt och visa i [segmentsurfvy](/help/segmentation/ui/overview.md#browse) och [välj segmentsteg](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) aktiveringsarbetsflödet.
>* I [mappningssteg för aktiveringsarbetsflödet](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)kan du bara visa och välja de fält som du har behörighet till för aktivering.
>* När du vill aktivera ytterligare segment till ett befintligt mål där du inte har tillgång till alla fält som är mappade för export, blockeras aktiveringsarbetsflödet.


Mer information om [!DNL Destinations], se [[!DNL Destinations] översikt](../../destinations/home.md).

### Identitetstjänst

Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

Som en del av den attributbaserade åtkomstkontrollen har `view-identity-graph` Med -behörighet kan du avgöra vilka användare i organisationen som har tillgång till identitetsdiagrammet via användargränssnittet eller API:erna. Mer information finns i handboken på [med identitetsdiagramvisningsprogrammet](../../identity-service/ui/identity-graph-viewer.md).

Mer information om [!DNL Identity Service], se [[!DNL Identity Service] översikt](../../identity-service/home.md).

### Kundprofil i realtid

Plattformen gör att ni kan skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av en profil kan ni sammanställa olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

Som administratör kan du använda attributbaserade åtkomstkontrollsfunktioner för att:

* Konfigurera användaråtkomst till specifika profilattribut baserat på roll, behörigheter och etiketter.
   * Som administratör kan du tilldela användare i din organisation att endast se profilattribut som är märkta med etiketter som användare har tillgång till och profilattribut som inte innehåller någon etikett.
   * Som administratör kan du tilldela användare i organisationen att endast se profilattribut som är märkta med etiketter som användare har tillgång till när de skapar segment.
* Konfigurera användaråtkomst till dataförhandsgranskning genom att etikettera specifika datafält som används i datamodellens XDM-schema.

Mer information om profil finns i [Profilöversikt](../../profile/home.md).

### Segmenteringstjänst

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

Som administratör kan du använda attributbaserade åtkomstkontrollsfunktioner för att:

* Konfigurera användaråtkomst för att visa och hantera specifika segment utifrån roll, behörigheter och etiketter.
   * Som administratör kan du tilldela användare i organisationen att endast se segment som är märkta med etiketter som användare har tillgång till, och segment som inte innehåller några etiketter, när segmentgränssnittet används.

Mer information om [!DNL Segmentation Service], se [[!DNL Segmentation Service] översikt](../../segmentation/home.md).

### XDM

Experience Data Model (XDM) är en öppen källkodsspecifikation som är utformad för att förbättra kraften i digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på plattformen. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

Med attributbaserad åtkomstkontroll kan du

* [Tillämpa dataanvändningsetiketter på fältgrupper och klasser](../../xdm/tutorials/labels.md). Detta gör att flera scheman med samma fältgrupper eller klasser kan ha fält taggade med samma attribut, beroende på konfigurationen på fältgrupps- eller klassnivå.
* Konfigurera användaråtkomst till specifika XDM-schemafält beroende på vilka behörighetsgrupper som används för roller som tilldelats användare.

Mer information om XDM finns i [XDM - översikt](../../xdm/home.md).