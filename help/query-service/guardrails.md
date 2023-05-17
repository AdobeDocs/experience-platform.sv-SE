---
keywords: Experience Platform;fråga;frågetjänst;felsökning;skyddsförslag;riktlinjer;gräns;
title: Guardsutkast för frågetjänsten
description: Det här dokumentet innehåller information om användningsgränser för frågetjänstdata som hjälper dig att optimera användningen av frågan.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 1%

---

# Guardsutkast för frågetjänsten

Garantier är trösklar som vägleder användning av data och system, prestandaoptimering och undvikande av fel och oväntade resultat i Adobe Experience Platform.

Det här dokumentet innehåller standardanvändningsgränser för frågetjänstdata som hjälper dig att optimera systemprestanda när du frågar efter data i relation till dina licensrättigheter.

## Förutsättningar

Innan du fortsätter med det här dokumentet bör du ha god förståelse för de viktigaste definitionerna och funktionerna i frågetjänsten. De beskrivs nedan:

* **Ad hoc-frågor**: För körning `SELECT` frågor för att utforska, experimentera och validera data där resultaten av frågorna **lagras inte** på Data Lake.

* **Gruppfrågor**: För körning `INSERT TABLE AS SELECT` och `CREATE TABLE AS SELECT` frågor för att rensa, forma, manipulera och berika data. Resultatet av dessa frågor **lagras** på Data Lake. Mätvärdet för att mäta användningen av den här funktionen är beräkningstimmar.

* **Frågetjänstanvändare**: Frågetjänstanvändare som ingår i din nuvarande licens för Customer Journey Analytics, Adobe Real-time Customer Data Platform och/eller Adobe Journey Optimizer kan också användas med Data Distiller. Frågetjänstanvändare delas mellan funktioner.

* **Ad hoc-användare**: Ad hoc-användare är de som kör ad hoc-frågor.

* **Gruppanvändare**: Batchanvändare är de som kör batchfrågor.

* **Rapporterings-API**: Ett API för att anropa datahämtning (internt eller externt). Utökade rapporteringsdatamodeller härleds från de inbyggda rapportdatamodellerna i Adobe Experience Platform, t.ex. datamodellen för Real-Time CDP dashboards.

Bilden nedan sammanfattar hur funktionerna i tjänsten Query är paketerade och licensierade:

## Begränsningstyper

Det finns två typer av standardgränser i det här dokumentet:

* **Mjuk gräns**: Du kan gå längre än en mjuk gräns, men mjuka gränser ger en rekommenderad vägledning för systemprestanda.

* **Hård gräns**: En hård gräns ger ett absolut maximum.

>[!NOTE]
>
>Standardgränserna som beskrivs i det här dokumentet förbättras kontinuerligt. Kontrollera regelbundet om det finns uppdateringar.

## Prestandagarantier för den primära enheten

Tabellerna nedan innehåller de rekommenderade säkerhetsgränserna och beskrivningarna för frågekörning när ett visst frågemönster används.

**Ad hoc-frågor**

| Guardrail | Gräns | Begränsningstyp | Beskrivning |
|---|---|---|---|
| Maximal körningstid | 10 minuter | Hård | Detta definierar den maximala utdatatiden för en ad hoc-SQL-fråga. Om du överskrider tidsgränsen för att returnera ett resultat genereras felkoden 53400. |
| Användare av Concurrent Query Service | <ul><li>Som anges i produktbeskrivningen för programmet.</li><li>+5 (med varje ytterligare Ad hoc-frågeanvändartillägg köpt)</li></ul> | Hård | Detta definierar hur många användare som kan skapa sessioner samtidigt för en viss organisation. Om samtidighetsgränsen överskrids får användaren en `Session Limit Reached` fel. |
| Frågesamtidighet | <ul><li>Som anges i produktbeskrivningen för programmet.</li><li>+1 (med varje ytterligare Ad hoc-fråga som användaren lägger till i SKU-paket)</li></ul> | Hård | Detta definierar hur många frågor som kan köras samtidigt för en viss organisation. Om samtidighetsgränsen överskrids ställs frågorna i kö. |
| Klientanslutning och utdatagräns för resultat | Klientanslutning<ul><li>Frågegränssnitt (100 rader)</li><li>Tredjepartsklient (50 000)</li><li>[!DNL PostgresSQL] klient (50 000)</li></ul> | Hård | Resultatet av en fråga kan tas emot på följande sätt:<ul><li>Användargränssnitt för frågetjänst</li><li>Tredjepartsklient</li><li>[!DNL PostgresSQL] klient</li></ul>Obs! Om du lägger till en begränsning i antalet utdata kan resultatet bli snabbare. Till exempel: `LIMIT 5`, `LIMIT 10`och så vidare. |
| Resultat returnerade via | Klientgränssnitt | Ej tillämpligt | Detta definierar hur resultaten görs tillgängliga för användarna. |

