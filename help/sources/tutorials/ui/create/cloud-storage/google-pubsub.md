---
keywords: Experience Platform;hem;populära ämnen;Google PubSub;google pubsub
solution: Experience Platform
title: Skapa en Google PubSub Source-anslutning i användargränssnittet
topic: översikt
type: Självstudiekurs
description: Lär dig hur du skapar en Google PubSub-källanslutning med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---


# Skapa en [!DNL Google PubSub]-källanslutning i användargränssnittet

>[!NOTE]
>
> [!DNL Google PubSub]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

I den här självstudiekursen beskrivs hur du skapar en [!DNL Google PubSub] (kallas nedan [!DNL PubSub]) med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Om du redan har en giltig [!DNL PubSub]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

Om du vill ansluta [!DNL PubSub] till plattformen måste du ange ett giltigt värde för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `projectId` | Det projekt-ID som krävs för att autentisera [!DNL PubSub]. |
| `credentials` | Autentiseringsuppgiften eller nyckeln som krävs för att autentisera [!DNL PubSub]. |

Mer information om dessa värden finns i följande [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication)-dokument.

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Blob]-konto till Platform.

## Anslut ditt [!DNL PubSub]-konto

I [Plattformsgränssnittet](https://platform.adobe.com) väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Cloud storage] väljer du **[!UICONTROL Google PubSub]** och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/google-pubsub/catalog.png)

Sidan **[!UICONTROL Connect to Google PubSub]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL PubSub]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och inloggningsuppgifterna för [!DNL PubSub] i indataformuläret. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Nästa steg

Genom att följa den här självstudiekursen måste du skapa en anslutning mellan ditt [!DNL PubSub]-konto och din plattform. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta direktuppspelningsdata från ditt molnlagringsutrymme till plattformen](../../dataflow/streaming/cloud-storage-streaming.md).
