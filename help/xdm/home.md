---
keywords: Experience Platform;hem;populära ämnen;XDM;XDM system;XDM individuell profil;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event event;mixins;mixin;mixin;mixin;experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experience event;XDM ExperienceEvent;experience data model;Experience data model;Experience data model;datamodell;datamodell;schemaregister;schemaregister;schemabibliotek;schema;postdata;tidsserie;tidsserie
solution: Experience Platform
title: XDM - systemöversikt
topic: overview
description: 'Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering. '
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---


# XDM - systemöversikt

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Den innehåller gemensamma strukturer och definitioner för alla program som används för att kommunicera med [!DNL Platform]-tjänster. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som kan ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut i personaliseringssyfte.

XDM är det grundläggande ramverk som gör att Adobe Experience Cloud, som drivs av [!DNL Experience Platform], kan leverera rätt budskap till rätt person i rätt kanal vid exakt rätt tidpunkt. Metoden som [!DNL Experience Platform] byggs på, XDM System, opererar [!DNL Experience Data Model] scheman för användning av [!DNL Platform]-tjänster.

Det här dokumentet innehåller en översikt över XDM-systemets roll i [!DNL Experience Platform].

## XDM-scheman

[!DNL Experience Platform] använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till [!DNL Platform] måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera blandningar.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [grunderna för schemakomposition](schema/composition.md).

### [!DNL Schema Registry] och [!DNL Schema Library]

**[!DNL Schema Registry]** innehåller ett användargränssnitt och RESTful API från vilket du kan visa och hantera alla schemarelaterade resurser i Adobe Experience Platform **[!DNL Schema Library]**. [!DNL Schema Library] innehåller resurser som är branschstandard och som gjorts tillgängliga av Adobe, samt resurser från [!DNL Experience Platform] partners och leverantörer vars program du använder. Användargränssnittet och API:t för schemaregister kan också användas för att skapa och hantera nya scheman och resurser som är unika för din organisation.

En utförlig guide till de viktigaste åtgärderna i [!DNL Schema Registry] finns i [Utvecklarhandbok för schemaregister](api/getting-started.md).

## Databeteenden i XDM-systemet {#data-behaviors}

Data som är avsedda att användas i [!DNL Experience Platform] är grupperade i två beteendetyper:

* **Postdata**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **Tidsseriedata**: Ger en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av ett postämne.

Alla XDM-scheman beskriver data som kan kategoriseras som post- eller tidsserier. Databeteendet för ett schema definieras av schemats klass, som tilldelas till ett schema när det skapas första gången. XDM-klasser beskriver det minsta antal egenskaper ett schema måste innehålla för att representera ett visst databeteende.

Även om du kan definiera egna klasser i [!DNL Schema Registry] rekommenderar vi att du använder de klasser **[!DNL XDM Individual Profile]** och **[!DNL XDM ExperienceEvent]** som du föredrar för post- respektive tidsseriedata. Dessa klasser beskrivs mer ingående nedan.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] är en postbaserad klass som bildar en enda representation av attributen hos både identifierade och delvis identifierade ämnen. Profiler som är välidentifierade kan användas för personlig kommunikation eller målinriktade åtaganden och kan innehålla detaljerad personlig information som namn, kön, födelsedatum, plats och kontaktinformation, inklusive telefonnummer och e-postadresser.

Mindre identifierade profiler kan bara bestå av anonyma beteendesignaler, som webbläsarcookies. I det här fallet används data för den gles profil för att bygga upp en informationsbas i vilken den anonyma profilens intressen och preferenser samlas in och lagras. Dessa identifierare kan bli mer detaljerade över tid när ämnet registrerar sig för meddelanden, prenumerationer, inköp och så vidare. Ökningen av profilattribut kan så småningom leda till ett identifierat ämne och möjliggöra en högre grad av målinriktat engagemang.

I takt med att kundprofilen växer blir den ett robust arkiv för en persons personuppgifter, identifieringsinformation, kontaktuppgifter och kommunikationsinställningar.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent är en tidsseriebaserad klass som används för att fånga systemets tillstånd när en händelse (eller uppsättning händelser) inträffar, inklusive tidpunkten och identiteten för det berörda ämnet. Experience Events är fakta om vad som har hänt, och de är därför oföränderliga och representerar det som hände utan aggregering eller tolkning. De är viktiga för tidsdomänanalys eftersom de kan användas för att analysera ändringar som inträffar under ett visst tidsfönster och för att jämföra olika tidsfönster för att spåra trender.

Experience Events kan vara antingen explicita eller implicita. Explicit händelser är direkt observerbara mänskliga handlingar som äger rum under en viss resa. Implicita händelser är händelser som inträffar utan någon direkt mänsklig åtgärd, men som fortfarande gäller en individ. Exempel på implicita händelser kan vara schemalagd sändning av e-postnyhetsbrev eller batteriladdning som når en viss tröskel.

Även om det inte är lätt att kategorisera alla händelser över alla datakällor är det oerhört värdefullt att harmonisera liknande händelser i liknande typer där det är möjligt för behandling.

![ExperienceEvent - kundresa](images/overview/experience-event-journey.png)

## XDM-scheman och [!DNL Experience Platform]-tjänster

