---
title: Skapa en Google PubSub Source-anslutning i användargränssnittet
description: Lär dig hur du skapar en Google PubSub-källanslutning med Experience Platform användargränssnitt.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Skapa en [!DNL Google PubSub]-källanslutning i användargränssnittet

>[!IMPORTANT]
>
>Källan [!DNL Google PubSub] är tillgänglig i källkatalogen för användare som har köpt Real-Time Customer Data Platform Ultimate.

I den här självstudiekursen beskrivs hur du skapar en [!DNL Google PubSub] (kallas nedan [!DNL PubSub]) med Experience Platform användargränssnitt.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

Om du redan har en giltig [!DNL PubSub]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

Du måste ange värden för de anslutningsegenskaper som beskrivs nedan för att kunna ansluta ditt [!DNL PubSub]-konto till Experience Platform. Mer information om autentisering och nödvändiga inställningar finns i [[!DNL PubSub source] översikten](../../../../connectors/cloud-storage/google-pubsub.md#prerequisites).


>[!BEGINTABS]

>[!TAB Projektbaserad autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Projekt-ID | Det projekt-ID som krävs för att autentisera [!DNL PubSub]. |
| Referenser | Autentiseringsuppgifterna som krävs för att autentisera [!DNL PubSub]. Du måste se till att du skickar den fullständiga JSON-filen när du har tagit bort blanktecknen från inloggningsuppgifterna. |

>[!TAB Ämnesbaserad och prenumerationsbaserad autentisering]

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Referenser | Autentiseringsuppgifterna som krävs för att autentisera [!DNL PubSub]. Du måste se till att du skickar den fullständiga JSON-filen när du har tagit bort blanktecknen från inloggningsuppgifterna. |
| Ämnesnamn | Namnet på din [!DNL PubSub]-prenumeration. I [!DNL PubSub] kan du med prenumerationer ta emot meddelanden genom att prenumerera på det ämne som meddelanden har publicerats i. **Obs!**: En enstaka [!DNL PubSub]-prenumeration kan bara användas för ett dataflöde. Om du vill kunna skapa flera dataflöden måste du ha flera prenumerationer. |
| Prenumerationsnamn | Namnet på din [!DNL PubSub]-prenumeration. I [!DNL PubSub] kan du med prenumerationer ta emot meddelanden genom att prenumerera på det ämne som meddelanden har publicerats i. |

>[!ENDTABS]

Mer information om dessa värden finns i följande [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication) -dokument. Om du använder tjänstkontobaserad autentisering kan du läsa följande [PubSub-guide](https://cloud.google.com/docs/authentication/production#create_service_account) för steg om hur du genererar dina autentiseringsuppgifter.

>[!TIP]
>
>Om du använder kontobaserad autentisering för tjänster måste du se till att du har beviljat tillräcklig användaråtkomst till ditt tjänstkonto och att det inte finns några extra tomrum i JSON när du kopierar och klistrar in dina autentiseringsuppgifter.

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att länka ditt [!DNL PubSub]-konto till Experience Platform.

## Anslut ditt [!DNL PubSub]-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Cloud storage] väljer du **[!UICONTROL Google PubSub]** och sedan **[!UICONTROL Add data]**.

![Källkatalogen i Experience Platform UI.](../../../../images/tutorials/create/google-pubsub/catalog.png)

Sidan **[!UICONTROL Connect to Google PubSub]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL PubSub]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontovalet i källarbetsflödet.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nytt konto

>[!TIP]
>
>* När du skapar ett konto med begränsad åtkomst måste du ange minst ett av ämnesnamnen eller prenumerationsnamnen. Autentiseringen misslyckas om båda värdena saknas.
>* När du väl har skapat den kan du inte ändra autentiseringstypen för en [!DNL Google PubSub]-basanslutning. Om du vill ändra autentiseringstypen måste du skapa en ny basanslutning.

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn och en valfri beskrivning för det nya [!DNL PubSub]-kontot.

![Det nya kontogränssnittet för Google PubSub-källan i källarbetsflödet](../../../../images/tutorials/create/google-pubsub/new.png)

Med [!DNL PubSub]-källan kan du ange vilken typ av åtkomst du vill tillåta under autentiseringen. Du kan konfigurera ditt konto så att det antingen har projektbaserad autentisering eller ämne- och prenumerationsbaserad autentisering. Med projektbaserad autentisering kan du bevilja åtkomst till rotnivåprojektet i ditt konto, medan ämnesbaserad och prenumerationsbaserad autentisering gör att du kan begränsa åtkomsten till ett visst [!DNL PubSub]-ämne och en viss prenumeration.

>[!BEGINTABS]

>[!TAB Projektbaserad autentisering]

Om du vill skapa ett konto med åtkomst till rotprojektmappen [!DNL PubSub]. Välj **[!UICONTROL Google PubSub authentication credentials]** som autentiseringstyp och ange ditt projekt-ID och dina autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet för Google PubSub-källan med rotåtkomst markerad.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Ämnesbaserad och prenumerationsbaserad autentisering]

Om du vill skapa ett konto med begränsad åtkomst endast till ett visst [!DNL PubSub]-ämne och en viss prenumeration väljer du **[!UICONTROL Google PubSub Scoped authentication credentials]** och anger sedan dina autentiseringsuppgifter, ämnesnamn och/eller prenumerationsnamn. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet för Google PubSub-källan med områdesåtkomst vald.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Principal (roller) som tilldelats ett [!DNL PubSub]-projekt ärvs i alla ämnen och prenumerationer som skapas i ett [!DNL PubSub]-projekt. Om du vill att ett huvudämne (en roll) ska ha tillgång till ett visst ämne, måste det huvudämnet (rollen) också läggas till i ämnets motsvarande prenumeration. Mer information finns i [[!DNL PubSub] dokumentationen om åtkomstkontroll](<https://cloud.google.com/pubsub/docs/access-control>).

## Markera data

En lyckad autentisering ger dig tillgång till steget [!UICONTROL Select data], där du kan navigera genom din [!DNL PubSub]-datakiarki och välja de data som du vill hämta till Experience Platform.

>[!BEGINTABS]

>[!TAB Projektbaserad autentisering]

Om du har autentiserat dig med projektbaserad åtkomst kommer [!UICONTROL Select data]-gränssnittet att visa alla prenumerationer i ditt projekt som har ett ämne kopplat till sig.

![Det valda datasteget i källarbetsflödet med projektbaserad autentisering.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Ämnesbaserad och prenumerationsbaserad autentisering]

Om du har autentiserat dig med ett ämne och en prenumerationsbaserad åtkomst kan visningen av gränssnittet i [!UICONTROL Select data] variera beroende på vilken information du har angett.

* Om du bara anger ämnesnamnet visas alla avsnitt-prenumerationspar som motsvarar det angivna ämnet i gränssnittet.
* Om du bara anger prenumerationsnamnet visar gränssnittet alla avsnitt-prenumerationspar som motsvarar det angivna prenumerationsnamnet.
* Om både ämne- och prenumerationsnamn anges visas det ämne/prenumerationspar som motsvarar båda angivna värden i gränssnittet.

![Det valda datasteget i källarbetsflödet med ämne- och prenumerationsbaserad autentisering.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en anslutning mellan ditt [!DNL PubSub]-konto och Experience Platform. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta direktuppspelningsdata från ditt molnlagringsutrymme till Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
