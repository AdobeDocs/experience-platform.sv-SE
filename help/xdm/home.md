---
keywords: Experience Platform;startsida;populära ämnen;XDM;XDM system;XDM individuell profil;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event;Field groups;field group;field group;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM ExperienceEvent;experience data model;Experience data model;Experience data model;datamodell;datamodell;schemaregister;schemaregister;schemabibliotek;schema;postdata;tidsserie;tidsserie
solution: Experience Platform
title: XDM - systemöversikt
description: Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 0%

---

# XDM - systemöversikt

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Den innehåller gemensamma strukturer och definitioner som gör att alla program kan kommunicera med plattformstjänster. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som kan ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut i personaliseringssyfte.

XDM är det grundläggande ramverk som gör att Adobe Experience Cloud, som drivs av Experience Platform, kan leverera rätt budskap till rätt person, i rätt kanal, i precis rätt ögonblick. Metoden som Experience Platform bygger på, XDM System, är operativt [!DNL Experience Data Model] scheman för användning av plattformstjänster.

Detta dokument ger en översikt över XDM-systemets roll i Experience Platform.

## XDM-scheman

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera schemafältgrupper.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [grunderna för schemakomposition](schema/composition.md).

### Standard-XDM-komponenter

XDM erbjuder en robust samling av standardfältgrupper och datatyper, som är avsedda att fånga upp vanliga koncept och användningsfall i olika branscher. Med Experience Platform kan ni filtrera komponenterna efter bransch, så att ni snabbt och säkert kan skapa scheman som passar just era affärsbehov.

När du skapar scheman i användargränssnittet i Experience Platform visas listade fältgrupper med ett popularitetsmått. Detta mått bestäms av hur ofta andra plattformsanvändare använder fältgruppen i sina scheman. Ju högre tal, desto populärare fältgrupp. Som standard visas resultaten från de mest populära till de minst populära och håller dig informerad om trender för datamodellering i din bransch.

