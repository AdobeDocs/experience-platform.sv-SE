---
keywords: Experience Platform;hem;populära ämnen;Oracle Service Cloud;oracle service cloud
title: Skapa en Oracle Service Cloud Source Connection i användargränssnittet
description: Lär dig hur du skapar en källanslutning till Oracle Service Cloud med hjälp av Adobe Experience Platform användargränssnitt.
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Skapa en källanslutning till Oracle Service Cloud i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en Oraclena Service Cloud-källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig källanslutning till Oracle Service Cloud kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/customer-success.md)

### Samla in nödvändiga inloggningsuppgifter

Du måste ange följande värden för att komma åt ditt Oracle Service Cloud-konto på [!DNL Platform]:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Värd | Värd-URL:en för din Oracle Service Cloud-instans. |
| Användarnamn | Användarnamnet för ditt användarkonto för Oracle Service Cloud. |
| Lösenord | Lösenordet för ditt Oracle Service Cloud-konto. |

Mer information om hur du autentiserar ditt Oracle Service Cloud-konto finns i [[!DNL Oracle] handboken om autentisering](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## Anslut ditt Oracle Service Cloud-konto

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Skärmen [!UICONTROL Catalog] innehåller en mängd olika källor som kan användas för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under kategorin [!UICONTROL Customer success] väljer du **[!UICONTROL Oracle Service Cloud]** och sedan **[!UICONTROL Add data]**.

![Källkatalogen med Oracle Service Cloud-källan är markerad.](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

Sidan **[!UICONTROL Connect to Oracle Service Cloud]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det Oracle Service Cloud-konto du vill ansluta till och sedan **[!UICONTROL Next]** för att fortsätta.

![Det befintliga kontogränssnittet.](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina inloggningsuppgifter för Oracle Service Cloud i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet med platshållarvärden för.](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Oracle Service Cloud-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att få in data om kundens framgång i plattformen](../../dataflow/crm.md).
