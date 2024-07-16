---
keywords: Experience Platform;hem;populära ämnen;åtkomstkontroll;attributbaserad åtkomstkontroll;
title: Attributbaserad åtkomstkontroll - översikt
description: Det här dokumentet innehåller information om attributbaserad åtkomstkontroll i Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 0%

---

# Attributbaserad åtkomstkontroll - översikt {#attribute-based-access-control-overview}

>[!CONTEXTUALHELP]
>id="platform_accesscontrol_abac_labelusageaccesspolicy"
>title="Åtkomstprincip för etikettanvändning"
>abstract=""

Attributbaserad åtkomstkontroll är en funktion i Adobe Experience Platform som gör att administratörer kan styra åtkomsten till specifika objekt och/eller funktioner baserat på attribut. Attribut kan läggas till i ett objekt, t.ex. en etikett som lagts till i ett schemafält eller segment. En administratör definierar åtkomstprinciper som innehåller attribut för att hantera behörigheter för användaråtkomst.

Använd den här funktionen för att etikettera XDM-schemafält (Experience Data Model) med etiketter som definierar användningsområde för organisationen eller data. Samtidigt kan administratörer använda användar- och rolladministrationsgränssnittet för att definiera åtkomstprinciper runt XDM-schemafält och bättre hantera åtkomsten som ges till användare eller grupper av användare (interna, externa eller externa användare). Dessutom gör attributbaserad åtkomstkontroll det möjligt för administratörer att hantera åtkomsten till specifika segment.

>[!IMPORTANT]
>
>Attributbaserad åtkomstkontroll ska inte blandas ihop med Experience Platform datastyrningsfunktioner, som gör att du kan använda etiketter och policyer för att styra hur data används i plattformar i stället för vilka användare i organisationen har tillgång till dem. Mer information finns i [översikten över datastyrning](../../data-governance/home.md).

Med attributbaserad åtkomstkontroll kan administratören styra användarnas tillgång till känsliga personuppgifter (SPD), personligt identifierbar information (PII) och anpassad typ av data i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

Följande video är avsedd att ge stöd för din förståelse av attributbaserad åtkomstkontroll och visar hur du konfigurerar roller, resurser och principer.

