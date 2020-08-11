---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Azure File Storage-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---


# Skapa en [!DNL Azure File Storage] källanslutning i användargränssnittet

>[!NOTE]
>Kopplingen [!DNL Azure File Storage] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du autentiserar en [!DNL Azure File Storage] källanslutning med [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en fillagringsanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna autentisera [!DNL Azure File Storage] källkopplingen måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Slutpunkten för den [!DNL Azure File Storage] instans du försöker komma åt. |
| `userId` | Användaren har tillräcklig åtkomst till [!DNL Azure File Storage] slutpunkten. |
| `password` | Åtkomstnyckeln [!DNL Azure File Storage] . |

Mer information om hur du kommer igång finns i [det här Azure File Storage-dokumentet](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Anslut ditt [!DNL Azure File Storage] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt [!DNL Azure File Storage] konto att ansluta till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa ett inkommande konto för, och varje källa visar antalet befintliga konton och dataflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL Azure File Storage]** följt av **[!UICONTROL Add data]** för att skapa en ny Azure File Storage-koppling.

![katalog](../../../../images/tutorials/create/azure-file-storage/catalog.png)

Sidan visas *[!UICONTROL Connect to Azure File Storage]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och autentiseringsuppgifter för fillagring. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/azure-file-storage/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Azure File Storage] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Azure File Storage] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).