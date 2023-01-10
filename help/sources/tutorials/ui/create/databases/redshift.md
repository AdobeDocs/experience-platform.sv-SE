---
keywords: Experience Platform;hemanvändare;populära ämnen;Amazon Redshift;amazon redshift;Redshift;redshift
solution: Experience Platform
title: Skapa en Amazon Redshift-källanslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en Amazon Redshift-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# Skapa en [!DNL Amazon Redshift] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL Amazon Redshift] (nedan kallad[!DNL Redshift]&quot;) som använder [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Redshift] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Redshift] konto på [!DNL Platform]måste du ange följande värden:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| `server` | Servern som är kopplad till din [!DNL Redshift] konto. |
| `username` | Användarnamnet som är associerat med din [!DNL Redshift] konto. |
| `password` | Lösenordet som är kopplat till [!DNL Redshift] konto. |
| `database` | The [!DNL Redshift] databas som du använder. |

Mer information om hur du kommer igång finns i [this [!DNL Redshift] dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Koppla samman [!DNL Redshift] konto

>[!NOTE]
>
>Standardkodningsstandard för [!DNL Redshift] är Unicode. Detta kan inte ändras.

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Redshift] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL Amazon Redshift]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Redshift] koppling.

![](../../../../images/tutorials/create/redshift/catalog.png)

The **[!UICONTROL Connect to Amazon Redshift]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Redshift] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/redshift/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Redshift] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/redshift/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL Redshift] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
