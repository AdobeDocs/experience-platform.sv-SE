---
title: Versionsinformation om Adobe Experience Platform november 2019
description: Versionsinformation november 2019 för Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 18 november 2019**

Nya funktioner i Adobe Experience Platform:
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Uppdateringar av befintliga funktioner:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Real-time Customer Data Platform (Real-Time CDP) bygger på Adobe Experience Platform och hjälper företag att sammanföra kända och okända data för att aktivera kundprofiler med intelligent beslutsfattande under hela kundresan. Real-Time CDP kombinerar flera olika datakällor för företag för att skapa enhetliga profiler i realtid som kan användas för att leverera personliga personaliserade kundupplevelser i alla kanaler och enheter.

[!DNL Real-Time Customer Data Platform] innehåller verktyg för datastyrning, identitetshantering, avancerad segmentering och datavetenskap, så att ni kan skapa profiler och definiera målgrupper samt få djupgående insikter samtidigt som ni kan tillämpa strikta policyer för datastyrning.

Adobe ansluter till ett stort antal partners, för att inte tala om integreringar med Adobe Experience Cloud, så att ni smidigt kan aktivera dessa målgrupper och leverera fantastiska kundupplevelser i alla kanaler, från personalisering på plats eller i appen till e-post, betalda medier, callcenters, anslutna enheter med mera.

Med Real-Time CDP kan man

* Få en samlad bild av kunden genom att strömma kunddata från hela företaget.
* Hantera profiler med tillförlitlig styrning och sekretesskontroller för kända och okända identifierare.
* Generera användbara insikter och skala målgrupper med hjälp av AI och maskininlärning från Adobe Sensei som är framtagen för marknadsförare.
* Leverera personaliserade upplevelser i realtid i alla kanaler och på alla destinationer.

Mer information finns i [Real-time Customer Data Platform-dokumentation](../../rtcdp/overview.md).

**Viktiga funktioner**

