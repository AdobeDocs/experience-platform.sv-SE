---
keywords: Experience Platform;home;popular topics;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Skapa en allmän OData-källanslutning i användargränssnittet
topic: overview
description: I den här självstudiekursen beskrivs hur du skapar en allmän källkoppling för Open Data Protocol (nedan kallad OData) med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# Skapa en [!DNL Generic OData] källanslutning i användargränssnittet

>[!NOTE]
>
> Kopplingen [!DNL Generic OData] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Generic Open Data Protocol] källkoppling (nedan kallad[!DNL OData]) med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL OData] anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [att konfigurera ett dataflöde](../../dataflow/protocols.md)

### Samla in nödvändiga inloggningsuppgifter

Du måste ange följande värden för att få åtkomst till ditt [!DNL OData] konto i [!DNL Platform]:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | URL-adressen till [!DNL OData] tjänsten. |

Mer information om hur du kommer igång finns i [ [!DNL OData] det här dokumentet](https://www.odata.org/getting-started/basic-tutorial/).

## Anslut ditt [!DNL OData] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL OData] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj under **[!UICONTROL Protocols]** kategorin **[!UICONTROL Generic OData]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa en ny [!DNL OData] koppling.

![katalog](../../../../images/tutorials/create/odata/catalog.png)

Sidan visas **[!UICONTROL Connect to Generic OData]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL OData] inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/odata/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL OData] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/odata/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL OData] konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta protokolldata till [!DNL Platform]](../../dataflow/protocols.md).