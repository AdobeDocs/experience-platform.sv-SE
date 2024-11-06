---
keywords: Experience Platform;hem;populära ämnen;Kuchbase;couchbase
solution: Experience Platform
title: Skapa en Couchbase Source Connection i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en källanslutning till Couchbase med hjälp av Adobe Experience Platform-gränssnittet.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Skapa en [!DNL Couchbase]-källanslutning i användargränssnittet

>[!IMPORTANT]
>
>[!DNL Couchbase]-källan kommer att bli inaktuell i slutet av maj 2025. Du kan använda [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) i stället för [!DNL Couchbase]-källan.

Source-anslutningar i [!DNL Adobe Experience Platform] ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Couchbase]-källkoppling med användargränssnittet i [!DNL Platform].

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i [!DNL Platform]:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Couchbase]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att autentisera [!DNL Couchbase]-källkopplingen måste du ange värden för följande anslutningsegenskap:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som används för att ansluta till din [!DNL Couchbase]-instans. Anslutningssträngsmönstret för [!DNL Couchbase] är `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Mer information om hur du hämtar en anslutningssträng finns i dokumentationen för [[!DNL Couchbase] anslutningen](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Anslut ditt [!DNL Couchbase]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Couchbase]-konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Couchbase]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Couchbase]-koppling.

![katalog](../../../../images/tutorials/create/couchbase/catalog.png)

Sidan **[!UICONTROL Connect to Couchbase]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Couchbase]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![anslut](../../../../images/tutorials/create/couchbase/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Couchbase]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** i det övre högra hörnet för att fortsätta.

![befintlig](../../../../images/tutorials/create/couchbase/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Couchbase]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