| Funktion | Beskrivning |
|---|---|
| Mål  | Färdiga integreringar med målplattformar som stöds av Adobe [!DNL Real-Time Customer Data Platform] som smidigt aktiverar data till dessa partners. Se [Destinationer](#destinations) nedan om du vill ha mer information. |
| Kontrollpanel för måttuppgifter på startsida | Hemsidan för Real-time Customer Data Platform (Real-Time CDP) innehåller en mätinstrumentpanel med information om profiler och segment. Hemsidan innehåller även länkar till utbildningsmaterial. Se avsnittet om [Real-time Customer Data Platform metrics](#real-time-customer-data-platform-metrics) nedan. |
| Källor | Du kan importera data från en mängd olika källor som Adobe Solutions, molnbaserad lagring, tredjepartsprogramvara och CRM. Se [Källor](#sources) nedan om du vill veta mer. |

**[!DNL Real-Time Customer Data Platform]mått**

Hemsidan för Real-time Customer Data Platform (Real-Time CDP), som innehåller en mätinstrumentpanel, visas när du loggar in på Real-Time CDP.

Hemsidan är bara en av platserna där metriska kort visas. Real-Time CDP tillhandahåller mätkort genom hela upplevelsen. Dessa mätvärden ger information om data, profiler och målgrupper i systemet.

Om det inte finns några data i systemet när du loggar in på Real-Time CDP visas inte instrumentpanelen på startsidan. I det här fallet innehåller startsidan utbildningsmaterial för en förstagångsupplevelse. När data samlas in uppdateras instrumentpanelen automatiskt för att visa information om dessa data.

Mer information finns i [Real-time Customer Data Platform metrics overview](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdigbyggda integreringar med målplattformar som stöds av Adobe Real-time Customer Data Platform som smidigt aktiverar data till dessa partners. Mer information finns i [Översikt över destinationer](../../destinations/home.md) artikel.

**Tillgängliga destinationer**

I november-versionen stöder Adobe Real-time Customer Data Platform följande destinationer:

* Advertising: [!DNL Google]
* E-postmarknadsföring: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Se [målkatalog](../../destinations/catalog/overview.md) för information om var och en av destinationerna.

**Kända begränsningar**

* Kontrollen som tillåter anpassade aktiveringsscheman i aktiveringsflödet (schemasteget) är inte tillgänglig i den första versionen.
* Det finns för närvarande inget sätt att redigera eller ta bort en målkonfiguration. Om du vill kringgå den här begränsningen kan du aktivera eller inaktivera målet i det övre högra hörnet av [målinformationssida](../../destinations/ui/destination-details-page.md).
* Det finns för närvarande ingen validering för kontoinformation, sökväg eller autentiseringsuppgifter vid anslutning till ditt mål eller lagringskonto. Se till att du anger rätt autentiseringsuppgifter och dubbelkontrollera om det finns stavfel eller stavfel.
* Inga autentiseringsuppgifter har förnyats i den första versionen. När ett konto har gått ut eller behöver uppdateras, måste du skapa en ny målanslutning och mappa om de segment som du tidigare har mappat.

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe Solutions, molnbaserad lagring, tredjepartsprogramvara och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera dig mot dina lagringssystem och CRM-tjänster, ange tider för hur mycket du får ta emot och hantera dataöverföringshastigheten.

**Viktiga funktioner**

| Funktion | Beskrivning |
| ---------- | ------------ |
| Källgränssnitt | Nytt användargränssnitt för att skapa, visa och hantera källanslutningar. |
| Förbättrade arbetsflöden för CRM-anslutningar | Nytt intuitivt arbetsflöde för användargränssnitt för att skapa och hantera [!DNL Microsoft Dynamics] och [!DNL Salesforce] kontakter. |
| Stöd för anslutning för molnbaserade lagringslösningar | Kopplingar kan nu komma åt molnbaserade lagringsmedier. Nya källor innehåller [!DNL Amazon S3], [!DNL Azure Blob]och FTP/SFTP-servrar. |

**Kända fel**

* Källanslutningar för molnbaserade lagringsenheter stöder inte inmatning av komprimerade filer.

Mer information om källor finns i [Översikt över källor](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] gör det möjligt för datavetare att sömlöst generera insikter från data och innehåll i olika Adobe-program och tredjepartssystem genom att bygga och driftsätta Machine Learning-modeller. [!DNL Data Science Workspace] är nära integrerat med [!DNL Platform] och driver datavetenskapens hela livscykel, inklusive utforskning och förberedelse av XDM-data, följt av utveckling och driftsättning av modeller för att automatiskt berika [!DNL Real-Time Customer Profile] med maskininlärningsinsikter.

**Nya funktioner**

| Funktion | Beskrivning |
| -----------| ---------- |
| Dataåtkomst med [!DNL Platform] SDK | Färdiga recept och startböcker för bärbara datorer i [!DNL Python] nu använda [!DNL Platform] SDK för åtkomst av data. |
| Stöd för sandlådor | Stöd för kommande sandlådefunktioner (som för närvarande är i betaversion), inklusive möjligheten att isolera bärbara datorer och recept till utvecklings- eller produktionssandlådor. Se [översikten över sandlådor](../../sandboxes/home.md) för mer information. |

Mer information finns i [Översikt över arbetsytan Datavetenskap](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardisering och interoperabilitet är viktiga begrepp bakom [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), som drivs av Adobe, är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som ska kommunicera med tjänster på Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som levererar insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| ---------- | ------------ |
| Meddelandeschema | Nytt schema som representerar meddelandedata som skickas under dataöverföringsprocessen. |
| Adobe AdCloud-DSP | Fem nya scheman har lagts till för att representera metadata för Adobe Advertising Cloud DSP (Demand-Side Platform) (DSP): Placement, Campaign, Package, Advertiser, Account. |
| Schemafältgrupper för implementeringsinformation för ExperienceEvent | Nya ExperienceEvent-fältgrupper som lägger till ett standardfält för att lagra information om programmet som används för att samla in händelsen. |
| [!DNL Profile Privacy] fältgrupper | Nya profilfältgrupper som lägger till fält som accepterar allmänna avanmälnings- och avanmälningssignaler för försäljning/delning för [!DNL Real-Time Customer Profile]. |
| Formatbegränsningar för `xdm:alternateDisplayInfo` | Fälten Titel och Beskrivning för `xdm:alternateDisplayInfo` måste båda vara strängar för att validera. |
| Namnändring: XDM [!DNL Individual Profile] | &quot;XDM-filens titel&quot; [!DNL Profile]&quot; har uppdaterats till &quot;XDM [!DNL Individual Profile]&quot;. Formellt `$id` för klassen har inte ändrats. |

**Kända fel**

* Ingen.

Mer information om hur du arbetar med XDM med [!DNL Schema Registry] API och [!DNL Schema Editor] användargränssnittet, läs [XDM-systemdokumentation](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-Time Customer Profile]kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| -----------| ---------- |
| Förbättringar av [!DNL Profile] sökning | Användarna kan nu söka efter profiler med hjälp av referensbeskrivningar och relaterade entiteter. |
| Rensa data för en viss datauppsättning | Användare kan nu ta bort data för en viss datauppsättning eller grupp med [!DNL Profile] API för systemjobb. |
| Edge [!DNL Profile] frågeförbättringar | Program kan nu fråga Edge [!DNL Profile] av någon av identiteterna för en viss profil. |
| Konfigurera sammanslagningsprinciper per per projektion | Program kan nu konfigurera sammanslagningsprinciper per per projektion för att generera en vy över data som styrs av en specifik sammanfogningsprincip. |
| Beräknade attribut | Beräknade attribut beräknar automatiskt fältets värde baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån för att samla värden som&quot;totalt inköp&quot;,&quot;livstidsvärde&quot; eller&quot;trattstatus&quot; baserat på en inkommande händelse, inkommande händelse- och profildata eller en inkommande händelse, profildata och historiska händelser. |

**Felkorrigeringar**

* Förenklad lista över tillgängliga strategier för id-sammanslagning när man skapar sammanslagningsprinciper.

**Kända fel**

* Ingen.

Mer information om [!DNL Real-Time Customer Profile], inklusive självstudiekurser och metodtips för att arbeta med [!DNL Profile] data, läs [Kundprofilöversikt i realtid](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper från [!DNL Real-Time Customer Profile] data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform], så att de är lättillgängliga i alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

| Funktion | Beskrivning |
| -----------| ---------- |
| Schemalagd segmentering | Användare kan nu aktivera schemalagd segmentutvärdering för alla segment via gränssnittet och API:t. När du har aktiverat utvärderas alla segment en gång om dagen. Detta påverkar inte segmenteringsfunktioner som fortsätter att fungera som tidigare.<br/><br/>Obs! Den schemalagda segmenteringsfunktionen kan inte användas i sandlådor med mer än fem sammanfogningsprinciper för [!DNL XDM Individual Profile]. |
| Direktuppspelningssegmentering | Stöd för kontinuerlig utvärdering av segment (direktuppspelningssegmentering) gör att de flesta segmentregler kan utvärderas när data skickas till [!DNL Platform]. Den här funktionen innebär att segmentmedlemskapet uppdateras utan att schemalagda segmenteringsjobb behöver köras. Vissa undantag gäller, t.ex. segment som använder relationer med flera enheter eller med anrikade nyttolaster. |
| Segment som byggstenar | När du skapar segment med hjälp av segmentbyggargränssnittet kan användare nu använda tidigare definierade segment som byggstenar för ytterligare segment. <ul><li>Se aktuellt medlemskap: uppdateringar när folk flyttar in och ut från målgrupper.</li><li>Kopieringslogik: använder den valda segmentdefinitionen och duplicerar den i det nya segmentet.</li></ul> |
| Visa segmentmedlemskap efter ID-namnområde | Segmentmedlemskap kan nu visas med ID-namnutrymme (e-post, ECID och totalt antal). |
| Stöd för RBAC | Segment Builder har nu stöd för grundläggande rollbaserade åtkomstkontroller och behörigheter. |
| Förbättrat stöd för extern målgruppsdelning mellan [!DNL Platform] och Adobe | Användarna kan nu ta in externa (icke-[!DNL Experience Platform]) målgruppsmetadata i scenarier där antalet målgrupper är stort eller inte är känt på förhand. Den här versionen innehåller åtkomst till [!DNL Audience Manager] metadata för kunder som har etablerat lösningskonnektorn. Dessa målgruppsmetadata kan användas i Segment Builder för att skapa nya [!DNL Experience Platform] segment. <br/><br/> Dessutom skapades segment i [!DNL Experience Platform] kommer nu att finnas för användning i integrerade Adobe-lösningar, inklusive [!DNL Audience Manager], [!DNL Target]och [!DNL Ad Cloud]. |

**Felkorrigeringar**

* Korrigerade ett problem som medförde att segmentering för flera enheter returnerade nollprofiler vid kapslade relationer.
* Ett problem har korrigerats där exkluderingslogiken returnerade vilseledande resultat.
* Förbättrad läsbarhet för mappar med flera enheter. De visar nu det egna namnet på XDM-klassen.
* Korrigerade ett tillfälligt problem där flera kopior av samma XDM-mapp påträffades.
* Meddelanden skapas nu för att informera en användare om segmentuppskattningar inte är tillgängliga för den valda sammanfogningsprincipen.

**Kända fel**

* Ingen.

Mer information om [!DNL Segmentation Service], kan du läsa [Översikt över segmenteringstjänsten](../../segmentation/home.md).
