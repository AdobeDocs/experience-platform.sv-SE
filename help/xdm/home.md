---
keywords: Experience Platform;home;populära topics;XDM;XDM system;XDM individuell profil;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event;Field groups;field group;field group;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM ExperienceEvent;experience data model;Experience data model;Experience data model;Experience data model;Experience data model;experience model datamodell;datamodell;schemaregister;schemaregister;schemabibliotek;schema;postdata;tidsserie;tidsserie
solution: Experience Platform
title: XDM - systemöversikt
description: Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 7527732c91e55f6ffaefbf98c37a2c4aad3aa3b9
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 0%

---

# XDM - systemöversikt

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Här finns gemensamma strukturer och definitioner som gör att alla program kan kommunicera med Experience Platform tjänster. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som kan ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut i personaliseringssyfte.

XDM är det grundläggande ramverk som gör att Adobe Experience Cloud, som drivs av Experience Platform, kan leverera rätt budskap till rätt person, i rätt kanal, i precis rätt ögonblick. Metoden som Experience Platform bygger på, XDM System, använder Experience Data Model-scheman för Experience Platform tjänster.

Läs om XDM-systemets roll i Experience Platform.

## XDM-scheman {#xdm-schemas}

Experience Platform använder scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt. Genom att definiera data på ett enhetligt sätt i olika system blir det enklare att behålla sin betydelse och därmed få värde av data.

Innan data kan hämtas in till Experience Platform måste ett schema sättas samman för att beskriva datastrukturen och tillhandahålla begränsningar för den typ av data som kan finnas i varje fält. Scheman består av en basklass och noll eller flera schemafältgrupper.

Mer information om schemakompositionsmodellen, inklusive designprinciper och bästa praxis, finns i [Grunderna för schemakomposition](schema/composition.md).

### Standard-XDM-komponenter {#Standard-xdm-components}

XDM erbjuder en robust samling av standardfältgrupper och datatyper, som är avsedda att fånga upp vanliga koncept och användningsfall i olika branscher. Med Experience Platform kan ni filtrera komponenterna efter bransch, så att ni snabbt och säkert kan skapa scheman som passar just era behov.

När du skapar scheman i användargränssnittet i Experience Platform visas listade fältgrupper med ett popularitetsmått. Detta mått bestäms av hur ofta andra Experience Platform-användare använder fältgruppen i sina scheman. Ju högre tal, desto populärare fältgrupp. Som standard visas resultaten från de mest populära till de minst populära och håller dig informerad om trender för datamodellering i din bransch.

