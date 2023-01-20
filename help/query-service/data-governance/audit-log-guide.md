---
title: Granska loggintegrering för frågetjänsten
description: Granskningsloggar för frågetjänsten bevarar poster för olika användaråtgärder för att skapa en åtkomsthistorik för felsökningsproblem eller följa företagets policyer för datahantering och lagstadgade krav. Den här självstudiekursen ger en översikt över granskningsloggsfunktioner som är specifika för frågetjänsten.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 1%

---

# [!DNL Query Service] integration av granskningslogg

Adobe Experience Platform [!DNL Query Service] integrering med granskningsloggen innehåller poster med frågerelaterade användaråtgärder. Granskningsloggar är ett viktigt verktyg för felsökning och för att följa företagets policyer för datahantering och krav på regelefterlevnad. Med den här funktionen kan du returnera en åtgärdslogg för många händelsetyper och filtrera och exportera posterna. Loggarna kan nås antingen via plattformsgränssnittet eller [API för granskningsfråga](https://www.adobe.io/experience-platform-apis/references/audit-query/) och hämtas i filformaten CSV eller JSON.

Mer information om användargränssnittet för granskningsloggar finns i [granskningsloggar översikt](../../landing/governance-privacy-security/audit-logs/overview.md). Mer information om hur du anropar plattforms-API:er finns i [API-guide för granskningsloggar](../../landing/api-guide.md).

## Förutsättningar

Du måste ha [!DNL Data Governance] [!UICONTROL View User Activity Log] behörighet aktiverad för att visa kontrollloggens kontrollpanel i plattformens användargränssnitt. Behörigheten aktiveras via Adobe [Admin Console](https://adminconsole.adobe.com/). Kontakta organisationens administratör om du inte har administratörsbehörighet för att aktivera den här behörigheten. I dokumentationen för åtkomstkontroll finns mer information om [fullständiga anvisningar om hur du lägger till behörigheter via Admin Console](../../access-control/home.md).

## [!DNL Query Service] granskningsloggskategorier {#audit-log-categories}

Granskningsloggkategorierna tillhandahålls av [!DNL Query Service] är som följer.

| Kategori | Beskrivning |
|---|---|
| [!UICONTROL Query] | Med den här kategorin kan du granska frågekörningar. |
| [!UICONTROL Query template] | Med den här kategorin kan du granska de olika åtgärder (skapa, uppdatera och ta bort) som har utförts på en frågemall. |
| [!UICONTROL Scheduled query] | Med den här kategorin kan du granska de scheman som har skapats, uppdaterats eller tagits bort i [!DNL Query Service]. |

## Utför en [!DNL Query Service] granskningslogg {#perform-an-audit-log}

Utföra en granskning för [!DNL Query Service] aktiviteter, välja **[!UICONTROL Audits]** från vänster navigering, följt av trattecknet (![En filterikon.](../images/audit-log/filter.png)) för att visa en lista med filterkontroller för att begränsa resultatet.

![Kontrollpanelen för Plattformsgränssnittets granskningslogg med Granskningar i den vänstra navigeringen och filterkontrollerna markerade.](../images/audit-log/filter-controls.png)

Från [!UICONTROL Audits] kontrollpanel [!UICONTROL Activity log] kan du filtrera alla inspelade plattformsåtgärder med [!DNL Query Service] kategorier. Loggresultaten kan filtreras ytterligare baserat på den tidsperiod som de kördes, vilken åtgärd/funktion som utfördes eller vilken användare som tog emot frågan. Dokumentation till granskningsloggen finns [fullständiga anvisningar om hur loggarna filtreras baserat på kategori, åtgärd, användare och status](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Returnerade granskningsloggdata innehåller följande information om alla frågor som uppfyller de valda filtervillkoren.

| Kolumnnamn | Beskrivning |
|---|---|
| [!UICONTROL Timestamp] | Exakt datum och tid för åtgärden som utfördes i en `month/day/year hour:minute AM/PM` format. |
| [!UICONTROL Asset Name] | Värdet för [!UICONTROL Asset Name] fältet beror på vilken kategori som valts som filter. När du använder [!UICONTROL Scheduled query] kategori här är **schemanamn**. När du använder [!UICONTROL Query template] -kategori, det här är **mallnamn**. När du använder [!UICONTROL Query] -kategori, det här är **sessions-ID** |
| [!UICONTROL Category] | Det här fältet matchar den kategori som du har valt i listrutan för filter. |
| [!UICONTROL Action] | Det kan vara antingen skapa, ta bort, uppdatera eller köra. Vilka åtgärder som är tillgängliga beror på vilken kategori som valts som filter. |
| [!UICONTROL User] | Det här fältet innehåller användar-ID:t som körde frågan. |

![Kontrollpanelen Granskningar med den filtrerade aktivitetsloggen markerad.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Mer frågeinformation ges genom att du hämtar loggresultaten i antingen CSV- eller JSON-filformat, än vad som visas som standard på kontrollpanelen för granskningsloggen.

## Panelen Detaljer

Välj en rad med granskningsloggresultat för att öppna en informationspanel till höger på skärmen.

![Granskar fliken Aktivitetslogg på kontrollpanelen med informationspanelen markerad.](../images/audit-log/details-panel.png)

Du kan använda informationspanelen för att hitta [!UICONTROL Asset ID] och [!UICONTROL Event status].

Värdet för [!UICONTROL Asset ID] ändringar beroende på vilken kategori som används i granskningen.

* När du använder [!UICONTROL Query] kategori, [!UICONTROL Asset ID] är  **sessions-ID**.
* När du använder [!UICONTROL Query template] kategori, [!UICONTROL Asset ID] är **mall-ID** och prefixat med `[!UICONTROL templateID:]`.
* När du använder [!UICONTROL Scheduled query] kategori, [!UICONTROL Asset ID] är  **schema-ID** och prefixat med `[!UICONTROL scheduleID:]`.

Värdet för [!UICONTROL Event status] ändringar beroende på vilken kategori som används i granskningen.

* När du använder [!UICONTROL Query] kategori, [!UICONTROL Event status] fältet innehåller en lista med alla **fråga-ID** som körs av användaren i sessionen.
* När du använder [!UICONTROL Query template] kategori, [!UICONTROL Event status] fältet innehåller **mallnamn** som ett prefix för händelsestatusen.
* När du använder [!UICONTROL Query schedule] kategori, [!UICONTROL Event status] fältet innehåller **schemanamn** som ett prefix för händelsestatusen.

## Tillgängliga filter för [!DNL Query Service] granskningsloggskategorier {#available-filters}

Vilka filter som är tillgängliga varierar beroende på vilken kategori som har valts i listrutan. Följande tabell visar vilka filter som är tillgängliga för [[!DNL Query Service] granskningsloggskategorier](#audit-log-categories).

| Filter | Beskrivning |
|---|---|
| Kategori | Se [[!DNL Query Service] granskningsloggskategorier](#audit-log-categories) för en fullständig lista över tillgängliga kategorier. |
| Åtgärd | När det refererar till [!DNL Query Service] granskningskategorier, uppdatering är **ändring av befintligt formulär**, delete är **borttagning av schemat eller mallen**, skapa **skapa ett nytt schema eller en ny mall** och kör är **köra en fråga**. |
| Användare | Ange det fullständiga användar-ID:t (till exempel johndoe@acme.com) som ska filtreras efter användare. |
| Status | The [!UICONTROL Allow], [!UICONTROL Success]och [!UICONTROL Failure] -alternativen filtrerar loggarna baserat på &quot;Status&quot; eller &quot;Händelsestatus&quot; medan [!UICONTROL Deny] alternativ filtreras bort **alla** loggar. |
| Datum | Välj ett startdatum och/eller ett slutdatum för att definiera ett datumintervall som resultaten ska filtreras efter. |

## Nästa steg

Genom att läsa det här dokumentet får du en bättre förståelse för [!DNL Query Service] granskningsloggfunktion och hur den kan användas för att filtrera [!DNL Query Service] användaråtgärder.

Om du använder [!DNL Query Service] för felsökning rekommenderar vi att du läser [felsökningsguide](../troubleshooting-guide.md).
