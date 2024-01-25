---
title: Skapa en [!DNL Oracle NetSuite Activities] källanslutning i användargränssnittet
description: Lär dig hur du skapar en källanslutning till en NetSuite-aktivitet i Oracle med hjälp av Adobe Experience Platform användargränssnitt.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 053cf0af327b39830f025686e0f8f67c27f1c45c
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Skapa en [!DNL Oracle NetSuite Activities] källanslutning i användargränssnittet

>[!NOTE]
>
>The [!DNL Oracle NetSuite Activities] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Läs följande självstudiekurs för att lära dig hur du kan hämta händelsedata från [!DNL Oracle NetSuite Activities] för Adobe Experience Platform i användargränssnittet.

## Komma igång {#getting-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Oracle NetSuite] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/marketing-automation.md).

>[!TIP]
>
>Läs [[!DNL Oracle NetSuite] översikt](../../../../connectors/marketing-automation/oracle-netsuite.md) om du vill ha information om hur du hämtar autentiseringsuppgifter.

## Koppla samman [!DNL Oracle NetSuite] konto {#connect-account}

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *Marknadsföringsautomatisering* kategori, välj **[!DNL Oracle NetSuite Activities]** och sedan markera **[!UICONTROL Add data]**.

![Skärmbild för plattformsgränssnitt för katalog med aktivitetskort i Oracle NetSuite](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/catalog-card.png)

The **[!UICONTROL Connect Oracle NetSuite Activities account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

>[!IMPORTANT]
>
>Uppdateringstoken upphör att gälla efter sju dagar. När din token upphör att gälla måste du skapa ett konto på Experience Platform med din uppdaterade token. Om du inte skapar ett nytt konto med din uppdaterade token kan följande felmeddelande visas: `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Befintligt konto {#existing-account}

Välj [!DNL Oracle NetSuite Activities] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![Skärmbild för användargränssnittet för plattformen som används för att ansluta ett NetSuite-aktivitetskonto för Oraclet till ett befintligt konto](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/existing.png)

### Nytt konto {#new-account}

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och dina uppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Skärmbild för användargränssnittet för plattformen för att ansluta ett NetSuite-aktivitetskonto för Oracle till ett nytt konto](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/new.png)

## Nästa steg {#next-steps}

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL Oracle NetSuite Activities] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/marketing-automation.md).

## Ytterligare resurser {#additional-resources}

I avsnitten nedan finns ytterligare resurser som du kan använda när du använder [!DNL Oracle NetSuite Activities] källa.

### Mappning {#mapping}

Plattformen ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd du valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittsguide för dataprep](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Fälten som visas beror på de prenumerationer som [!DNL Oracle NetSuite] kontot har åtkomst till. Om du till exempel inte har tillgång till fakturering kommer du inte att se faktureringsrelaterade fält.

### Schemaläggning {#scheduling}

När du schemalägger [!DNL Oracle NetSuite Activities] dataflöde för förtäring måste du välja följande frekvens- och intervallkonfiguration:

| Frekvens | Intervall |
| --- | --- |
| `Once` | 1 |

När data hämtas kan [!DNL Oracle NetSuite] svarar med det senast ändrade eller skapade datumet som ett datumformat i stället för som en tidsstämpel. Schemaläggningen är därför begränsad till en dag.

När du har angett värdena för schemat väljer du **[!UICONTROL Next]**.

![Schemaläggningssteget för källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/scheduling.png)