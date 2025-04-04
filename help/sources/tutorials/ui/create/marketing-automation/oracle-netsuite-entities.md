---
title: Skapa en  [!DNL Oracle NetSuite Entities] källanslutning i användargränssnittet
description: Lär dig hur du skapar en källanslutning för Oracle NetSuite Entities med Adobe Experience Platform-gränssnittet.
hide: true
hidefromtoc: true
badge: Beta
exl-id: ce0ea37f-16e0-4aef-9809-72c0b11e0440
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Skapa en [!DNL Oracle NetSuite Entities]-källanslutning i användargränssnittet

>[!NOTE]
>
>Källan [!DNL Oracle NetSuite Entities] är i betaversion. Mer information om hur du använder betatecknade källor finns i [källöversikten](../../../../home.md#terms-and-conditions).

Läs följande självstudiekurs om du vill veta mer om hur du kan få kontakt- och kunddata från ditt [!DNL Oracle NetSuite Entities]-konto till Adobe Experience Platform i användargränssnittet.

## Komma igång {#getting-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt [!DNL Oracle NetSuite]-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/marketing-automation.md).

>[!TIP]
>
>Läs [[!DNL Oracle NetSuite] översikten](../../../../connectors/marketing-automation/oracle-netsuite.md) om du vill ha mer information om hur du hämtar autentiseringsuppgifter.

## Anslut ditt [!DNL Oracle NetSuite Activities]-konto {#connect-account}

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Marknadsföringsautomatisering* väljer du **[!DNL Oracle NetSuite Entities]** och sedan **[!UICONTROL Add data]**.

![Experience Platform UI, skärmbild för katalog med Oracle NetSuite Entities-kort](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/catalog-card.png)

Sidan **[!UICONTROL Connect Oracle NetSuite Entities account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

>[!IMPORTANT]
>
>Uppdateringstoken upphör att gälla efter sju dagar. När din token upphör att gälla måste du skapa ett konto på Experience Platform med din uppdaterade token. Om du inte skapar ett nytt konto med din uppdaterade token kan följande felmeddelande visas: `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Befintligt konto {#existing-account}

Om du vill använda ett befintligt konto väljer du det [!DNL Oracle NetSuite Entities]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Experience Platform UI-skärmbild för att ansluta Oracle NetSuite-entiteter till ett befintligt konto](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/existing.png)

### Nytt konto {#new-account}

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och dina autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Experience Platform UI-skärmbild för att ansluta Oracle NetSuite Entities-kontot till ett nytt konto](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/new.png)

### Markera data

Välj sedan den objekttyp som du vill importera till Experience Platform.

| Enhetstyp | Beskrivning |
| --- | --- |
| Kontakt | Hämta kontaktnamn, e-post, telefonnummer och anpassade kontaktrelaterade fält som är kopplade till kunder. |
| Kund | Hämta specifika kunddata, t.ex. kundnamn, adresser och nyckelidentifierare. |

>[!BEGINTABS]

>[!TAB Kontakt]

![Skärmbild för Experience Platform-gränssnitt för Oracle Netsuite-enheter som visar konfigurationen med alternativet Kontakt markerat](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-contact.png)

>[!TAB Kund]

![Skärmbild för Experience Platform-gränssnitt för Oracle Netsuite-enheter som visar konfigurationen med alternativet Kund valt](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-customer.png)

>[!ENDTABS]

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Oracle NetSuite Entities]-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta marknadsföringsdata till Experience Platform](../../dataflow/marketing-automation.md).

## Ytterligare resurser {#additional-resources}

Avsnitten nedan innehåller ytterligare resurser som du kan referera till när du använder källan [!DNL Oracle NetSuite Entities].

### Mappning {#mapping}

Experience Platform ger intelligenta rekommendationer för automatiskt mappade fält baserat på det målschema eller den datamängd som du har valt. Du kan justera mappningsreglerna manuellt så att de passar dina användningsfall. Beroende på dina behov kan du välja att mappa fält direkt eller använda förinställningsfunktioner för data för att omvandla källdata för att härleda beräknade eller beräknade värden. Mer information om hur du använder mappningsgränssnittet och beräkningsfälten finns i [Användargränssnittshandboken för dataförinställningar](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Vilka fält som visas beror på vilka prenumerationer ditt [!DNL Oracle NetSuite]-konto har åtkomst till. Om du till exempel inte har tillgång till fakturering kommer du inte att se faktureringsrelaterade fält.

### Schemaläggning {#scheduling}

När du schemalägger [!DNL Oracle NetSuite Entities]-dataflödet för förtäring måste du välja följande frekvens- och intervallkonfiguration:

| Frekvens | Intervall |
| --- | --- |
| `Once` | 1 |

När data hämtas svarar [!DNL Oracle NetSuite] med det senast ändrade eller skapade datumet som ett datumformat i stället för en tidsstämpel. Schemaläggningen är därför begränsad till en dag.

När du har angett värden för ditt schema väljer du **[!UICONTROL Next]**.

![Schemaläggningssteget för källarbetsflödet.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/scheduling.png)
