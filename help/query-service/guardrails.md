---
keywords: Experience Platform;fråga;frågetjänst;felsökning;skyddsförslag;riktlinjer;gräns;
title: Guardsutkast för frågetjänsten
description: Det här dokumentet innehåller information om användningsgränser för frågetjänstdata som hjälper dig att optimera användningen av frågan.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---

# Guardsutkast för frågetjänsten

Garantier är trösklar som vägleder användning av data och system, prestandaoptimering och undvikande av fel och oväntade resultat i Adobe Experience Platform.
Det här dokumentet innehåller standardanvändningsgränser för frågetjänstdata som hjälper dig att optimera systemprestanda när du frågar efter data i relation till dina licensrättigheter.

>[!IMPORTANT]
>
>Kontrollera dina licensrättigheter i din försäljningsorder och motsvarande [produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions.html) om faktiska användningsbegränsningar, utöver den här sidan med skyddsförslag.

## Förhandskrav

Innan du fortsätter med det här dokumentet bör du ha god förståelse för de viktigaste definitionerna och funktionerna i frågetjänsten. De beskrivs nedan:

* **Ad hoc-frågor**: För att köra `SELECT` -frågor för att utforska, experimentera och validera data där resultaten av frågorna **inte lagras** i datasjön.

* **Gruppfrågor**: För att köra `INSERT TABLE AS SELECT` - och `CREATE TABLE AS SELECT`-frågor för att rensa, forma, manipulera och förbättra data. Resultaten av de här frågorna **lagras** på datarjön. Mätvärdet för att mäta användningen av den här funktionen är beräkningstimmar.

* **Query Service-användare**: Frågetjänstanvändare som tillhandahålls i din aktuella licens för Customer Journey Analytics, Adobe Real-time Customer Data Platform och/eller Adobe Journey Optimizer kan också användas med Data Distiller. Frågetjänstanvändare delas mellan funktioner.

* **Ad hoc-användare**: Det är Ad hoc-användare som kör ad hoc-frågor.

* **Gruppanvändare**: Det är gruppanvändare som kör gruppfrågor.

* **Rapporterings-API**: Ett API för att anropa datahämtning (internt eller externt). Utökade rapporteringsdatamodeller härleds från de inbyggda rapportdatamodellerna i Adobe Experience Platform, t.ex. datamodellen för Real-Time CDP dashboards.

Bilden nedan sammanfattar hur funktionerna i tjänsten Query är paketerade och licensierade:

## Skyddstyper

Det finns två typer av standardgränser i det här dokumentet:

| Typ av skyddsräcke | Beskrivning |
|----------|---------|
| **Prestandaskydd (mjuk gräns)** | Prestandaskydd är användarbegränsningar som relaterar till omfattningen av dina användningsfall. När du överskrider prestandaskyddet kan du uppleva prestandaförsämringar och fördröjning. Adobe ansvarar inte för sådana prestandaförsämringar. Kunder som genomgående överskrider ett prestandaresäkerhetsskydd kan välja att licensiera ytterligare kapacitet för att undvika prestandaförsämringar. |
| **Systemstyrda skyddsräcken (hård begränsning)** | Systemstyrda skyddsräcken används av Real-Time CDP gränssnitt eller API. Det här är begränsningar som du inte kan överskrida eftersom gränssnittet och API kommer att blockera dig från att göra det eller returnera ett fel. |

{style="table-layout:auto"}

>[!NOTE]
>
>Standardgränserna som beskrivs i det här dokumentet förbättras kontinuerligt. Kontrollera regelbundet om det finns uppdateringar.

## Prestandagarantier för den primära enheten

Tabellerna nedan innehåller de rekommenderade säkerhetsgränserna och beskrivningarna för frågekörning när ett visst frågemönster används.

**Ad hoc-frågor**

| Guardrail | Gräns | Begränsningstyp | Beskrivning |
|---|---|---|---|
| Maximal körningstid | 10 minuter | Systemstyrt skyddsräcke | Detta definierar den maximala utdatatiden för en ad hoc-SQL-fråga. Om du överskrider tidsgränsen för att returnera ett resultat genereras felkoden 53400. |
| Användare av Concurrent Query Service | <ul><li>Som anges i produktbeskrivningen för programmet.</li><li>+5 (med varje ytterligare Ad hoc-frågeanvändartillägg inköpt)</li></ul> | Systemstyrt skyddsräcke | Detta definierar hur många användare som kan skapa sessioner samtidigt för en viss organisation. Om samtidighetsgränsen överskrids får användaren ett `Session Limit Reached`-fel. |
| Frågesamtidighet | <ul><li>Som anges i produktbeskrivningen för programmet.</li><li>+1 (med varje ytterligare Ad hoc-fråga som användaren lägger till i SKU-paket)</li></ul> | Systemstyrt skyddsräcke | Detta definierar hur många frågor som kan köras samtidigt för en viss organisation. Om samtidighetsgränsen överskrids ställs frågorna i kö. |
| Klientanslutning och utdatagräns för resultat | Klientanslutning<ul><li>Frågegränssnitt (100 rader)</li><li>Tredjepartsklient (50 000)</li><li>[!DNL PostgresSQL] klient (50 000)</li></ul> | Systemstyrt skyddsräcke | Resultatet av en fråga kan tas emot på följande sätt:<ul><li>Användargränssnitt för frågetjänst</li><li>Tredjepartskund</li><li>[!DNL PostgresSQL]-klient</li></ul>Obs! Om du lägger till en begränsning i antalet utdata kan resultatet bli snabbare. Till exempel `LIMIT 5`, `LIMIT 10` och så vidare. |
| Resultat returnerade via | Klientgränssnitt | N/A | Detta definierar hur resultaten görs tillgängliga för användarna. |

