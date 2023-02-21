---
title: Skapa en Google PubSub Source-anslutning i användargränssnittet
description: Lär dig hur du skapar en Google PubSub-källanslutning med hjälp av användargränssnittet för plattformen.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

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
| Projekt-ID | Det projekt-ID som krävs för autentisering [!DNL PubSub]. |
| Autentiseringsuppgifter | Autentiseringsuppgiften eller det privata nyckel-ID som krävs för autentisering [!DNL PubSub]. |
| Ämne-ID | ID för [!DNL PubSub] en resurs som representerar en feed med meddelanden. Du måste ange ett ämne-ID om du vill ge åtkomst till en viss dataström i ditt [!DNL Google PubSub] källa. |
| Prenumerations-ID | Ditt ID [!DNL PubSub] prenumeration. I [!DNL PubSub]kan du få meddelanden genom att prenumerera på det ämne som meddelanden har publicerats i. |

Mer information om dessa värden finns i följande [PubSub-autentisering](https://cloud.google.com/pubsub/docs/authentication) -dokument. Om du använder kontobaserad autentisering för tjänster, se följande [PubSub Guide](https://cloud.google.com/docs/authentication/production#create_service_account) för steg om hur du genererar dina autentiseringsuppgifter.

>[!TIP]
>
>Om du använder kontobaserad autentisering för tjänster måste du se till att du har beviljat tillräcklig användaråtkomst till ditt tjänstkonto och att det inte finns några extra tomrum i JSON när du kopierar och klistrar in dina autentiseringsuppgifter.

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL PubSub] konto till plattform.

## Koppla samman [!DNL PubSub] konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL Google PubSub]** och sedan markera **[!UICONTROL Add data]**.

![Källkatalogen i användargränssnittet i Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

The **[!UICONTROL Connect to Google PubSub]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!DNL PubSub] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontovalet i källarbetsflödet.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och [!DNL PubSub] autentiseringsuppgifter för indataformuläret. Under det här steget kan du definiera de data som ditt konto har åtkomst till genom att ange ett ämne-ID. Det är bara prenumerationer som är kopplade till detta ämne-ID som är tillgängliga.

>[!NOTE]
>
>Principal (roller) som tilldelats ett underordnat projekt ärvs i alla ämnen och prenumerationer som skapas i ett [!DNL PubSub] projekt. Om du vill lägga till ett huvudämne (roll) för att få tillgång till ett visst ämne, måste det huvudämnet (rollen) också läggas till i ämnets motsvarande prenumeration. Mer information finns i [[!DNL PubSub] dokumentation om åtkomstkontroll](https://cloud.google.com/pubsub/docs/access-control).

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet i källarbetsflödet.](../../../../images/tutorials/create/google-pubsub/new.png)

## Nästa steg

Om du följer den här självstudiekursen måste du skapa en anslutning mellan [!DNL PubSub] konto och plattform. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta strömmande data från ditt molnlagringsutrymme till plattformen](../../dataflow/streaming/cloud-storage-streaming.md).
