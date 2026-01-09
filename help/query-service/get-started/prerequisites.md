---
keywords: Experience Platform;frågetjänst;frågetjänst;fråga
title: Komma igång med Adobe Experience Platform Query Service
description: En beskrivning av de steg som krävs för att fullt ut utnyttja Adobe Experience Platform Query Service
exl-id: 36ab9354-23f9-4cb8-bcd4-00fe076386ab
source-git-commit: fa22a0ca0c79d5d62fd39de3a808f84a11a80c4d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Komma igång med Adobe Experience Platform [!DNL Query Service] {#getting-started}

Använd Adobe Experience Platform Query Service för att köra SQL-frågor mot kapslade datauppsättningar, koppla data från flera källor och generera härledda datauppsättningar för analyser, maskininlärningsarbetsflöden eller kundprofil i realtid. När du har inhämtat data kan du få åtkomst till Query Service via gränssnittet för interaktiv analys och samarbete, eller via API:t för automatiserad och programmatisk frågekörning.

## Förhandskrav {#prerequisites}

Kontrollera att du har:

- **Nödvändig behörighet**: Ditt användarkonto har åtkomst till frågetjänsten i Experience Platform. Om tjänsten inte är tillgänglig i användargränssnittet läser du [permissions-dokumentationen](../../access-control/home.md#permissions) och kontaktar systemadministratören.
- **Inläsning av data**: Du har inhämtat data till Experience Platform.

Om du behöver importera data kan du titta i självstudievideon [för datafrågor](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=sv-SE) och få en översikt över hur du skapar datauppsättningar, schemamappning, inmatning och validering. Läs översiktsdokumentationen för [frågor](../../ingestion/home.md) om du vill ha mer information och länkar till andra utbildningsresurser.

## Snabbstartbanor

När du har importerat dina data till Experience Platform kan du börja arbeta med frågetjänsten med antingen [!DNL Query Editor] i Experience Platform eller API:t för frågetjänsten.

### [!DNL Query Editor]

Använd [!DNL Query Editor] för analys, datautforskning och utveckling av samarbetsfrågor. En översikt över gränssnittsfunktionerna finns i [dokumentationen för frågetjänstens användargränssnitt](../ui/overview.md). Läs [[!DNL Query Editor user guide]](../ui/user-guide.md) om du vill veta mer om hur du skriver och kör frågor i användargränssnittet.

### API för frågetjänst

Använd API:t för frågetjänster för automatiserade arbetsflöden, hantering av frågemallar och programmatiska integreringar. Mer information om hur du använder API:t för frågetjänsten finns i [Utvecklarhandboken för frågetjänsten](../api/getting-started.md).

## Nästa steg

Det här dokumentet innehåller de krav som krävs för att använda [!DNL Query Service]-funktioner i Experience Platform. Du rekommenderas att läsa följande dokument för att snabbt komma igång med att använda funktionerna i frågetjänsten:

- [Allmän vägledning för frågekörning](../best-practices/writing-queries.md)
- [SQL-syntax i Query Service](../sql/syntax.md)
- [Skapa härledda datauppsättningar med SQL](../data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

Du kan även läsa mer om hur Query Service fungerar med databearbetning i Experience Platform genom att titta på [presentationen av det övergivna bläddringsexemplet](../use-cases/abandoned-browse.md#video-example).

Följande resurser är användbara för att förbättra din förståelse av [!DNL Query Service]:

- [Översikt över användargränssnittet för [!DNL Query Service]](../ui/overview.md)
- [[!DNL Query Service] autentiseringsuppgifter](../ui/credentials.md)
- [Översikt över klientanslutningar](../clients/overview.md)
