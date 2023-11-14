---
keywords: Experience Platform;hem;populära ämnen;HP Vertica
solution: Experience Platform
title: Skapa en HP Vertica Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en HP Vertica-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Skapa en HP [!DNL Vertica] källanslutning i användargränssnittet

>[!NOTE]
>
> HP [!DNL Vertica] anslutningen är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en HP [!DNL Vertica] källkoppling med [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig HP [!DNL Vertica] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till HP [!DNL Vertica] med [!DNL Flow Service] API.

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som används för att ansluta till din HP [!DNL Vertica] -instans. Anslutningssträngsmönstret för HP [!DNL Vertica] är `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Mer information om hur du kommer igång finns i [den här HP [!DNL Vertica] dokument](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## Anslut din HP [!DNL Vertica] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka din HP [!DNL Vertica] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL HP Vertica]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny HP [!DNL Vertica] koppling.

![katalog](../../../../images/tutorials/create/hp-vertica/catalog.png)

The **[!UICONTROL Connect to HP Vertica]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din HP på indataformuläret som visas [!DNL Vertica] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/hp-vertica/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du HP [!DNL Vertica] konto som du vill ansluta till och välj **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![befintlig](../../../../images/tutorials/create/hp-vertica/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till din HP [!DNL Vertica] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
