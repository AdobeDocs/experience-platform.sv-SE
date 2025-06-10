---
title: Amazon Kinesis Source Connector - översikt
description: Lär dig hur du ansluter Amazon Kinesis till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# [!DNL Amazon Kinesis]-källa

>[!IMPORTANT]
>
>- Källan [!DNL Amazon Kinesis] är tillgänglig i källkatalogen för användare som har köpt Real-Time CDP Ultimate.
>
>- Du kan nu använda källan [!DNL Amazon Kinesis] när du kör Adobe Experience Platform på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../landing/multi-cloud.md).


Adobe Experience Platform erbjuder inbyggd anslutning för molnleverantörer som AWS, [!DNL Google Cloud Platform] och [!DNL Azure]. Du kan hämta data från dessa system till [!DNL Experience Platform].

Molnlagringskällor kan hämta dina egna data till [!DNL Experience Platform] utan att du behöver hämta, formatera eller överföra dem. Inkapslade data kan formateras som XDM JSON, XDM Parquet eller avgränsade. Varje steg i processen är integrerat i arbetsflödet för källor. Med [!DNL Experience Platform] kan du hämta data från [!DNL Amazon Kinesis] i realtid.

>[!NOTE]
>
>Skalningsfaktorn för [!DNL Kinesis] måste ökas om du behöver importera data med hög volym. För närvarande är den maximala datavolymen som du kan hämta från ditt [!DNL Kinesis]-konto till Experience Platform 4 000 poster per sekund. Om du vill skala upp och importera data i större volymer kontaktar du Adobe.

## Förhandskrav

I följande avsnitt finns mer information om nödvändiga inställningar som krävs innan du kan skapa en [!DNL Kinesis]-källanslutning.

### Ställ in åtkomstprincip

En [!DNL Kinesis]-dataström kräver följande behörigheter för att skapa en källanslutning:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Dessa behörigheter ordnas via [!DNL Kinesis]-konsolen och kontrolleras av Experience Platform när du anger dina autentiseringsuppgifter och väljer dataström.

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

Mer information om hur du styr åtkomst för [!DNL Kinesis] dataströmmar finns i följande [[!DNL Kinesis] dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Konfigurera iteratortyp

[!DNL Kinesis] har stöd för följande iteratortyper så att du kan ange ordningen för hur data läses:

| Iterator-typ | Beskrivning |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Data läses från en position som identifieras av ett visst sekvensnummer. |
| `AFTER_SEQUENCE_NUMBER` | Data läses med början efter en position som identifieras av ett visst sekvensnummer. |
| `AT_TIMESTAMP` | Data läses från en position som identifieras av en viss tidsstämpel. |
| `TRIM_HORIZON` | Data läses från den äldsta dataposten. |
| `LATEST` | Data läses från den senaste dataposten. |

En [!DNL Kinesis]-gränssnittskälla har för närvarande bara stöd för `TRIM_HORIZON`, medan API:t har stöd för både `TRIM_HORIZON` och `LATEST` som lägen för att hämta data. Standarditeratorvärdet som används av Experience Platform för källan [!DNL Kinesis] är `TRIM_HORIZON`.

Mer information om iteratortyper finns i följande [[!DNL Kinesis] dokument](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Anslut [!DNL Amazon Kinesis] till [!DNL Experience Platform]

>[!NOTE]
>
>När du har skapat eller uppdaterat ett dataflöde för direktuppspelning krävs en kort 5-minuters paus i datainmatningen för att förhindra eventuella fall av dataförlust eller dataförlust.

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Amazon Kinesis] till [!DNL Experience Platform] med API:er eller användargränssnittet:

### Använda API:er

- [Skapa en Amazon Kinesis-källanslutning med API:t för Flow Service](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Samla in strömmande data med API:t för Flow Service](../../tutorials/api/collect/streaming.md)

### Använda gränssnittet

- [Skapa en Amazon Kinesis-källanslutning i användargränssnittet](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurera ett dataflöde för en molnlagringsanslutning i användargränssnittet](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
