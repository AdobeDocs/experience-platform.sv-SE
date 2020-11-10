---
keywords: Experience Platform;home;popular topics;Azure Data Explorer;azure data explorer;data explorer;Data Explorer
solution: Experience Platform
title: Skapa en Azure Data Explorer-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: I den här självstudiekursen beskrivs hur du skapar en Azure Data Explorer-källkoppling (nedan kallad Data Explorer) med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---


# Skapa en [!DNL Azure Data Explorer] källanslutning i användargränssnittet

>[!NOTE]
>
> Kopplingen [!DNL Azure Data Explorer] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Azure Data Explorer] källkoppling (nedan kallad[!DNL Data Explorer]) med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Data Explorer] anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Data Explorer] konto [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `endpoint` | Serverns slutpunkt.. [!DNL Data Explorer] . |
| `database` | Namnet på [!DNL Data Explorer] databasen. |
| `tenant` | Det unika klient-ID som används för att ansluta till [!DNL Data Explorer] databasen. |
| `servicePrincipalId` | Det unika tjänstens huvudnamn-ID som används för att ansluta till [!DNL Data Explorer] databasen. |
| `servicePrincipalKey` | Den unika tjänstens huvudnyckel som används för att ansluta till [!DNL Data Explorer] databasen. |

Mer information om hur du kommer igång finns i [ [!DNL Data Explorer] det här dokumentet](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Anslut ditt [!DNL Azure Data Explorer] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Data Explorer] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj under **[!UICONTROL Databases]** kategorin **[!UICONTROL Azure Data Explorer]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa en ny Data Explorer-koppling.

![katalog](../../../../images/tutorials/create/data-explorer/catalog.png)

Sidan visas **[!UICONTROL Connect to Azure Data Explorer]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Data Explorer] inloggningsuppgifter i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/data-explorer/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Data Explorer] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/data-explorer/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Data Explorer] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).