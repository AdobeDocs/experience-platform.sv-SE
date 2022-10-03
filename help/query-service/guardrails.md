---
keywords: Experience Platform;fråga;frågetjänst;felsökning;skyddsförslag;riktlinjer;gräns;
title: Guardsutkast för frågetjänsten
description: Det här dokumentet innehåller information om användningsgränser för frågetjänstdata som hjälper dig att optimera användningen av frågan.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: d874fed681449c6f5114196cface157c8c406d69
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 1%

---

# Garantier för frågetjänstdata

Garantier är trösklar som ger vägledning för data- och systemanvändning, prestandaoptimering och undvikande av fel eller oväntade resultat i Adobe Experience Platform.

Det här dokumentet innehåller standardanvändningsgränser för frågetjänstdata som hjälper dig att optimera systemprestanda när du frågar efter data i relation till dina licensrättigheter.

## Förutsättningar

Innan du fortsätter med det här dokumentet bör du ha en god förståelse för de två nyckelfunktionerna i frågetjänsten som beskrivs nedan:

* **Ad hoc-frågor**: För körning `SELECT` frågor för att utforska, experimentera och validera data där resultaten av frågorna **lagras inte** på Data Lake.

* **Gruppfrågor**: För körning `INSERT TABLE AS SELECT` och `CREATE TABLE AS SELECT` frågor för att rensa, forma, manipulera och berika data. Resultatet av dessa frågor **lagras** på Data Lake. Mätvärdet för att mäta användningen av den här funktionen är beräkningstimmar.

>[!IMPORTANT]
>
>För att säkerställa att varje fråga för en Real-time Customer Data Platform insights-instrumentpanel har tillräckligt med resurser för att kunna köras effektivt, spårar API:t resursanvändningen genom att tilldela varje fråga kortplatser för samtidig användning. Systemet kan bearbeta upp till fyra samtidiga frågor, och därför är fyra samtidiga frågeplatser tillgängliga vid en given tidpunkt. Frågor placeras i en kö baserat på kortplatser för samtidig användning och väntar sedan i kön tills det finns tillräckligt med kortplatser för samtidig användning.

Bilden nedan sammanfattar hur funktionerna i tjänsten Query är paketerade och licensierade:

![Ett diagram som förklarar distributionen och paketeringen av Query Service-funktioner i samband med licensiering.](./images/guardrails/query-capabilities.png)

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

| **Guardrail** | **Gräns** | **Begränsningstyp** | **Beskrivning** |
|---|---|---|---|
| Maximal körningstid | 10 minuter | Hård | Detta definierar den maximala utdatatiden för en ad hoc-SQL-fråga. Om du överskrider tidsgränsen för att returnera ett resultat genereras felkoden 53400. |
| Frågesamtidighet | <ul><li>Som anges i produktbeskrivningen för programmet.</li><li>+1 (med varje ytterligare SKU-paket för ad hoc-fråga som användaren lägger till)</li></ul> | Hård | Detta definierar hur många frågor som kan köras samtidigt för en viss organisation. Om samtidighetsgränsen överskrids ställs frågorna i kö. |
| Klientanslutning och utdatagräns för resultat | Klientanslutning<ul><li>Frågegränssnitt (100 rader)</li><li>Tredjepartsklient (50 000)</li><li>[!DNL PostgresSQL] klient (50 000)</li></ul> | Hård | Resultatet av en fråga kan tas emot på följande sätt:<ul><li>Användargränssnitt för frågetjänst</li><li>Tredjepartsklient</li><li>[!DNL PostgresSQL] klient</li></ul>Obs! Om du lägger till en begränsning i antalet utdata kan resultatet bli snabbare. Till exempel: `LIMIT 5`, `LIMIT 10`och så vidare. |
| Resultat returnerade via | Klientgränssnitt | Ej tillämpligt | Detta definierar hur resultaten görs tillgängliga för användarna. |

{style=&quot;table-layout:auto&quot;}

**Gruppfrågor**

| **Guardrail** | **Gräns** | **Begränsningstyp** | **Beskrivning** |
|---|---|---|---|
| Maximal körningstid | 24 timmar | Hård | Detta definierar den maximala körningstiden för en batch-SQL-fråga.<br>Bearbetningstiden för en fråga beror på mängden data som ska bearbetas och frågans komplexitet. |
| Samtidighet för användare | Ingen användarbegränsning | Ej tillämpligt | Schemalagda gruppfrågor är asynkrona jobb så det finns ingen begränsning för användaren. |
| Beräkningstimmar för batchdatabearbetning | Enligt vad som anges i kundens Adobe Experience Platform Intelligence Query Custom SKU Sales Order | Mjuk | Detta definierar den mängd beräkningstid per år som en kund tillåts köra batchfrågor för att skanna, bearbeta och skriva in data i datasjön. |
| Frågesamtidighet | Stöds | Ej tillämpligt | Schemalagda batchfrågor är asynkrona jobb och samtidiga frågor stöds därför. |
| Klientanslutning och utdatagräns | Klientanslutning<ul><li>Frågegränssnitt (ingen övre gräns till rader)</li><li>Tredjepartsklient (ingen övre gräns för rader)</li><li>[!DNL PostgresSQL] klient (ingen övre gräns till rader)</li><li>REST API:er (ingen övre gräns för rader)</li></ul> | Hård | Resultatet av en fråga kan göras tillgängligt på följande sätt:<ul><li>Kan lagras som härledda datauppsättningar</li><li>Kan infogas i befintliga härledda datauppsättningar</li></ul>Obs! Det finns ingen övre gräns för antal poster från frågeresultatet. |
| Resultat returnerade via | Datauppsättning | Ej tillämpligt | Detta definierar hur resultaten görs tillgängliga för användarna. |

{style=&quot;table-layout:auto&quot;}

## Nästa steg

När du har läst det här dokumentet bör du få en bättre förståelse för standardgränserna för frågekörning med de tillgängliga frågemönstren.

Mer information om frågetjänsten finns i följande dokumentation:

* [API för frågetjänst](./api/getting-started.md)
* [Användargränssnitt för frågetjänst](./ui/overview.md)
