---
title: Metodtips för tillstånd för datahantering
description: Lär dig mer om de bästa metoderna och verktygen du kan använda för att bättre hantera dina licensrättigheter med Adobe Experience Platform.
exl-id: f23bea28-ebd2-4ed4-aeb1-f896d30d07c2
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---

# Bästa praxis för tillstånd till datahantering

Adobe Experience Platform är ett öppet system som omvandlar era data till robusta kundprofiler som uppdateras i realtid och använder AI-baserade insikter för att hjälpa er att leverera rätt upplevelser i alla kanaler. Ni kan lägga in data av olika typer, volymer och historik i Experience Platform med hjälp av olika källor och sedan ta hänsyn till dessa data för att kunna använda allt från segmentering och personalisering till analys och maskininlärning.

Plattformen erbjuder licenser som fastställer antalet profiler du kan skapa och den mängd data du kan hämta in. Med tanke på kapaciteten att hämta in alla datakällor, volymer och historik för data är det möjligt att överskrida era licensrättigheter när datavolymer växer.

I det här dokumentet beskrivs de bästa sätten att följa och de verktyg du kan använda för att hantera dina licensrättigheter bättre med Adobe Experience Platform.

## Förstå Adobe Experience Platform datalagring

Experience Platform består huvudsakligen av två datalager: [!DNL data lake] och profilarkivet.

The **[!DNL data lake]** främst har följande syften:

* fungerar som mellanlagringsområde för information om introduktion på Experience Platform,
* fungerar som långsiktig datalagring för alla data från Experience Platform,
* Möjliggör användningsfall som dataanalys och datavetenskap.

The **Profilarkiv** är där kundprofiler skapas och i första hand har följande syften:

* fungerar som datalagring för profiler som används för att stödja realtidsupplevelser,
* Aktiverar användningsexempel som segmentering, aktivering och personalisering.

>[!NOTE]
>
>Din åtkomst till [!DNL data lake] kan bero på vilken produkt-SKU du har köpt. Mer information om SKU:er finns hos Adobe.

## Licensanvändning {#license-usage}

När du licensierar Experience Platform får du licensanvändningsrättigheter som varierar beroende på SKU:

**[!DNL Addressable Audience]** - det totala antalet kundprofiler som enligt avtal tillåts i Experience Platform, inklusive både kända och pseudonyma profiler.

**[!DNL Profile Richness]** - den genomsnittliga storleken på dina profildata i Experience Platform. Du kan öka dina [!DNL Profile Richness] genom att köpa ett fyllnadspaket.

The [!DNL Profile Richness] mätvärdena varierar beroende på vilken licens du har köpt. Det finns två beräkningar för [!DNL Profile Richness] tillgänglig:

* Summan av alla produktionsdata som lagras i Adobe Real-time Customer Data Platform (dvs. kundprofil och identitetstjänst i realtid) vid varje tidpunkt, dividerat med [!DNL Addressable Audience];
* Summan av alla data som lagras inom plattformen (inklusive men inte begränsat till [!DNL data lake], kundprofil i realtid och identitetstjänst) när som helst och alla data som du direktuppspelar via (i stället för att lagra i) Platform under de senaste 12 månaderna, dividerat med [!DNL Addressable Audience].

Vilka mätvärden som är tillgängliga och vilken definition som finns för varje mätvärde varierar beroende på vilken licensiering din organisation har köpt.

## Kontrollpanel för licensanvändning

Adobe Experience Platform användargränssnitt tillhandahåller en kontrollpanel där du kan visa en ögonblicksbild av din organisations licensrelaterade data för Platform. Informationen i kontrollpanelen visas exakt som den visas vid den specifika tidpunkt då ögonblicksbilden togs. Ögonblicksbilden är varken en ungefärlig eller ett urval data och instrumentpanelen uppdateras inte i realtid.

