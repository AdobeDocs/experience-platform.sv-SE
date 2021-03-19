---
keywords: Experience Platform;hem;populära ämnen;uppdatera dataflöden;redigera schema
description: I den här självstudiekursen beskrivs stegen för att uppdatera ett dataflödesschema, inklusive dess ingångsfrekvens och intervall, med hjälp av arbetsytan Källor.
solution: Experience Platform
title: Uppdatera schema för källanslutningsdataflöde i användargränssnittet
topic: översikt
type: Självstudiekurs
translation-type: tm+mt
source-git-commit: 31e4b15ad71a0d17278fbdb4d88ff42029cbe655
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Uppdatera dataflöden i användargränssnittet

I den här självstudiekursen beskrivs stegen för att uppdatera ett dataflödesschema, inklusive dess ingångsfrekvens och intervall, med arbetsytan [!UICONTROL Sources].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Källor](../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
- [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Redigera schema

Välj **[!UICONTROL Sources]** från vänster navigering i plattformsgränssnittet för att komma åt arbetsytan [!UICONTROL Sources]. Välj **[!UICONTROL Dataflows]** i den övre rubriken om du vill visa en lista över befintliga dataflöden.

![katalog](../../images/tutorials/update-dataflows/catalog.png)

Sidan [!UICONTROL Dataflows] innehåller en lista med alla befintliga dataflöden, inklusive information om körningsstatus, senaste körningsdatum och kontonamn.

Välj filterikonen ![filter](../../images/tutorials/update/filter.png) längst upp till vänster för att starta sorteringspanelen.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Sorteringspanelen innehåller en lista med alla tillgängliga källor. Du kan välja mer än en källa i listan för att få tillgång till ett filtrerat urval av dataflöden som tillhör olika källor.

Välj den källa som du vill arbeta med för att visa en lista över de befintliga dataflödena. När du har identifierat det dataflöde som du vill schemalägga om markerar du ellipserna (`...`) bredvid kontonamnet.

![ändra schema](../../images/tutorials/update-dataflows/reschedule.png)

En listruta visas med alternativ för **[!UICONTROL Edit schedule]**, **[!UICONTROL Disable dataflow]**, **[!UICONTROL View in monitoring]** och **[!UICONTROL Delete]**. Välj **[!UICONTROL Edit schedule]** på menyn.

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

Genom att följa den här självstudiekursen har du använt arbetsytan [!UICONTROL Sources] för att uppdatera ett dataflödes användningsschema.

Anvisningar om hur du utför dessa åtgärder programmatiskt med API:t [!DNL Flow Service] finns i självstudiekursen om att [uppdatera dataflöden med API:t för Flow Service](../../tutorials/api/update-dataflows.md).