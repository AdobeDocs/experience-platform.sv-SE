---
keywords: Experience Platform;hem;populära ämnen;Phoenix;phoenix
solution: Experience Platform
title: Skapa en Phoenix-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en Phoenix-källanslutning med Adobe Experience Platform-gränssnittet.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# Skapa en [!DNL Phoenix]-källanslutning i användargränssnittet

>[!NOTE]
>
> [!DNL Phoenix]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs stegen för hur du skapar en [!DNL Phoenix]-källkoppling med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Phoenix]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/databases.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Phoenix]-konto på [!DNL Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för [!DNL Phoenix]-servern. |
| `port` | Den TCP-port som [!DNL Phoenix]-servern använder för att avlyssna klientanslutningar. Om du ansluter till [!DNL Azure HDInsights] anger du porten som 443. |
| `httpPath` | Den partiella URL som motsvarar [!DNL Phoenix]-servern. Ange /hbasephoenix0 om du använder klustret [!DNL Azure HDInsights]. |
| `username` | Användarnamnet som du använder för att komma åt [!DNL Phoenix]-servern. |
| `password` | Lösenordet som motsvarar användaren. |
| `enableSsl` | En växel som anger om anslutningarna till servern är krypterade med SSL. |

Mer information om hur du kommer igång finns i [det här [!DNL Phoenix] dokumentet](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Anslut ditt [!DNL Phoenix]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Phoenix]-konto för att ansluta till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Phoenix]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa ett nytt [!DNL Phoenix]-konto.

![katalog](../../../../images/tutorials/create/phoenix/catalog.png)

Sidan **[!UICONTROL Connect to Phoenix]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för [!DNL Phoenix] i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/phoenix/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL Phoenix]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/phoenix/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Phoenix]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).