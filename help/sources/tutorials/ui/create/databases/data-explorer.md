---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Azure Data Explorer-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---


# Skapa en [!DNL Azure Data Explorer] källanslutning i användargränssnittet

>[!NOTE]
> Kopplingen [!DNL Azure Data Explorer] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Azure Data Explorer] källkoppling (nedan kallad[!DNL Data Explorer]) med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Data Explorer] anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Data Explorer] konto [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `endpoint` | Serverns slutpunkt.. [!DNL Data Explorer] . |
| `database` | Namnet på [!DNL Data Explorer] databasen. |
| `tenant` | Det unika klient-ID som används för att ansluta till [!DNL Data Explorer] databasen. |
| `servicePrincipalId` | Det unika tjänstens huvudnamn-ID som används för att ansluta till Datans Explorer databas. |
| `servicePrincipalKey` | Den unika tjänstens huvudnyckel som används för att ansluta till Datans Explorer databas. |

Mer information om hur du kommer igång finns i [det här Datan Explorer](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Anslut ditt [!DNL Azure Data Explorer] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt [!DNL Data Explorer] konto att ansluta till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL Azure Data Explorer]** följt av **[!UICONTROL Add data]** för att skapa en ny koppling för Datan Explorer.

![katalog](../../../../images/tutorials/create/data-explorer/catalog.png)

Sidan visas *[!UICONTROL Connect to Azure Data Explorer]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Data Explorer] inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/data-explorer/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Data Explorer] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/data-explorer/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Data Explorer] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).