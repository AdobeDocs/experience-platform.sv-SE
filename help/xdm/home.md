---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Experience Data Model (XDM) System
topic: overview
translation-type: tm+mt
source-git-commit: 8ea3b09f86fe11ce7043f22c56ff9756b909e716
workflow-type: tm+mt
source-wordcount: '1777'
ht-degree: 0%

---


# XDM - systemöversikt

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som används för att kommunicera med Platform tjänster. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som kan ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut i personaliseringssyfte.

XDM är det grundläggande ramverk som gör att Adobe Experience Cloud, som drivs av Experience Platform, kan leverera rätt budskap till rätt person i rätt kanal vid exakt rätt tidpunkt. Metoden som Experience Platform bygger på, **XDM System**, används för att göra Experience Data Model-scheman tillgängliga för Platform-tjänster.

Detta dokument ger en översikt över XDM-systemets roll i Experience Platform.

## XDM-scheman

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera blandningar.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa metoder, finns i [grunderna för schemakomposition](schema/composition.md).

### Schemaregister och schemabibliotek

I **schemaregistret** finns ett användargränssnitt och RESTful API som du kan använda för att visa och hantera alla schemarelaterade resurser i **schemabiblioteket** i Adobe Experience Platform. Schemabiblioteket innehåller standardresurser från Adobe och resurser från Experience Platform partners och leverantörer vars program du använder. Användargränssnittet och API:t för schemaregister kan också användas för att skapa och hantera nya scheman och resurser som är unika för din organisation.

En utförlig guide till de större åtgärder som är tillgängliga i schemaregistret finns i Utvecklarhandbok [för](api/getting-started.md)schemaregister.

## Databeteenden i XDM-system {#data-behaviors}

Data som är avsedda att användas i Experience Platform är grupperade i två beteendetyper:

* **Postdata**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **Tidsseriedata**: Ger en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av ett postämne.

Alla XDM-scheman beskriver data som kan kategoriseras som post- eller tidsserier. Databeteendet för ett schema definieras av schemats **klass**, som tilldelas ett schema när det skapas för första gången. XDM-klasser beskriver det minsta antal egenskaper ett schema måste innehålla för att representera ett visst databeteende.

Även om du kan definiera egna klasser i schemaregistret rekommenderar vi att du använder de önskade klasserna **XDM Individual Profile** och **XDM ExperienceEvent** för post- respektive tidsseriedata. Dessa klasser beskrivs mer ingående nedan.

### Individuell XDM-profil

XDM Individual Profile är en postbaserad klass som bildar en unik representation av attributen för både identifierade och delvis identifierade ämnen. Profiler som är välidentifierade kan användas för personlig kommunikation eller målinriktade åtaganden och kan innehålla detaljerad personlig information som namn, kön, födelsedatum, plats och kontaktinformation, inklusive telefonnummer och e-postadresser.

Mindre identifierade profiler kan bara bestå av anonyma beteendesignaler, som webbläsarcookies. I det här fallet används data för den gles profil för att bygga upp en informationsbas i vilken den anonyma profilens intressen och preferenser samlas in och lagras. Dessa identifierare kan bli mer detaljerade över tid när ämnet registrerar sig för meddelanden, prenumerationer, inköp och så vidare. Ökningen av profilattribut kan så småningom leda till ett identifierat ämne och möjliggöra en högre grad av målinriktat engagemang.

I takt med att kundprofilen växer blir den ett robust arkiv för en persons personuppgifter, identifieringsinformation, kontaktuppgifter och kommunikationsinställningar.

### XDM ExperienceEvent

XDM ExperienceEvent är en tidsseriebaserad klass som används för att fånga systemets tillstånd när en händelse (eller uppsättning händelser) inträffar, inklusive tidpunkten och identiteten för det berörda ämnet. Experience Events är fakta om vad som har hänt, och de är därför oföränderliga och representerar det som hände utan aggregering eller tolkning. De är viktiga för tidsdomänanalys eftersom de kan användas för att analysera ändringar som inträffar under ett visst tidsfönster och för att jämföra olika tidsfönster för att spåra trender.

Experience Events kan vara antingen explicita eller implicita. Explicit händelser är direkt observerbara mänskliga handlingar som äger rum under en viss resa. Implicita händelser är händelser som inträffar utan någon direkt mänsklig åtgärd, men som fortfarande gäller en individ. Exempel på implicita händelser kan vara schemalagd sändning av e-postnyhetsbrev eller batteriladdning som når en viss tröskel.

Även om det inte är lätt att kategorisera alla händelser över alla datakällor är det oerhört värdefullt att harmonisera liknande händelser i liknande typer där det är möjligt för behandling.

![ExperienceEvent - kundresa](images/overview/experience-event-journey.png)

## XDM-scheman och Experience Platform-tjänster

Experience Platform är schemagnostikerat, vilket innebär att alla scheman som uppfyller XDM-standarden är tillgängliga för användning av Platform tjänster. Hur olika Platform-tjänster använder scheman beskrivs närmare nedan.

### Katalogtjänst, datainmatning och datasjön

Katalogtjänsten är registersystemet för tillgångar i Experience Platform och tillhörande scheman. Katalogen är inte de filer eller kataloger som innehåller data, utan den innehåller metadata och beskrivningar för dessa filer och kataloger.