![Popularitetskolumnen i dialogrutan [!UICONTROL Add field group].](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

Experience Platform tillhandahåller ett användargränssnitt och RESTful API från vilket du kan visa och hantera alla schemarelaterade resurser i Experience Platform **[!DNL Schema Library]**. [!DNL Schema Library] innehåller XDM-standardkomponenter som har gjorts tillgängliga av Adobe, samt resurser från Experience Platform partners och leverantörer vars program du använder.

Du kan också skapa och hantera nya scheman och resurser som är unika för din organisation med arbetsytan [!DNL Schema Registry API] eller [!UICONTROL Schemas] i Experience Platform-gränssnittet.

Mer information om hur du hanterar och interagerar med scheman i Experience Platform finns i följande dokumentation:

* [Användargränssnittshandbok för XDM](./ui/overview.md)
* [API-guide för schemaregister](./api/overview.md)

## Databeteenden i XDM-system {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Databeteenden"
>abstract="Data som är avsedda att användas i Experience Platform är grupperade i tre beteendetyper: post, tidsserie och ad hoc. Registreringsscheman ger information om attributen för ett motiv, medan tidsseriescheman tar en ögonblicksbild av systemet när en åtgärd vidtas. Ad hoc-scheman hämtar fält som namnges för att endast användas av en enskild datauppsättning. Mer information om databeteenden i Experience Platform finns i dokumentationen."

Data som är avsedda att användas i Experience Platform är grupperade i tre beteendetyper:

* **Post**: Anger information om attributen för ett ämne. Ett ämne kan vara en organisation eller individ.
* **Tidsserie**: Ger en ögonblicksbild av systemet när en åtgärd vidtas, antingen direkt eller indirekt, av ett postämne.
* **Ad-hoc**: Hämtar fält som endast namnges för användning av en enskild datauppsättning. Ad-hoc-scheman används i olika arbetsflöden för dataöverföring för Experience Platform, inklusive inhämtning av CSV-filer och skapande av vissa typer av källanslutningar.

Alla XDM-scheman beskriver data som kan kategoriseras som post- eller tidsserier. Databeteendet för ett schema definieras av schemats klass, som tilldelas till ett schema när det skapas första gången. XDM-klasser beskriver det minsta antal egenskaper ett schema måste innehålla för att representera ett visst databeteende.

Även om du kan definiera egna klasser i [!DNL Schema Registry] rekommenderar vi att du använder standardklasserna **[!UICONTROL XDM Individual Profile]** och **[!UICONTROL XDM ExperienceEvent]** för post- respektive tidsseriedata. Dessa klasser beskrivs mer ingående nedan.

>[!NOTE]
>
>Det finns inga standardklasser baserade på ad hoc-beteendet. Ad hoc-scheman genereras automatiskt av de Experience Platform-processer som använder dem, men de kan också [skapas manuellt med API:t för schemaregister](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] är en postbaserad klass som bildar en unik representation av attributen för både identifierade och delvis identifierade ämnen. Profiler som är välidentifierade kan användas för personlig kommunikation eller målinriktade åtaganden. Välidentifierade profiler kan innehålla detaljerad personlig information som namn, kön, födelsedatum, plats och kontaktinformation, inklusive telefonnummer och e-postadresser.

Mindre identifierade profiler kan bara bestå av anonyma beteendesignaler, som webbläsarcookies. I det här fallet används data för den gles profil för att bygga upp en informationsbas i vilken den anonyma profilens intressen och preferenser samlas in och lagras. Dessa identifierare kan bli mer detaljerade över tid när ämnet registrerar sig för meddelanden, prenumerationer, inköp och så vidare. Ökningen av profilattribut kan så småningom leda till ett identifierat ämne och möjliggöra en högre grad av målinriktat engagemang.

I takt med att profilen växer blir den ett robust arkiv för en persons personuppgifter, identifieringsinformation, kontaktuppgifter och kommunikationsinställningar.

Mer information om struktur och skiftläge för fälten som tillhandahålls av klassen finns i [[!UICONTROL XDM Individual Profile]-referenshandboken &#x200B;](./classes/individual-profile.md).

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent är en tidsseriebaserad klass som används för att fånga systemets tillstånd när en händelse (eller uppsättning händelser) inträffar, inklusive tidpunkten och identiteten för det berörda ämnet. Experience Events är oföränderliga, faktauppgifter om vad som inträffade vid den tidpunkten, som representerar det som hände utan aggregering eller tolkning. De är viktiga för tidsdomänanalys eftersom de kan användas för att analysera ändringar som inträffar under ett visst tidsfönster och för att jämföra olika tidsfönster för att spåra trender.

Experience Events kan vara antingen explicita eller implicita. Explicit händelser är direkt observerbara mänskliga handlingar som äger rum under en viss resa. Implicita händelser är händelser som inträffar utan någon direkt mänsklig åtgärd, men som fortfarande gäller en individ. Exempel på implicita händelser kan vara schemalagd sändning av e-postnyhetsbrev eller batteriladdning som når en viss tröskel.

Även om det inte är lätt att kategorisera alla händelser över alla datakällor är det oerhört värdefullt att harmonisera liknande händelser i liknande typer där det är möjligt för behandling.

![En infografik av kundresan visualiserad med upplevelsehändelser över tid.](images/overview/experience-event-journey.png)

Mer information om struktur och skiftläge för fälten som tillhandahålls av klassen finns i [[!UICONTROL XDM ExperienceEvent]-referenshandboken &#x200B;](./classes/experienceevent.md).

## XDM-scheman och Experience Platform-tjänster {#schemas-and-platform-services}

Experience Platform är schemagnostiskt, vilket innebär att alla scheman som uppfyller XDM-standarden görs tillgängliga för Experience Platform tjänster. Hur olika Experience Platform-tjänster använder scheman beskrivs närmare nedan.

### Katalogtjänst, datainmatning och datasjön {#ingestion-catalog-and-storage}

Katalogtjänsten är registersystemet för Experience Platform-resurser och tillhörande scheman. Katalogen innehåller inte de faktiska datafilerna eller katalogerna, utan innehåller i stället metadata och beskrivningar för dessa filer och kataloger.

Katalogdata lagras i datasjön, ett mycket detaljerat datalager som innehåller alla data som hanteras av Experience Platform, oavsett ursprung eller filformat.

Om du vill börja inhämta data till Experience Platform kan du använda katalogtjänsten för att skapa en datauppsättning. Datauppsättningen refererar till ett XDM-schema som beskriver strukturen för de data som ska importeras. Om en datauppsättning skapas utan ett schema, härleds ett &quot;observerat schema&quot; av Experience Platform genom att typen och innehållet i inkapslade datafält kontrolleras. Datauppsättningar spåras sedan i katalogtjänsten och lagras i datasjön tillsammans med de scheman och observerade scheman som de baseras på.

Mer information finns i [Katalogtjänstöversikt](../catalog/home.md). Mer information om Adobe Experience Platform datainmatning finns i [Översikt över datainmatning](../ingestion/home.md).

### Data Mirror och modellbaserade scheman {#model-based-schemas}

>[!AVAILABILITY]
>
>Data Mirror och modellbaserade scheman är tillgängliga för innehavare av Adobe Journey Optimizer **samordnade kampanjer**. De är också tillgängliga som en **begränsad version** för Customer Journey Analytics-användare, beroende på din licens och aktivering av funktioner. Kontakta din Adobe-representant för att få åtkomst.

Data Mirror är en Adobe Experience Platform-funktion som möjliggör avancerad databassynkronisering med modellbaserade scheman. En fullständig översikt över Data Mirror funktioner och användningsexempel finns i [Data Mirror-översikten](./data-mirror/overview.md).

Data Mirror använder modellbaserade scheman som är utformade för strukturerade, relationella datamönster. De använder primärnycklar, ID:n för supportversion och definierar relationer mellan schema och schema med hjälp av primära och externa nycklar. Till skillnad från vanliga XDM-scheman kräver de inte klasser eller fältgrupper och är optimerade för arbetsflöden för inhämtning av ändringsdata.

Mer information om hur du definierar scheman-till-schema-relationer finns i [deskriptorns slutpunktsdokumentation](./api/descriptors.md).

Använd Data Mirror när du behöver:

* Synkronisera dataändringar från externa system som Snowflake, Databricks eller BigQuery
* Bevara databasrelationerna och bevara dataintegriteten vid inmatning
* Stöd för avancerad analys och resesamordning
* Aktivera exakt ändringsspårning med överföringar och borttagningar

Om du vill skapa ett modellbaserat schema väljer du **[!UICONTROL model-based]** när du skapar ett schema. Modellbaserade scheman använder inte klasser eller fältgrupper. I stället definierar du strukturen manuellt eller överför en DDL-fil. Modellbaserade scheman kräver en primärnyckel, versionsidentifierare och, om tillämpligt, tidsstämpelidentifierarfält. Sedan kan du konfigurera ytterligare fält och definiera relationer med andra scheman.

>[!NOTE]
>
>Kontrollkolumner som används vid inmatning (till exempel `_change_request_type` för arbetsflöden för registrering av ändringsdata) läses vid inmatningstiden och lagras inte i schemat eller mappas till XDM-fält. Relationsscheman är tillgängliga med lämpliga Experience Platform-berättiganden och funktioner.

Detaljerade anvisningar och fallvägledning finns i:

* [Data Mirror - översikt](./data-mirror/overview.md) - Funktioner, användningsexempel och implementeringsplanering
* [Modellbaserad teknisk referens för schema](./schema/model-based.md) - Tekniska specifikationer och begränsningar
* [Självstudiekurs om användargränssnitt](./ui/resources/schemas.md#create-model-based-schema)
* [API, genomgång](./api/schemas.md#create-model-based-schema)
* [Beskrivningsdokumentation (ID)](./api/descriptors.md#relationship-descriptor)
* [Aktivera inhämtning av ändringsdata](../sources/tutorials/api/change-data-capture.md)

### Frågetjänst {#query-service}

Du kan använda standard-SQL för att fråga efter Experience Platform-data som stöder många olika användningsfall med Adobe Experience Platform Query Service.

När ett schema har skapats och en datauppsättning har skapats som refererar till det schemat, hämtas data och lagras i datasjön. Du kan sedan använda frågetjänsten för att ansluta till datauppsättningar i datasjön och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, maskininlärning eller förtäring i realtidskundprofilen.

Mer information om tjänsten finns i [frågetjänstens översikt](../query-service/home.md).

### Kundprofil i realtid {#real-time-customer-profile}

Kundprofilen i realtid är en centraliserad konsumentprofil för riktad och personaliserad upplevelsehantering. Varje profil innehåller data som sammanställs i alla system och innehåller användbara tidsstämplade konton med händelser som berör profilmotivet. Dessa händelser kan ha inträffat i något av de system du använder med Experience Platform.

Kundprofilen i realtid förbrukar schemaformaterade data baserat på klasserna [!UICONTROL XDM Individual Profile] och [!UICONTROL XDM ExperienceEvent] och svarar på frågor baserade på dessa data.

Systemet upprätthåller en instans av varje kundprofil och sammanfogar data till en&quot;enda källa till sanning&quot; för den enskilda personen. Dessa enhetliga data representeras med hjälp av ett så kallat fackschema (kallas ibland för en fackvy). Ett unionsschema samlar fälten för alla scheman som implementerar samma klass i ett enda schema. När du komponerar ett schema med användargränssnittet eller API kan du aktivera schemat för användning med kundprofilen i realtid och tagga det för inkludering i unionen. Det taggade schemat kommer sedan att ingå i den schemadefinition som matas in i profilen.

När [!UICONTROL XDM Individual Profile]- och [!UICONTROL XDM ExperienceEvent]-data hämtas till datasjön, kommer kundprofilen i realtid att innehålla data som har aktiverats för användning. Ju fler interaktioner och detaljer som är inkapslade, desto stabilare blir de enskilda profilerna.

[!UICONTROL XDM Individual Profile]-data hjälper till att informera om och förstärka åtgärder över alla kanaler och Adobe-produktintegrering. När dessa data kombineras med en lång historik med beteendedata och interaktionsdata kan de användas för att underlätta maskininlärning. Real-Time Customer Profile API kan också användas för att utöka funktionaliteten hos tredjepartslösningar, CRM och företagslösningar.

Mer information finns i [Översikt över kundprofilen i realtid](../profile/home.md).

### Arbetsyta för datavetenskap {#data-science-workspace}

>[!NOTE]
>
>Data Science Workspace finns inte längre att köpa. Denna dokumentation är avsedd för befintliga kunder med tidigare tillstånd till Data Science Workspace.

Adobe Experience Platform Data Science Workspace använder maskininlärning och artificiell intelligens för att få insikter från data som lagras i Experience Platform. Med Data Science Workspace kan datavetare skapa recept baserat på [!UICONTROL XDM Individual Profile]- och [!UICONTROL XDM ExperienceEvent]-data om kunder och deras aktiviteter. Dessa recept underlättar prognoser som köpbenägenhet och rekommenderade erbjudanden som individen troligtvis uppskattar och använder.

Med Data Science Workspace kan datavetare enkelt skapa API:er för intelligenta tjänster som bygger på maskininlärning. Dessa tjänster fungerar tillsammans med andra lösningar från Adobe, inklusive Adobe Target och Adobe Analytics Cloud, och hjälper er att automatisera personaliserade, målinriktade digitala upplevelser.

Mer information om hur du använder Experience Platform-data för att få bättre insikter finns i [Översikt över Workspace Data Science](../data-science-workspace/home.md).

## Nästa steg och ytterligare resurser

Nu när du bättre förstår schemats roll i hela Experience Platform kan du börja skapa egna.

Om du vill lära dig designprinciper och bästa praxis för att komponera scheman som ska användas med Experience Platform börjar du med att läsa [grunderna för schemakomposition](schema/composition.md). Stegvisa instruktioner om hur du skapar ett schema finns i självstudiekurserna om hur du skapar ett schema [med API](tutorials/create-schema-api.md) eller [med användargränssnittet](tutorials/create-schema-ui.md).

Titta på följande video om du vill få en bättre förståelse för [!DNL XDM System] i Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
