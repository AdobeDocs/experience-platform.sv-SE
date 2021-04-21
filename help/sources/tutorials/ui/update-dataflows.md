---
keywords: Experience Platform;hem;populära ämnen;uppdatera dataflöden;redigera schema
description: I den här självstudiekursen beskrivs stegen för att uppdatera ett dataflödesschema, inklusive dess ingångsfrekvens och intervall, med hjälp av arbetsytan Källor.
solution: Experience Platform
title: Uppdatera ett källanslutningsdataflöde i användargränssnittet
topic-legacy: overview
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# Uppdatera dataflöden i användargränssnittet

I den här självstudiekursen får du lära dig hur du uppdaterar ett befintligt källkodsdataflöde, inklusive information om hur du redigerar ett dataflödesschema och mappning med arbetsytan [!UICONTROL Sources].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
- [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Redigera mappning

>[!NOTE]
>
>Redigeringsmappningsfunktionen stöds för närvarande inte för följande källor: Adobe Analytics, Adobe Audience Manager, HTTP API och [!DNL Marketo Engage].

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Välj **[!UICONTROL Dataflows]** i den övre rubriken om du vill visa en lista över befintliga dataflöden.

![katalog](../../images/tutorials/update-dataflows/catalog.png)

Sidan [!UICONTROL Dataflows] innehåller en lista med alla befintliga dataflöden, inklusive information om körningsstatus, senaste körningsdatum och kontonamn.

Välj filterikonen ![filter](../../images/tutorials/update/filter.png) längst upp till vänster för att starta sorteringspanelen.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Sorteringspanelen innehåller en lista med alla tillgängliga källor. Du kan välja mer än en källa i listan för att få tillgång till ett filtrerat urval av dataflöden som tillhör olika källor.

Välj den källa som du vill arbeta med för att visa en lista över de befintliga dataflödena. När du har identifierat det dataflöde som du vill uppdatera markerar du ellipserna (`...`) bredvid kontonamnet.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

En listruta visas med alternativ för att uppdatera det dataflöde du valde. Härifrån kan du välja att uppdatera ett dataflöds mappningsuppsättningar och schema för inmatning. Du kan också välja alternativ för att inspektera dataflödet på kontrollpanelen samt inaktivera eller ta bort dataflödet.

Välj **[!UICONTROL Edit source]** om du vill uppdatera mappningen.

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

[!UICONTROL Add data]-steget visas. Välj lämpligt dataformat för att granska innehållet i dina markerade data och välj sedan **[!UICONTROL Next]** för att fortsätta.

![tilläggsdata](../../images/tutorials/update-dataflows/add-data.png)

Sidan [!UICONTROL Mapping] innehåller ett gränssnitt där du kan lägga till och ta bort mappningsuppsättningar som är kopplade till datauppsättningen.

>[!TIP]
>
>Mappningsuppdateringar tillämpas bara på framtida schemalagda dataflöden.

Välj **[!UICONTROL Add new mapping]** om du vill lägga till en ny mappningsuppsättning.

![add-new-mapping](../../images/tutorials/update-dataflows/add-new-mapping.png)

Ange sedan rätt källfältsattribut och mål-XDM-fältvärden för att slutföra den ytterligare mappningsuppsättningen. Välj **[!UICONTROL Next]** för att fortsätta.

![new-mapping-added](../../images/tutorials/update-dataflows/new-mapping-added.png)

Steget [!UICONTROL Scheduling] visas så att du kan uppdatera dataflödets schema för inmatning och automatiskt importera valda källdata med uppdaterade mappningar.

>[!NOTE]
>
>Det går inte att uppdatera mappningsuppsättningar för dataflöden som schemalagts för engångsinmatning och som redan har startats.

![schemaläggning](../../images/tutorials/update-dataflows/scheduling.png)

På sidan [!UICONTROL Dataflow detail] kan du ange ett uppdaterat namn och en beskrivning för dataflödet samt konfigurera om feltröskeln för dataflödet.

När du har angett dina uppdaterade värden väljer du **[!UICONTROL Next]**.

![dataflöde-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

Steget **[!UICONTROL Review]** visas så att du kan granska dataflödet innan det uppdateras.

När du har granskat dataflödet väljer du **[!UICONTROL Finish]** och anger en tid för dataflödet med de nya mappningsuppsättningarna som ska skapas.

![recension](../../images/tutorials/update-dataflows/review.png)

## Redigera schema

Om du vill redigera inmatningsschemat för ett befintligt dataflöde markerar du ellipserna (`...`) bredvid ett dataflödesnamn och väljer sedan **[!UICONTROL Edit schedule]** i listrutan.

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

Dialogrutan **[!UICONTROL Edit schedule]** innehåller alternativ för att uppdatera dataflödets matningsfrekvens och intervallhastighet. När du har angett uppdaterade värden för frekvens och intervall väljer du **[!UICONTROL Save]**.

>[!NOTE]
>
>Det går inte att schemalägga om ett dataflöde som schemalagts för engångsintag.

![schedule-dialog-box](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| Schemaläggning | Beskrivning |
| ---------- | ----------- |
| Frekvens | Frekvensen med vilken dataflödet samlar in data. Giltiga värden för redigering av frekvensschema för ett befintligt dataflöde är: `minute`, `hour`, `day` eller `week`. |
| Intervall | Intervallet anger perioden mellan två på varandra följande flödeskörningar. Intervallets värde ska vara ett heltal som inte är noll och måste vara större än eller lika med `15`. |

Efter en stund visas en bekräftelseruta längst ned på skärmen som bekräftar att uppdateringen lyckades.

![schemalägg-bekräfta](../../images/tutorials/update-dataflows/schedule-confirm.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt arbetsytan [!UICONTROL Sources] för att uppdatera inmatningsschemat och mappningsuppsättningarna för dataflödet.

Anvisningar om hur du utför dessa åtgärder programmatiskt med API:t [!DNL Flow Service] finns i självstudiekursen om att [uppdatera dataflöden med API:t för Flow Service](../../tutorials/api/update-dataflows.md).
