---
keywords: Experience Platform;home;populära topics;Azure Data Explorer;azure data explorer;data explorer;Data Explorer
solution: Experience Platform
title: Skapa en Azure Data Explorer Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Azure Data Explorer-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Skapa en [!DNL Azure Data Explorer]-källanslutning i användargränssnittet

Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Azure Data Explorer]-källkoppling (kallas nedan [!DNL Data Explorer]) med användargränssnittet i [!DNL Experience Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Data Explorer]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Data Explorer]-konto på [!DNL Experience Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `endpoint` | Slutpunkten för servern [!DNL Data Explorer]. |
| `database` | Namnet på databasen [!DNL Data Explorer]. |
| `tenant` | Det unika klient-ID som används för att ansluta till databasen [!DNL Data Explorer]. |
| `servicePrincipalId` | Det unika tjänstens huvudnamn-ID som används för att ansluta till databasen [!DNL Data Explorer]. |
| `servicePrincipalKey` | Den unika tjänstens huvudnyckel som används för att ansluta till databasen [!DNL Data Explorer]. |

Mer information om hur du kommer igång finns i [det här [!DNL Data Explorer] dokumentet](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Anslut ditt [!DNL Azure Data Explorer]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Data Explorer]-konto till [!DNL Experience Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Azure Data Explorer]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny Data Explorer-anslutning.

![katalog](../../../../images/tutorials/create/data-explorer/catalog.png)

Sidan **[!UICONTROL Connect to Azure Data Explorer]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Data Explorer]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![anslut](../../../../images/tutorials/create/data-explorer/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Data Explorer]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/data-explorer/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Data Explorer]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Experience Platform]](../../dataflow/databases.md).
