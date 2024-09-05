---
title: Versionsinformation om Adobe Experience Platform, augusti 2024
description: Versionsinformation från augusti 2024 för Adobe Experience Platform.
exl-id: 153891e9-fd82-4894-a047-c8d82f214fef
source-git-commit: 4fecb47084a522b4eb9808dc317e0d70e7ef42c6
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 20 augusti 2024**

>[!TIP]
>
>Visa en [översikt över exempeldokumentationen ](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview) om användningsfall för att lära dig mer om olika användningsfall, som prospektering, förvärv och mer som din organisation kan uppnå med Real-Time CDP.

Uppdateringar av befintliga funktioner och dokumentation i Experience Platform:

- [Attributbaserad åtkomstkontroll](#abac)
- [Datainmatning](#data-ingestion)
- [Mål ](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identitetstjänst](#identity-service)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Attributbaserad åtkomstkontroll {#abac}

Attributbaserad åtkomstkontroll är en funktion hos Adobe Experience Platform som ger sekretessmedvetna varumärken större flexibilitet att hantera användaråtkomst. Enskilda objekt som schemafält och segment kan tilldelas användarroller. Med den här funktionen kan du bevilja eller återkalla åtkomst till enskilda objekt för specifika plattformsanvändare i organisationen.

Med attributbaserad åtkomstkontroll kan administratören styra användarnas tillgång till känsliga personuppgifter (SPD), personligt identifierbar information (PII) och andra anpassade typer av data i alla plattformsarbetsflöden och resurser. Administratörer kan definiera användarroller som bara har åtkomst till specifika fält och data som motsvarar dessa fält.

**Ny funktion**

| Funktionsuppdatering | Beskrivning |
| --- | --- |
| Ny behörighetshanterarfunktion | Du kan nu använda [behörighetshanteraren](../../access-control/abac/permission-manager/overview.md) för att generera rapporter med enkla frågor, vilket hjälper dig att förstå åtkomsthantering och spara tid när du verifierar åtkomstbehörigheter i flera arbetsflöden och granularitetsnivåer. Mer information om hur du skapar rapporter för användare och roller finns i användarhandboken för [Permission Manager](../../access-control/abac/permission-manager/permissions.md). ![Användargränssnittet i Image Experience Platform markerar behörighetshanteraren i det vänstra navigeringsfönstret.](assets/august/permission-manager-rn.png "Behörighetshanteraren i användargränssnittet."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Mer information om attributbaserad åtkomstkontroll finns i [Översikt över attributbaserad åtkomstkontroll](../../access-control/abac/overview.md). En utförlig guide om det attributbaserade arbetsflödet för åtkomstkontroll finns i [attributbaserad åtkomstkontroll från början till slut](../../access-control/abac/end-to-end-guide.md).

## Dataintag (uppdaterad 23 augusti) {#data-ingestion}

Adobe Experience Platform har en omfattande uppsättning funktioner för att importera alla typer av data och all fördröjning. Du kan importera med hjälp av API:er för gruppbearbetning eller direktuppspelning, med hjälp av Adobe-byggda källor, dataintegrationspartners eller Adobe Experience Platform användargränssnitt.

**Uppdatera till datumformatshantering vid batchdatainmatning**

Den här versionen åtgärdar ett problem med *datumformatshantering* vid batchdatainmatning. Tidigare transformerades datumfält som infogats av klienter som `Date` till `DateTime`-format. Detta innebar att tidszonen automatiskt lades till i fält och det orsakade problem för användare som föredrog eller krävde formatet `Date`. Om du fortsätter kommer tidszonen inte automatiskt att läggas till i fält av typen `Date`. Uppdateringen ser till att det exporterade dataformatet matchar det format som finns representerat i profilen för det fältet enligt kundens önskemål.

`Date` fält före releasen: `"birthDate": "2018-01-12T00:00:00Z"`
`Date` fält efter releasen: `"birthDate": "2018-01-12"`

Läs mer om [gruppinmatning](/help/ingestion/batch-ingestion/overview.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade mål** {#new-updated-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | [!UICONTROL Braze] hanterar ett antal olika instanser för sin kontrollpanel och REST-slutpunkter. [!UICONTROL Braze]-kunder bör använda rätt REST-slutpunkt baserat på vilken instans du har tilldelats. Den här versionen lägger till en ny US-07-slutpunkt som du kan välja när du ansluter till [!UICONTROL Braze]. |

{style="table-layout:auto"}

**Ny eller uppdaterad funktion** {#destinations-new-updated-functionality}

| Funktion | Beskrivning |
| ----------- | ----------- |
| Export av filer on-demand till batchdestinationer är nu allmänt tillgängligt. | Alternativet att exportera filer on demand till batchdestinationer är nu tillgängligt för alla kunder. Mer information finns i den [dedikerade dokumentationen](../../destinations/ui/export-file-now.md). |
| Redigera exportscheman för flera exporterade målgrupper i [schemaläggningssteget](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | Möjligheten att redigera exportscheman för flera exporterade målgrupper direkt från schemaläggningssteget i arbetsflödet för målgruppsaktivering är nu tillgängligt för alla kunder. ![Bild av användargränssnittet i Experience Platform som markerar alternativet Redigera schema i schemaläggningssteget.](assets/august/edit-schedule.png "Redigera schemaalternativ i schemaläggningssteget."){width="250" align="center" zoomable="yes"} |
| Redigera filnamn för flera exporterade målgrupper i [schemaläggningssteget](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | Nu kan alla kunder redigera namnen på flera exporterade filer direkt från schemaläggningssteget i målgruppsaktiveringsarbetsflödet. ![Bild av användargränssnittet i Experience Platform som markerar alternativet Redigera filnamn i schemaläggningssteget.](assets/august/edit-file-name.png "Redigera filnamnsalternativ i schemaläggningssteget."){width="250" align="center" zoomable="yes"} |
| Ta bort flera målgrupper från ett dataflöde från sidan [Målinformation](../../destinations/ui/destination-details-page.md#bulk-remove). | Alternativet att ta bort flera målgrupper från befintliga dataflöden från sidan **[!UICONTROL Destination Details]** är nu tillgängligt för alla kunder. ![Bild av användargränssnittet i Experience Platform som markerar alternativet Ta bort målgrupper på sidan Målinformation.](assets/august/bulk-remove-audiences.png "Alternativet Ta bort målgrupper på sidan Målinformation."){width="250" align="center" zoomable="yes"} |
| Exportera flera filer på begäran till gruppmål från sidan [Målinformation](../../destinations/ui/destination-details-page.md#bulk-export). | Alternativet att exportera flera filer on-demand till gruppmål från sidan **[!UICONTROL Destination Details]** är nu tillgängligt för alla kunder. ![Bild av användargränssnittet i Experience Platform som markerar alternativet Exportera fil nu på sidan Målinformation.](assets/august/bulk-export-file-now.png "Alternativet Exportera fil nu på sidan Målinformation."){width="250" align="center" zoomable="yes"} |
| Redigera filnamn för flera exporterade målgrupper på sidan [Målinformation](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | Nu kan du redigera namnen på flera exporterade filer direkt från sidan **[!UICONTROL Destination Details]**. ![Bild av användargränssnittet i Experience Platform som markerar alternativet Redigera filnamn på sidan med målinformation.](assets/august/edit-file-name-destination-details.png "Redigera filnamnsalternativ på målinformationssidan."){width="250" align="center" zoomable="yes"} |
| Ta bort flera datauppsättningar från ett dataflöde från sidan [Målinformation](../../destinations/ui/export-datasets.md#remove-dataset). | Alternativet att ta bort flera datauppsättningar från ett dataflöde är nu tillgängligt för alla kunder. ![Bild av användargränssnittet i Experience Platform som markerar alternativet Ta bort datauppsättningar på sidan med målinformation.](assets/august/bulk-remove-datasets.png "Ta bort datauppsättningsalternativ på sidan med målinformation."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Mer information finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Arbetsflöde för att skapa XML-stödda scheman | Använd avancerade maskininlärningsalgoritmer för att analysera dina exempeldatafiler och automatiskt skapa optimerade scheman med hjälp av standardfält och anpassade fält.<br>Nyckelfunktioner:<br><ul><li>Skapa schema snabbare: Generera scheman direkt från exempeldatafiler med XML-rekommenderade och genererade XDM-fält.</li><li>Flexibel schemautveckling: Lägg enkelt till eller uppdatera fält i det genererade schemat.</li><li>Smidig integrering: Helt integrerat med det centrala schemaflödet i Schema UL, vilket ger en smidig och sammanhängande användarupplevelse.</li><li>Effektiv granskning och redigering: Visa och uppdatera snabbt schemat med hjälp av Flat View-redigeraren, vilket gör arbetet mer effektivt och användarvänligt.</li></ul><br>Mer information finns i [Arbetsflödesguiden ](../../xdm/ui/ml-assisted-schema-creation.md) för att skapa XML-stödda scheman. |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Identitetstjänst {#identity-service}

Använd Adobe Experience Platform identitetstjänst för att skapa en heltäckande bild av era kunder och deras beteenden genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterad dokumentation**

| Funktion | Beskrivning |
| --- | --- |
| Guide för diagramkonfigurationer | Läs [diagramkonfigurationsguiden](../../identity-service/identity-graph-linking-rules/example-configurations.md) om du vill ha information om vanliga diagramscenarier som du kan stöta på när du arbetar med länkningsregler för identitetsdiagram och identitetsdata. Guiden för diagramkonfigurationer innehåller exempel från enkla enpersonsdiagram till komplexa och hierarkiska flerpersonsdiagram. Du kan också använda guiden för exempel på händelser och algoritmkonfigurationer som du kan ange i [diagramsimuleringens användargränssnitt](../../identity-service/identity-graph-linking-rules/graph-simulation.md), samt för att dela upp hur primära identiteter väljs utifrån vissa diagramscenarier. |

{style="table-layout:auto"}

Mer information om identitetstjänsten finns i [Översikt över identitetstjänsten](../../identity-service/home.md).

## Segmenteringstjänst {#segmentation}

Med [!DNL Segmentation Service] kan du segmentera data som lagras i [!DNL Experience Platform] och som relaterar till individer (t.ex. kunder, potentiella kunder, användare eller organisationer) till målgrupper. Du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform] och är tillgängliga för alla Adobe-lösningar.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Inmatningsinformation | För målgrupper med ursprung i Custom Upload kan du mer ingående visa information om målgruppens förtäring på sidan med målgruppsinformation. Dessutom kan du lägga till etiketter i nyttolastattributen genom att markera schemat och välja önskade attribut för etiketteringen. Mer information om avsnittet med information om inmatning finns i [guiden för målportalen](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Mer information om [!DNL Segmentation Service] finns i [Segmenteringsöversikt](../../segmentation/home.md).

## Källor

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

Använd källor i Experience Platform för att importera data från ett Adobe-program eller en datakälla från tredje part.

**Uppdaterad funktion**

| Funktion | Beskrivning |
| --- | --- |
| Uppdateringar av Adobe Analytics källanslutning | Datamängdens aktivitetssida visar ingen information om grupper eftersom Analytics Source Connector hanteras helt av Adobe. Ni kan övervaka att data flödar genom att titta på mätvärdena runt inkapslade poster. Läs guiden om hur du skapar en [källanslutning för Analytics-data](../../sources/tutorials/ui/create/adobe-applications/analytics.md) om du vill ha mer information. |

**Uppdaterad dokumentation**

| Uppdaterad dokumentation | Beskrivning |
| --- | --- |
| Utökad dokumentation om uppdatering av dataflöden | Guiden [Uppdatera befintliga källfilsdataflöden i användargränssnittet ](../../sources/tutorials/ui/update-dataflows.md) har uppdaterats för att ge mer information om olika konfigurationer som du kan göra i ett befintligt dataflöde. Handboken har också uppdaterats för att förtydliga det förväntade beteendet när ett inaktiverat dataflöde återaktiveras. |

{style="table-layout:auto"}

Mer information finns i [Källöversikt](../../sources/home.md).
