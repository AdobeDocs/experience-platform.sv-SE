---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en källanslutning för Amazon Kinesis i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Skapa en källanslutning för Amazon Kinesis i användargränssnittet

>[!NOTE]
> Amazon Kinesis-kontakten är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du autentiserar en källanslutning till en Amazon Kinesis (nedan kallad Kinesis) med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett Kinesis-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/streaming/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna autentisera Kinesis-källkopplingen måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | Åtkomstnyckel-ID för ditt Kinesis-konto. |
| `Secret access key` | Den hemliga åtkomstnyckeln för ditt Kinesis-konto. |
| `region` | AWS-serverns region. |

Mer information om dessa värden finns i [det här Kinesis-dokumentet](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Anslut ditt Kinesis-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt Kinesis-konto till plattformen.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På fliken *Katalog* visas en rad olika källor som kan anslutas till plattformen. Varje källa visar antalet befintliga konton som är kopplade till dem.

Under kategorin *Cloud-lagring* väljer du **Amazon Kinesis** och klickar **på plusikonen (+)** för att skapa en ny Kinesis-anslutning.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Dialogrutan *Anslut till Amazon Kinesis* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. Ange ett namn, en valfri beskrivning och dina Kinesis-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **Anslut** och tillåt sedan en tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/eventhub/new.png)

### Befintligt konto

Om du vill ansluta till ett befintligt konto väljer du det Kinesis-konto som du vill ansluta till och väljer sedan **Nästa** för att fortsätta.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit till ditt Kinesis-konto till Platform. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/streaming/cloud-storage.md).