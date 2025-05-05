---
title: Skapa en Source-anslutning med flera paneler i användargränssnittet
description: Lär dig hur du skapar en källanslutning till en blandpanel med Adobe Experience Platform-gränssnittet.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Skapa en [!DNL Mixpanel]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Mixpanel]-källanslutning med användargränssnittet i Adobe Experience Platform Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL Mixpanel] till Experience Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Användarnamn | Användarnamnet för tjänstkontot som motsvarar ditt [!DNL Mixpanel]-konto. Mer information finns i [[!DNL Mixpanel] tjänstkontodokumentationen](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account). | `Test8.6d4ee7.mp-service-account` |
| Lösenord | Lösenordet för tjänstkontot som motsvarar ditt [!DNL Mixpanel]-konto. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| Projekt-ID | Ditt projekt-ID för [!DNL Mixpanel]. Detta ID krävs för att skapa en källanslutning. Mer information finns i [[!DNL Mixpanel] projektinställningsdokumentationen](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) och [[!DNL Mixpanel] handboken om att skapa och hantera projekt](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) . | `2384945` |
| Tidszon | Tidszonen som motsvarar ditt [!DNL Mixpanel]-projekt. Tidszon krävs för att skapa en källanslutning. Mer information finns i [dokumentationen för projektinställningar på blandpanelen](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings). | `Pacific Standard Time` |

Mer information om hur du autentiserar [!DNL Mixpanel]-källan finns i [[!DNL Mixpanel] källöversikten](../../../../connectors/analytics/mixpanel.md).

## Anslut ditt [!DNL Mixpanel]-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Analyser* väljer du [!DNL Mixpanel] och sedan **[!UICONTROL Add data]**.

![katalog](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

Sidan **[!UICONTROL Connect Mixpanel account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL Mixpanel]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![befintlig](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och dina autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![ny](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Välj projekt-ID och tidszon {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Ange en tidszon för blandpanelsinmatning"
>abstract="Tidszonen måste vara densamma som tidszonsinställningen för profilen i Mixpanel, eftersom Experience Platform använder den angivna tidszonen för projektet för att importera relevanta data från Mixpanel. Mixpanel justerar sin tidszon så att den överensstämmer med projektets tidszon innan händelsen spelas in i ett datalager i Mixpanel."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=sv-SE#project-id-and-timezone" text="Läs mer i dokumentationen"

När källan har autentiserats anger du ditt projekt-ID och tidszon och väljer sedan **[!UICONTROL Select]**.

Tidszonen som du anger innan dina [!DNL Mixpanel]-data hämtas till Experience Platform måste vara samma som tidszonsinställningen för din [!DNL Mixpanel]-profil. Ändringar i tidszonen för dina data kommer endast att tillämpas på nya händelser och gamla händelser kommer att finnas kvar i den tidszon som du angav tidigare. [!DNL Mixpanel] har plats för sommartid och kommer att justera din tidsstämpel för inmatning korrekt. Mer information om hur tidszoner påverkar dina data finns i [!DNL Mixpanel]-guiden om att [hantera tidszoner för projekt](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Efter en liten stund uppdateras rätt gränssnitt till en förhandsgranskningspanel, vilket gör att du kan kontrollera schemat innan du skapar ett dataflöde. När du är klar väljer du **[!UICONTROL Next]**.

![konfiguration](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Mixpanel]-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta analysdata till Experience Platform](../../dataflow/analytics.md).

## Ytterligare resurser {#additional-resources}

Avsnitten nedan innehåller ytterligare resurser som du kan referera till när du använder källan [!DNL Mixpanel].

### Validering {#validation}

Följande visar hur du kan kontrollera att du har anslutit källan till [!DNL Mixpanel] och att [!DNL Mixpanel]-händelser importeras till Experience Platform.

I Experience Platform-gränssnittet väljer du **[!UICONTROL Datasets]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Datasets]. Skärmen [!UICONTROL Dataset Activity] visar information om körningar.

![datauppsättningsaktivitet](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Välj sedan det dataflödes-ID för dataflödet som du vill visa för att se specifik information om dataflödeskörningen.

![dataflödesövervakning](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Välj slutligen **[!UICONTROL Preview dataset]** för att visa de data som har importerats.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Du kan verifiera dessa data mot data på sidan [!DNL Mixpanel] > [!DNL Events]. Mer information finns i [[!DNL Mixpanel] dokumentet om händelser](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-).

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Schema för blandpanel

Tabellen nedan visar vilka mappningar som stöds och som måste konfigureras för [!DNL Mixpanel].

>[!TIP]
>
>Mer information om API finns i [API för händelseexport > Hämta](https://developer.mixpanel.com/reference/raw-event-export).


| Source | Typ |
|---|---|
| `distinct_id` | string |
| `event_name` | string |
| `import` | boolesk |
| `insert_id` | string |
| `item_id` | string |
| `item_name` | string |
| `item_price` | string |
| `mp_api_endpoint` | string |
| `mp_api_timestamp_ms` | heltal |
| `mp_processing_time_ms` | heltal |
| `time` | heltal |

### Gränser {#limits}

* Du har högst 100 samtidiga frågor och 60 frågor per timme enligt vad som anges i [Gränser för export av API-hastighet](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
