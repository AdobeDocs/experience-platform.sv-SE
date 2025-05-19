---
title: Metodtips för tillstånd för datahantering
description: Lär dig mer om de bästa metoderna och verktygen du kan använda för att bättre hantera dina licensrättigheter med Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: a14d94a87eb433dd0bb38e5bf3c9c3a04be9a5c6
workflow-type: tm+mt
source-wordcount: '2338'
ht-degree: 1%

---

# Bästa praxis för tillstånd till datahantering

Adobe Experience Platform är ett öppet system som omvandlar era data till robusta kundprofiler som uppdateras i realtid och använder AI-baserade insikter för att hjälpa er att leverera rätt upplevelser i alla kanaler. Ni kan lägga in data av olika typer, volymer och historik i Experience Platform med hjälp av olika källor och sedan ta hänsyn till dessa data för att kunna använda allt från segmentering och personalisering till analys och maskininlärning.

Experience Platform erbjuder licenser som fastställer antalet profiler du kan skapa och hur mycket data du kan hämta in. Med tanke på kapaciteten att hämta in alla datakällor, volymer och historik för data är det möjligt att överskrida era licensrättigheter när datavolymer växer.

Läs den här guiden för bästa praxis och verktyg som du kan använda för att hantera dina licensrättigheter bättre med Experience Platform.

## Sammanfattning av funktioner {#summary-of-features}

Använd de bästa metoderna och verktygen som beskrivs i det här dokumentet för att bättre hantera användningen av dina licenser inom Experience Platform. Det här dokumentet uppdateras i takt med att ytterligare funktioner släpps för att ge synlighet och kontroll till alla Experience Platform-kunder.

I följande tabell visas en lista över de funktioner som är tillgängliga för tillfället, så att du bättre kan hantera din rätt till licensanvändning.

