---
title: Filtrera källobjekt i användargränssnittet
description: Lär dig navigera bland källobjekt som konton och dataflöden i användargränssnittet i Experience Platform.
hide: true
hidefromtoc: true
exl-id: 59c200cc-1be7-45a8-9d7a-55e6f11dbcf2
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 0%

---

# Filtrera källobjekt i användargränssnittet

Använd verktygen för filtrering, sökning och infogad åtgärd i Adobe Experience Platform-användargränssnittet för att effektivisera arbetsflödet på arbetsytan i [!UICONTROL Sources]

* Använd filtrerings- och sökfunktioner för att navigera genom källkonton och dataflöden i organisationen.
* Använd textbundna åtgärder för att ändra konfigurationsinställningarna för dataflödena och förbättra arbetsflödena i organisationen. Du kan använda textbundna åtgärder för att lägga till taggar, ställa in aviseringar eller skapa förtäringsjobb på begäran.

## Kom igång

Det är praktiskt att ha en förståelse för följande funktioner och begrepp i Experience Platform innan du arbetar med objektnavigeringsverktygen på källarbetsytan:

* [Källor](../../home.md): Använd källor i Experience Platform för att importera data från ett Adobe-program eller en datakälla från en tredje part.
* [Administrativa taggar](../../../administrative-tags/overview.md): Använd administrativa taggar för att tillämpa metadatanyckelord på dina objekt och aktivera sökning för att hitta det objektet i Experience Platform-ekosystemet.
* [Varningar](../../../observability/home.md): Använd varningar för att ta emot meddelanden som ger en uppdatering av status för objekt, t.ex. källans dataflöde.
* [Dataflöden](../../../dataflows/home.md): Dataflöden är representationer av datajobb som flyttar data mellan Experience Platform. Du kan använda källarbetsytan för att skapa dataflöden som importerar data från en viss källa till Experience Platform.
* [Datauppsättningar](../../../catalog/datasets/user-guide.md): En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader).
* [Sandlådor](../../../sandboxes/home.md): Använd sandlådor i Experience Platform för att skapa virtuella partitioner mellan dina Experience Platform-instanser och skapa miljöer som är dedikerade till utveckling eller produktion.

## Filterkällor, dataflöden {#filter-sources-dataflows}

I användargränssnittet för Experience Platform väljer du **[!UICONTROL Sources]** i den vänstra navigeringen och sedan **[!UICONTROL Dataflows]** i den övre rubriken.

![Dataflödessidan i källarbetsytan](../../images/tutorials/filter/dataflows-page.png)

Som standard visas filtermenyn till vänster om gränssnittet. Om du vill dölja menyn väljer du **[!UICONTROL Hide filters]**.

![Filteralternativet Dölj har valts.](../../images/tutorials/filter/hide-filters.png)

Du kan filtrera källans dataflöden med följande parametrar:

| Filter | Beskrivning |
| --- | --- |
| [Source-plattform](#filter-dataflows-by-source-platform) | Filtrera dataflödena baserat på källan som de skapades med. |
| [Taggar](#filter-dataflows-by-tags) | Filtrera dataflödena baserat på de taggar som används i dem. |
| [Status](#filter-dataflows-by-status) | Filtrera dataflödena baserat på deras aktuella status. |
| [Måldatauppsättning](#filter-dataflows-by-target-dataset) | Filtrera dataflödena baserat på måldatauppsättningen som de skapades med. |
| [Kontonamn](#filter-dataflows-by-account-name) | Filtrera dataflödena baserat på namnet på kontot som de motsvarar. |
| [Skapad av](#filter-dataflows-by-user) | Filtrera dataflödena baserat på vem som skapade dem. |
| [Skapad](#filter-dataflows-by-creation-date) | Filtrera dataflödena baserat på vilket datum de skapades. |
| [Ändringsdatum](#filter-dataflows-by-modification-date) | Filtrera dataflödena baserat på det datum då de senast uppdaterades. |

### Filtrera dataflöden efter källplattform {#filter-dataflows-by-source-platform}

Använd panelen [!UICONTROL Source platform] för att filtrera dataflödena efter källtyp. Du kan antingen skriva in en viss källa eller använda listrutan för att visa en lista med källor i katalogen. Du kan också filtrera efter flera olika källor för en given fråga. Du kan till exempel välja [!DNL Amazon S3], [!DNL Azure Data Lake Storage Gen2] och [!DNL Google Cloud Storage] för att uppdatera katalogen och bara visa de dataflöden som skapades med de valda källorna.

### Filtrera dataflöden efter taggar {#filter-dataflows-by-tags}

Använd taggpanelen för att filtrera dataflödena efter deras respektive taggar.

Markera **[!UICONTROL Has any tag]** och markera sedan de taggar som du vill filtrera med hjälp av listrutan. Använd den här inställningen för att filtrera efter dataflöden som har någon av de taggar som du har valt.

![En fråga som filtrerar dataflöden efter en tagg.](../../images/tutorials/filter/has-any-tag.png)

Markera **[!UICONTROL Has all tags]** och markera sedan de taggar som du vill filtrera med hjälp av listrutan. Använd den här inställningen om du vill filtrera efter dataflöden som har alla taggar som du har valt.

![En fråga om att filtrera dataflöden efter alla taggar.](../../images/tutorials/filter/has-all-tags.png)

### Filtrera dataflöden efter status {#filter-dataflows-by-status}

Du kan filtrera efter status med panelen [!UICONTROL Status].

| Status | Beskrivning |
| --- | --- |
| Aktiverad | Välj **[!UICONTROL Enabled]** om du vill filtrera vyn och bara visa aktiva dataflöden. |
| Handikappade | Välj **[!UICONTROL Disabled]** om du vill filtrera vyn och endast visa inaktiverade dataflöden. |
| Utkast | Välj **[!UICONTROL Draft]** om du vill filtrera vyn och bara visa dataflöden som är i utkastläge. |

### Filtrera dataflöden efter måldatauppsättning {#filter-dataflows-by-target-dataset}

Välj **[!UICONTROL Target dataset]** om du vill komma åt en listruta med alla måldatamängder. Välj sedan en måldatauppsättning som du vill filtrera vyn och bara visa de dataflöden som har skapats med de angivna måldatauppsättningarna.

### Filtrera dataflöden efter kontonamn {#filter-dataflows-by-account-name}

Välj **[!UICONTROL Account name]** om du vill öppna en listruta med alla konton. Välj sedan ett konto för att filtrera vyn och visa dataflöden som har skapats av det valda kontot.

### Filtrera dataflöden efter användare {#filter-dataflows-by-user}

Använd panelen [!UICONTROL Created by] för att filtrera dataflöden efter den användare som skapade eller senast uppdaterade dataflödena. Markera listrutan och välj sedan användarnamnet för att filtrera dataflödena efter.

### Filtrera dataflöden efter skapandedatum {#filter-dataflows-by-creation-date}

Du kan filtrera dataflödena efter när de skapades. Konfigurera ett startdatum och ett slutdatum på panelen [!UICONTROL Created date] för att skapa ett tidsramsfönster och filtrera vyn så att endast dataflöden som skapats i fönstret visas.

Du kan konfigurera tidsramen genom att ange start- och slutdatum. Du kan också välja kalenderikonen och använda kalendern för att konfigurera dina datum.

Du kan också följa samma steg, men filtrera dataflöden efter det senaste ändringsdatumet, i motsats till det datum då de skapades.

### Filtrera dataflöden efter ändringsdatum {#filter-dataflows-by-modification-date}

På samma sätt kan du tillämpa samma principer och filtrera dataflödet efter ändringsdatum. Använd **[!UICONTROL Modified date]** för att konfigurera en viss tidsram och filtrera vyn så att endast dataflöden som har ändrats under den perioden visas.

### Kombinera filter {#combine-filters}

Du kan kombinera olika filter för att göra sökningen bredare eller smalare. I exemplet nedan används ett filter för att söka efter:

* Dataflöden som skapades med källan [!DNL Amazon S3].
* Dataflöden som innehåller taggen **[!DNL ACME]**.
* Datamöjligheter som är aktiverade.
* Dataflöden som skapades med datauppsättningen [!DNL Loyalty Dataset B2C].
* Dataflöden som skapades mellan den 4 januari 2024 och den 4 november 2024.

![Ett listrutefönster med alla använda filter.](../../images/tutorials/filter/combine-filters.png)

Om du vill ta bort alla filter väljer du **[!UICONTROL Clear all]**.

![Alternativet Rensa alla har valts.](../../images/tutorials/filter/clear-all.png)

## Filtrera källkonton {#filter-sources-accounts}

I användargränssnittet för Experience Platform väljer du [!UICONTROL Sources] i den vänstra navigeringen och sedan **[!UICONTROL Accounts]** i den övre rubriken. Du kan filtrera dina källkonton baserat på källan som de skapades med eller användaren som skapade dem.

![Kontosidan i källarbetsytan](../../images/tutorials/filter/accounts.png)

## Sök efter konton och dataflöden {#search-for-accounts-and-dataflows}

Du kan öka effektiviteten genom att använda sökfältet för att direkt navigera till ett visst konto eller dataflöde.

>[!BEGINTABS]

>[!TAB Sök efter dataflöden]

Använd sökfältet på sidan [!UICONTROL Dataflows] för att hitta ett specifikt dataflöde. Du kan söka efter ett dataflöde med hjälp av dess namn eller beskrivning.

![En sökfråga för ett ACME-dataflöde](../../images/tutorials/filter/search-dataflow.png)

>[!TAB Sök efter konton]

Använd sökfältet på sidan [!UICONTROL Accounts] för att hitta ett specifikt konto. Du kan söka efter ett konto med hjälp av dess namn eller beskrivning.

![En sökfråga för ett April-konto](../../images/tutorials/filter/search-account.png)

>[!ENDTABS]

## Textbundna åtgärder för källdata {#inline-actions-for-sources-dataflows}

Markera ellipserna (`...`) bredvid ett dataflödesnamn för en lista med infogade åtgärder som du kan använda för att göra ändringar i dataflödet.

![Markeringen av infogade åtgärder som du kan välja mellan för ett givet dataflöde.](../../images/tutorials/filter/inline-actions.png)

| Inline-åtgärder | Beskrivning |
| --- | --- |
| [!UICONTROL Edit schedule] | Välj **[!UICONTROL Edit schedule]** om du vill uppdatera matningsschemat för ditt dataflöde. Det går inte att redigera ett dataflöde som har ställts in på engångsintag. |
| [!UICONTROL Disable dataflow] | Välj **[!UICONTROL Disable dataflow]** om du vill inaktivera ett dataflöde. Det här alternativet tar inte bort dataflödet. |
| [!UICONTROL View in monitoring] | Välj **[!UICONTROL View in monitoring]** om du vill visa mått och status för dataflödet på kontrollpanelen. Mer information finns i handboken om [övervakning av källdata ](../../../dataflows/ui/monitor-sources.md). |
| [!UICONTROL Delete] | Välj **[!UICONTROL Delete]** om du vill ta bort dataflödet. |
| [!UICONTROL Run on-demand] | Välj **[!UICONTROL Run on-demand]** om du vill utlösa en enda iteration för ett dataflöde. Mer information finns i guiden [Skapa ett dataflöde på begäran](../ui/on-demand-ingestion.md). |
| [!UICONTROL Subscribe to alerts] | Välj **[!UICONTROL Subscribe to alerts]** om du vill visa ett popup-fönster med aviseringar som du kan prenumerera på: <ul><li>Körningsstart för källdataflöde: Välj den här aviseringen om du vill få ett meddelande när körningen av dataflödet på begäran börjar.</li><li>Källdataflöde har körts: Välj den här aviseringen om du vill få ett meddelande när körningen av dataflödet på begäran har slutförts.</li><li>Körningsfel för källdataflöde: Välj den här aviseringen när körningen av dataflödet på begäran misslyckas på grund av fel.</li></ul> Mer information finns i guiden om att [prenumerera på aviseringar för källdataflöden](../ui/alerts.md). |
| [!UICONTROL Add to package] | Välj **[!UICONTROL Add to package]** om du vill lägga till dataflödet i ett paket och exportera det för användning i en annan sandlåda. Under det här steget kan du antingen skapa ett nytt paket eller lägga till dataflödet i ett befintligt paket. Mer information finns i handboken om [sandlådeverktyg](../../../sandboxes/ui/sandbox-tooling.md). |
| [!UICONTROL Manage tags] | Välj **[!UICONTROL Manage tags]** om du vill lägga till eller ta bort taggar från dataflödet. Använd taggar för att hantera metadatataxonomier och klassificera affärsobjekt för enklare identifiering och kategorisering. Mer information finns i handboken om [hantering av taggar](../../../administrative-tags/ui/managing-tags.md). |

## Nästa steg

Genom att läsa det här dokumentet har du lärt dig navigera genom källkonton och dataflödessidor. Mer information om källor finns i [Källöversikt](../../home.md).
