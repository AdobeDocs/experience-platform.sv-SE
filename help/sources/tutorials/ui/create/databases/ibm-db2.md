---
keywords: Experience Platform;hem;populära ämnen;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Skapa en IBM DB2-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en IBM DB2-källanslutning med Adobe Experience Platform UI.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---



# Skapa en IBM DB2-källanslutning i användargränssnittet

>[!NOTE]
>
> IBM DB2-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en IBM DB2-källkoppling (kallas nedan &quot;DB2&quot;) med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig DB2-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till DB2 med API:t [!DNL Flow Service].

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `server` | Namnet på DB2-servern. Du kan ange portnumret efter servernamnet som avgränsas av ett kolon. Till exempel: server:port. |
| `database` | Namnet på DB2-databasen. |
| `username` | Användarnamnet som används för att ansluta till DB2-databasen. |
| `password` | Lösenordet för användarkontot som du angav som användarnamn. |

Mer information om hur du kommer igång finns i [det här DB2-dokumentet](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Anslut ditt IBM DB2-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt DB2-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL IBM DB2]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny DB2-koppling.

![katalog](../../../../images/tutorials/create/ibm-db2/catalog.png)

Sidan **[!UICONTROL Connect to IBM DB2]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina DB2-autentiseringsuppgifter i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/ibm-db2/new.png)

### Befintligt konto

Om du vill ansluta till ett befintligt konto väljer du det DB2-konto som du vill ansluta till och fortsätter sedan med **[!UICONTROL Next]**.

![befintlig](../../../../images/tutorials/create/ibm-db2/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt DB2-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).