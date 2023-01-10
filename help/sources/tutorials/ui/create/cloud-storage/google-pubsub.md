---
keywords: Experience Platform;hem;populära ämnen;Google PubSub;google pubsub
solution: Experience Platform
title: Skapa en Google PubSub Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Google PubSub-källanslutning med hjälp av användargränssnittet för plattformen.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# Skapa en [!DNL Google PubSub] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Google PubSub] (nedan kallad[!DNL PubSub]&quot;) med användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Om du redan har en giltig [!DNL PubSub] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL PubSub] till Platform måste du ange ett giltigt värde för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `projectId` | Det projekt-ID som krävs för autentisering [!DNL PubSub]. |
| `credentials` | Autentiseringsuppgiften eller det privata nyckel-ID som krävs för autentisering [!DNL PubSub]. |

Mer information om dessa värden finns i följande [PubSub-autentisering](https://cloud.google.com/pubsub/docs/authentication) -dokument. Om du använder kontobaserad autentisering för tjänster, se följande [PubSub Guide](https://cloud.google.com/docs/authentication/production#create_service_account) för steg om hur du genererar dina autentiseringsuppgifter.

>[!TIP]
>
>Om du använder kontobaserad autentisering för tjänster måste du se till att du har beviljat tillräcklig användaråtkomst till ditt tjänstkonto och att det inte finns några extra tomrum i JSON när du kopierar och klistrar in dina autentiseringsuppgifter.

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL PubSub] konto till plattform.

## Koppla samman [!DNL PubSub] konto

I [Plattformsgränssnitt](https://platform.adobe.com), markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL Google PubSub]** och sedan markera **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/google-pubsub/catalog.png)

The **[!UICONTROL Connect to Google PubSub]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!DNL PubSub] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och [!DNL PubSub] autentiseringsuppgifter för indataformuläret. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Nästa steg

Om du följer den här självstudiekursen måste du skapa en anslutning mellan [!DNL PubSub] konto och plattform. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta strömmande data från ditt molnlagringsutrymme till plattformen](../../dataflow/streaming/cloud-storage-streaming.md).
