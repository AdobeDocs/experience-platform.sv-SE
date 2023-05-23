---
title: Skapa en Google PubSub Source-anslutning i användargränssnittet
description: Lär dig hur du skapar en Google PubSub-källanslutning med hjälp av användargränssnittet för plattformen.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 79149274c28507041ad89be9d7afdefaedb6aaa0
workflow-type: tm+mt
source-wordcount: '973'
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
| Ämnesnamn | Namnet på [!DNL PubSub] prenumeration. I [!DNL PubSub]kan du få meddelanden genom att prenumerera på det ämne som meddelanden har publicerats i. **Anteckning**: En enstaka [!DNL PubSub] prenumerationen kan bara användas för ett dataflöde. Om du vill kunna skapa flera dataflöden måste du ha flera prenumerationer. |
| Prenumerationsnamn | Namnet på [!DNL PubSub] prenumeration. I [!DNL PubSub]kan du få meddelanden genom att prenumerera på det ämne som meddelanden har publicerats i. |

Mer information om dessa värden finns i följande [PubSub-autentisering](https://cloud.google.com/pubsub/docs/authentication) -dokument. Om du använder kontobaserad autentisering för tjänster, se följande [PubSub Guide](https://cloud.google.com/docs/authentication/production#create_service_account) för steg om hur du genererar dina autentiseringsuppgifter.

>[!TIP]
>
>Om du använder kontobaserad autentisering för tjänster måste du se till att du har beviljat tillräcklig användaråtkomst till ditt tjänstkonto och att det inte finns några extra tomrum i JSON när du kopierar och klistrar in dina autentiseringsuppgifter.

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL PubSub] konto till plattform.

## Koppla samman [!DNL PubSub] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL Google PubSub]** och sedan markera **[!UICONTROL Add data]**.

![Källkatalogen i användargränssnittet i Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

The **[!UICONTROL Connect to Google PubSub]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!DNL PubSub] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontovalet i källarbetsflödet.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nytt konto

>[!TIP]
>
>När du skapar ett konto med begränsad åtkomst måste du ange minst ett av ämnesnamnen eller prenumerationsnamnen. Autentiseringen misslyckas om båda värdena saknas.

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn och en valfri beskrivning av ditt nya [!DNL PubSub] konto.

![Det nya kontogränssnittet för Google PubSub-källan i källarbetsflödet](../../../../images/tutorials/create/google-pubsub/new.png)

The [!DNL PubSub] Med -källa kan du ange vilken typ av åtkomst du vill tillåta under autentiseringen. Du kan konfigurera ditt konto så att det antingen har projektbaserad autentisering eller ämne- och prenumerationsbaserad autentisering. Projektbaserad autentisering ger dig åtkomst till rotnivåprojektet i ditt konto, medan ämnesbaserad och prenumerationsbaserad autentisering gör att du kan begränsa åtkomsten till ett visst [!DNL PubSub] ämne och prenumeration.

>[!BEGINTABS]

>[!TAB Projektbaserad autentisering]

Skapa ett konto med åtkomst till din rot [!DNL PubSub] projektmapp. Välj **[!UICONTROL Google PubSub authentication credentials]** som din autentiseringstyp och ange ditt projekt-ID och dina autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet för Google PubSub-källan med rotåtkomst vald.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Ämnesbaserad och prenumerationsbaserad autentisering]

Så här skapar du ett konto med begränsad åtkomst endast till en viss [!DNL PubSub] ämne och prenumeration, välja **[!UICONTROL Google PubSub Scoped authentication credentials]** och ange dina uppgifter, ämnesnamn och/eller prenumerationsnamn. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet för Google PubSub-källan med områdesåtkomst vald.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Principal (roller) som tilldelats en [!DNL PubSub] -projektet ärvs i alla ämnen och prenumerationer som skapas i ett [!DNL PubSub] projekt. Om du vill att ett huvudämne (en roll) ska ha tillgång till ett visst ämne, måste det huvudämnet (rollen) också läggas till i ämnets motsvarande prenumeration. Mer information finns i [[!DNL PubSub] dokumentation om åtkomstkontroll](<https://cloud.google.com/pubsub/docs/access-control>).

## Markera data

En lyckad autentisering tar dig till [!UICONTROL Select data] steg, där du kan navigera i [!DNL PubSub] datahierarki och markera de data som du vill hämta till Experience Platform.

>[!BEGINTABS]

>[!TAB Projektbaserad autentisering]

Om du har autentiserats med projektbaserad åtkomst visas [!UICONTROL Select data] -gränssnittet visar alla prenumerationer i ditt projekt som har ett tema kopplat till sig.

![Steg för val av data i källarbetsflödet med projektbaserad autentisering.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Ämnesbaserad och prenumerationsbaserad autentisering]

Om du har autentiserat dig med ett ämne och en prenumerationsbaserad åtkomst visas [!UICONTROL Select data] hur gränssnittet visas kan variera beroende på vilken information du anger.

* Om du bara anger ämnesnamnet visas alla avsnitt-prenumerationspar som motsvarar det angivna ämnet i gränssnittet.
* Om du bara anger prenumerationsnamnet visar gränssnittet alla avsnitt-prenumerationspar som motsvarar det angivna prenumerationsnamnet.
* Om både ämne- och prenumerationsnamn anges visas det ämne/prenumerationspar som motsvarar båda angivna värden i gränssnittet.

![Steg för val av data i källarbetsflödet med ämne- och prenumerationsbaserad autentisering.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en anslutning mellan [!DNL PubSub] konto och plattform. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta strömmande data från ditt molnlagringsutrymme till plattformen](../../dataflow/streaming/cloud-storage-streaming.md).