{style="table-layout:auto"}

**Gruppfrågor**

| **Guardrail** | **Gräns** | **Begränsa typ** | **Beskrivning** |
|---|---|---|---|
| Maximal körningstid | 24 timmar | Systemstyrt skyddsräcke | Detta definierar den maximala körningstiden för en batch-SQL-fråga.<br>Bearbetningstiden för en fråga beror på mängden data som ska bearbetas och frågans komplexitet. |
| Användare av Concurrent Query Service för oschemalagd batch | <ul><li>Som anges i produktbeskrivningen för programmet.</li><li>+5 (med varje ytterligare Ad hoc-frågeanvändartillägg inköpt)</li></ul> | Systemstyrt skyddsräcke | För oschemalagda gruppfrågor (till exempel CTAS-/ITAS-frågor i interaktivt läge) definierar detta hur många användare som kan skapa sessioner samtidigt för en viss organisation. Om samtidighetsgränsen överskrids får användaren ett `Session Limit Reached`-fel. |
| Användare av Concurrent Query Service för schemalagd batch | Ingen användarbegränsning | N/A | Schemalagda batchfrågor är asynkrona jobb så det finns ingen användarbegränsning. |
| Beräkningstimmar för batchdatabearbetning | Enligt vad som anges i kundens Adobe Experience Platform Intelligence Query Custom SKU Sales Order | Prestandaskydd | Detta definierar den beräknade beräkningstiden per år som en kund tillåts köra batchfrågor för att skanna, bearbeta och skriva in data i datasjön. |
| Frågesamtidighet | Stöds | N/A | Schemalagda batchfrågor är asynkrona jobb och samtidiga frågor stöds därför. |
| Klientanslutning och utdatagräns | Klientanslutning<ul><li>Frågegränssnitt (ingen övre gräns till rader)</li><li>Tredjepartsklient (ingen övre gräns för rader)</li><li>[!DNL PostgresSQL]-klient (ingen övre gräns för rader)</li><li>REST API:er (ingen övre gräns för rader)</li></ul> | Systemstyrt skyddsräcke | Resultatet av en fråga kan göras tillgängligt på följande sätt:<ul><li>Kan lagras som härledda datauppsättningar</li><li>Kan infogas i befintliga härledda datauppsättningar</li></ul>Obs! Det finns ingen övre gräns för antal poster från frågeresultatet. |
| Resultat returnerade via | Datauppsättning | N/A | Detta definierar hur resultaten görs tillgängliga för användarna. |

{style="table-layout:auto"}

## Query Accelerated Store {#query-accelerated-store}

Tabellen nedan innehåller de rekommenderade gränserna för skyddsutkast och en beskrivning av det frågeaccelererade arkivet.

| Guardrail | Gräns | Begränsningstyp | Beskrivning |
|---|---|---|---|
| Frågesamtidighet | 4 | Systemstyrt skyddsräcke | För att säkerställa att frågor om aggregerade data via rapporterings-API:t (inklusive frågor som förbättrar datamodeller som Real-Time CDP datamodeller) har de resurser som krävs för att kunna köras effektivt, spårar API:t resursanvändning genom att tilldela kortplatser för samtidig användning till varje fråga. Systemet placerar frågor i en kö och väntar tills kortplatser för samtidig användning blir tillgängliga eller de kan hanteras från cachen. Högst fyra samtidiga frågekortplatser är tillgängliga vid en given tidpunkt.<br>Om du får åtkomst till rapporterings-API:t via ett BI-verktyg och behöver mer samtidighet, krävs en BI-server. |

{style="table-layout:auto"}

## Nästa steg

När du har läst det här dokumentet bör du få en bättre förståelse för standardgränserna för frågekörning med de tillgängliga frågemönstren.

Mer information om frågetjänsten finns i följande dokumentation:

* [API för frågetjänst](./api/getting-started.md)
* [Användargränssnitt för frågetjänst](./ui/overview.md)

Följande dokumentation innehåller mer information om andra Experience Platform-servicesäkrar, om total latenstid och licensinformation från Real-Time CDP produktbeskrivningsdokument:

* [Real-Time CDP skyddsräcken](/help/rtcdp/guardrails/overview.md)
* [Latensdiagram från början till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) för olika Experience Platform-tjänster.
* [Real-time Customer Data Platform (B2C-utgåva - Premiere- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)