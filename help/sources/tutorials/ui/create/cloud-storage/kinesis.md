---
title: Skapa en Amazon Kinesis Source Connection i användargränssnittet
description: Lär dig hur du skapar en källanslutning till Amazon Kinesis med Adobe Experience Platform gränssnitt.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Skapa en [!DNL Amazon Kinesis]-källanslutning i användargränssnittet

>[!IMPORTANT]
>
>Källan [!DNL Amazon Kinesis] är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudien beskrivs hur du autentiserar en [!DNL Amazon Kinesis]-källkoppling (kallas nedan [!DNL "Kinesis"]) med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   - [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Kinesis]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/streaming/cloud-storage-streaming.md).

### Samla in nödvändiga inloggningsuppgifter

Om du vill autentisera [!DNL Kinesis]-källkopplingen måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | Åtkomstnyckel-ID för ditt [!DNL Kinesis]-konto. |
| `Secret access key` | Den hemliga åtkomstnyckeln för ditt [!DNL Kinesis]-konto. |
| `region` | Regionen för din AWS-server. |

Mer information om dessa värden finns i [det här [!DNL Kinesis] dokumentet](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Anslut ditt [!DNL Kinesis]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Kinesis]-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Amazon Kinesis]** under kategorin **[!UICONTROL Cloud Storage]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Kinesis]-koppling.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Dialogrutan **[!UICONTROL Connect to Amazon Kinesis]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New Account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Kinesis]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/kinesis/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Kinesis]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit till ditt [!DNL Kinesis]-konto till [!DNL Platform]. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till  [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
