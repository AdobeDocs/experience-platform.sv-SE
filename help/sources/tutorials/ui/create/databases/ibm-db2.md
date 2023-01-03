---
keywords: Experience Platform;hem;populära ämnen;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Skapa en IBM DB2-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en IBM DB2-källanslutning med Adobe Experience Platform användargränssnitt.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Skapa en IBM DB2-källanslutning i användargränssnittet

>[!NOTE]
>
> IBM DB2-anslutningen är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en IBM DB2-källkoppling (nedan kallad DB2) med hjälp av [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig DB2-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen på [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till DB2 med [!DNL Flow Service] API.

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `server` | Namnet på DB2-servern. Du kan ange portnumret efter servernamnet som avgränsas av ett kolon. Till exempel: server:port. |
| `database` | Namnet på DB2-databasen. |
| `username` | Användarnamnet som används för att ansluta till DB2-databasen. |
| `password` | Lösenordet för användarkontot som du angav som användarnamn. |

Mer information om hur du kommer igång finns i [det här DB2-dokumentet](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Anslut ditt IBM DB2-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt DB2-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL IBM DB2]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny DB2-anslutning.

![katalog](../../../../images/tutorials/create/ibm-db2/catalog.png)

The **[!UICONTROL Connect to IBM DB2]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina DB2-autentiseringsuppgifter i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/ibm-db2/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det DB2-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/ibm-db2/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt DB2-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
