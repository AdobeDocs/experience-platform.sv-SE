---
keywords: Experience Platform;hem;populära ämnen;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Source Connector - översikt
topic-legacy: overview
description: Lär dig hur du ansluter Amazon Kinesis till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
translation-type: tm+mt
source-git-commit: af11bc966889be54fc27e02f3eee321519cef88f
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] koppling

Adobe Experience Platform erbjuder systemspecifika anslutningsmöjligheter för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure]. Du kan överföra data från dessa system till [!DNL Platform].

Lagringskällor i molnet kan hämta dina egna data till [!DNL Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. [!DNL Platform] gör att ni kan hämta in data  [!DNL Amazon Kinesis] i realtid.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Förutsättningar

I följande avsnitt finns mer information om nödvändiga inställningar som krävs innan du kan skapa en [!DNL Kinesis]-källanslutning.

### Ställ in åtkomstprincip

En [!DNL Kinesis]-ström kräver följande behörigheter för att skapa en källanslutning:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Dessa behörigheter ordnas via [!DNL Kinesis]-konsolen och kontrolleras av plattformen när du anger dina autentiseringsuppgifter och väljer dataström.

I exemplet nedan visas den lägsta åtkomstbehörighet som krävs för att skapa en [!DNL Kinesis]-källanslutning.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Egenskap | Beskrivning |
| -------- | ----------- |
| `kinesis:GetShardIterator` | En åtgärd som krävs för att gå igenom poster. |
| `kinesis:GetRecords` | En åtgärd som krävs för att hämta poster från ett visst förskjutnings- eller delnings-ID. |
| `kinesis:DescribeStream` | En åtgärd som returnerar information om strömmen, inklusive skuggkartan, som behövs för att generera ett kort-ID. |
| `kinesis:ListStreams` | En åtgärd som krävs för att visa en lista över tillgängliga strömmar som du kan välja i användargränssnittet. |

Mer information om hur du styr åtkomst för [!DNL Kinesis]-dataströmmar finns i följande [[!DNL Kinesis] dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Konfigurera iteratortyp

[!DNL Kinesis] har stöd för följande iteratortyper så att du kan ange ordningen för hur data läses:

| Iteratortyp | Beskrivning |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Data läses från en position som identifieras av ett visst sekvensnummer. |
| `AFTER_SEQUENCE_NUMBER` | Data läses med början efter en position som identifieras av ett visst sekvensnummer. |
| `AT_TIMESTAMP` | Data läses från en position som identifieras av en viss tidsstämpel. |
| `TRIM_HORIZON` | Data läses från den äldsta dataposten. |
| `LATEST` | Data läses från den senaste dataposten. |

En [!DNL Kinesis]-gränssnittskälla stöder för närvarande bara `TRIM_HORIZON`, medan API:t stöder både `TRIM_HORIZON` och `LATEST` som lägen för att hämta data. Standarditeratorvärdet som används för källan [!DNL Kinesis] är `TRIM_HORIZON`.

Mer information om iteratortyper finns i följande [[!DNL Kinesis] dokument](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Anslut [!DNL Amazon Kinesis] till [!DNL Platform]

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Amazon Kinesis] till [!DNL Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Amazon Kinesis-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

- [Skapa en källanslutning till Amazon Kinesis i användargränssnittet](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