Katalogdata lagras i Data Lake, ett mycket detaljerat datalager som innehåller alla data som hanteras av Platform, oavsett ursprung eller filformat.

För att börja inhämta data till Experience Platform skapas en datauppsättning med hjälp av katalogtjänsten. Datauppsättningen refererar till ett XDM-schema som beskriver strukturen för de data som ska importeras. Om en datauppsättning skapas utan ett schema, kommer Experience Platform att härleda ett &quot;observerat schema&quot; genom att undersöka typen och innehållet i inkapslade datafält. Datauppsättningar spåras sedan i Catalog och lagras i Data Lake tillsammans med de scheman och observerade scheman som de baseras på.

Mer information om katalog finns i [Katalogtjänstöversikt](../catalog/home.md). Mer information om datainmatning i Adobe Experience Platform finns i översikten över [datainmatning](../ingestion/home.md).

### Frågetjänst

Med Adobe Experience Platform Query Service kan du använda standard-SQL för att fråga efter Experience Platform-data som stöder många olika användningsfall.

När ett schema har disponerats och en datauppsättning har skapats som refererar till det schemat, hämtas data och lagras i datasjön. Med hjälp av frågetjänsten kan du ansluta till alla datauppsättningar i datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller för förtäring i kundprofilen i realtid.

Mer information om frågetjänsten finns i introduktionen till [frågetjänsten](../query-service/home.md).

### Kundprofil i realtid

Kundprofilen i realtid utgör en centraliserad konsumentprofil för riktad och personaliserad upplevelsehantering. Varje profil innehåller data som aggregeras över alla system, samt användbara tidsstämplade konton med händelser som involverar den person som har inträffat i något av de system som du använder med Experience Platform.

Kundprofilen i realtid använder schemaformaterade data baserat på klasserna XDM Individual Profile eller XDM ExperienceEvent och svarar på frågor baserade på dessa data. Profilen stöder inte användning av scheman baserade på andra klasser.

Profilen bevarar en instans av varje kundprofil och sammanfogar data till en&quot;enda källa till sanning&quot; för den enskilda personen. Dessa enhetliga data representeras med hjälp av en s.k. fackvy. En unionsvy samlar fälten för alla scheman som implementerar samma klass i ett enda schema.  När du komponerar ett schema med användargränssnittet eller API kan du aktivera schemat för användning med kundprofilen i realtid och tagga det för inkludering i unionsvyn. Det taggade schemat kommer sedan att ingå i den schemadefinition som matas in i profilen.

När enskilda XDM-profiler och XDM ExperienceEvent-data hämtas och hanteras av Catalog, aktiveras kundprofilen i realtid för att börja inhämta data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

XDM Individuella profildata hjälper till att informera om och möjliggöra åtgärder över alla kanaler eller Adobe-lösningar, och tillsammans med en lång historik med beteendedata och interaktionsdata används dessa data för att underlätta maskininlärning. Real-time Customer Profile API kan också användas för att berika funktionaliteten hos tredjepartslösningar, CRM och företagslösningar.

Mer information finns i [Kundprofilöversikt](../profile/home.md) i realtid.

### Datavetenskapens arbetsyta

Adobe Experience Platform Data Science Workspace använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i Experience Platform. Med Data Science Workspace kan datavetare skapa recept som baseras på enskilda XDM-profiler och XDM ExperienceEvent-data om kunder och deras aktiviteter, vilket underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen troligtvis uppskattar och använder.

Med Data Science Workspace kan datavetare enkelt skapa API:er för intelligenta tjänster som bygger på maskininlärning. Dessa tjänster fungerar tillsammans med andra Adobe-lösningar, inklusive Adobe Target och Adobe Analytics Cloud, och hjälper er att automatisera personaliserade, målinriktade digitala upplevelser.

Mer information om hur du använder data från Experience Platform för att få bättre insikter finns i översikten över arbetsytan för [datavetenskap](../data-science-workspace/home.md).

### Beslutstjänst

Beslutstjänsten ger möjlighet att konfigurera personaliserade offertbeslut i Platform-integrerade program. Erbjudandena kan vara produktrekommendationer, innehållskomponenter för en webbupplevelse, konversationsskript och åtgärder som ska vidtas.

Beslutstjänsten utnyttjar kundprofildata i realtid och är därför endast kompatibel med datauppsättningar baserade på scheman som implementerar den enskilda XDM-profilen eller klassen XDM ExperienceEvent.

Mer information finns i översikten över [](../decisioning-service/home.md) beslutstjänsten.

## Nästa steg och ytterligare resurser

Nu när du är bättre på att förstå schemats roll i hela Experience Platform är du redo att börja komponera ditt eget. Om du vill fortsätta att komplettera din inlärning börjar du med att läsa den föreslagna dokumentationen och tittar på videon nedan.

Om du vill lära dig designprinciper och bästa metoder för att komponera scheman som ska användas med Experience Platform börjar du med att läsa [grunderna för schemakomposition](schema/composition.md). Stegvisa instruktioner om hur du skapar ett schema finns i självstudiekurserna om hur du skapar ett schema [med API](tutorials/create-schema-api.md) eller [med användargränssnittet](tutorials/create-schema-ui.md).

Titta på följande video för att få en bättre förståelse för XDM System i Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