{style="table-layout:auto"}

**Gruppfrågor**

| **Guardrail** | **Gräns** | **Begränsningstyp** | **Beskrivning** |
|---|---|---|---|
| Maximal körningstid | 24 timmar | Hård | Detta definierar den maximala körningstiden för en batch-SQL-fråga.<br>Bearbetningstiden för en fråga beror på mängden data som ska bearbetas och frågans komplexitet. |
| Användare av Concurrent Query Service för oschemalagd batch | <ul><li>Som anges i produktbeskrivningen för programmet.</li><li>+5 (med varje ytterligare Ad hoc-frågeanvändartillägg köpt)</li></ul> | Hård | För oschemalagda gruppfrågor (till exempel CTAS-/ITAS-frågor i interaktivt läge) definierar detta hur många användare som kan skapa sessioner samtidigt för en viss organisation. Om samtidighetsgränsen överskrids får användaren en `Session Limit Reached` fel. |
| Användare av Concurrent Query Service för schemalagd batch | Ingen användarbegränsning | Ej tillämpligt | Schemalagda batchfrågor är asynkrona jobb så det finns ingen användarbegränsning. |
| Beräkningstimmar för batchdatabearbetning | Enligt vad som anges i kundens Adobe Experience Platform Intelligence Query Custom SKU Sales Order | Mjuk | Detta definierar den beräknade beräkningstiden per år som en kund tillåts köra batchfrågor för att skanna, bearbeta och skriva in data i datasjön. |
| Frågesamtidighet | Stöds | Ej tillämpligt | Schemalagda batchfrågor är asynkrona jobb och samtidiga frågor stöds därför. |
| Klientanslutning och utdatagräns | Klientanslutning<ul><li>Frågegränssnitt (ingen övre gräns till rader)</li><li>Tredjepartsklient (ingen övre gräns för rader)</li><li>[!DNL PostgresSQL] klient (ingen övre gräns till rader)</li><li>REST API:er (ingen övre gräns för rader)</li></ul> | Hård | Resultatet av en fråga kan göras tillgängligt på följande sätt:<ul><li>Kan lagras som härledda datauppsättningar</li><li>Kan infogas i befintliga härledda datauppsättningar</li></ul>Obs! Det finns ingen övre gräns för antal poster från frågeresultatet. |
| Resultat returnerade via | Datauppsättning | Ej tillämpligt | Detta definierar hur resultaten görs tillgängliga för användarna. |

{style="table-layout:auto"}

## Query Accelerated Store {#query-accelerated-store}

Tabellen nedan innehåller de rekommenderade gränserna för skyddsutkast och en beskrivning av det frågeaccelererade arkivet.

| Guardrail | Gräns | Begränsningstyp | Beskrivning |
|---|---|---|---|
| Frågesamtidighet | 4 | Hård | För att säkerställa att frågor om aggregerade data via rapporterings-API:t (inklusive frågor som förbättrar datamodeller som Real-Time CDP datamodeller) har de resurser som krävs för att kunna köras effektivt, spårar API:t resursanvändning genom att tilldela kortplatser för samtidig användning till varje fråga. Systemet placerar frågor i en kö och väntar tills kortplatser för samtidig användning blir tillgängliga eller kan hanteras från cachen. Högst fyra samtidiga frågekortplatser är tillgängliga vid en given tidpunkt.<br>Om du får åtkomst till rapporterings-API:t via ett BI-verktyg och behöver mer samtidighet, krävs en BI-server. |

{style="table-layout:auto"}

## Nästa steg

När du har läst det här dokumentet bör du få en bättre förståelse för standardgränserna för frågekörning med de tillgängliga frågemönstren.

Mer information om frågetjänsten finns i följande dokumentation:

* [API för frågetjänst](./api/getting-started.md)
* [Användargränssnitt för frågetjänst](./ui/overview.md)