![Fältgrupppopularitet](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform har ett användargränssnitt och RESTful API från vilket du kan visa och hantera alla schemarelaterade resurser i Experience Platform **[!DNL Schema Library]**. The [!DNL Schema Library] innehåller XDM-standardkomponenter som Adobe har gjort tillgängliga för dig, samt resurser från partners och leverantörer i Experience Platform vars program du använder.

Använda [!DNL Schema Registry API] eller [!UICONTROL Schemas] i plattformsgränssnittet kan du också skapa och hantera nya scheman och resurser som är unika för din organisation.

Mer information om hur du hanterar och interagerar med scheman i Platform finns i följande dokumentation:

* [Användargränssnittshandbok för XDM](./ui/overview.md)
* [API-guide för schemaregister](./api/overview.md)

## Databeteenden i XDM-system {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Databeteenden"
>abstract="Data som är avsedda att användas i Experience Platform är indelade i tre beteendetyper: spela in, tidsserier och ad hoc. Registreringsscheman ger information om attributen för ett motiv, medan tidsseriescheman tar en ögonblicksbild av systemet när en åtgärd vidtas. Ad hoc-scheman hämtar fält som är namnutrymmen som bara kan användas av en enskild datauppsättning. Mer information om databeteenden i Platform finns i dokumentationen."

Data som är avsedda att användas i Experience Platform är indelade i tre beteendetyper:

* **Post**: Innehåller information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **Tidsserie**: Ger en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av ett postämne.
* **Ad hoc**: Hämtar fält som namnges för användning endast av en enda datauppsättning. Ad-hoc-scheman används i olika arbetsflöden för dataöverföring för Experience Platform, inklusive inhämtning av CSV-filer och skapande av vissa typer av källanslutningar.

Alla XDM-scheman beskriver data som kan kategoriseras som post- eller tidsserier. Databeteendet för ett schema definieras av schemats klass, som tilldelas till ett schema när det skapas första gången. XDM-klasser beskriver det minsta antal egenskaper ett schema måste innehålla för att representera ett visst databeteende.

Även om du kan definiera egna klasser i [!DNL Schema Registry]rekommenderar vi att du använder standardklasserna **[!UICONTROL XDM Individual Profile]** och **[!UICONTROL XDM ExperienceEvent]** för post- respektive tidsseriedata. Dessa klasser beskrivs mer ingående nedan.

>[!NOTE]
>
>Det finns inga standardklasser baserade på ad hoc-beteendet. Ad hoc-scheman genereras automatiskt av de plattformsprocesser som använder dem, men de kan också [skapas manuellt med API:t för schemaregister](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] är en postbaserad klass som bildar en enda representation av attributen hos både identifierade och delvis identifierade ämnen. Profiler som är välidentifierade kan användas för personlig kommunikation eller målinriktade åtaganden och kan innehålla detaljerad personlig information som namn, kön, födelsedatum, plats och kontaktinformation, inklusive telefonnummer och e-postadresser.

Mindre identifierade profiler kan bara bestå av anonyma beteendesignaler, som webbläsarcookies. I det här fallet används data för den gles profil för att bygga upp en informationsbas i vilken den anonyma profilens intressen och preferenser samlas in och lagras. Dessa identifierare kan bli mer detaljerade över tid när ämnet registrerar sig för meddelanden, prenumerationer, inköp och så vidare. Ökningen av profilattribut kan så småningom leda till ett identifierat ämne och möjliggöra en högre grad av målinriktat engagemang.

I takt med att profilen växer blir den ett robust arkiv för en persons personuppgifter, identifieringsinformation, kontaktuppgifter och kommunikationsinställningar.

Se [[!UICONTROL XDM Individual Profile] referenshandbok](./classes/individual-profile.md) om du vill ha mer information om strukturen och användningsfallet för fälten som klassen tillhandahåller.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent är en tidsseriebaserad klass som används för att fånga systemets tillstånd när en händelse (eller uppsättning händelser) inträffar, inklusive tidpunkten och identiteten för det berörda ämnet. Experience Events är oföränderliga, faktauppgifter om vad som inträffade vid den tidpunkten, som representerar det som hände utan aggregering eller tolkning. De är viktiga för tidsdomänanalys eftersom de kan användas för att analysera ändringar som inträffar under ett visst tidsfönster och för att jämföra olika tidsfönster för att spåra trender.

Experience Events kan vara antingen explicita eller implicita. Explicit händelser är direkt observerbara mänskliga handlingar som äger rum under en viss resa. Implicita händelser är händelser som inträffar utan någon direkt mänsklig åtgärd, men som fortfarande gäller en individ. Exempel på implicita händelser kan vara schemalagd sändning av e-postnyhetsbrev eller batteriladdning som når en viss tröskel.

Även om det inte är lätt att kategorisera alla händelser över alla datakällor är det oerhört värdefullt att harmonisera liknande händelser i liknande typer där det är möjligt för behandling.

![ExperienceEvent - kundresa](images/overview/experience-event-journey.png)

Se [[!UICONTROL XDM ExperienceEvent] referenshandbok](./classes/experienceevent.md) om du vill ha mer information om strukturen och användningsfallet för fälten som klassen tillhandahåller.

## XDM-scheman och Experience Platform-tjänster

Experience Platform är schemagnostiskt, vilket innebär att alla scheman som uppfyller XDM-standarden görs tillgängliga för plattformstjänster. Hur olika plattformstjänster använder scheman beskrivs närmare nedan.

### Katalogtjänst, datainmatning och datasjön

Katalogtjänsten är registersystemet för tillgångar i Experience Platform och tillhörande scheman. Katalogen innehåller inte de faktiska datafilerna eller katalogerna, utan innehåller i stället metadata och beskrivningar för dessa filer och kataloger.

Katalogdata lagras i Data Lake, ett mycket detaljerat datalager som innehåller alla data som hanteras av Platform, oavsett ursprung eller filformat.

Om du vill börja inhämta data till Experience Platform kan du använda katalogtjänsten för att skapa en datauppsättning. Datauppsättningen refererar till ett XDM-schema som beskriver strukturen för de data som ska importeras. Om en datauppsättning skapas utan ett schema, härleds ett &quot;observerat schema&quot; från Experience Platform genom att typen och innehållet i inkapslade datafält kontrolleras. Datauppsättningar spåras sedan i Catalog och lagras i Data Lake tillsammans med de scheman och observerade scheman som de baseras på.

Mer information om Katalog finns i [Katalogtjänst - översikt](../catalog/home.md). Mer information om Adobe Experience Platform datainmatning finns i [Översikt över datainmatning](../ingestion/home.md).

### Frågetjänst

Med Adobe Experience Platform Query Service kan du använda standard-SQL för att fråga efter Experience Platform-data som stöder många olika användningsfall.

När ett schema har disponerats och en datauppsättning har skapats som refererar till det schemat, hämtas data och lagras i datasjön. Med hjälp av frågetjänsten kan du ansluta till alla datauppsättningar i datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller för förtäring i realtidskundprofil.

Se [Översikt över frågetjänsten](../query-service/home.md) för mer information om tjänsten.

### Kundprofil i realtid

Kundprofilen i realtid är en centraliserad konsumentprofil för riktad och personaliserad upplevelsehantering. Varje profil innehåller data som aggregeras över alla system, samt användbara tidsstämplade konton med händelser som involverar den person som har inträffat i något av de system som du använder med Experience Platform.

Kundprofilen i realtid förbrukar schemaformaterade data baserat på [!UICONTROL XDM Individual Profile] och [!UICONTROL XDM ExperienceEvent] och svarar på frågor som baseras på dessa data. Profilen stöder inte användning av scheman baserade på andra klasser.

Systemet upprätthåller en instans av varje kundprofil och sammanfogar data till en&quot;enda källa till sanning&quot; för den enskilda personen. Dessa enhetliga data representeras med hjälp av ett så kallat fackschema (kallas ibland för en fackvy). Ett unionsschema samlar fälten för alla scheman som implementerar samma klass i ett enda schema.  När du komponerar ett schema med användargränssnittet eller API kan du aktivera schemat för användning med kundprofilen i realtid och tagga det för inkludering i unionen. Det taggade schemat kommer sedan att ingå i den schemadefinition som matas in i profilen.

Som [!UICONTROL XDM Individual Profile] och [!UICONTROL XDM ExperienceEvent] data hämtas in i datasjön, medan kundprofilen i realtid innehåller data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

[!UICONTROL XDM Individual Profile] data hjälper till att informera och underlätta åtgärder över alla kanaler och Adobe-produktintegreringar. När dessa data kombineras med en lång historik med beteendedata och interaktionsdata kan de användas för att underlätta maskininlärning. Real-Time Customer Profile API kan också användas för att utöka funktionaliteten hos tredjepartslösningar, CRM och företagslösningar.

Se [Översikt över kundprofiler i realtid](../profile/home.md) för mer information.

### Datavetenskapens arbetsyta

Adobe Experience Platform Data Science Workspace använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i Experience Platform. Med Data Science Workspace kan datavetare skapa recept som bygger på [!UICONTROL XDM Individual Profile] och [!UICONTROL XDM ExperienceEvent] data om kunder och deras aktiviteter, vilket underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen troligtvis kommer att uppskatta och använda.

Med Data Science Workspace kan datavetare enkelt skapa intelligenta tjänst-API:er som bygger på maskininlärning. Dessa tjänster fungerar tillsammans med andra Adobe-lösningar, inklusive Adobe Target och Adobe Analytics Cloud, och hjälper er att automatisera personaliserade, målinriktade digitala upplevelser.

Mer information om hur du använder data från Experience Platform för att ge bättre insikter finns i [Översikt över arbetsytan Datavetenskap](../data-science-workspace/home.md).

## Nästa steg och ytterligare resurser

Nu när du är bättre på att förstå schemats roll i hela Experience Platform är du redo att börja komponera ditt eget.

Börja med att läsa [grunderna för schemakomposition](schema/composition.md). Stegvisa instruktioner om hur du skapar ett schema finns i självstudiekurserna om hur du skapar ett schema [med API](tutorials/create-schema-api.md) eller [med användargränssnittet](tutorials/create-schema-ui.md).

För att förstärka er förståelse för [!DNL XDM System] i Experience Platform: se följande video:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