[!DNL Experience Platform] är schemagnostiska, vilket innebär att alla scheman som följer XDM-standarden är tillgängliga för användning av  [!DNL Platform] tjänster. De sätt som olika [!DNL Platform]-tjänster använder scheman beskrivs närmare nedan.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] är registersystemet för  [!DNL Experience Platform] tillgångar och tillhörande scheman. [!DNL Catalog] är inte de faktiska filerna eller katalogerna som innehåller data, utan innehåller i stället metadata och beskrivningar för dessa filer och kataloger.

[!DNL Catalog] data lagras i  [!DNL Data Lake]ett mycket detaljerat datalager som innehåller alla data som hanteras av,  [!DNL Platform]oavsett ursprung eller filformat.

För att börja inhämta data till [!DNL Experience Platform] skapas en datauppsättning med [!DNL Catalog Service]. Datauppsättningen refererar till ett XDM-schema som beskriver strukturen för de data som ska importeras. Om en datauppsättning skapas utan ett schema, kommer [!DNL Experience Platform] att härleda ett &quot;observerat schema&quot; genom att undersöka typen och innehållet i inkapslade datafält. Datauppsättningar spåras sedan i [!DNL Catalog] och lagras i [!DNL Data Lake] tillsammans med de scheman och observerade scheman som de baseras på.

Mer information om [!DNL Catalog] finns i [Katalogtjänstöversikt](../catalog/home.md). Mer information om Adobe Experience Platform datainmatning finns i [Översikt över datainmatning](../ingestion/home.md).

### [!DNL Query Service]

Med Adobe Experience Platform [!DNL Query Service] kan du använda standard-SQL för att fråga efter [!DNL Experience Platform]-data som stöder många olika användningsfall.

När ett schema har skapats och en datauppsättning har skapats som refererar till det schemat, hämtas data och lagras i [!DNL Data Lake]. Med [!DNL Query Service] kan du koppla alla datauppsättningar i [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller för förtäring i [!DNL Real-time Customer Profile].

Mer information om [!DNL Query Service] finns i [introduktionen av frågetjänsten](../query-service/home.md).

### [!DNL Real-time Customer Profile]

Kundprofilen i realtid utgör en centraliserad konsumentprofil för riktad och personaliserad upplevelsehantering. Varje profil innehåller data som aggregeras i alla system, samt användbara tidsstämplade konton med händelser som involverar den person som har inträffat i något av de system som du använder med [!DNL Experience Platform].

[!DNL Real-time Customer Profile] använder schemaformaterade data baserat på  [!DNL XDM Individual Profile] eller  [!DNL XDM ExperienceEvent] klasser och svarar på frågor som baseras på dessa data. [!DNL Profile] stöder inte användning av scheman baserade på andra klasser.

[!DNL Profile] har en instans av varje kundprofil och sammanfogar data för att skapa en&quot;enda källa till sanning&quot; för individen. Dessa enhetliga data representeras med hjälp av en s.k. fackvy. En unionsvy samlar fälten för alla scheman som implementerar samma klass i ett enda schema.  När du komponerar ett schema med användargränssnittet eller API:t kan du aktivera schemat för användning med [!DNL Real-time Customer Profile] och tagga det för inkludering i unionsvyn. Det taggade schemat deltar sedan i den schemadefinition som matas till [!DNL Profile].

Eftersom [!DNL XDM Individual Profile]- och [!DNL XDM ExperienceEvent]-data importeras och hanteras av [!DNL Catalog], utlöses [!DNL Real-time Customer Profile] för att börja inhämta data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

[!DNL XDM Individual Profile] data hjälper till att informera och underlätta åtgärder över alla kanaler och Adobe-lösningar, och när de kombineras med en lång historik med beteendedata och interaktionsdata används dessa data som stöd för maskininlärning. API:t [!DNL Real-time Customer Profile] kan även användas för att utöka funktionaliteten hos tredjepartslösningar, CRM-system och företagslösningar.

Mer information finns i [Kundprofilöversikt](../profile/home.md) i realtid.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i [!DNL Experience Platform]. [!DNL Data Science Workspace] gör det möjligt för datavetare att bygga recept som bygger på XDM Individual  [!DNL Profile] och  [!DNL XDM ExperienceEvent] data om kunder och deras aktiviteter, vilket underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen troligtvis uppskattar och använder.

Med [!DNL Data Science Workspace] kan datavetare enkelt skapa API:er för intelligenta tjänster som bygger på maskininlärning. Dessa tjänster fungerar tillsammans med andra Adobe-lösningar, inklusive Adobe Target och Adobe Analytics Cloud, och hjälper er att automatisera personaliserade, målinriktade digitala upplevelser.

Mer information om hur du använder [!DNL Experience Platform]-data för att ge bättre insikter finns i översikten över arbetsytan för datavetenskap](../data-science-workspace/home.md).[

## Nästa steg och ytterligare resurser

Nu när du är bättre på att förstå schemats roll i [!DNL Experience Platform] är du redo att börja skapa din egen. Om du vill fortsätta att komplettera din inlärning börjar du med att läsa den föreslagna dokumentationen och tittar på videon nedan.

Om du vill lära dig designprinciper och bästa metoder för att komponera scheman som ska användas med [!DNL Experience Platform] börjar du med att läsa [grunderna för schemakomposition](schema/composition.md). Stegvisa instruktioner om hur du skapar ett schema finns i självstudiekurserna om hur du skapar ett schema [med API](tutorials/create-schema-api.md) eller [med användargränssnittet](tutorials/create-schema-ui.md).

Titta på följande video för att få en bättre förståelse för [!DNL XDM System] i [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

