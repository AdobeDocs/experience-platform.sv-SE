---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Amazon Kinesis-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---


# Skapa en [!DNL Amazon Kinesis] källanslutning i användargränssnittet

>[!NOTE]
>Kopplingen [!DNL Amazon Kinesis] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du autentiserar en [!DNL Amazon Kinesis] källkoppling (nedan kallad [!DNL "Kinesis"]) med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett [!DNL Kinesis] konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/streaming/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna autentisera [!DNL Kinesis] källkopplingen måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `accessKeyId` | Åtkomstnyckel-ID för ditt [!DNL Kinesis] konto. |
| `Secret access key` | Den hemliga åtkomstnyckeln för ditt [!DNL Kinesis] konto. |
| `region` | AWS-serverns region. |

Mer information om dessa värden finns i [det här Kinesis-dokumentet](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Anslut ditt [!DNL Kinesis] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Kinesis] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På fliken *Katalog* visas olika källor som du kan ansluta till [!DNL Platform]. Varje källa visar antalet befintliga konton som är kopplade till dem.

Under *[!UICONTROL Cloud Storage]* kategorin väljer du **[!UICONTROL Amazon Kinesis]** följt av **[!UICONTROL Add data]** för att skapa en ny [!DNL Kinesis] koppling.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Dialogrutan *[!UICONTROL Connect to Amazon Kinesis]* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New Account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Kinesis] inloggningsuppgifter i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/kinesis/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Kinesis] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du anslutit till ditt [!DNL Kinesis] konto till [!DNL Platform]. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/streaming/cloud-storage.md).