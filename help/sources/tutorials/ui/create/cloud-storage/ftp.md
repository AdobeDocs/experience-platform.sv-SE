---
keywords: Experience Platform;hem;populära ämnen;FTP;ftp
solution: Experience Platform
title: Skapa en FTP-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en FTP-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Skapa en FTP-källanslutning i användargränssnittet

>[!NOTE]
>
>FTP-kopplingen är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder beta-märkta anslutningar.

I den här självstudiekursen beskrivs hur du skapar en FTP-källanslutning med Adobe Experience Platform-gränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig FTP-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/batch/cloud-storage.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta till FTP måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Namnet eller IP-adressen som är associerad med FTP-servern. |
| `username` | Användarnamnet med åtkomst till FTP-servern. |
| `password` | Lösenordet för FTP-servern. |

## Anslut till FTP-servern

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa ett nytt FTP-konto för att ansluta till plattformen.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett inkommande konto för.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Cloud storage] kategori, välj **[!UICONTROL FTP]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny FTP-anslutning.

![katalog](../../../../images/tutorials/create/ftp/catalog.png)

The **[!UICONTROL Connect to FTP]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![new](../../../../images/tutorials/create/ftp/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det FTP-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/ftp/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt FTP-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data från ditt molnlagringsutrymme till plattformen](../../dataflow/batch/cloud-storage.md).
