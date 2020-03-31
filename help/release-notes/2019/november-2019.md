---
title: Versionsinformation om Adobe Experience Platform
description: Versionsinformation om Experience Platform 18 november 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 9bfb2ca8726421363c8446ecf581ed58d427eabf

---


# Versionsinformation om Adobe Experience Platform

## Releasedatum: 18 november 2019

Nya versioner:
* [Kunddataplattform i realtid](#real-time-customer-data-platform)
* [Mål](#destinations)
* [Källor](#sources)

Uppdateringar av befintliga funktioner:
* [Datavetenskapens arbetsyta](#data-science-workspace)
* [Experience Data Model (XDM) System](#experience-data-model-xdm-system)
* [Kundprofil i realtid](#real-time-customer-profile)
* [Segmenteringstjänst](#segmentation-service)

## Kunddataplattform i realtid

Adobe Customer Data Platform (CDP) i realtid bygger på Adobe Experience Platform och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. CDP i realtid kombinerar flera datakällor för företag för att skapa enhetliga profiler i realtid som kan användas för att leverera personliga personaliserade kundupplevelser i alla kanaler och enheter.

Kunddataplattformen i realtid innehåller verktyg för datastyrning, identitetshantering, avancerad segmentering och datavetenskap, så att ni kan skapa profiler och definiera målgrupper samt få omfattande insikter samtidigt som ni kan tillämpa strikta policyer för datastyrning.

Adobe är kopplat till ett stort antal partners, för att inte tala om integreringar med Adobe Experience Cloud, så att ni kan aktivera dessa målgrupper sömlöst och leverera fantastiska kundupplevelser i alla kanaler, från personalisering på plats eller i appen till e-post, betalda medier, callcenters, anslutna enheter med mera.

Med CDP i realtid kan man

* Få en samlad bild av kunden genom att strömma kunddata från hela företaget.
* Hantera profiler med tillförlitlig styrning och sekretesskontroller för kända och okända identifierare.
* Generera användbara insikter och skala målgrupper med hjälp av AI och maskininlärning från Adobe Sensei som är framtagen för marknadsförare.
* Leverera personaliserade upplevelser i realtid i alla kanaler och på alla destinationer.

Mer information finns i dokumentationen [till](../../rtcdp/overview.md)Adobe Customer Data Platform i realtid.

### Viktiga funktioner

| Funktion | Beskrivning |
|---|---|
| Mål  | Färdiga integreringar med målplattformar som stöds av Adobes kunddataplattform i realtid och som möjliggör smidig datainmatning till dessa partners. Mer information finns i [Destinationer](#destinations) nedan. |
| Kontrollpanel för måttuppgifter på startsida | På Adobe Real-time Customer Data Platform (CDP i realtid) finns en mätinstrumentpanel som visar information om profiler och segment. Hemsidan innehåller även länkar till utbildningsmaterial. Se avsnittet om kunddata för [kundens dataplattmått](#real-time-customer-data-platform-metrics) i realtid nedan. |
| Källor | Du kan importera data från en mängd olika källor, till exempel Adobe Solutions, molnbaserad lagring, tredjepartsprogramvara och ditt CRM. Läs mer i avsnittet [Källor](#sources) nedan. |

### Mätvärden för kunddataplattform i realtid

Hemsidan för Adobe Customer Data Platform (CDP i realtid), som innehåller en mätinstrumentpanel, visas när du loggar in på CDP i realtid.

Hemsidan är bara en av platserna där metriska kort visas. CDP ger dig mätkort i realtid genom hela upplevelsen. Dessa mätvärden ger information om data, profiler och målgrupper i systemet.

Om det inte finns några data i systemet när du loggar in på CDP i realtid visas inte instrumentpanelen på startsidan. I det här fallet innehåller startsidan utbildningsmaterial för en förstagångsupplevelse. När data samlas in uppdateras instrumentpanelen automatiskt för att visa information om dessa data.

Mer information finns i Översikt över kunddata för [kunddataplattformen i realtid](../../rtcdp/home-page-dashboards.md)

## Mål 

Destinationer är färdiga integrationer med målplattformar som stöds av Adobes kunddataplattform i realtid och som aktiverar data till dessa partners på ett smidigt sätt. Mer information finns i artikeln Översikt över [](../../rtcdp/destinations/destinations-overview.md) destinationer.

### Tillgängliga destinationer

I november-versionen stöder Adobes kunddataplattform i realtid följande destinationer:

* Reklam: Google
* E-postmarknadsföring: Adobe Campaign, Salesforce Marketing Cloud, Oracle Responsys, Oracle Eloqua

Information om var och en av destinationerna finns i [målkatalogen](../../rtcdp/destinations/destinations-catalog.md) .

### Kända begränsningar

* Kontrollen som tillåter anpassade aktiveringsscheman i [aktiveringsflödet](../../rtcdp/destinations/activate-destinations.md#activate-data) (schemasteget) är inte tillgänglig i den första versionen.
* Det finns för närvarande inget sätt att redigera eller ta bort en målkonfiguration. Du kan undvika den här begränsningen genom att aktivera eller inaktivera målet i det övre högra hörnet på sidan [med](../../rtcdp/destinations/destination-details-page.md)målinformation.
* Det finns för närvarande ingen validering för kontoinformation, sökväg eller autentiseringsuppgifter vid anslutning till ditt mål eller lagringskonto. Se till att du anger rätt autentiseringsuppgifter och dubbelkontrollera om det finns stavfel eller stavfel.
* Inga autentiseringsuppgifter har förnyats i den första versionen. När ett konto har gått ut eller behöver uppdateras, måste du skapa en ny målanslutning och mappa om de segment som du tidigare har mappat.

## Källor

Adobe Experience Platform kan importera data från externa källor samtidigt som ni kan strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe Solutions, molnbaserad lagring, tredjepartsprogramvara och ditt CRM-system.

Experience Platform har ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dig mot dina lagringssystem och CRM-tjänster, ange tider för hur mycket information som ska matas in och hantera dataöverföringshastigheten.

### Viktiga funktioner

| Funktion | Beskrivning |
| ---------- | ------------ |
| Källgränssnitt | Nytt användargränssnitt för att skapa, visa och hantera källanslutningar. |
| Förbättrade arbetsflöden för CRM-anslutningar | Nytt intuitivt gränssnittsarbetsflöde för att skapa och hantera Microsoft Dynamics- och Salesforce-anslutningar. |
| Stöd för anslutning för molnbaserade lagringslösningar | Kopplingar kan nu komma åt molnbaserade lagringsmedier. Bland de nya källorna finns Amazon S3, Azure Blob och FTP/SFTP-servrar. |

### Kända fel

* Källanslutningar för molnbaserade lagringsenheter stöder inte inmatning av komprimerade filer.

Mer information om källor finns i [Källor - översikt](../../source-connectors/home.md).

## Datavetenskapens arbetsyta

Med Adobe Experience Platform Data Science Workspace kan datavetare smidigt generera insikter från data och innehåll i olika Adobe-program och tredjepartssystem genom att skapa och driftsätta Machine Learning-modeller. Data Science Workspace är nära integrerat med Platform och är en drivkraft för datavetenskapens hela livscykel, inklusive utforskning och förberedelse av XDM-data, följt av utveckling och driftsättning av modeller för att automatiskt berika kundprofilen i realtid med maskininlärningsinsikter.

### Nya funktioner

| Funktion | Beskrivning |
| -----------| ---------- |
| Dataåtkomst med Platform SDK | Färdiga Recipes och launcher-anteckningsböcker i Python använder nu Platform SDK för att komma åt data. |
| Stöd för sandlådor | Stöd för kommande sandlådefunktioner (som för närvarande är i betaversion), inklusive möjligheten att isolera bärbara datorer och recept till utvecklings- eller produktionssandlådor. Mer information finns i översikten över [](../../sandboxes/home.md) sandlådor. |

Mer information finns i översikten över arbetsytan för [datavetenskap](../../data-science-workspace/home.md).

## Experience Data Model (XDM) System

Standardisering och interoperabilitet är viktiga begrepp bakom Experience Platform. Experience Data Model (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

### Nya funktioner

| Funktion | Beskrivning |
| ---------- | ------------ |
| Meddelandeschema | Nytt schema som representerar meddelandedata som skickas under dataöverföringsprocessen. |
| Adobe AdCloud DSP-scheman | Fem nya scheman har lagts till för att representera metadata för Adobe Advertising Cloud DSP (Demand-Side Platform): Placement, Campaign, Package, Advertiser, Account. |
| Blandning av implementeringsinformation för ExperienceEvent | Ny ExperienceEvent-blandning som lägger till ett standardfält för att lagra information om programmet som används för att samla in händelsen. |
| Blandning av profilsekretess | Ny profilblandning som lägger till fält som accepterar allmänna avanmälnings- och avanmälningssignaler för försäljning/delning för kundprofil i realtid. |
| Formatbegränsningar för `xdm:alternateDisplayInfo` | Fälten Rubrik och Beskrivning för `xdm:alternateDisplayInfo` måste båda vara strängar för att validera. |
| Namnändring: Individuell XDM-profil | &quot;Titeln&quot; för klassen &quot;XDM Profile&quot; har uppdaterats till &quot;XDM Individual Profile&quot;. Klassens formell `$id` har inte ändrats. |

### Kända fel

* Ingen.

Mer information om hur du arbetar med XDM med API:t för schemaregister och användargränssnittet för Schemaredigeraren finns i [XDM-systemdokumentationen](../../xdm/home.md).

## Kundprofil i realtid

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder, oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av en profil kan ni sammanställa olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| -----------| ---------- |
| Förbättringar av profilsökning | Användarna kan nu söka efter profiler med hjälp av referensbeskrivningar och relaterade entiteter. |
| Rensa data för en viss datauppsättning | Användare kan nu ta bort data för en viss datauppsättning eller grupp med hjälp av profilsystemets jobb-API. |
| Förbättrade Edge Profile-frågor | Program kan nu fråga Edge Profile efter någon av identiteterna för en viss profil. |
| Konfigurera sammanslagningsprinciper per per projektion | Program kan nu konfigurera sammanslagningsprinciper per per projektion för att generera en vy över data som styrs av en specifik sammanfogningsprincip. |
| Beräknade attribut | Beräknade attribut beräknar automatiskt fältets värde baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån för att samla värden som&quot;totalt inköp&quot;,&quot;livstidsvärde&quot; eller&quot;trattstatus&quot; baserat på en inkommande händelse, inkommande händelse- och profildata eller en inkommande händelse, profildata och historiska händelser. |

### Felkorrigeringar

* Förenklad lista över tillgängliga strategier för id-sammanslagning när man skapar sammanslagningsprinciper.

### Kända fel

* Ingen.

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa metoder för att arbeta med profildata, finns i [Kundprofilöversikt](../../profile/home.md)i realtid.

## Segmenteringstjänst

Adobe Experience Platform Segmentation Service tillhandahåller ett användargränssnitt och RESTful API som gör att ni kan skapa segment och generera målgrupper utifrån era kundprofildata i realtid. Dessa segment är centralt konfigurerade och underhållna på Platform, vilket gör dem tillgängliga för alla Adobe-program.

Segmenteringstjänsten definierar en viss delmängd av profiler genom att beskriva de kriterier som särskiljer en marknadsföringsbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

| Funktion | Beskrivning |
| -----------| ---------- |
| Schemalagd segmentering | Användare kan nu aktivera schemalagd segmentutvärdering för alla segment via gränssnittet och API:t. När du har aktiverat utvärderas alla segment en gång om dagen. Detta påverkar inte segmenteringsfunktioner som fortsätter att fungera som tidigare.<br/><br/>Obs! Den schemalagda segmenteringsfunktionen kan inte användas i sandlådor med mer än fem sammanfogningsprinciper för den enskilda XDM-profilen. |
| Direktuppspelningssegmentering | Stöd för kontinuerlig utvärdering av segment (direktuppspelningssegmentering) gör att de flesta segmentregler kan utvärderas när data skickas till plattformen. Den här funktionen innebär att segmentmedlemskapet uppdateras utan att schemalagda segmenteringsjobb behöver köras. Vissa undantag gäller, t.ex. segment som använder relationer med flera enheter eller med anrikade nyttolaster. |
| Segment som byggstenar | När du skapar segment med hjälp av segmentbyggargränssnittet kan användare nu använda tidigare definierade segment som byggstenar för ytterligare segment. <ul><li>Se aktuellt medlemskap: uppdateringar när folk flyttar in och ut från målgrupper.</li><li>Kopieringslogik: använder den valda segmentdefinitionen och duplicerar den i det nya segmentet.</li></ul> |
| Visa segmentmedlemskap efter ID-namnområde | Segmentmedlemskap kan nu visas med ID-namnutrymme (e-post, ECID och totalt antal). |
| Stöd för RBAC | Segment Builder har nu stöd för grundläggande rollbaserade åtkomstkontroller och behörigheter. |
| Förbättrat stöd för extern målgruppsdelning mellan plattformslösningar och Adobe-lösningar | Användare kan nu hämta externa (icke-Experience Platform) målgruppsmetadata i scenarier där antalet målgrupper är stort eller inte är känt på förhand. Den här versionen innehåller åtkomst till Audience Manager-metadata för kunder som har etablerat lösningskonnektorn. Dessa målgruppsmetadata kan användas i Segment Builder för att skapa nya Experience Platform-segment. <br/><br/> Dessutom kommer segment som skapats i Experience Platform nu att vara tillgängliga för användning i integrerade Adobe-lösningar, inklusive Audience Manager, Target och Ad Cloud. |

### Felkorrigeringar

* Korrigerade ett problem som medförde att segmentering för flera enheter returnerade nollprofiler vid kapslade relationer.
* Ett problem har korrigerats där exkluderingslogiken returnerade vilseledande resultat.
* Förbättrad läsbarhet för mappar med flera enheter. De visar nu det egna namnet på XDM-klassen.
* Korrigerade ett tillfälligt problem där flera kopior av samma XDM-mapp påträffades.
* Meddelanden skapas nu för att informera en användare om segmentuppskattningar inte är tillgängliga för den valda sammanfogningsprincipen.

### Kända fel

* Ingen.

Mer information om segmenteringstjänsten finns i Översikt över [segmenteringstjänsten](../../segmentation/home.md).