>[!VIDEO](https://video.tv.adobe.com/v/345641?learn=on)

## Attributbaserad åtkomstkontrollterminologi

Attributbaserad åtkomstkontroll omfattar följande komponenter:

| Terminologi | Definition |
| --- | --- |
| Attribut | Attribut är de identifierare som anger korrelationen mellan en användare och de plattformsresurser som de har åtkomst till. Attribut kan läggas till i ett objekt, t.ex. en etikett som lagts till i ett schemafält eller segment. En administratör definierar åtkomstprinciper som innehåller attribut för att hantera behörigheter för användaråtkomst. |
| Etiketter | Med etiketter kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Etiketter kan användas när som helst, vilket ger flexibilitet i hur du väljer att styra data. Bästa praxis uppmuntrar till etikettdata så snart de har importerats till Platform, eller så snart data blir tillgängliga för användning i Platform. |
| Behörigheter | Behörigheter omfattar möjligheten att visa och/eller använda plattformsfunktioner, som att skapa sandlådor, definiera scheman och hantera datauppsättningar. |
| Behörighetsuppsättningar | Behörighetsuppsättningar representerar en grupp behörigheter som en administratör kan tillämpa på en roll. En administratör kan tilldela behörighetsgrupper till en roll i stället för att tilldela enskilda behörigheter. Detta gör att du kan skapa anpassade roller från en fördefinierad roll som innehåller en grupp behörigheter. |
| Policyer | Profiler är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Profiler kan antingen vara lokala eller globala och kan åsidosätta andra profiler. |
| Resurs | En resurs är den resurs eller det objekt som ett ämne kan eller inte kan komma åt. Resurser kan vara segment eller schemafält. |
| Roller | Roller är sätt att kategorisera de typer av användare som interagerar med din plattformsinstans och är byggstenar för åtkomstkontrollprinciper. I en rollbaserad miljö för åtkomstkontroll är etableringen av användaråtkomst grupperad genom vanliga ansvarsområden och behov. En roll har en given uppsättning behörigheter och medlemmar i organisationen kan tilldelas till en eller flera roller, beroende på vilket synområde eller vilken skrivbehörighet de behöver. |
| Ämne | Ett ämne är den användare som begär åtkomst till en resurs för att utföra en åtgärd. |
| Användargrupper | Användargrupper är flera användare som har grupperats tillsammans och har tillgång till samma funktioner. |

## Behörigheter

>[!IMPORTANT]
>
>När din organisation har aktiverats för attributbaserad åtkomstkontroll kan du börja använda behörigheter på Adobe Experience Cloud i stället för roller i Adobe Admin Console för att hantera behörigheter för användare, funktioner, etiketter och andra resurser i din organisation.

Behörigheter är det område i Experience Cloud där administratörer kan definiera användarroller och åtkomstprinciper för att hantera åtkomstbehörigheter för funktioner och objekt i ett produktprogram.

Genom Behörigheter kan du skapa och hantera roller samt tilldela önskade resursbehörigheter för dessa roller. Med behörigheter kan du också hantera etiketter, sandlådor och användare som är kopplade till en viss roll. Mer information finns i [Behörighetsguiden](ui/browse.md).

## Attributbaserad API för åtkomstkontroll

Med det attributbaserade API:t för åtkomstkontroll kan du programmässigt hantera roller, principer och produkter inom plattformen med API:er. Mer information finns i guiden om [att använda API:t för att hantera attributbaserade åtkomstkontrollskonfigurationer](api/overview.md).

## Attributbaserad åtkomstkontroll i Adobe Experience Platform

I följande avsnitt finns information om hur attributbaserad åtkomstkontroll är integrerad med andra plattformskomponenter:

### Åtkomstkontroll

Plattformen använder [Adobe Admin Console](https://adminconsole.adobe.com)-roller för att länka användare med behörigheter och sandlådor. Behörigheter styr åtkomsten till en mängd plattformsfunktioner, inklusive datamodellering, profilhantering och sandlådeadministration. När din organisation har aktiverats för attributbaserad åtkomstkontroll kan du börja använda behörigheter på Adobe Experience Cloud i stället för roller i Adobe Admin Console för att hantera behörigheter för användare, funktioner, etiketter och andra resurser i din organisation.

Det finns begränsad tillgång till attributbaserad åtkomstkontroll för kunder som köper hälso- och sjukvård och/eller sekretessrutiner. Funktionerna är följande:

* Behörighetsgränssnitt: Tillhandahåller ett gränssnitt där du kan definiera användarroller, behörigheter och profiler för attributbaserad åtkomstkontroll.

* Etikett: Lägg till, redigera, ta bort etiketter till användarroller, schemafält, segment och andra objekt som stöds för att utnyttja åtkomstkontrollprinciper. **Obs!** Alla segment som använder ett attribut med etikett måste också ha en etikett om du vill att samma åtkomstbegränsningar ska gälla för det.

Administrationsarbetsflödena för alla Experience Platform-baserade program från Admin Console till det nya behörighetsgränssnittet håller på att ändras.

>[!IMPORTANT]
>
>Dina roller migreras automatiskt till behörighetsgränssnittet när din organisation är aktiverad. Rollerna i Admin Console kommer att vara som de är tills vidare. **Ändra inte** dina roller när din organisation har aktiverats.

Mer information om åtkomstkontroll finns i [åtkomstkontrollsöversikten](../home.md).

### Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från plattformen. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

Som administratör kan du använda attributbaserade åtkomstkontrollsfunktioner för att:

* Konfigurera användaråtkomst för att visa specifika segment i aktiveringsprocessen, baserat på roll, behörigheter och etiketter.
   * Under aktiveringsprocessen kan man behöva välja segment som man vill aktivera till ett mål. Som administratör kan du tilldela användare i organisationen att endast se segment som är märkta med etiketter som användare har tillgång till, och segment som inte innehåller några etiketter.
* Konfigurera användaråtkomst för att visa specifika fält i aktiveringsprocessen, baserat på roll, behörigheter och etiketter.
   * Under aktiveringsprocessen kan användaren behöva välja fält som ska aktiveras till ett mål. Som administratör kan du tilldela användare i din organisation behörighet att endast visa fält som är märkta med etiketter som användare har tillgång till och fält som inte innehåller några etiketter.

>[!IMPORTANT]
>
>Sammanfattningsvis bör du tänka på följande när du arbetar med mål och attributbaserad åtkomstkontroll:
>
>* Du kan bara aktivera målgrupper som du har behörighet att komma åt och visa i [målportalen](/help/segmentation/ui/audience-portal.md#browse) och [välj segmentsteg](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) i aktiveringsarbetsflödet.
>* I [mappningssteget i aktiveringsarbetsflödet](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) kan du bara visa och välja de fält som du har behörighet till för aktivering.
>* När du vill aktivera ytterligare segment till ett befintligt mål där du inte har tillgång till alla fält som är mappade för export, blockeras aktiveringsarbetsflödet.

Mer information om [!DNL Destinations] finns i [[!DNL Destinations] översikten](../../destinations/home.md).

### Identitetstjänst

Adobe Experience Platform [!DNL Identity Service] hjälper dig att få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system, så att du kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

Som en del av den attributbaserade åtkomstkontrollen kan du med behörigheten `view-identity-graph` avgöra vilka användare i organisationen som har åtkomst till identitetsdiagrammet via användargränssnittet eller API:erna. Mer information finns i guiden om [att använda identitetsdiagramvisningsprogrammet](../../identity-service/features/identity-graph-viewer.md).

Mer information om [!DNL Identity Service] finns i [[!DNL Identity Service] översikten](../../identity-service/home.md).

### Kundprofil i realtid

Plattformen gör att ni kan skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av en profil kan ni sammanställa olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

Som administratör kan du använda attributbaserade åtkomstkontrollsfunktioner för att:

* Konfigurera användaråtkomst till specifika profilattribut baserat på roll, behörigheter och etiketter.
   * Som administratör kan du tilldela användare i din organisation att endast se profilattribut som är märkta med etiketter som användare har tillgång till och profilattribut som inte innehåller någon etikett.
   * Som administratör kan du tilldela användare i din organisation att endast se profilattribut som är märkta med etiketter som användare har tillgång till när de skapar segment.
* Konfigurera användaråtkomst till dataförhandsgranskning genom att etikettera specifika datafält som används i datamodellens XDM-schema.

Mer information om profil finns i [Profilöversikt](../../profile/home.md).

### Segmenteringstjänst

[!DNL Segmentation Service] definierar en viss delmängd av profiler genom att beskriva kriterierna som särskiljer en marknadsföringsbar grupp av personer inom din kundbas. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

Som administratör kan du använda attributbaserade åtkomstkontrollsfunktioner för att:

* Konfigurera användaråtkomst för att visa och hantera specifika segment utifrån roll, behörigheter och etiketter.
   * Som administratör kan du tilldela användare i organisationen att endast se segment som är märkta med etiketter som användare har tillgång till, och segment som inte innehåller några etiketter, när segmentgränssnittet används.

Mer information om [!DNL Segmentation Service] finns i [[!DNL Segmentation Service] översikten](../../segmentation/home.md).

### XML

Experience Data Model (XDM) är en öppen källkodsspecifikation som är utformad för att förbättra kraften i digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på plattformen. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

Med attributbaserad åtkomstkontroll kan du:

* [Använd dataanvändningsetiketter på fältgrupper och klasser](../../xdm/tutorials/labels.md). Detta gör att flera scheman med samma fältgrupper eller klasser kan ha fält taggade med samma attribut, beroende på konfigurationen på fältgrupps- eller klassnivå.
* Konfigurera användaråtkomst till specifika XDM-schemafält beroende på vilka behörighetsgrupper som används för roller som tilldelats användare.

Mer information om XDM finns i [XDM-översikten](../../xdm/home.md).