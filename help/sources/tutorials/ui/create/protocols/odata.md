---
keywords: Experience Platform;home;populära topics;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Skapa en allmän OData-källanslutning i användargränssnittet
topic: overview
type: Tutorial
description: Lär dig hur du skapar en allmän källanslutning till ett öppet dataprotokoll med hjälp av Adobe Experience Platform-gränssnittet.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# Skapa en [!DNL Generic OData]-källanslutning i användargränssnittet

>[!NOTE]
>
> [!DNL Generic OData]-kopplingen är i betaversion. Se [Källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade anslutningar.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudien beskrivs stegen för hur du skapar en [!DNL Generic Open Data Protocol]-källkoppling (kallas nedan &quot;[!DNL OData]&quot;) med hjälp av användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverket som  [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL OData]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [konfigurera ett dataflöde](../../dataflow/protocols.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL OData]-konto i [!DNL Platform] måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | Rot-URL:en för tjänsten [!DNL OData]. |

Mer information om hur du kommer igång finns i [det här [!DNL OData] dokumentet](https://www.odata.org/getting-started/basic-tutorial/).

## Anslut ditt [!DNL OData]-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL OData]-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan **[!UICONTROL Sources]**. Skärmen **[!UICONTROL Catalog]** visar en mängd olika källor som du kan skapa ett konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Generic OData]** under kategorin **[!UICONTROL Protocols]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL OData]-koppling.

![katalog](../../../../images/tutorials/create/odata/catalog.png)

Sidan **[!UICONTROL Connect to Generic OData]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du en anslutning med ett namn, en valfri beskrivning och dina [!DNL OData]-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/odata/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det [!DNL OData]-konto du vill ansluta till och sedan väljer du **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/odata/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL OData]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta protokolldata till [!DNL Platform]](../../dataflow/protocols.md).