| Funktion | Beskrivning |
| --- | --- |
| [Användargränssnitt för datauppsättning - Upplev datalagring för händelse](../../catalog/datasets/user-guide.md#data-retention-policy) | Konfigurera en fast kvarhållningsperiod för data i datavagn och profilarkiv. Poster tas bort när den konfigurerade kvarhållningsperioden avslutas. |
| [Aktivera/inaktivera datauppsättningar för kundprofil i realtid](../../catalog/datasets/user-guide.md) | Aktivera eller inaktivera datamängdsmatning i kundprofilen i realtid. |
| [Händelseförfallodatum i profilarkivet](../../profile/event-expirations.md) | Använd en förfallotid för alla händelser som är inkapslade i en profilaktiverad datauppsättning. Kontakta ditt Adobe-kontoteam eller kundtjänst om du vill aktivera den här funktionen. |
| [Adobe Analytics Data Prep-filter](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) | Använd [!DNL Kafka] filter för att exkludera onödiga data från inmatning. |
| [Adobe Audience Manager källanslutningsfilter](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Använd Audience Manager källanslutningsfilter för att exkludera onödiga data från intag. |
| [Datafilter för vidarebefordran av händelser](../../tags/ui/event-forwarding/overview.md) | Använd filter på serversidan [!DNL Kafka] för att exkludera onödiga data från inmatning.  Mer information finns i dokumentationen om [taggregler](../../tags/ui/managing-resources/rules.md). |
| [Gränssnitt för kontrollpanel för licensanvändning](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Övervaka hur era Experience Platform-produkter konsumeras av licenserna. Få tillgång till vardagliga användningsögonblicksbilder, prediktiva trender och detaljerade sandlådenivådata som stöd för proaktiv licenshantering. |
| [Rapport-API för datauppsättningsöverlappning](../../profile/tutorials/dataset-overlap-report.md) | Ger de datauppsättningar som bidrar mest till er adresserbara målgrupp. |
| [Rapport-API för identitetsöverlappning](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Visar de identitetsnamnutrymmen som bidrar mest till din adresserbara publik. |
| [Pseudonyma profildata upphör](../../profile/pseudonymous-profiles.md) | Konfigurera förfallotider för pseudonyma profiler och ta automatiskt bort data från profilarkivet. |

{style="table-layout:auto"}

## Förstå Experience Platform datalagring

Experience Platform består huvudsakligen av två datalager: dataländen och profillagringsplatsen.

Datasjön har i första hand följande syften:

* fungerar som mellanlagringsområde för information om introduktion till Experience Platform,
* fungerar som långsiktig datalagring för alla Experience Platform-data,
* Möjliggör användningsfall som dataanalys och datavetenskap.

**Profilarkivet** är där kundprofiler skapas och har i första hand följande syften:

* fungerar som datalagring för profiler som används för att stödja realtidsupplevelser,
* Aktiverar användningsexempel som segmentering, aktivering och personalisering.

>[!NOTE]
>
>Åtkomsten till [!DNL data lake] kan bero på vilken produkt-SKU du har köpt. Mer information om SKU:er får du av Adobe.

## Licensanvändning {#license-usage}

När du licensierar Experience Platform får du licensanvändningsrättigheter som varierar beroende på SKU:

**[!DNL Addressable Audience]**: Det totala antalet kundprofiler som enligt avtal tillåts i Experience Platform, inklusive både kända och pseudonyma profiler.

**[!DNL Total Data Volume]**: Den totala mängden data som är tillgängliga för kundprofil i realtid som kan användas i engagemangsarbetsflöden.

Vilka mätvärden som är tillgängliga och vilken definition som finns för varje mätvärde varierar beroende på vilken licensiering din organisation har köpt.

## Kontrollpanel för licensanvändning

Adobe Experience Platform användargränssnitt innehåller en kontrollpanel där du kan visa en ögonblicksbild av din organisations licensrelaterade data för Experience Platform. Informationen i kontrollpanelen visas exakt som den visas vid den specifika tidpunkt då ögonblicksbilden togs. Ögonblicksbilden är varken en ungefärlig eller ett urval data och instrumentpanelen uppdateras inte i realtid.

Mer information finns i guiden om [användning av kontrollpanelen för licensanvändning i Experience Platform-gränssnittet](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

## Bästa praxis för datahantering

I följande avsnitt beskrivs de bästa metoderna att följa för att bättre hantera dina data.

### Förstå era data

Alla data är inte desamma i Adobe Experience Platform. Vissa data kan vara täta, men har lågt värde, medan andra kan vara glesare, men med högt värde. Vissa data kan förlora i värde så snart de har genererats, medan andra kan vara värdefulla i månader, eller till och med år.

Det finns tre dimensioner att tänka på när du ska förstå värdet av dina data:

| Dimension | Beskrivning | Exempel |
| --- | --- | --- |
| Volym | Representerar mängden och den totala mängden data som har importerats. | Webbklickningar - stora volymer och måttlig originaltrohet. Värdet kan minska snabbt. |
| Tidsintervall | Representerar den tid som inmatade data fortsätter att vara värdefulla. | Inköp offline - måttlig i volym och återgivning, men kan vara värdefullt under långa perioder. |
| Följsamhet | Representerar hur rik informationen är med information. | Kundkonton - låg volym, men hög återgivning. Kan vara värdefull även efter en kunds livstid. |

### Datahanteringsverktyg {#data-management-tools}

Det finns två centrala scenarier att tänka på när du ser till att din dataanvändning ligger inom licensens gränser:

### Vilka data ska föras in i Experience Platform?

Data kan importeras till ett eller flera system i Experience Platform, nämligen [!DNL data lake] och/eller profilarkivet. Det innebär att det kan finnas olika data i båda systemen för olika användningsområden. Du kanske vill lagra historiska data i [!DNL data lake], men inte i profilarkivet. Du kan välja vilka data som ska skickas till profilarkivet genom att aktivera en datauppsättning för profilinmatning.

>[!NOTE]
>
>Åtkomsten till [!DNL data lake] kan bero på vilken produkt-SKU du har köpt. Mer information om SKU:er får du av Adobe.

### Vilka data ska sparas?

Du kan använda både dataöverföringsfilter och förfalloregler för att ta bort data som har blivit föråldrade för dina användningsfall. Vanligtvis förbrukar beteendedata (som analysdata) betydligt mer lagringsutrymme än postdata (som CRM-data). Många Experience Platform-användare har till exempel upp till 90 % av de profiler som enbart fylls i med beteendedata jämfört med postdata. Därför är det viktigt att du hanterar dina beteendedata för att säkerställa att licenserna efterlevs.

Det finns ett antal verktyg som du kan använda för att hålla dig inom dina licensanvändningsrättigheter:

* [Intag](#ingestion-filters)
* [Profilarkiv](#profile-service)

### Identitetstjänst och adresserbar publik {#identity-service}

Identitetsdiagram räknas inte av mot det totala adresserbara målgruppsberättigandet eftersom adresserbara målgrupper refererar till det totala antalet kundprofiler.

Gränserna för identitetsdiagram kan dock påverka den adresserbara publiken på grund av delade identiteter. Om till exempel det äldsta ECID:t tas bort från diagrammet kommer ECID att finnas kvar i kundprofilen i realtid som en pseudonym profil. Du kan ange att [pseudonyma utgångsdatum för profildata](../../profile/pseudonymous-profiles.md) ska kringgå det här beteendet. Mer information finns i [skyddsjournalerna för identitetstjänstens data](../../identity-service/guardrails.md).

### Intag {#ingestion-filters}

Injektionsfilter gör att du bara kan hämta in de data som behövs för dina användningsfall och filtrera bort alla händelser som inte behövs.

| filtret Intag | Beskrivning |
| --- | --- |
| Adobe Audience Manager källfiltrering | När du skapar en Adobe Audience Manager-källanslutning kan du välja vilka segment och egenskaper som ska hämtas till kundprofilen [!DNL data lake] och Real-Time, i stället för att bara hämta in Audience Manager-data i sin helhet. Mer information finns i guiden om att [skapa en Audience Manager-källanslutning](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| Adobe Analytics Data Prep | Du kan använda [!DNL Data Prep]-funktioner när du skapar en Analytics-källanslutning för att filtrera bort data som inte behövs för dina användningsfall. Genom [!DNL Data Prep] kan du definiera vilka attribut/kolumner som måste publiceras till Profil. Du kan också tillhandahålla villkorssatser för att informera Experience Platform om data förväntas publiceras till Profil eller bara till [!DNL data lake]. Mer information finns i guiden om att [skapa en Analytics-källanslutning](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Stöd för att aktivera/inaktivera datauppsättningar för profil | Om du vill importera data till kundprofilen i realtid måste du aktivera en datauppsättning för användning i profilarkivet. Om du gör det läggs dina [!DNL Addressable Audience]- och [!DNL Total Data Volume]-berättiganden till. När en datauppsättning inte längre behövs för att använda kundprofiler kan du inaktivera datauppsättningens integrering till Profil för att säkerställa att dina data fortfarande är licenskompatibla. Mer information finns i guiden [Aktivera och inaktivera datauppsättningar för profilen](../../catalog/datasets/enable-for-profile.md). |
| SDK och SDK för mobiler | Det finns två typer av data som samlas in av webb och Mobile SDK: data som samlas in automatiskt och data som uttryckligen samlas in av din utvecklare. Om du vill hantera licensefterlevnaden bättre kan du inaktivera automatisk datainsamling i SDK-konfigurationen med hjälp av kontextinställningarna. Anpassade data kan också tas bort eller inte ställas in av utvecklaren. |
| Undantag för vidarebefordrande data på serversidan | Om du skickar data till Experience Platform via vidarebefordran på serversidan kan du utesluta vilka data som skickas genom att antingen ta bort mappningen i en regelåtgärd för att exkludera den i alla händelser, eller genom att lägga till villkor i regeln så att endast data aktiveras för vissa händelser. Mer information finns i dokumentationen om [händelser och villkor](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if). |
| Filtrera data på källnivå | Du kan använda logiska operatorer och jämförelseoperatorer för att filtrera radnivådata från dina källor innan du skapar en anslutning och hämtar data till Experience Platform. Mer information finns i handboken om [filtrering av radnivådata för en källa med  [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Profilarkiv {#profile-service}

Profilarkivet består av följande komponenter:

| Profillagringskomponent | Beskrivning |
| --- | --- |
| Profilfragment | Varje kundprofil består av flera **profilfragment** som har sammanfogats till en enda vy av kunden. Om en kund till exempel interagerar med ert varumärke i flera kanaler kommer organisationen att ha flera **profilfragment** som är kopplade till den enskilda kunden som visas i flera datauppsättningar. När de här fragmenten hämtas till Experience Platform sammanfogas de med hjälp av identitetsdiagrammet för att skapa en profil för kunden. **Profilfragment** består av ett identitetsnamnutrymme som identifierare, med associerade postdata och/eller tidsseriedata. |
| Postdata (attribut) | En profil är en representation av ett ämne, en organisation eller en individ, som består av många **attribut** (kallas även **postdata**). Profilen för en produkt kan t.ex. innehålla en SKU och en beskrivning, medan profilen för en person innehåller information som förnamn, efternamn och e-postadress. **Postdata** har vanligtvis låg/måttlig volym, men är värdefullt under långa perioder. |
| Tidsseriedata (beteende) | **Tidsseriedata** ger information om ett användarbeteende. Tidsseriedata representeras av den vanliga schemaklassen Experience Data Model (XDM) [!DNL ExperienceEvent] och kan beskriva händelser som objekt som läggs till i en kundvagn, länkar som klickas och videofilmer som visas. Beteendevärdet kan minska med tiden. |
| Identitetsnamnutrymme (identiteter) | När kunddata sammanställs sammanfogas de till en enda profil med hjälp av **identitetsnamnutrymmen** och möjligheten att knyta samman dessa identiteter när mer information blir känd om användaren. Mer information finns i [översikten över identitetsnamnutrymmen](../../identity-service/features/namespaces.md). |

{style="table-layout:auto"}

### Dispositionsrapporter för profilarkiv

Det finns ett antal rapporter som hjälper dig att förstå hur profilarkivet är uppbyggt. Dessa rapporter hjälper er att fatta välgrundade beslut om hur och var era Experience Event-utgångsdatum ska anges för att optimera er licensanvändning:

* **Rapports-API:t för datauppsättningsöverlappning**: Visar de datauppsättningar som bidrar mest till din adresserbara publik. Du kan använda den här rapporten för att identifiera vilka [!DNL ExperienceEvent] datauppsättningar som du vill ange en förfallotid för. Mer information finns i självstudiekursen om att [generera överlappningsrapporten för datauppsättningen](../../profile/tutorials/dataset-overlap-report.md).
* **Rapport-API:t för identitetsöverlappning**: Visar de identitetsnamnutrymmen som bidrar mest till din adresserbara publik. Mer information finns i självstudiekursen om att [generera rapporten om identitetsöverlappning](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report).
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

### Förfallodatum för pseudonyma profildata {#pseudonymous-profile-expirations}

Använd funktionen för pseudonyma profiler för att automatiskt ta bort data som inte längre är giltiga eller användbara för dina användningsfall från profilarkivet. Om data för pseudonym profil går ut tas både händelse- och profilposter bort. Den här inställningen minskar därmed adresserbara målvolymer. Mer information om den här funktionen finns i [Översikt över förfallodatum för pseudonyma profildata](../../profile/pseudonymous-profiles.md).

### Användargränssnitt för datauppsättning - Upplev kvarhållande av händelsedatauppsättning {#data-retention}

Konfigurera inställningar för förfallodatum och kvarhållande för datauppsättningar för att framtvinga en fast kvarhållningsperiod för dina data i datasjön och profilarkivet. När kvarhållningsperioden är slut tas data bort. Experience Event-datas förfallodatum tar bara bort händelser och tar inte bort profilklassdata, vilket minskar den totala datavolymen ](total-data-volume.md) i användningsstatistik för licenser. [ Mer information finns i handboken om [inställning av datalagringsprincip](../../catalog/datasets/user-guide.md#data-retention-policy).

### Utgångsdatum för profilupplevelsehändelser {#event-expirations}

Konfigurera förfallotider så att beteendedata automatiskt tas bort från din profilaktiverade datauppsättning när de inte längre är värdefulla för dina användningsfall. Mer information finns i översikten om [Experience Event-utgångsdatum](../../profile/event-expirations.md).

## Sammanfattning av de bästa sätten att uppfylla licensanvändningsvillkoren {#best-practices}

Nedan följer en lista över rekommenderade metoder som du kan följa för att säkerställa att din rätt till licensanvändning följs bättre:

* Använd kontrollpanelen [för licensanvändning](../../dashboards/guides/license-usage.md) för att spåra och övervaka trender för kundanvändning. På så sätt kan du ligga steget före eventuella överbelastningar som kan uppstå.
* Konfigurera [intessionsfilter](#ingestion-filters) genom att identifiera de händelser som krävs för din segmentering och dina användningsfall för personalisering. Detta gör att du bara kan skicka viktiga händelser som krävs för dina användningsfall.
* Kontrollera att du bara har [aktiverade datauppsättningar för profilen](#ingestion-filters) som krävs för din segmentering och din personalisering.
* Konfigurera [Händelseförfallodatum för upplevelse](../../catalog/datasets/user-guide.md#data-retention-policy) och [pseudonyma profildata](../../profile/pseudonymous-profiles.md) för högfrekventa data som webbdata.
* Konfigurera [TTL-kvarhållningsprinciper (Time-to-Live) för Experience Event-datamängder](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) i datasjön för att automatiskt ta bort föråldrade poster och optimera lagringsanvändningen i enlighet med licensrättigheterna.
* Kontrollera [Profildispositionsrapporter](#profile-store-composition-reports) regelbundet för att förstå din profilarkivkomposition. På så sätt kan ni förstå vilka datakällor som bidrar mest till er licensanvändning.