Mer information finns i handboken [med kontrollpanelen för licensanvändning på plattformsgränssnittet](../../dashboards/guides/license-usage.md#license-usage-dashboard-data).

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

### Vilka data ska tas med i plattformen?

Data kan inhämtas till ett eller flera system i plattformen, nämligen [!DNL data lake] och/eller profilarkivet. Det innebär att det kan finnas olika data i båda systemen för olika användningsområden. Du kanske vill lagra historiska data i [!DNL data lake], men inte i profilarkivet. Du kan välja vilka data som ska skickas till profilarkivet genom att aktivera en datauppsättning för profilinmatning.

>[!NOTE]
>
>Din åtkomst till [!DNL data lake] kan bero på vilken produkt-SKU du har köpt. Mer information om SKU:er finns hos Adobe.

### Vilka data ska sparas?

Du kan använda både dataöverföringsfilter och förfalloregler för att ta bort data som har blivit föråldrade för dina användningsfall. Vanligtvis förbrukar beteendedata (som analysdata) betydligt mer lagringsutrymme än postdata (som CRM-data). Många plattformsanvändare har till exempel upp till 90 % av de profiler som enbart fylls i av beteendedata, jämfört med postdata. Därför är det viktigt att du hanterar dina beteendedata för att säkerställa att licenserna efterlevs.

Det finns ett antal verktyg som du kan använda för att hålla dig inom dina licensanvändningsrättigheter:

* [Intag](#ingestion-filters)
* [Profilarkiv](#profile-service)

### Identitetstjänst och adresserbar publik {#identity-service}

Identitetsdiagram räknas inte av mot det totala adresserbara målgruppsberättigandet eftersom adresserbara målgrupper refererar till det totala antalet kundprofiler.

Gränserna för identitetsdiagram kan dock påverka den adresserbara publiken på grund av delade identiteter. Om till exempel det äldsta ECID:t tas bort från diagrammet kommer ECID att finnas kvar i kundprofilen i realtid som en pseudonym profil. Du kan ange [Förfallodatum för pseudonyma profildata](../../profile/pseudonymous-profiles.md) för att kringgå detta beteende. Mer information finns i [skyddsutkast för identitetstjänstens data](../../identity-service/guardrails.md).

### Intag {#ingestion-filters}

Injektionsfilter gör att du bara kan hämta in de data som behövs för dina användningsfall och filtrera bort alla händelser som inte behövs.

| filtret Intag | Beskrivning |
| --- | --- |
| Adobe Audience Manager källfiltrering | När du skapar en Adobe Audience Manager-källanslutning kan du välja vilka segment och egenskaper som ska ingå i [!DNL data lake] och Kundprofil i realtid, i stället för att hämta in alla data från Audience Manager. Se guiden på [skapa en Audience Manager-källanslutning](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) för mer information. |
| Adobe Analytics Data Prep | Du kan använda [!DNL Data Prep] funktioner när du skapar en anslutning till en Analytics-källa för att filtrera bort data som inte behövs för dina användningsfall. Via [!DNL Data Prep]kan du definiera vilka attribut/kolumner som ska publiceras till Profil. Du kan också ange villkorssatser för att informera plattformen om data förväntas publiceras till Profil, eller bara till [!DNL data lake]. Se guiden på [skapa en källanslutning för analys](../../sources/tutorials/ui/create/adobe-applications/analytics.md) för mer information. |
| Stöd för att aktivera/inaktivera datauppsättningar för profil | Om du vill importera data till kundprofilen i realtid måste du aktivera en datauppsättning för användning i profilarkivet. Om du gör det läggs till i [!DNL Addressable Audience] och [!DNL Profile Richness] rättigheter. När en datauppsättning inte längre behövs för att använda kundprofiler kan du inaktivera datauppsättningens integrering till Profil för att säkerställa att dina data fortfarande är licenskompatibla. Se guiden på [aktivera och inaktivera datauppsättningar för profil](../../catalog/datasets/enable-for-profile.md) för mer information. |
| SDK för webb och SDK för mobiler | Det finns två typer av data som samlas in via webb och Mobile SDK: data som samlas in automatiskt och data som uttryckligen samlas in av din utvecklare. Om du vill hantera licenskompatibiliteten bättre kan du inaktivera automatisk datainsamling i SDK-konfigurationen via kontextinställningen. Anpassade data kan också tas bort eller inte ställas in av utvecklaren. |
| Undantag för vidarebefordrande data på serversidan | Om du skickar data till plattformen med hjälp av vidarebefordran på serversidan kan du utesluta vilka data som skickas genom att antingen ta bort mappningen i en regelåtgärd för att exkludera den i alla händelser, eller genom att lägga till villkor i regeln så att endast data aktiveras för vissa händelser. Läs dokumentationen om [händelser och villkor](/help/tags/ui/managing-resources/rules.md#events-and-conditions-if) för mer information. |
| Filtrera data på källnivå | Du kan använda logiska operatorer och jämförelseoperatorer för att filtrera radnivådata från dina källor innan du skapar en anslutning och hämtar data till Experience Platform. Mer information finns i guiden [filtrera data på radnivå för en källa med [!DNL Flow Service] API](../../sources/tutorials/api/filter.md). |

{style="table-layout:auto"}

### Profilarkiv {#profile-service}

Profilarkivet består av följande komponenter:

| Profillagringskomponent | Beskrivning |
| --- | --- |
| Profilfragment | Varje kundprofil består av flera **profilfragment** som har sammanfogats till en enda bild av kunden. Om en kund till exempel interagerar med ert varumärke i flera kanaler har organisationen flera **profilfragment** som är relaterade till den enskilda kunden och förekommer i flera datauppsättningar. När de här fragmenten hämtas till Platform sammanfogas de med hjälp av identitetsdiagrammet för att skapa en profil för den kunden. **Profilfragment** består av ett identitetsnamnutrymme som identifierare, med tillhörande postdata och/eller tidsseriedata. |
| Postdata (attribut) | En profil är en representation av ett ämne, en organisation eller en individ som består av många **Attribut** (kallas även **postdata**). Profilen för en produkt kan t.ex. innehålla en SKU och en beskrivning, medan profilen för en person innehåller information som förnamn, efternamn och e-postadress. **Registrera data** är vanligtvis låg/måttlig i volym, men värdefull under långa perioder. |
| Tidsseriedata (beteende) | **Tidsseriedata** innehåller information om ett användarbeteende. Representeras av standardschemaklassen Experience Data Model (XDM) [!DNL ExperienceEvent]kan tidsseriedata beskriva händelser som objekt som läggs till i en kundvagn, länkar som klickas och videofilmer visas. Beteendevärdet kan minska med tiden. |
| Identitetsnamnutrymme (identiteter) | När kunddata sammanställs sammanfogas de i en enda profil med hjälp av **identitetsnamnutrymmen** och möjligheten att knyta samman dessa identiteter när mer information blir känd om användaren. Se [Översikt över identitetsnamnutrymmen](../../identity-service/features/namespaces.md) för mer information. |

{style="table-layout:auto"}

#### Dispositionsrapporter för profilarkiv

Det finns ett antal rapporter som hjälper dig att förstå hur profilarkivet är uppbyggt. Dessa rapporter hjälper er att fatta välgrundade beslut om hur och var era Experience Event-utgångsdatum ska anges för att optimera er licensanvändning:

* **Rapport-API för datasammanslagning**: Visar de datauppsättningar som bidrar mest till er adresserbara publik. Du kan använda den här rapporten för att identifiera vilka [!DNL ExperienceEvent] datauppsättningar för att ange en förfallotid för. Se självstudiekursen om [generera överlappningsrapport för datauppsättning](../../profile/tutorials/dataset-overlap-report.md) för mer information.
* **API för identitetsöverlappningsrapport**: Visar de identitetsnamnutrymmen som bidrar mest till din adresserbara publik. Se självstudiekursen om [generera rapporten om identitetsöverlappning](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) för mer information.
<!-- * **Unknown Profiles Report API**: Exposes the impact of applying pseudonymous expirations for different time thresholds. You can use this report to identify which pseudonymous expirations threshold to apply. See the tutorial on [generating the unknown profiles report](../../profile/api/preview-sample-status.md#generate-the-unknown-profiles-report) for more information.
-->

#### Förfallodatum för pseudonyma profildata {#pseudonymous-profile-expirations}

Med den här funktionen kan du automatiskt ta bort inaktuella pseudonyma profiler från profilarkivet. Mer information om den här funktionen finns i [Översikt över förfallodatum för pseudonyma profildata](../../profile/pseudonymous-profiles.md).

#### Förfallodatum för upplevelsehändelser {#event-expirations}

Med den här funktionen kan du automatiskt ta bort beteendedata från en profilaktiverad datauppsättning som inte längre är värdefull för dina användningsfall. Se översikten på [Förfallodatum för upplevelsehändelser](../../profile/event-expirations.md) om du vill ha mer information om hur den här processen fungerar när den har aktiverats för en datauppsättning.

## Sammanfattning av de bästa sätten att uppfylla licensanvändningsvillkoren {#best-practices}

Nedan följer en lista över rekommenderade metoder som du kan följa för att säkerställa att din rätt till licensanvändning följs bättre:

* Använd [kontrollpanel för licensanvändning](../../dashboards/guides/license-usage.md) för att följa upp och övervaka trender för kundanvändning. På så sätt kan du ligga steget före eventuella överbelastningar som kan uppstå.
* Konfigurera [filter för förtäring](#ingestion-filters) genom att identifiera de händelser som krävs för er segmentering och personalisering. Detta gör att du bara kan skicka viktiga händelser som krävs för dina användningsfall.
* Se till att du bara har [aktiverade datauppsättningar för profil](#ingestion-filters) som krävs för er segmentering och personalisering.
* Konfigurera [Förfallodatum för upplevelsehändelser](#event-expirations) och [Förfallodatum för pseudonyma profildata](#pseudonymous-profile-expirations) för högfrekventa data som webbdata.
* Kontrollera regelbundet [Kompositionsrapporter för profil](#profile-store-composition-reports) för att förstå din profilbutikskomposition. På så sätt kan ni förstå vilka datakällor som bidrar mest till er licensanvändning.

## Sammanfattning av funktioner och tillgänglighet {#feature-summary}

De bästa metoderna och verktygen som beskrivs i det här dokumentet hjälper dig att bättre hantera användningen av dina licenser inom Adobe Experience Platform. Det här dokumentet kommer att uppdateras i takt med att ytterligare funktioner släpps för att ge synlighet och kontroll till alla Experience Platform-kunder.

I följande tabell visas en lista över de funktioner som är tillgängliga för tillfället, så att du bättre kan hantera din rätt till licensanvändning.

| Funktion | Beskrivning |
| --- | --- |
| [Aktivera/inaktivera datauppsättningar för profil](../../catalog/datasets/user-guide.md) | Aktivera eller inaktivera datamängdsmatning i kundprofilen i realtid. |
| [Förfallodatum för upplevelsehändelser](../../profile/event-expirations.md) | Använd en förfallotid för alla händelser som är inkapslade i en profilaktiverad datauppsättning. Kontakta kontoteamet eller kundtjänst på Adobe för att aktivera den här funktionen. |
| [Adobe Analytics Data Prep-filter](../../sources/tutorials/ui/create/adobe-applications/analytics.md) | Använd [!DNL Kafka] filter för att utesluta onödiga data från inmatning |
| [Adobe Audience Manager källanslutningsfilter](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) | Använd anslutningsfilter för Audience Manager-källa för att exkludera onödiga data från intag |
| [Datafilter för vidarebefordran av händelser](../../tags/ui/event-forwarding/overview.md) | Använd serversidan [!DNL Kafka] filter för att utesluta onödiga data från intag.  Läs dokumentationen om [taggregler](../../tags/ui/managing-resources/rules.md) om du vill ha mer information. |
| [Användargränssnitt för kontrollpanel för licensanvändning](../../dashboards/guides/license-usage.md#license-usage-dashboard-data) | Visa en ögonblicksbild av din organisations licensrelaterade data för Experience Platform |
| [Rapport-API för datasammanslagning](../../profile/tutorials/dataset-overlap-report.md) | Visar de datauppsättningar som ger mest för er adresserbara publik |
| [API för identitetsöverlappningsrapport](../../profile/api/preview-sample-status.md#generate-the-identity-namespace-overlap-report) | Visar de identitetsnamnutrymmen som bidrar mest till din adresserbara publik |

{style="table-layout:auto"}
