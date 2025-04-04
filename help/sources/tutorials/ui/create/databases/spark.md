---
keywords: Experience Platform;hem;populära ämnen;Azure HDInsights;Apache Spark
solution: Experience Platform
title: Skapa en Apache Spark på Azure HDInsights Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Apache Spark på Azure HDInsights-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Skapa en [!DNL Apache Spark] på [!DNL Azure HDInsights]-källanslutning i användargränssnittet

>[!NOTE]
>
> [!DNL Apache Spark] på [!DNL Azure HDInsights]-anslutningen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../../../home.md#terms-and-conditions).

Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Apache Spark] på [!DNL Azure HDInsights]-källkoppling med användargränssnittet i [!DNL Experience Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil i realtid](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Spark]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Spark]-konto på [!DNL Experience Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för servern [!DNL Spark]. |
| `username` | Användarnamnet som du använder för att komma åt servern [!DNL Spark]. |
| `password` | Lösenordet som motsvarar användaren. |

Mer information om hur du kommer igång finns i [det här Spark-dokumentet](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## Anslut ditt [!DNL Spark]-konto

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att länka ditt [!DNL Spark]-konto till [!DNL Experience Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Spark]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Spark]-koppling.

![katalog](../../../../images/tutorials/create/spark/catalog.png)

Sidan **[!UICONTROL Connect to Spark]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Spark]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![ny](../../../../images/tutorials/create/spark/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Spark]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/spark/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Spark]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Experience Platform]](../../dataflow/databases.md).
