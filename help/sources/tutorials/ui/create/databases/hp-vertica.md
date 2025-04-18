---
keywords: Experience Platform;hem;populära ämnen;HP Vertica
solution: Experience Platform
title: Skapa en HP Vertica Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en HP Vertica-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Skapa en HP [!DNL Vertica]-källanslutning i användargränssnittet

>[!NOTE]
>
> HP [!DNL Vertica]-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källöversikt](../../../../home.md#terms-and-conditions).

Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en HP [!DNL Vertica]-källkoppling med användargränssnittet i [!DNL Experience Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig HP [!DNL Vertica]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till HP [!DNL Vertica] med API:t [!DNL Flow Service].

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som används för att ansluta till HP [!DNL Vertica]-instansen. Anslutningssträngsmönstret för HP [!DNL Vertica] är `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Mer information om hur du kommer igång finns i [det här HP [!DNL Vertica] dokumentet](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## Anslut ditt HP [!DNL Vertica]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt HP [!DNL Vertica]-konto till [!DNL Experience Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL HP Vertica]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny HP [!DNL Vertica]-koppling.

![katalog](../../../../images/tutorials/create/hp-vertica/catalog.png)

Sidan **[!UICONTROL Connect to HP Vertica]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina HP [!DNL Vertica]-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![anslut](../../../../images/tutorials/create/hp-vertica/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det HP [!DNL Vertica]-konto du vill ansluta till och sedan **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![befintlig](../../../../images/tutorials/create/hp-vertica/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt HP [!DNL Vertica]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Experience Platform]](../../dataflow/databases.md).
